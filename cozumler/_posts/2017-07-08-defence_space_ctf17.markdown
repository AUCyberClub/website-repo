---
layout: post
title: Defence Space CTF:2017 Walkthrough
date: '2017-07-07 11:00:00 +0300'
categories: cozumler
---


Merhaba arkadaşlar, 
Bu yazımda [Vulnhub](https://www.vulnhub.com) üzerinde yayınlanan DEFENCESPACECTF-17 zafiyetli makinesinin çözümüyle karşınızdayım :)

__Bilgi__

Bu makine silexsecure denen arkadaşımız tarafından Nijerya'nın bütünlüğünü savunmak için savaşan, orduda ilk canını veren askere saygı amaçlı oluşturulmuş. Makinemizin bir hikayesi var ve yazan arkadaşımız bu hikayenin Kuzey Nijerya'da yaşanmış gerçek bir olaydan esinlendiğini söylüyor. Biz de  bu hikayeyi takip ederek flaglere ulaşacağız. Toplamda makinemizde 7 adet flag var ve en son ulaşmamız gereken şehit olan asker tarafından gönderilmiş topsecret belgeye ulaşmak.

__Linkler__

[Vulnhub Bağlantısı](https://www.vulnhub.com/entry/defence-space-ctf-2017,179/ "Vulnhub Bağlantısı")

__Çözüm__

İlk olarak kullandığım sanallaştırma ortamı olan Oracle VirtualBox'ta hem Kali Linux'umu hem de hedef makinem olan DEFENCESPACE'i ayaklandırıyorum ve her zamanki gibi Kali makinemin ip adresini bularak başlıyorum.
```
    $ ifconfig
```
![IP_BULMA]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/1.png )

Daha sonra Kali’min bulunduğu scope taki IP’leri tarayarak devam ediyorum.
```
    $ netdiscover -i eth0 -r 192.168.56.0/24
```
![NETDISCOVER]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/2.png )

Ve hedef IP'yi bulduğuma göre nmap atarak devam ediyorum.
```
    $ nmap -A -p- -Pn -sT 192.168.56.20
```
![NMAP]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/3.png )

Nmap ile detaylı tarama yaptığım için çalışan ssl servisinin sertifikası da geldi ve burda istemeden Flag3'ü elde etmiş oldum:) Ama sırayla gitmeyi tercih ederek açık portları inceliyorum ve bir Http servisinin çalıştığını görüyorum. Hemen Browser'ıma IP adresini yapıştırıyorum.

![WEB_PAGE]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/4.png )

Karşıma bir web sayfası geliyor ve ilk dikkatimi çeken şey sağ üstte bir FLAGS butonu oluyor:) Bu kadar da basit olmamalı diyerek basıyorum vee hiçbir şey gelmiyor:) Tamam moral bozmak yok :) VM'in bir hikayesi olduğunu en başta söylemiştik. O yüzden web sayfasını iyice inceliyorum. İki kahraman komutanın bilgileri yer alıyor ve başka da bi şey bulamıyorum. Elimde bir web sayfası olduğu için aklıma ilk gelen şey sayfanın kaynak kodlarına bakmak oluyor.

![SOURCE_CODE]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/5.png )

Kaynak kodlarını açtım ve incelemeye başladım derken aşağı kısımlarda bi eşittir gördüm sanki oluyorum ve hemen base64 decode ediyorum ve Flag0 gelmiş oluyor.

`-> Flag 0 (netdiscover)`

Arkadaş biraz geriden geliyor:) Biz bu aşamaları geçeli çok oldu dostum diyerek ikinci Flag'i aramaya koyuluyoruz derken hemen alt kısımda kırmızıyla yazılmış bi yorum satırı görüyorum resmen bana baaakk! diye bağırıyor. Hemen /assets/lafiya.js ye gidiyorum. 

![assets]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/6.png )

Ve ne göreyim orda bir hex var. Hemen hex to text yapıyorum ve ikinci Flag'imi elde ediyorum 

`-> Flag 2 9a8780281d3e37c597cee7ca58bfd435`

