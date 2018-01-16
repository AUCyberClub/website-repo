---
layout: post
title: En Basit Hali ile HTTP Api Oluşturmak (PHP)
date: '2017-02-26 20:44:47 +0300'
categories: makaleler
---

**Backstory:** HTTP Api her ne kadar "büyük" bir şey gibi durmasına karşın, aslında implement etmesi ve kullanılır hale getirmesinin çok basit olduğunu göstermek amacıyla ekibimizden HTTP Api konusunda hiç bir bilgisi olmayan 2 arkadaşımıza, gelen POST verisini okuyan ve post verisindeki data'yı bir .txt dosyasında tutan basit bir HTTP Api oluşturmalarını istedik.

Arkadaşlarımız kullanımının basitliği (kodun da kısalığından göreceğiniz gibi) nedeniyle PHP ile yazmaya karar verdiler.

--------------------------------------------------------------------------------

Günlük hayatta standart olarak görebileceğimiz platform veya programlama dili kaygısı olmadan veri kayıt eden (Register Form) bir WEB (HTTP) API var elimizde. Uygulama sizden bir takım veriler istiyor ve aldığı verileri bir text dosyasına yazıyor. Bu bir database'de olabilirdi. Biz bu işleme 'Post Method' diyoruz.

Örneğimizde Standart bir form oluşturduk ve bu forma girdiğimiz verileri, PHP komutları ile alıp birer değişkene atadık. Sonra PHP dosya işleme komutlarını (fopen,fwrite) kullanarak bunlara bir text dosyasına yazdırdık. Bu söylediğimiz gibi bir Database'de olabilirdi.

Server tarafında yazdığımız PHP kodunu görelim;

```php
<?php
  // gelecek veri keyleri olan name ve surname değerlerini
  // değişkene atıyoruz.
  $name = $_POST["name"];
  $surname = $_POST["surname"];

  // gelen veriyi, data.txt dosyasını açıp ekliyoruz.
  $myfile = fopen("data.txt", "w") or die("Unable to open file!");

    fwrite($myfile, $name);
    fwrite($myfile, $surname);
    fclose($myfile);

  echo "Adınız txt dosyasına eklendi: "

  echo $name;
    echo $surname;   
?>
```

Bu dosyanın server.php olarak kayıt edilip, sunucuya apache tarafından sunulan bir konuma yüklenmiş olduğunu düşünelim. Bu durumda <http://site.com/HttpApi/server.php> adresine gönderdiğimiz post requestleri eğer name ve surname değerlerini içeriyorsa, text dosyamıza eklenecek.

İkinci aşama olarak, örneğin Perl dilini kullanarak POST işlemi gerçekleştirmeye çalıştık. 'LWP::UserAgent' sınıfını import ettik ve burada tanımlı 'POST' işlemi ile hedef siteye POST işlemi gerçekleştirdik. Post fonksiyonu parametre olarak URL ve post edilecek verileri alıyor. Bu program sayesinde tarayıcıdan giriş yapmadanda uygulamaya verileri 'POST' edebilirsiniz.

Perl ile yazdığımız post requesti kodunu görelim;

```perl
#!/usr/bin/perl

use strict;
use warnings;

use LWP::UserAgent;
use CGI;

my $isim = 'Armagan';
my $soyisim = 'Plus';
my $url = 'http://site.com/HttpApi/server.php';

my $ua       = LWP::UserAgent->new();
my $response = $ua->post( $url, { 'name' => $isim , 'surname' => $soyisim } );
my $content  = $response->decoded_content();

my $cgi = CGI->new();
print $cgi->header(), $content;
```

Dikkat ediniz, bu perl kodu, farklı bir server'de veya bir lokal bilgisayarda execute edilebilir.

- Not: LWP :: UserAgent nesneleri, web isteklerini göndermek için kullanılabilir.
- Not: CGI , HTTP isteklerini ve yanıtlarını hazırlamak için kullanılır.

Herhangi bir backend dilini kullanarak POST işlemi gerçekleştirebilirsiniz, örneğin son zamanlarda çok kullanılan yeni bir web backend dili olaran nodejs ile;

```javascript
var requestify = require('requestify');

requestify.post('http://site.com/HttpApi/server.php', {
    name: 'ismim',
    surname: 'soyismim'
})
.then(function(response) {
    response.getBody();
});
```

POST gönderen client olarak, tarayıcınızda HTML form elementini ve inputları da kullanabilirsiniz;

```html
<form action="server.php" method="post">
    <h1> REGISTER!</h1>
        Name: <input type="text" placeholder="Enter Name" name="name">
         <br>
        Surname: <input type="text" placeholder="Enter Surname" name="surname">
           <br>
       Register  <input type="submit" value="Go">
</form>
```

Tüm bunlara ek olarak, bir POST requesti yapmak için, programlama dili kullanmak zorunda da değiliz. Postman gibi, chrome tool'ları kullanarak, herhangi bir post isteği kabul eden HTTP api'ına post isteği gönderebilirsiniz.

![](https://www.getpostman.com/img/v1/docs/thumbs/9.png)

Prep: **[Hakan Bayır](https://twitter.com/)**, **[Mücahid Ceylan](https://twitter.com/m3o_cey)**
