---
layout: post
title: Linux Nedir/Neden?
date: '2021-03-10 22:26:47 +0300'
author: Berkay Çelebi
categories: linux
index: 1
---
<center><h1>Linux Nedir/Neden?</h1></center>

<img src="{{ AUCyberClub.github.io }}/hackingfalan/assets/linux-nedir-neden/2021-03-12-linux-nedir-neden-2.jpg" width="" alt="alt_text" title="image_tooltip">

<p>
Linux'un ne demek olduğunu ve neden kullanılması gerektiğinden bahsetmeden önce
yazmış olduğumuz “GNU/Linux ve Özgür Yazılım”  ve “Linux Sistemi” başlıklı
yazılarımızı okumanızı şiddetle tavsiye ediyorum çünkü burada bahsedeceğimiz
Özgür Yazılım, Açık Kaynak, işletim sistemi gibi birçok terimin üstünde
duracağız.
</p>
<h3>Linux Nedir?</h3>
<p>
Çok sade ve anlaşılır bir soru: Linux Nedir? Kısaca linux, bir işletim sistemi
çekirdeğidir. Böyle söylendiği zaman hiçbir şey çağrıştırmadığının farkındayım.
Çekirdek dendiği zaman önemli bir işe yaradığını anlıyoruz fakat bu “çekirdek”
dediğimiz şeyin tam olarak ne işe yaradığına bir bakalım.
</p>
<h3>Çekirdek(Kernel) Ne İşe Yarıyor?</h3>
<p>
	“GNU/Linux ve Özgür Yazılım” başlığında kısaca işletim sistemlerinin tarihinden
bahsetmiştik ve çekirdek ve kabuk gibi şeylerle birlikte işletim sistemlerinin
daha karmaşık ama bir o kadar da kullanışlı bir hal aldığını söylemiştik.
</p>
<p>
	Kernel, yani çekirdek; basitçe, donanım ile uygulamalar arasında köprü görevi
gören bir yazılımdır. Yani kernel sayesinde ekrana “Merhaba Dünya” yazdırmak
için ekran kartına “bunu yap”, ya da monitöre “ekran kartı bu çıktıyı verdi bunu
al yazdır” gibi emirler vermemiz gerekmiyor. Aslında çekirdek dediğimiz şey
bundan ibaret! Peki bir de kabuk(shell) dediğimiz bir şey var. Bir de kısaca
bunun görevine bakalım.
</p>
<h3>Kabuk(Shell) Ne İşe Yarıyor?</h3>
<p>
Kabuk da aslında kernel ile kullanıcılar ve uygulamalar arasındaki köprüyü kuran
yazılım olarak tanımlanabilir. Aşağıdaki fotoğraf çok basit bir şekilde ne demek
istediğimizi açıklar nitelikte. Shell’e komutu veririz, shell bu komutu kernel’a
iletir ve sonrasında yapmak istediğimiz işlem gerçekleşir.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/hackingfalan/assets/linux-nedir-neden/2021-03-12-linux-nedir-neden-1.png" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Modern işletim sistemlerinin birçoğu bu mantıkla çalışmaktadır. Örnek olarak en
çok kullandığımız Windows, MacOS, İOS, Android; kernel-shell yapısındaki işletim
sistemlerinden bazılarıdır.
</p>
<p>
Daha fazla detay için(linux sistemi yazısı)
</p>
<p>
Peki Windows ya da MacOS değil de neden Linux kullanmalıyız? Linux “tabanlı”
işletim sistemlerinin artıları ve eksileri nelerdir? Şimdi de buna bakalım.
</p>
<h3>Güvenli - Özgür - Güvenilir</h3>
<p>
Linux tabanlı işletim sistemleri için en önemli üç özelliğin başlıktakiler
olduğunu düşünüyorum.
</p>
<p>
<strong>Linux güvenlidir</strong>
</p>
<p>
Linux tabanlı bir işletim sistemi kullandığınız zaman çeşitli güvenlik riskleri
ile karşılaşma ihtimaliniz dramatik şekilde düşer. Açık Kaynaklı olduğu için
geliştirilme sürecinde çıkabilecek potansiyel güvenlik açıkları herkes
tarafından görülebildiği için kısa sürede kapatılabilir. Devasa boyutta
satırlarca koddan oluşan bu çekirdeği stabil tutmak çok zor olduğu için tamamen
güvenlidir diyemeyiz fakat diğer işletim sistemlerine kıyasla çok daha güvenli
olduğunu söyleyebiliriz.
</p>
<p>
<strong>Linux Özgürdür </strong>
</p>
<p>
Linux bir özgür yazılımdır. İşletim sistemini kullanırken istediğiniz parçasını
değiştirebilir güncelleyebilir ve paylaşabilirsiniz. GNU/Linux dağıtımlarının
içeriğinde yine birlikte gelen birçok 3. parti özgür yazılımlar ile lisans ve
anahtar gibi dertlerle uğraşmak zorunda kalmazsınız. Bu yüzden günümüzde birçok
sunucu linux dağıtımlarını kullanmayı tercih etmektedir.
</p>
<p>
<strong>Linux Güvenilirdir</strong>
</p>
<p>
Güvenilir olmak ile güvenli olmak farklı şeylerdir. Linux güvenilirdir diğer
işletim sistemlerine göre çok daha stabildir. Beklemediğiniz hatalar, durduk
yere çıkan mavi ekran hataları olmaz. Hataların sebebini anlamak ve hataları
çözmek görece kolaydır.
</p>
<p>
Linux işletim sistemi kullanmaya başladığınız zaman fark edeceğiniz ilk şey
özgürlük olacaktır. Bazı basit şeyleri terminalden yapmak başta size çok
zahmetli ve anlamsız gelecektir fakat zamanla bunun çok daha pratik olduğunu
fark edeceksiniz. Diğer işletim sistemlerini kullanmak araba sürmek ise linux
kullanmak uzay gemisi kullanmak gibidir.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/hackingfalan/assets/linux-nedir-neden/2021-03-12-linux-nedir-neden-6.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<h3>Peki nasıl indireceğim?</h3>
<p>Eğer bir Linux dağıtımı indirecekseniz öncelikle çekirdeğin tek başına bir
anlamının olmadığını hatırlatmak isterim. Bu yüzden geliştiriciler çeşitli
amaçlara yönelik çeşitli GNU/Linux dağıtımları(distro) çıkarmışlardır. Bunlardan
En popülerlerinden bazıları:</p>
<h4>Ubuntu</h4>
<p>

