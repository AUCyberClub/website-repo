---
layout: post
title: Quaoar Walkthrough
Date: '2017-4-20 00:10 +0300'
categories: blog
---
Selam,  
Öncelikle bu benim çözdüğüm ilk sanal zafiyetli makinem. Bu yüzden pek çok şeyi araştırmam gerekti. Daha önce arkadaşlarımın çözdükleri VM'lere bakarak az buçuk bir şeyler kaptığımı düşünüyordum. Öğrendiklerimin faydasını yeni yeni gördüğümü söyleyebilirim.  

İlk olarak makineyi [şu linkten](https://www.vulnhub.com/entry/hackfest2016-quaoar,180/) indirerek WMware Player ile ayaklandırdım. Açtığımda beni şöyle bir ekran karşıladı. 

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/1.png)

Bu makinenin çözümü üç aşamada gerçekleşti:
 - İlk adımda, hedef sisteme shell erişimi elde ettim.
 - İkinci adımda, yetkili kullanıcı haklarına eriştim.
 - Üçüncü adımda ise post exploitation işlemleri ile flag'i elde ettim.  
İlk adımı gerçekleştirebilmek için hedef sistemde açık olan portları ve servisleri **nmap** aracı ile analiz etmeye başladım. Yaptığım versiyon taramasının sonucu şöyleydi: 

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/2.png)

80 portunun açık olduğunu görünce tarayıcım ile ziyarette bulundum. 

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/3.png)

Web sitesi hakkında bir şeyler öğrenmek için **Nikto** aracı ile tarama yaptım.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/4.png)

Nikto bana robots.txt dosyası bulmuştu, mutlu olup içinde hangi dizinlere hangi izinlerin verildiğine baktım. 

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/5.png)

**/wordpress** dizinine gittiğimde karşıma Wordpress içerik yönetim sistemi tarafından oluşturulmuş bir blog çıktı. Aynı dizini uygun bir wordlist ile Dirbuster gibi araçlar kullanarak de bulabilirdik fakat burada robots.txt içeriğini okuyarak zahmet etmeden bu bilgiyi elde etmiş olduk.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/6.png)

Ardından acaba bu aşamayı nasıl geçebilirim diye düşündüm. Kali Linux'taki araçlardan daha önce gördüğüm veya bana 
yardımcı olabilecek bir tool var mı diye biraz araştırma yaptım. Karşıma **WPScan** çıktı. WPScan'ın nasıl kullanılacağını pek bilmesem de Youtube'da biraz araştırma ile işime yarayabilecek bir kaç komut buldum ve taradım bizim linki.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/7.png)

WPScan'den gelen sonuca göre bu makineyi oluşturan arkadaş öntanımlı kullanıcı adı ve parolayı değiştirmemiş.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/8.png)

Elde ettiğim **admin/admin** kullanıcı adı ve parola ikilisi ile panele yani 
```
http://192.168.1.106/wordpress/wp-login.php
```
adresine (URL'deki 192.168.1.106 kısmı makinenin IP adresi) giriş yapabildim. Şimdi hedef sisteme shell erişimi elde etmek için neler yapabiliriz onu düşünmek kaldı. Elimde yönetici paneline yetkili kullanıcı ile erişim elde edebildiğim bir wordpress sitesi vardı. Ben de geçmiş tecrübelerime dayanarak php shell'e yöneldim. Tarayıcı üzerinden erişebildiğim bir yere sistem komutları çalıştırabileceğim ya da doğrudan sisteme bağlantı elde edebileceğim zararlı kodlar barındıran bir php dosyası üretmem gerekiyordu. Bunun için de **msfvenom** aracını kullandım.  

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/9.png)

Ardından, wordpress panelinde tema ayarlarından son kullanıcıya gösterilen 404 hata sayfasının kodlarına küçük bir müdahalede bulunarak bir önceki aşamada msfvenom ile ürettiğim zararlı php kodunu buraya yapıştırdım. Böylelikle sitede varolmayan bir URL'e ulaşmak istediğimde Wordpress bana bu 404 sayfasını dönecekti. Yani benim zararlı kodum çalışacaktı.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/10.png)

Bu aşamada, var olmayan bir URL'e istekte bulunduğumda wordpress bana 404 hata sayfasını dönecekti. 404 hata sayfasının değiştirilmiş içeriğinde ise sistemime doğrudan bağlantı isteği gönderecek php kodu vardı. Yani benim önce dinlemeye geçmem lazım ki 404 hata sayfasına istek gönderdiğimde, php kodu çalışıp bana ulaşabilsin. Bu nedenle Metasploit Framework içerisinde bulunan **exploit/multi/handler** modülünü msfvenom ile oluşturduğum php shell'e göre ayarladım.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/11.png)

Ziyaret ettiğim sayfa bana 404 hatasının msfconsola ulaşmadığını görüp dinlemeye başladım.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/12.png)

Handler bağlantıyı yakaladı!

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/13.png)

Geriye iki adım kaldı. İlki çok vakit almıştı, şimdi hedef ikincisindeydi "root olmak" bunun için web sitesine
biraz göz gezdirdim. Meterpreter erişimi üzerinden ilerlemeye karar verdim.   
```python
python -c 'import pty;pty.spawn("/bin/bash")'  
```  
komutu ile etkileşimli shell'e geçerek daha rahat hareket etmeye başladım ve sistemin içinde bulunan konfigürasyon dosyalarını incelemeye başladım.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/14.png)

Bu basit bir makine dedim kendi kendime. Çok kapsamlı düşünmeye gerek yok, ya oradadır ya burada diye düşünüp, 2 yaşındaki misafir çocuğu edasıyla makinenin içindeki her dosyayı açıp kapatıp oynarken, karşıma bir şey daha geldi. 

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/15.png)

Hemen ardından gelen hunharca kahkahayı da unutmamalı. İşte parola:

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/16.png)

Bulduğum kullanıcı adı ve parolayı kullanarak yalnız parolanın sonundaki ünlem işaretini unutmadığıma emin olarak root oluyorum.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/17.png)

Şimdi sadece flag'i bulmak  kaldı. Makinede root oluduğumda bulunduğum dizini yani /root dizinini kontrol ediyorum. Beni flag karşılıyor.

![]({{ AUCyberClub.github.io }}/assets/img/quaoar/18.png)

Bu makinede böyle hüzünlü bir sonla bitiyor daha nice makinelerde görüşmek üzere ...

---
**[Ahmet Muhammet Kocabıyık](https://twitter.com/KcbykAhmet)** 