0'dan 2 ye atladılar ama olsun:) Benim için bi problem yok. Neyse:) Orda 32 karakterli harf ve rakamlardan oluşan bir string görüyorum ve md5 decode yapıyorum. Bana Nmap ipucunu veriyor. Hala bize yetişemedi arkadaş biz o aşamayı da geçmiştik:) ve orda Flag3'ü görmüştüm ama sırayla gitmek istediğim için bi yere not edip geçmiştim. Şimdi sıra ona geldiği için geri dönüyorum. Nmap taramamda gördüğüm sayfanın ssl sertifikasına bakıyorum. (Bu ssl sertifikasını aynı zamanda Web Browser'da IP adresinin önüne https:// koyduktan sonra sayfanın özellikleri kısmından da görebilirsiniz.)

![Flag3]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/7.png )

`Flag3 [19c562a36aeb455d093b4f5236f] + [39 39 30]`

Bu Flag de yine 32 karakter ve md5 decode ama ondan sonra bi hex görüyorum arada da + var ben de ilk kısmı md5 decode yapıp sonra diğerini hex to binary yapıp yan yana yazıyorum ve BAM!!!

`Unit990` 

Bunu web sayfasında da okuduğum kadarıyla asıl proje buydu. Sanırım Lafiya Dole Operasyonu'nun kod adı diyerek IP adresinin sonuna ekleme yapıp siteye gidiyorum.

![Unit990]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/8.png )

Lafia Dole Operasyonu'nun anasayfasına ulaşıyorum. Çok güzell. Elimde bir web sitesi var ve bir de login ekranı aslında ilk aklıma gelen sql injection denemesi oluyor ama ondan önce bi sayfanın kaynak kodlarını inceleyim diyorum.

![RESİM]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/9.png )

İlk olarak dikkatimi çeken şey yorum satırı oluyor ve orda bir encoded string görüyorum. Hemen md5 deniyorum ve bu sefer patladım. Alıştık gidiyoruz ama orda 32 karakter yokmuş :) Base64 gibi duruyor o zaman bi de onu deneyim derken geldi:)

`-> flag 4 {admin.php}`

Hemen altta bi de kırmızı bir yorum satırı görüyorum ve resmen ' OR '1'='1 sql injection denemesi yap demiş bana:) Bu biraz basit oldu:( Neyse ilk önce admin.php uzantısını kontrol ediyorum. 

![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/10.png )

Çok güzeeelll. Bir admin login paneli geldi. İlk işim yine kaynak kodlara bakmak ve yorum satırının içinde bir base64 encoded string görüyorum. Base64 decode edince 5. Flag'im geliyor.

![acd]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/11.png )

`-> Flag 5 {SQL injection}`

İlk önce normal operasyon sayfasına giriyorum ve nmap taramamda ssh portunu açık görmüştüm ama elimde bir kullanıcı adı olmadığı için bağlantı yapamamıştım burdaysa kullanıcı adı değil direk terminal komutunu vermiş :) Altında da bir base64 ile encode edilmiş bir şifre görüyorum. Decode yaptıktan sonra kendi Kali'mden hedef makineye bir ssh bağlantısı gönderiyorum.

![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/12.png )

Parolayı girmeden bana bu servise sadece yetkili kullanıcıların girebileceğini belirten bir uyarı veriyor ve onun altında da bir Flag daha görüyorum.

`-> Flag2B{53c82eba31f6d416f331de9162ebe997}`

Md5 decode ettiğimde encyrpt stringini elde ediyorum ve burdan içerdeki bilgilerin encrypted olabileceğini düşünüyorum. Aslında bu flag biraz gereksiz olmuş:=) Ama Flag bulmak ne olursa olsun çok eğlenceli:DD Neyse devam ediyorum.

Parolayı girdikten sonra abuali kullanıcısının dizinine ulaşıyorum içine baktığımda Muhammed-Ali'nin son sözlerini görüyorum. Abimiz ölmeden önce buraya son sözlerini yazıp koymuş. Ama makinenin içinde gezmedik yer bırakmamama rağmen herhangi bir flag bulamıyorum. Burda demek ki sadece abimizin son sözleri varmış diyerek burdan çıkıyorum. 

