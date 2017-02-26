---
layout: post
title: HackThis Walkthrough Part 2
date: '2017-02-26 20:09:42 +0300'
categories: blog
---




Merhabalar,

Bu ikinci walkthrough yazımda, **hackthis.co.uk** sitesinin ikinci partı olan **basic level** seviyesindeki
soruları inceleyeceğiz.
**main level**'e nazaran basic level biraz daha bilgi birikimi gerektiriyor.

**Basic Level 1**

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/1.png)


Ilk soruda bize bir metin belgesi veriliyor ve içinden username ve password çıkarmamız isteniyor.
Dosyanın içindeki **string** değerlerini görmek için terminalden **strings** komutuyla
dosyayı inceliyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/2.png)

FFFF gibi anlamsız bir string değeri çıkıyor. Bu durumda farklı seçenekleri değerlendirmemiz gerekiyor.
Dosya gerçekten bir txt dosyası mı görmek için terminalden **file** komutuyla dosyanın tipine bakıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/3.png)

**bitmap** kelimesinden anlayacağımız üzere bu bir metin belgesi degil resim dosyası.
Dosyaya sağ tıklayıp **ImageMagick** programı ile açtığımda gerekli bilgiler geliyor.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/4.png)


**Basic Level 2**

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/5.png)

Bu sorumuz **User Agent**ler ile ilgili bir soru.

``` Kullandığımız internet tarayıcılarının tümü içerisinde bir User Agent, yani kod dizgisi/string barındırır. Bu kod dizgisi yardımıyla bağlanmaya çalıştığımız web sunucusu tıpkı IP adresimizde olduğu gibi bizim hangi tarayıcıyı ve hangi işletim sistemini kullandığımızı öğrenir.```

Soru bizden farklı bir **secure_user_agent** user agent bilgisini kullanarak siteye bağlanmamızı istiyor. 
User Agent değiştirmek ve/veya eklemek için çeşitli switcherler mevcut. Basit olarak **chrome** ve **firefox** için 
googleda aratırsanız eklenti olarak tarayıcınıza ekleyebilirsiniz.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/6.png)

Ekleme işlemini yaptıkdan sonra , **Switcher**ı açıp kendimize yeni bir user agent ekliyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/7.png)

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/8.png)

Daha sonra bu user agent'ı kullanarak siteye tekrar giriyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/9.png)




**Basic Level 3**

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/10.png)

Bu soruda soruyu tamamlayabilmemiz için **194175** puana sahip olmamız gerektiği yazıyor.
Ilk başta pek göze çarpmasa da **final score** kısmının altındaki **submit** kısmı tıklanabiliyor.
Burdan şu anlamı çıkarabiliriz , bir bilgi gönderiyoruz buda bir **POST** isteği demek.
Submit kısmına tıkladığımda arka planda neler gittiğini görmek için **tamper data** eklentisini kullanıyorum.

``` Tamper data : HTTP/HTTPS başlıklarını ve POST/GET parametrelerini izleyip, değiştirmeye ve kaydetmenize yarayan bir eklentidir.```

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/11.png)

**Start Tamper** kısmına tıkladıkdan sonra submit kısmına tıklıyorum ve giden **POST** isteğini görüyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/12.png)

**POST** isteğindeki değeri sitenin bizden istediği **194175** değeriyle değiştiriyorum ve soru böylece bitmiş oluyor.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/13.png)

**Basic Level 4**

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/14.png)

Bu soruda bize bir **jpg** dosyası veriliyor.Ilk soruda yaptığımız gibi öncelikle bunun gerçekten bir **jpg**
dosyası olup olmadığını kontrol etmek için terminalden **file** komutunu kullanıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/15.png)
Dönen sonuca göre bu dosya gerçekten bir **jpg** dosyası.Bu durumda yine farklı seçenekleri düşünmemiz gerekiyor.Içinde bir **string** değeri saklayabileceğini düşünerek dosyası **strings** komutuyla kontrol ediyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/16.png)



![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/17.png)

Içinden çıkan bilgilere göz attığımızda bir kaç farklı olası username görünüyor. Username'in tek kelime olacağını varsayarak **username** olarak **james**i aliyorum.
**Password** olarak da bir kaç denemenin ardından **chocolate**'nın doğru password olduğunu buluyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/18.png)

**Basic Level 5**

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/19.png)

Önceki soruda olduğu gibi yine bir **jpg** dosyası verilmiş. Dosyayı **file** komutuyla incelediğimde gerçekten bir **jpg** dosyası olduğunu görüyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/20.png)

Yine farklı seçeneklere yöneliyorum ve içinde herhangi bir **text**,**zip** vs saklanmış mı bakmak için terminalden **binwalk** komutunu kullanıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/21.png)

Resim dosyasının içine gömülmüş bir **zip** dosyası görüyoruz. Bu durumda bunu çıkarmak için sadece **unzip** komutunu kullanmam yeterli olacaktır.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/22.png)


**Basic Level 6**

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/23.png)

Bu soruda bizden site hakkında bazı bilgileri toplamamız isteniyor. Ip bilgisini almak için terminalden **ping** komutunu kullanıyorum.

```Ping : Karşı IP ye ufak veri paketleri gönderip, alarak baglantiyi test eder.```

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/24.png)

Ilk bilgiyi elde ettik.Şimdi siteye hosting hizmeti veren company'i bulmamız gerekiyor.Bu bilgiye online olarak bazı sitelerden erişebilirsiniz.
Googleda ufak bir arama yaparak **http://whoishostingthis.com/** sitesini buldum.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/25.png)

Ve geldik son bilgiye , **X-B6-Key** uzunca bir süre ne olduğunu anlayamadığım bu header'ı bir kaç kişiye danıştıktan sonra emaillerde bulunduğunu
öğrendim. Yani bu durumda siteden bir email almam gerekiyordu. **Forgot password** sekmesinden kendime bir parola sıfırlama **emaili** gönderttim.
Gelen emailin kaynağını incelediğimde **X-B6-Key** bilgisini gördüm.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/26.png)

**Basic Level 7**

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/27.png)

Sorudaki **suspicious services** ipucundan yola çıkarak , **nmap** veya **zenmap** kullanmam gerektiğini düşündüm.

```Nmap : Taranan ağın haritasını çıkarabilir ve ağ makinalarında çalışan servislerin durumlarını, işletim sistemlerini, 
portların durumlarını gözlemleyebilir.
Zenmap : Nmap'ın grafik ayaryüzlü versiyonu.```

Tarama yaptığımda ilginç bir sonuç ile karşılaştım.

![]({{ AUCyberClub.github.io }}/assets/img/hackthispart2/28.png)

Welcome weary traveller. I believe you are looking for this : **mapthat**.

mapthat keywordunu flag olarak kullandım ve bu soruda böylece bitmiş oldu.


---
**[Engin Demirbilek](https://twitter.com/Hyal0id)**
---