<img src="{{ AUCyberClub.github.io }}/hackingfalan/assets/linux-nedir-neden/2021-03-12-linux-nedir-neden-4.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Artık duymayan kalmamıştır herhalde. Minimalist bir tasarımla gelen ubuntu, yeni
sürümler ve arayüz güncellemeleri ile modern bir işletim sisteminde olması
gereken(uygulama marketi, kişiselleştirme gibi) her şeyi de beraberinde sunuyor.
İlk defa bir Linux dağıtımı kullanacaksanız tavsiyem kesinlikle Ubuntu olurdu.
</p>
<h4>Linux Mint</h4>
<p>

<img src="{{ AUCyberClub.github.io }}/hackingfalan/assets/linux-nedir-neden/2021-03-12-linux-nedir-neden-3.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
	Yine ilk defa Linux işletim sistemini kullanacak olan kullanıcılar için
biçilmiş kaftan diyebiliriz. Linux Mint da Ubuntu gibi genel amaçlı bir kullanım
sunuyor ve arayüz tecrübesi olarak Windows’a yakın bir deneyim sunuyor
</p>
<h4>Kali Linux</h4>
<h4>

<img src="{{ AUCyberClub.github.io }}/hackingfalan/assets/linux-nedir-neden/2021-03-12-linux-nedir-neden-7.png" width="" alt="alt_text" title="image_tooltip">
</h4>
<p>
	Siber güvenlik topluluğu olup da Kali Linux’tan bahsetmezsek olmaz. Kali linux
bir siber güvenlik uzmanı için gerekli olacak neredeyse tüm temel “tool”ları
beraberinde getiriyor ve bunları sınıflandırarak basit bir arayüzde sunuyor.
Kali ve kullanımı başlı başına bir konu olacağı için burada saygımızı sunuyor ve
devam ediyoruz.
</p>
<h4>ParrotOS</h4>
<h4>

<img src="{{ AUCyberClub.github.io }}/hackingfalan/assets/linux-nedir-neden/2021-03-12-linux-nedir-neden-5.jpg" width="" alt="alt_text" title="image_tooltip">
</h4>
<p>
Ve benim favorim, kalbimin fatihi ParrotOS… ParrotOS da aynı Kali gibi ofansif
güvenlik ve defansif güvenlik araçları ile birlikte geliyor. ParrotOS’un farkı
ise kali’ye oranla çok daha fazla tool bulundurması. Bunun yanında yazılım
geliştirmek için de birçok modül de yüklü halde geliyor. Ayrıca çok daha az
kaynak kullanan bir işletim sistemi. Fakat Kali ile karşılaştırıldığı zaman en
büyük eksisi az sayıdaki destekçi. Bu yüzden bazı zamanlar karşılaşılan buglar
çok can sıkıcı olabiliyor.
</p>
<p>
Başlangıç için bu işletim sistemlerini Windows ya da Mac kullanırken
deneyebilmek için VMWare ya da VirtualBox gibi emülatörler kullanarak sanal
olarak çalıştırmanızı öneririm.
</p>
<h3>Peki Hangisi Bana Uygun?</h3>
<p>
Kendi kişisel tavsiyem eğer ki bir yandan linux öğrenip bir yandan da siber
güvenlik ile ilgilenecekseniz Kali Linux başlangıç ve sonrası için hayatınızın
sonuna kadar size yeterli olabilecek güçte bir işletim sistemidir. Fakat farklı
amaçlar için kendinize uygun bir dağıtım arıyorsanız binlerce farklı dağıtım
var. Eninde sonunda kendinize en uygun olanı bulacağınızdan eminim.
</p>
<h3>Eksileri hiç mi yok?</h3>
<p>
Elbette var! Linux işletim sistemlerinin belki de en büyük eksikliği uygulama
eksikliği. Pazar payından dolayı geliştiriciler Windows ve Mac gibi işletim
sistemlerine uygulamalarını geliştirmeyi daha karlı olduğu için tercih
ediyorlar. Bu yüzden de her uygulamayı bulmak mümkün olmuyor. Fakat iyi yanı
ise; yapılmış birçok uygulamanın özgür alternatifleri de saymakla bitmez. Bunun
yanında eğer ki bir geliştirici iseniz şartlar sizi bir şekilde linux kullanmaya
itecektir.
</p>
<h3>Sonuç</h3>
<p>
Bu yazımızda size Linux’un ne olduğunu ve neden kullanılması gerektiğinden
bahsettik. Birçok artısının yanında eksilerinin de olduğu bir gerçek fakat bu da
yine özgür yazılım felsefesinin benimsenmemesinden kaynaklı bir yanılgı. Umarız
her geçen gün farkındalığı daha da artan özgür yazılım felsefesi bir gün
GNU/Linux dağıtımlarının hak ettiği yeri bulmasını sağlar ve çok daha özgür bir
gelecek bizi bekler.
</p>