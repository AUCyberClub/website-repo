---
layout: post
title: Blockchain ve Bitcoin
date: '2021-03-28 22:00:47 +0300'
author: Can Öztaş
categories: blockchain
index: 1
---

<h4><center><strong>BlockChain ve Bitcoin</strong></center></h4> 

Blokzincir, kriptografi ile bağlanan artan bir kayıt listesi, kayıt tutma biçimidir. Günümüzde bu kavramı en çok bitcoin kriptoparası ile duyuyoruz. Bu yazıda blockchain'in genel özelliklerini verirken, örnek uygulamalarda ise bitcoin'i örnek vermeyi düşünüyorum. Blockchain sadece para işleri için değil, seçimlerden tutun sağlık alanına aslında veri saklamak istediğimiz her yerde kullanabileceğimiz bir sistematik. Bu sistematik'in özelleşmiş halini bitcoin olarak düşünmenin pek yanlış olmayacağını düşünüyorum, dolayısıyla yazıda blockchain'in temel özelliklerinden bahsederken, daha somutlaştırmak için bitcoin'i de anlatacağım. Yazının son kısmında iste daha az teknik bitcoin ve belki de bitcoin kültürü diyebileceğimiz konularına değineceğim.


Problemimiz şu, veri saklamak istiyoruz, ki bu yazıda bitcoin üzerinden gideceğiz. Bunun için bir ağa ihtiyacımız var. Ağı kurma prensibi olarak alışa geldiğimiz "centralized" sistemlerde güvenlik problemi tüm verinin aynı yerde yani merkezileşmiş yerde tutulmasıdır. Verinin tutulduğu yerde yaşanacak bir siber saldırı, elektrik kesintisi, problem tüm sistemimizi bozacaktır. Oysa bu işi bir ağdaki bir sürü donanıma ki buna "node" diyeceğiz, yaptırmak için ilk fikir 1982 yılında atıldı. 1992 yılında bu tasarım Merkle Ağaç'ları eklenmesiyle problemimiz çözüme çok yaklaştı, 2008 yılında ise Satoshi Nakamoto Bitcoin kavramını ortaya çıkarak günümüze getirdi.

Veriyi ağda dağıtık bir şekilde tutmamız gerektiğini anladık. Bunu başarabilmek için verinin tüm donanımlarda aynı anda aynı şekilde olması lazım, aksi takdirde verimizin doğruluğuyla ilgili problem yaşarız. Biz bir veri saklamak istiyoruz, ki bitcoin örneğimizde bu veri aslında kimin ne kadar bitcoin'i olduğudur. Kimin ne kadar bitcoin'i olduğunu yapılan tüm işlemlere (transaction) bakarak anlayabiliriz. İşte bu noktada karşımıza ledger(hesap defteri) kavramı çıkıyor. Aslında biz yapılan her birim işlemi ledger'a, ledger belirli bir uzunluğa gelince bu işlemleri de blok'a eklemek istiyoruz. 

**Ledger**

Ledger bu ağdaki herkesin birbirine gönderdiği veriyi tuttuğumuz yapıdır. Başarmak istediğimiz şey bu ağdaki bir sürü makinenin tuttuğu ledger'ların aynı  olmasıdır. Çünkü bu olduğu zaman bu verinin doğru veri olduğuna hepimiz anlaşmış oluruz. Bitcoin'de bu yapıda yapılan transaciton'ları tutacağız yani kimin kime kaç bitcoin gönderdiğini. Ama ağdaki herkeste ledger'ın olması ve kuracağımız yapıda bu ledger'a yeni şeyler eklenmesi şu sorunu ortaya çıkarıyor. _Ben bu ledger'a istediğimi ekleyebilirim, örnek olarak para gibi önemli bir mevzuda ben buraya AUCC Can'a 100 Bitcoin gönderdi yazabilirim._ İşte bu nokta bize Bizanslı General Problemi'ni ortaya çıkarıyor.

Bizanslı General'ler bir kuşatmada, ve bu aşamada atak veya geri çekilme emri verilmesi gerekiyor. Fakat generaller birbirlerine bir noktada bağlı değiller, dağıtık bir yapıdalar. Sadece kendi kararlarını ilan edebiliyorlar. Ve arada bir takım oyunbozucular var. Atak emri verenlere ben de atak veriyorum, geri çekilme emri verenlere ben de geri çekiliyorum diyor. Bu problemi çözebilen sistemlere Bizanslı Hatasına Tolore Sistemler deniyor. Bitcoin böyle bir sistem, bunu ise (yazının son kısmında bahsedeceğim) Cypherpunk akımında gelen Proof-Of-Work (veya alternatifi Proof-Of-Stake gelecekte geçilmesi planlanıyor) sistemi ile sağlıyor.