![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/13.png )

Şimdi asıl önemli yere, admin paneline geldim. Aynı SQL Injection metoduyla giriyorum.

![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/14.png )

İçeriyi biraz kurcalıyorum. Pek bi şey çıkmayacakmış gibi geliyor derken ID numarası 13 olan arkadaşın telefon numarası base64 encode edildiği gözüme çarptı. Heralde telefon numarası base64 encode edilip koyulacak hali yok :) Decode edince `Nigairforcecloud` stringi geliyor. İlk başta bi anlam ifade etmese de daha sonra web sitesinin uzantısı olabileceği aklıma geldi ve yapıştırdım. (Bunu elde etmenin bir yolu daha var Kali Linux dağıtımında bulunan sqlmap tool'unu kullanarak da bunu flag olarak çekebilirsiniz eğer sqlmap kullanmayı da görmek istiyorum diyen varsa yazının sonunda onun da nasıl yapılacağını göstereceğim.)

![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/15.png )

Bi login ekranı geldi ve her login paneli gibi benden bi kullanıcı adı ve parola bekliyor:) Ama elimde kullanıcı adı veya parola olabilecek hiç bi şey yok şu anda. Hmmmm... diyip biraz düşünmemiz gerekecek:) Bunun hava kuvvetleri ile alakalı bir servis olduğunu anlamak için Sherlock olmaya gerek yok:) Bunu anladım en azından ve aklıma web sayfasındaki kahraman askerler geldi. Bir tanesi Late Wing Commander Chinda Hedima idi ve sanırım Wing Commander Hava Kuvvetleri Komutanı'na benzer bir şeydir diye düşündüm. Daha sonra VM'in hikayesinde gerçek bir olaydan esinlenildiğinin yazdığını hatırlayıp bunu bi google'ladım. Biraz araştırma yaptıktan sonra mantığımın doğru olduğunu gördüm ve sıradaki düşüncem bu askerin hesabıyla bu sunucuya giriş yapmam gerekiyor olduğu. 

Ben de yine ana web sayfasına gidip ordaki hikayeyi bir kez daha okudum sayfanın kaynak kodlarını bir kez daha okudum. Hala bi kullanıcı adı ve parola arıyorum. Ama en azından neye baktığımı biliyorum şu anda. Kaynak kodlarda gezinirken /assets/lafiya.js' nin yanındaki ibare beni bir kez daha oraya yönlendirdi.

![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/16.png )

Çok fazla karışık şey olduğu için ilk buraya girdiğimde hiç dikkatimi çekmemişti ama şöyle bi göz gezdirince tam da aradığım şeyi buldum. Aradığım askerin mail adresi. Aslında ondan önce bir mesaj  var ama açıkçası mesajdan nasıl bir şey çıkarabilirim bilemedim:)) Bu bir kullancı adı olabilir diyerek hemen bi yere yazıyorum. Dikkatimi çeken bir şey daha vardı, aynı satırda `Bama1987` stringi bir parola olabilir diyerek onu da hemen aldım ve denememi yaptım fakat kabul etmedi. Hmm parola farklı bi şey olmalı diyerek kaynak kodlara bir kez daha döndüm o satırı bir kez daha inceledim ve orda sanki bir harita koordinatı verilmiş bir şehir ismi verilmiş `Borno`. Bunu biraz araştırınca mail adresini bulduğumuz bu abimizin doğduğu yer olduğunu öğrendim ve hemen parola olarak bunu denedim. 

Ve içerdeyim:) Kocaman bir Flag beni karşıladı. 

![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/17.png )

`-> FLAGE 7: 3aa652f41d8b4a23e17937149c784868`

