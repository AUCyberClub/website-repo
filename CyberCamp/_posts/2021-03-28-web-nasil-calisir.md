---
layout: post
title: Web Nasıl Çalışır?
date: '2021-03-28 22:02:47 +0300'
author: Berkay Çelebi
categories: web
index: 2
---


<h1>Web Nasıl Çalışır?</h1>
<p>
Bilgisayarın başına oturduk ve bir şeyi merak ettik: Web Nasıl Çalışır? Bunu
anlamak için tarayıcımızı açtık, google’a girdik, sonra “Web Nasıl Çalışır”
yazdık ve karşımıza en üstte bu yazı çıktı ve tıkladık okumaya başladık diyelim.
Bu yazıda, bu yazıyı okuyabilmemiz için arkada nelerin çalıştığını ve bunların
nasıl çalıştığını anlamaya çalışacağız.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/2020-03-28-web-nasil-calisir/image2.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
	İlk olarak adım adım neler olduğunu anlamamız lazım. Sonrasında ise bu olan
şeylerin nasıl olduğuna bakacağız.
</p>
<p>
Bu yazıyı açmak için linke tıkladık:
</p>
<p>
1-> Tarayıcımız (Google Chrome,Firefox,Opera vs.) tıklama sinyalini anladı
bununla ilgili veriyi işletim sistemimize gönderdi.
</p>
<p>
2-> İşletim sistemimiz paketi aldı modeme gönderdi
</p>
<p>
3-> Modemimiz bu paketi aldı ve internete gönderdi
</p>
<p>
4-> İnternette paket yolunu buldu sunucu paketi anladı cevabı geri internete
gönderdi
</p>
<p>
5-> Paket tekrardan modeme modemden bilgisayarımıza, ordan işletim sisteminden
tarayıcımıza geldi ve ordan da ekrana sayfamız geldi.
</p>
<p>
	Böyle bakıldığı zaman bi sinyal bizden sunucuya sunucudan bize geliyor. Basitçe
olan şeyler bu fakat kısaca 5 adımda özetlediğimiz bu olaylar zincirinde
“aldı,anladı,buldu” gibi bazı kelimeler kullandık. Bilgisayar bilimlerinde
maalesef anladı deyince kurtulmak olmuyor. Şimdi de daha derinden neler olduğuna
bakalım.
</p>
<p>
	Her şey yazıya tıklamamızla başlıyor. Ulaşmak istediğimiz site “<a
