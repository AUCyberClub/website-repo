---
layout: post
title: Lazysysadmin Walkthrough
date: '2018-01-16 16:00:00 +0300'
categories: cozumler
---


Merhabalar,  
İlk yazım olan Lazysysadmin makinesinin çözümünü sizlerle paylaşacağım. Bu makinedeki amaç root dizini altındaki proof.txt dosyasına erişmek.  
Makineye şuradan erişebilirsiniz: 

[Vulnhub](https://www.vulnhub.com/entry/lazysysadmin-1,205/)


Nmap taraması yaparak işlemlerime başladım: 

```
nmap -n -p1-655535 -sV 192.168.24.1/24
```

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/1.png)


İlk bakışta **ssh(22)**, **http(80)**, ve **mysql(3306)** portları dikkatimi çekti. Belki ssh üzerinden bir brute-force saldırısı yapabilirim diye düşünürken, mysql ve http servisinin güzelliğine kapılıp web üzerinden işlemlerime başlamaya karar verdim.

Tarayıcım ile  hedefin 80 numaralı (http) portuna bağlandığımda beni şöyle bir sayfa karşıladı:

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/2.jpg)

Sayfa üzerinde ne kadar debelendiysem debeleneyim manuel olarak bir şey bulamadım, belki işime yarayacak birkaç ayrıntı bilgiye ulaşabilirim ümidiyle **nikto** aracını kullanmaya karar verdim.

```
nikto -h 192.168.24.128
```

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/3.jpg)

Sonuçta ilk gözüme çarpan detaylar, **robots.txt**, **wordpress**, ve **phpmyadmin** dosya ve dizinleri oldu.
Belki birkaç ipucu çıkartırım heyecanıyla hemen robots.txt dosyasını kontrol ettim.

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/4.jpg)

Fakat içinden çıkan hangi dizine gittiysem gideyim işime yarayabilecek hiçbir şey elde edemedim. Wordpress dizinine gittiğimde ise beni klasik bir wordpress sayfası karşıladı.

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/5.jpg)

Yaklaşık 100 tane alt alta yazan ***My name is togie*** yazısından yola çıkarak odaklanmam gereken kullanıcının **togie** olduğu kanısına vardım.  
Belki bu kullanıcıya ait basit bir parola bulabilmek amacıyla varsayılan wordpress giriş sayfasını kontrol ettim **(/wp-login.php)**. Evet default giriş sayfası vardı fakat ne kadar brute-force yaptıysam yapayım ne giriş sayfası üzerinde ne de **phpmyadmin** üzerinde herhangi bir geçerli giriş bilgisi elde edemedim. Web üzerinde umutsuzca biraz daha vakit geçirdikten sonra **nmap** taramasında çıkan **SMB(139,445)** servisi aklıma geldi. Web üzerinde ki umutlarımın tükenmesininde etkisiyle SMB servisine yöneldim ve **enum4linux** aracı ile bilgi toplamaya başladım.

```
enum4linux 192.168.24.128
```

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/6.png)

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/7.jpg)

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/8.jpg)

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/9.jpg)

Yaptığım tarama sonucunda, 2 adet user ve 3 adet de share noktasının bilgisine ulaştım. SMB share noktalarını nasıl kullanacağım ile ilgili yeteri kadar bilgim yoktu, bu yüzden biraz googleda araştırma yaptıktan sonra bu noktalarla ilgili ekstra bilgi edinebilmek için **smbmap** aracını buldum.
Aracı kullandığımda bana **share$** noktasının **READ-ONLY** olduğu bilgisini verdi.

```
smbmap -H 192.168.24.128
```

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/10.jpg)

Yani bir şekilde burada paylaşılan dosyalara erişip okuyabilirdim. Yine ufak bir google araştırması sonucunda GNU/Linux terminal üzerinden share noktalarına erişmek için **smbclient** isimli yazılımı kullanabileceğimi öğrendim ve bu aracı kullanarak **share$** noktasına bağlandığımda:

```
smbclient \\\\192.168.24.128\\share$
```

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/11.jpg)

Web dizinin dosyalarına eriştim !  
Hemen içerdeki dosyaları kurcalamaya başladım ve **deets.txt** dosyasını açtığımda:

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/12.jpg)

Beni bir mesaj ve bir parola karşıladı.  
Peki 12345 neyin parolasıydı?  
Daha önceden tespit ettiğim userlardan(togie, nobody) birinin parolası olabilir diye heyecana kapılarak hemen web üzerinde **/wordpress/wp-login.php** sayfasına koştum, fakat yine hevesim kursağımda kaldı ve giriş yapamadım. 
Bu parolayı başka nerede kullanabilirim diye düşünürken aklıma hiç uğramadığım ssh servisi geldi;
togie ve nobody kullanıcılarıyla sisteme bağlanmaya çalıştım ve
**togie:12345** giriş bilgilerini kullandığımda:

```
ssh togie@192.168.24.128
```

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/13.jpg)

sisteme giriş yapabilmeyi başardım fakat aldığım shell yetkileri oldukça kısıtlı olan bir **rbash**ti.


Shellimiz **rbash** olmasına karşın, sudo komutu kullanma yetkim vardı. Çok zaman kaybetmeden **sudo su** komutu ile yetkilerimi root yetkilerine yükseltip **proof.txt** ye ulaştım.

![]({{ AUCyberClub.github.io }}/assets/img/lazysysadmin/14.jpg)


 ---
 **[Sema ÖRNEK](https://twitter.com/semarnek)**