**Proof-Of-Work**

Problemimiz ortak blokzincirimize eklediğimiz yeni veri için hepimizin aynı fikirde olması. Bunun için en güzel çözümümüz, her yerde duyduğumuz madencilik kavramını da doğuran, bir blok ekleneceği zaman bunu zorlu bir şekilde donanım harcayarak bir bilgisayarın yapması fikri. Bitcoin'in proof-of-work'unden aşağıda söz edeceğim.

Kriptografi herhangi bir verinin belirli kurallara göre gizlenmesidir. Örnek olarak ben ABC için 123 kodladığımı söylersem ve size 123 yollarsam siz bunun ABC anlamına geldiğini bilirsiniz. Tabii ki böyle büyük bir sistemde bu işi bu kadar basit yapamayız. Bitcoin bunun için SHA-256 fonksiyonunu kullanır. SHA-256 olduça komplex ve güçlü bir kriptolama çeşididir. Detaylı bilgi ve hatta pseudo-code'u için : [Buraya](https://tr.wikipedia.org/wiki/SHA-2) bakabiliriz. Hatta python implemantasyonu için : [Burası](https://foss.heptapod.net/pypy/pypy/-/blob/branch/default/lib_pypy/_sha256.py) buraya da bakabiliriz.

SHA-256 girilen veriyi 256 bite çevirir, yani 256 tane 1 veya 0'a. Bu kolay kırılabilecek bir şey gibi ilk başta görünebilir fakat üstel sayılar her zaman şakacıdır, zira bu durumda 2^256 olasılık vardır. 

Bitcoin'de blokzincire yeni bir blok ekleneceği zaman bilgisayar şu soruya cevap arar:

Duyduğun işlemlerden oluşan blok belirli bir büyüklüğe ulaşınca SHA-256 uygulayarak 256 bitlik bir sayı yaratacaksın, fakat bu şifrenin ilk n basamağı 0 olmalı ve bu kuralı sağlayan 256 biti bulmak için, hesap defterindeki blokun sonuna bir sayı eklenmeli, bu sayı nedir ?

**Blokzincirdeki node'larımız yani ledger'ı tutan makinelerimiz ya da madenciliremiz bu nonce değerini bulmaya çalışırlar.** Bu nonce'u ilk bulan ise sistem tarafında bitcoin ile ödüllendirilir. Sonuç olarak sistem bilgisayarının donanım gücü karşısında size bitcoin vermiş olur. 

Bitcoin'de 'n' sayısı ağdaki toplam node sayısına göre değişkenlik gösteriyor ve bu hash rate (birim zamanda yapılan matematiksel işlem) kavramını doğuruyor. Ayrıca burada yine şöyle bir trick doğmuş oluyor, hash kodları on altılık sayı sisteminde (hexadesimal) hesaplandığından n'in her artışında zorluk 16 kat artıyor. Yine üstel oyunlarla görebiliyoruz ki aslında daha çok insan bitcoin kazdıkça (yani nonce aradıkça) daha az blok sisteme ekleniyor, yani sistem daha az ödül vermiş oluyor.

![]({{ AUCyberClub.github.io }}/CyberCamp/assets/blockchain/asdasdasd.png)



<h4>Yazının bu noktasına kadar geldiysek şunu anlamış olmamız gerekiyor. Veriler ledger'lara yazılıyor, belirli bir uzunlukta legder'ları bütün blokzincirimizin sonuna eklemek için için bir proof-of-work, proof-of-stake sistemi var. Peki bu bloklarda ne saklanıyor, kuracağımız blokzincir sistemine göre değişebilir, sonuç olarak veri saklıyoruz fakat bitcoin ve kripto para nezlinde bloklarda ne ve nasıl tutuluyor kısmına giriş yapalım.</h4>


Yazının başına geri dönelim, Can AUCC'ye 2 bitcoin gönderdi, fakat biz sistemimizi anonim ve desantralize kurmak istiyoruz dolayısıyla Can'ın adı veya kimliği bizim için önemli değil. Ama Can'a haydi bir username versek bile, bu biricik (unique) olmalı ledger'a kimse Can adına kafasına göre bir şey eklememeli, işte bu noktada karşımıza iki kavram çıkıyor:



Public ve Private Key, Encryption:

Bu bloklarda işlem saklamak istiyorum ve işlemde 2 tane değişkenim var, parayı yollayan ve para yollanan. Para yollanan için rastgele verilmiş bir açık anahtar (kabaca rastgele bir takım karakterler ki bitcoin için bu 34 hanedir), korkunç sayılarda biricik "hesap numarası" üretmemiz demektir. Açık anahtarımı herkesle paylaşabilirim, birisi bir şey yollayacağı zaman bu açık anahtarıma yollayabilir. Fakat parayı yollayan için sadece yollayanın bilebileceği bir sistem kurmalıyız, private key._


![]({{ AUCyberClub.github.io }}/CyberCamp/assets/blockchain/bitcoin-privatekey-publickey-lock.png)


<h5>Görsel çok güzel anlatılmış, herkesin herkesinkini görebildiği bir public key var, fakat bir şey yollamak için benim kendime ait bir private key'im var</h5>


Fikri uygulamaya geçirirken bir ekleme daha yapmamız gerekiyor, hangi private key'in hangi public key olduğunu bilmeliyim, fakat zıttını asla bilmemeliyim.

Bitcoin temelli bir örnekle gidersek, bitcoin için bir private key 32 bytelık yani 256 bitlik bir sayıdır. Bunu günlük hayatta kullanmak için [WIF](https://en.bitcoin.it/wiki/Wallet_import_format) adı verilen görece basit bir encoding yapılır ki sitesinde bulabiliriz. Public key'ler ise private key'den bir algoritmaya göre üretilir. Bitcoin özelinde ise bunu yaparken Eliptik Eğri Kriptografisi kullanır. Burada K(public key) = k(private key) * G(generator point isimli bir sabit) uygulanır. Bunun tersi yani private key'den public'i bulmak ki terminolojide "finding discrete logarithm" deniyor, bütün olası sayıları denemek kadar zordur ya da bildiğimiz tabir ile brute-force yapmak kadar zordur (ki bu yüzden Eliptik Eğri kriptolojisine terminolojide tuzak kapısı da denir.) Bitcoin spesifik örneğinde bu eğrinin fonksiyonu ve grafiği aşağıda gibidir:

![](https://www.oreilly.com/library/view/mastering-bitcoin-2nd/9781491954379/assets/eq_2.png) 

burada p  =  [secp256k1](https://en.bitcoin.it/wiki/Secp256k1) denilen sayıdır



![]({{ AUCyberClub.github.io }}/CyberCamp/assets/blockchain/mbc2_0402.png)



Burada private key üretilirken Eliptik Eğri Nokta Çarpımı yapılır, bu bildiğimiz çarpma kadar kolay değildir, içerisinde noktalara yapılacak katlama ve ekleme işlemleri bol bol vardır. Detayları için : [Buraya bakabiliriz](https://www.oreilly.com/library/view/mastering-bitcoin-2nd/9781491954379/ch04.html#:~:text=The%20bitcoin%20private%20key%20is,generated%20from%20the%20private%20key).

Public key'imizde olduktan sonra anlaşılması için yine bitcoin örneğinde bunu adrese çevirmek için şöyle bir standart kullanılır:![](https://www.oreilly.com/library/view/mastering-bitcoin-2nd/9781491954379/assets/mbc2_0405.png)



Yani günün sonunda benim için veri yollamak şu anlama gelmiş oldu: "public_keyCan public_keyAUCC'ye 2bitcoin yolladı". Bunu doğrulamak için ise kriptografik imza denilen ve her işlem sonuna yollayanın sadece o işlem için oluşturulmuş özel bir imzası kullanılır. Bu imza oluşturulurken yukarıda bahsettiğim Eiptik Eğri Algoritması (ki biliyoruz tek yönlü çalışıyordu) 'nı biraz gelişmişi Elliptic Curve Digital Signature Algorithm kullanılır. Yine yukarıdaki mantıkla buraya inputlardan birini private key olarak verdiğimizde oluşturacağımız imzadan bizim keyimize ulaşılamayacak, private key'imiz zaten sadece bizde olduğu kimse bu algoritma sonucu bizim imzamızı taklit edemeyecek. O zaman veri yollamak ya da artık bildiğimiz tabir ile "ledger"(hesap defteri)ne bir şey eklemek şu hale gelmiş oldu:

![]({{ AUCyberClub.github.io }}/CyberCamp/assets/blockchain/hash.png)


Görselde de sadece bitcoin olması şart değil herhangi bir şekilde dijital imzaların çalışma mantığını görmekteyiz. Blockchain ve bitcoin için ise imzamız eğer özelliği sağlıyor ise ledger'a bir girdi eklemiş olacağız.

**Ledger'a değer eklemek ve Merkle Ağaçları**

Ledger'a bir değer ekledik ve bunun doğru olduğuna kontrol ettik. Ledger'daki veriler belirli bir uzunluğa geldikten sonra ise bunu yukarıda anlattığımız gibi teknolojimiz temeli olan blokzincirdeki bloklara ekleceğiz ve bloka eklenen her yeni blok yine yukarıda anlattığımız doğrulama sistemi ile hepimizin anlaştığı bir anlaşma olacak. Yine bitcoin için saniyede binlerce işlem yapılıyor ve her bir işlemi tek bir blok gibi eklemek bizim için mantıklı görünmüyor. İşte tam olarak bu noktada yardımımıza merkle ağaçları giriyor. Merkle ağaçları çok kaba bir kolay düşünce ile, yapılan işlemlerin hepsini gösteren bir işlem oluşturma olarak düşünebilir. Ledger'daki bir sürü yollama verimizi (bunlara hash diyelim) blok ekleceğimiz zaman bir merkle ağacı altında toplayıp, blokzincirin sonuna ekleyebiliriz. ![](https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Hash_Tree.svg/1920px-Hash_Tree.svg.png)

Ve aslında sihirli hikayemizin sonuna doğru yaklaşıyoruz, aşağıdaki tabloda bir bitcoin blok içeriğini göreceksiniz, ve tablonun altında da ne yaptık yine basit bir dille tekrarlamaya çalışacağım:

| BITCOIN BLOK İÇERİĞİ |          |                                                              |      |
| -------------------- | -------- | ------------------------------------------------------------ | ---- |
| Sihirli sayı         | 4 byte   | "0xD9B4BEF9" şeklinde sabit değer                            |      |
| Yükseklik            | 4 byte   | Blok numarası                                                |      |
|                      |          |                                                              |      |
| Önceki başlık        | 32 byte  | Önceki blokun başlık özeti (hash)                            |      |
| Merkle kökü          | 32 byte  | İşlemlerin özet değeri (hash)                                |      |
| Zaman damgası        | 4 byte   | 1 Ocak 1970'ten itibaren geçen süre                          |      |
| Zorluk               | 4 byte   | Ağın zorluk bilgisi                                          |      |
| Nonce                | 4 byte   | Ağ zorluğuna göre ayarlanmış rastgele sayı                   |      |
| İşlem sayısı         | 1-9 byte | Belirli uzunlukta tam sayı değeri ([integer](https://en.wikipedia.org/wiki/Integer_(computer_science))) |      |
| İşlemler             | -        | Bloktaki transferlerin listesi                               |      |



<h4>Herkese açık public key ile sadece bana ait private key ile oluşturulmuş dijital imza doğrulaması ile, hesap defterine bir hash ekledim. Bu hash'ler belirli bir uzunluğa gelince merkle ağaçları dediğimiz veri yapısı aracılığı ile daha az yer kaplayacak şekilde tutuldu. Bu olay olurken yukarıdaki yapıdaki bir bitcoin bloku oluşturuldu. Bitcoin madencisi dediğimiz, blockchain node'ları yukarıda anlattığımız zor sayıyı yani nonce'u buldu ve blokzincirin sonuna bu bloku ekledi. Sistem ise bu bloku ilk bulan madenciye zamana göre değişen değerli 'n' tane bitcoin verdi.</h4>


![]({{ AUCyberClub.github.io }}/CyberCamp/assets/blockchain/1_pRMj7C7wsAWinpE3Yf9LDQ.png)





Görece basitleştirmeye çalıştığım teknik kısımların sonuna doğru gelirken, bitcoin örneğinde aklınıza şu soru geldiyse bu sorunun cevabı ile birlikte benim Bitcoin Kültürü diyeceğim, noktaya geçiş yapalım:

**Sistem ödülü nereden verdi ?:**

Ledger'a eklenen her bir işlem için bir (transaction fee) yani işlem ücreti alınır. Bu işlem ücretleri de bir noktada bir madencinin cebine girerek, aslında parasal olarak sağlam bir sisteme oturmuş olur, zira yazının devamında anlatacağım gibi bitcoin sınırlıdır.



<h2>Bitcoin Kültürü</h2>

Bitcoin ortaya çıkışında [Cypherpunk](https://en.wikipedia.org/wiki/Cypherpunk) akımından sadece ismen bahsetmiştim, kısaca anlatmak gerekirse bu akıma bağlı üyeler merkezileşmeye karşı, anonimliğin yanında ve otoriter devletlerin interneti kontrolü fikrine karşı bir takım insanlardan oluşan bir fikir birliği gibi düşünebilir. Üyeleri arasında Julian Assange ve aslında bitcoin ve blokparaların yine ilkel hali sayılabilecek hashcash'ın bulucusu Adam Back gibi insanlar vardır. Bu şahısların listesi için : https://en.wikipedia.org/wiki/Cypherpunk ve bazıları hakkında hack kültürü yazımızda zaten bahsetmiştik.  

**Satoshi Nakamoto:**

Aslında bu hikayenin hayatımıza bu kadar girmesinin [o meşhur pdf](https://bitcoin.org/bitcoin.pdf) Bitcoin: A Peer-to-Peer Electronic Cash System isimli yazıyla girmesinden başladığını söyleyebiliriz. Peki kim bu Satoshi Nakamoto ise internetin en çok merak ettiği sorulardan bir tanesi.

İsimle ilgili  “SAmsung – TOSHIba – NAKAmichi – MOTOrola” dev şirketlerinden esinlendiği söyleniyor, gerçek kimliği veya kimlikleri bilinmiyor. Satoshi Nakamoto isimli bir şahıs gerçekten var, fakat o da bu işlerle çok alakasız bir insan.

Kim olduğu ile ilgili onlarca teoriyi bulma araştırma kısmını sizin komplo teorisi araştırma hevesinize bırakıyorum. Son olarak bu konuda eklemem gereken şey ise "genesis block" denilen tarihin ilk bitcoin işlemi ve blok'unun Satoshi Nakamoto'ya ait olduğu söyleniyor.(blok numarası 0)

**Bitcoin ve DeepWeb ilişkisi:**

Bitcoin yapısı itibari ile anonim olduğu için özellikle ilk çıktığı dönemlerde DeepWeb tarafında çok fazla tercih ediliyordu. Bu dönemlerde kripto para borsalarında hesap açarken anonim hesap da açılabiliyordu, bu çok yüksek biz gizlilik sağlıyordu. Günümüzde artık bildiğim kadarıyla bu işlere çok fazla düzenleme geldi, anonim hesap açtıran borsalar kalmadı.

**Bitcoin bitecek mi ?:**

Yine yazının bir noktasında bahsetmiştim, bitcoin yapısı itibari ile 21 milyon tane olabilecek şekilde yapıldı ve bugün 18-19 milyona yakını kazıldı. Ama tabii ki zaman geçtikçe blok kazmanın zorlaşmasından bahsetmiştim, zira yine üstel bir takım olaylar oluyor ve kalan bitcoinlerin tahminen 2140 yılında tamamen biteceği öngörülüyor.

**Oyunbozan -> Kuantum:**

Kuantum bilgisayarı veri üzerinde işlem yapmak için bindirme ve dolaşma gibi kuantum-mekanik fenomenin doğrudan kullanımını sağlayan teorik hesaplama sistemlerini kullanan bilgisayarlardır, wikipedia tanımına göre. Pratikte bu bilgisayarlar normal bilgisayarlara göre korkunç fazla hızlı işlem yapabilirler. Ki buradan şunu diyebiliriz, yazıda bahsettiğimiz tüm sistemler brute-force'un yapılamayacak korkunç büyüklükte olduğundan güvenli, gelecekte bir gün Kuantum Personal Computer'larımız olur ise evet bir oyunbozanımız var gibi görünüyor.

<h2>Köşeyi Dönmek 101</h2>

**Kripto Para Borsaları**

Yazının bu noktasına geldiyseniz, arka planda blockchain ve bitcoin'in çalışma prensipleri hakkında bir takım fikirleriniz olduğunu varsayıyorum. İşin finansal kısmından bahsetmek gerekirse, Kripto Para Borsaları adlarından da olduğu gibi sizin kripto paraları alıp-satmanızı sağlıyor. Yine aynı şekilde birim kripto para fiyatları da her borsada olduğu gibi piyasa kavramı ile belirleniyor. Hangi kripto parayı al-sat yapmak için yapay-zeka/veri işleme ile çalışanlar var, yüksek ekonomi bilgisi ve piyasa takibi ile bunu yapanlar var veya hiçbir fikri olmadan sallayanlar da var ! Ancak bunların hiçbirisi bu yazının konusu değil.

**Kazı**

Yine artık nasıl çalıştığını bildiğimiz mining olayı için ise, Proof-of-work sisteminden yazıda detaylıca anlatmadığım Proof-of-stake sistemine Etherium'un 2.0 ile geçmesi planlanıyor. Bu işleri nasıl değiştirir, bilmek lazım. Bir de aynı zamanda donanım üreticileri artık ekran kartlarını mining ve diğer kullanım için iki ayrı sınıfta üreteceğini söylüyor. Zaten piyasada ekran kartı bulmak da zor, mining için çok fazla araştırma yaptıktan sonra girmenizi şiddetle tavsiye ediyorum.





































