href="www.aucyberclub.org">www.aucyberclub.org</a>” olsun. Tarayıcımızın ilk
görevi bu adresin IP adresini bulmak. Bunun için “<strong>cache</strong>”
dediğimiz bir tabloya bakıyor ve daha önce bu siteye girmişsek hiç uğraşmadan ip
adresini buluyor. Eğer ki bulamazsa işletim sistemimize soruyor ve eğer işletim
sistemimiz de daha önceden hiç gidilmemişse o zaman işler karışıyor.
</p>
<h4>DNS(Domain Name System)</h4>
<p>
Ev telefonlarının ilk yaygınlaştığı zamanlarda insanlar birinin telefon
numarasını bulmak için dağıtılan adres defterlerinden alırmış ve aradığı
numarayı oradan bulurmuş. DNS dediğimiz şey de aynı işi yapan bir çeşit adres
defteri sistemi. “aucyberclub.com” aradığımız yer ve bu sitenin tam adresini
bulabilmek için; belli bir hiyerarşiye sahip olan bu DNS sunucularına sormamız
gerekiyor ve böylece adresin tam yerini bulabilmemiz mümkün oluyor.
</p>
<p>
<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/2020-03-28-web-nasil-calisir/image3.png" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
Şimdi DNS’in ne olduğu hakkında birazcık fikrimiz var ve modemimiz de paketi
göndermek için hazır. Modemi aldığımız zaman o hiç dokunmadığımız internet
kablosunun nereye gittiğini açıklama vakti geldi.O kablo kullandığınız internet
servis sağlayıcısına gidiyor. Evet öyle çok da ilginç bir şey değil. Bu kablo
sayesinde modemimiz, internet servis sağlayıcısı(ISP)’nin “DNS Çözümleyici”
dediğimiz sunucuları üzerinden gitmek istediği adresi öğrenebiliyor. DNS
Çözümleyici’yi de bilgisayardaki “cache”in büyük hali gibi düşünebiliriz.
Diyelim ki burası da bulamadı o zaman önce Root Server dediğimiz bir üst
sunucuya soruyor, orda da yoksa bir üstteki Top Level Domain(TLD) sunucularına
soruyor.O da bilemezse en son Authorative Name Server dediğimiz bi sunucu bize
söylüyor. Yani dediğimiz gibi o ona soruyor o ona soruyor ve biri diyor ki
sonunda abi ben biliyorum onun adresi ***.***.***.** diyor ve tekrar adres bizim
işletim sistemimize kadar ulaşıyor.
</p>
<p>
Daha hiçbir şey olmuş değil. Nereye göndereceğimizi öğrendik şimdi ne
istediğimizi sunucuya iletmek için paketi oluşturmamız gerekiyor.
“aucyberclub.org” güvenli bir site olduğu için https ile bağlanmamız gerekiyor.
Şimdi işler biraz daha teknik olmaya başlıyor.
</p>
<p>
HTTPS için paketlerimizin şifrelenmesi ve bunların SSL ya da TLS dediğimiz
protokoller üzerinden şifrelenmiş haliyle aktarılması gerekiyor. Böylece
“ortadaki adam saldırıları” gibi saldırılardan korunmuş oluyoruz. Protokol mü
adam mı? diye soruyorsanız Network101 yazımızı okumanızı öneririm.
</p>
<p>
Son olarak paketimizi oluşturabilmemiz için bir takım metodları öğrenmemiz
gerekiyor:
</p>
<p>
<strong><span style="text-decoration:underline;">GET :</span></strong> URI
kullanarak belirli bir sunucudan bilgi istemek için kullanılır. GET isteği ile
sadece veri alırız ve herhangi bir değişiklikte bulunmayız.
</p>
<p>
<strong><span style="text-decoration:underline;">DELETE : </span></strong>Adı
üstünde karşı sunucudan bir şey silmek için kullanılır.
</p>
<p>
<strong><span style="text-decoration:underline;">PUT : </span></strong>Sunucuda
veri oluşturmak ya da güncellemek için kullanılır.
</p>
<p>
<strong><span style="text-decoration:underline;">POST : </span></strong>Post da
sunucuda veri oluşturmak için kullanılır.
</p>
<p>
Şimdi biz sadece linke tıkladık ve sayfayı görmek istiyoruz. Bu yüzden GET
isteğinde bulunacağız. Paketimizi hazırladık ve fırlatmaya hazırız.
</p>
<p>
Paketi fırlatmadan önce bilmemiz gereken bir şey var, sunucu şu an açık mı? Bizi
kabul edecek mi? Bunları öğrenmemiz için öncelikle sunucuyla aramızda TCP
bağlantısı kurmamız gerekiyor. TCP’nin ne olduğunu merak ediyorsanız yine
Network101 yazımızı okuyabilirsiniz. TCP bağlantısını kurduktan sonra HTTP
paketimizi göndermeye hazırız. Paketi modemden adrese gönderdik ISP üzerinden
kablolar aracılığıyla o routerdan bu router’a derken paketimiz gideceği yere
ulaştı.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/2020-03-28-web-nasil-calisir/image1.jpg" width="" alt="alt_text" title="image_tooltip">

</p>
<p>
Yukarıdaki fotoğraftaki diz üstü bilgisayarların olduğu tarafı bizim kendi
evimiz, diğer tarafı da  ,duvar da dahi,l ulaşmak istediğimiz sunucu olarak
düşünelim.
</p>
<p>
Paketimiz sunucu tarafına ulaştığı anda bu duvara toslayacak. Bu duvar
birçoğumuzun duyduğu o malum Firewall(Güvenlik Duvarı,Ateş Duvarı). Firewall’un
basitçe yaptığı şey aslında şu şu portlardan, şu şu adreslerden gelen paketlere
izin ver diğerlerine izin verme demek. Bizim paketimizi firewall inceledikten
sonra uygun olduğuna karar verdikten sonra içeri alacak. İçerisi de birçok
farklı görev için gruplandırılmış çeşitli bilgisayarlardan oluşuyor. Mesela web
sayfasındaki fotoğraflar için farklı bir sunucu, oturum için farklı bir sunucu
olabilir. Bu, sunucu sisteminin tasarımına göre değişebilir. Biz şimdilik basit
gidelim bir tane içinde Apache(bir çeşit web sunucusu) yüklü olan bir
bilgisayara ulaştığımızı varsayalım. Paketimiz bu yazılıma ulaştıktan sonra
yazılım bizim gönderdiğimiz paketin içeriğini okuyacak: “hmm GET aucyberclub.org
demiş, o zaman bu siteyi ona geri gönderelim diyecek” o sırada aramızdaki TCP
bağlantısı da devam ettiği için bizimle iletişimin kopmadığından emin olunca o
da yine bir paket oluşturacak ve o paket sunucudan bize kadar yine uzuun bir
yoldan geçip gelecek. Bize ulaştıktan sonra da yine işletim sistemimiz
tarayıcıya bu paketi ulaştıracak. Tarayıcımız da bu paketi içindeki motor
sayesinde ekrana yansıtacak.
</p>
<p>
Bu şekilde anlatılınca bile aslında çok yüzeysel kalan birçok konu var. Fakat
kendi başına bir ders olarak okutulan webin nasıl çalıştığını her ayrıntısı ile
tek yazıda anlatmak mümkün değil. Bu yüzden takipte kalın ve daha da derine
ineceğimiz diğer yazılarımızı bekleyin.
</p>