Yine beni kandırır mı diye bi baktım ve evet 32 karakter var md5 decode:) Decode edince `widgets` çıktısını aldım ve sayfanın solunda widgets diye bir link görüyorum. Hemen basıyorum. İçerde bir ses dosyası bir de resim dosyası var. İkisini de bilgisayarıma çektikten sonra ilk önce resimi gözüme kestirip üzerinde baya bi araştırma yaptıktan sonra içinde hiçbir şey bulamadım :) Ben de ses dosyasına geçtim. Dosyayı açıyorum sürüyor sürüyor... Ama içinde herhangi bir ses yok muhtemelen ses olarak gönderilmiş ama içine bir şeyler gömülmüş. Tabi tamamen tahmin aşamasında şu anda:) Hemen araştırmaya başlıyorum. 
```
    $ file Alfajet106.wav
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/18.png )
Tamam normal bir .wav dosyası olarak görünüyor.
```
    $ strings Alfajet106.wav
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/19.png )

Hmmm... Strings komutuyla bakınca çok değişik şeyler geldi :) Kesin içinde bir txt dosyası veya benzer bir şeyler var. Yüksek ihtimalle stego ile karşı karşıyayım. 
```
    $ steghide --info Alfajet106.wav 
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/20.png )
Bu komutla içine stego yöntemiyle içine bir şey gizlenmiş mi ona bakıyorum ama benden bir passphrase bekliyor. Hmmmm... Az önce bir kenara not ettiğim `Bama1987` stringi vardı ilk önce Nigairforcecloud sayfasına girerken denemiştim fakat o değildi. Bu da aynı arkadaşın sisteme yüklediği bi dosya olduğu için bu passphrase o olmalı. Deniyorum ve geldi:)))
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/26.png )
İçinde "Topsecret.txt" adında bir dosya var. Bunu gördüm. Passphrase' i de bildiğim için çıkartıyorum ve çıkan dosyayı okuyorum.
```
    $ steghide extract -sf Alfajet106.wav -p Bama1987
    $ cat Topsecret.txt
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/21.png )

Veeee..... Bütün amacım burada duruyor. "Topsecret.txt" adlı bir text dosyası çıktı içinde dört kişinin bilgileri bulunmakta. Zaten ana web sayfasında hatırlarsanız bu abimizin gönderdiği gizli mesajı arıyorduk Flag'ler de bize yardımcı olmaya çalışıyorlardı.

Bir dahaki VM çözümünde görüşmek üzere....

__sqlmap Tool Kullanımı__

Yukarda bahsettiğim gibi burda da admin sayfasında bulunan sql açıklarından yararlanarak bilgileri bize çekecek olan sqlmap tool'unu kullanarak Flag6'yı elde edeceğiz.

İlk önce sqlmap ile admin.php sayfasında herhangi bir client'ın sayfasına girerek bir tarama başlatıyorum.
```
    $ sqlmap -u http://192.168.56.20/Unit990/pages/clientView.php?id=13 
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/22.png )
Bana arka planda kullanılan database'in MySql olduğunu versiyon bilgisini zafiyet olup olmadığını hatta bilgisayarda kullanılan işletim sistemi bilgilerini bile getiriyor. Şimdi database'i çekebilmek için aşağıdaki komutu veriyorum.
```
    $ sqlmap -u http://192.168.56.20/Unit990/pages/clientView.php?id=13 --dbs
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/23.png )
Şimdi sayfada bulduğu time-based sql açığını kullanarak uygun database'lerin listesini getirdi. Şimdi daha içeri giriyorum.
```
    $ sqlmap -u http://192.168.56.20/Unit990/pages/clientView.php?id=13 -D silex --tables
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/24.png )
Silex'in içindeki tabloları listeliyorum. Burdan da ilgimi çeken admin değeri oluyor. O tablonun içinde ne olduğunu görmek için de aşağıdaki komutu veriyorum.
```
    $ sqlmap -u http://192.168.56.20/Unit990/pages/clientView.php?id=13 -D silex -T admin -C code --dump
```
![Picture]({{ AUCyberClub.github.io }}/assets/img/defencespacectf/25.png )
Dump ile içerdeki veriyi çektim ve sanırım base64 encoded bir string elde ettim. Base64 decode edince flag 6'yı elde ediyorum.

`-> flag 6 {Nigairforcecloud}`
Burdan yukarıdaki işlemlere devam edip Flag7'yi bulur aynı şekilde "Topsecret.txt" dosyasına ulaşabiliriz:)

---
[Talha Eryaşar](https://twitter.com/__talhaeryasar)
