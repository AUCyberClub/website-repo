---
layout: post
title: GNU/Linux ve Özgür Yazılım
date: '2021-03-11 22:59:47 +0300'
author: Berkay Çelebi
categories: linux
index: 2
---
<center><h1><strong>GNU/Linux ve Özgür Yazılım</strong></h1></center>

<h3>Kısaca GNU/Linux nedir?</h3>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-4.jpg" width="" alt="alt_text" title="image_tooltip">

<p>
	GNU/Linux’un ne olduğunu merak edip kısaca okuyup hemen çıkacaklar için ne
olduğunu açıklayarak başlayalım çünkü anlatacak çok olay ve öğrenecek çok şey
var.
</p>
<p>
GNU’nun sayfasına baktığımız zaman GNU’nun ne olduğunu kısa ve öz şekilde ilk
paragrafta şöyle açıklamışlar:
</p>
<p>
	“<em>GNU, açılımı GNU is Not Unix, <a
href="https://www.gnu.org/philosophy/free-sw.html">özgür yazılım</a> olan bir
işletim sistemidir, yani kullanıcıların özgürlüğüne saygı duyar. GNU işletim
sistemi; GNU paketlerinden (özellikle GNU Projesi tarafından yayımlanan
programlar) ve üçüncü taraflarca yayımlanan özgür yazılımdan oluşur. GNU'nun
geliştirilmesi, özgürlüğünüzü ihlal eden yazılımlar olmadan bir bilgisayarın
kullanılmasını mümkün kılmıştır.”</em>
</p>
<p>
“Peki GNU/Linux nedir?” sorusunu merak ediyorsanız, hikayesi için yazının
tamamını okumanızı öneririm.
</p>
<h3>Bilgisayar ve İşletim Sistemleri Tarihi </h3>
<h3>(Başlığa aldırmayın eğlenceli konulardan bahsedeceğim)</h3>
<p>
	Bilgisayarlar günümüzde alışverişten ödeve, mutfak robotundan nükleer
santraldeki bir kontrolcüye kadar her yerde kullanılıyor.
</p>
<p>
	Siz de düşünmüşsünüzdür: “Bu kadar karmaşık bir makineyi gerçekten insanlar mı
yaptı, yoksa uzaylılar mı getirdi?” Kısa cevap, maalesef bildiğimiz kadarıyla
uzaylılarla pek bir alakası yok.
</p>
<p>
Bilgisayarlar çok yeni şeyler gibi görünse de aslında tarihi milattan öncelere
kadar dayanıyor. Aşağıdaki fotoğrafta şu an bildiğimiz ilk analog bilgisayarın
kalıntılarını görüyoruz. Altında da yine analog bir bilgisayar görüyoruz.
İlk makinenin gök cisimlerinin hareketlerini hesaplamak gibi işlerde
kullanıldığını düşünüyoruz. Altındakinin ise tek görevi programladığımız müziği
bilyeler ile çalmak!
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-7.jpg" width="" alt="alt_text" title="image_tooltip">

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-1.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Modern -elektrikle çalışan, dijital- bilgisayarlar ise çok uzak zamanlarda yoktu
elbette. İlk elektrikle çalışan bilgisayar, şaşırmayacaksınız, savaşlar için
kullanıldı. Elektro-mekanik diyebileceğimiz bu bilgisayar 1938 yılında ABD’de
deniz altı torpidolarının hesaplamaları için trigonometrik hesaplamaları yapmada
kullanıldı. Daha sonrasında ise yine çok duyduğumuz vakum tüplü devasa
bilgisayarlar ve ilk örneği ENIAC ise yine 2. dünya savaşında telsiz
konuşmalarını deşifre etmek için ünlü matematikçi Alan Turing tarafından
geliştirildi.
</p>
<p>
	İlk bilgisayarları kullanabilmek için bilgisayarların kablolarını söküp
amacımıza göre tekrardan takıp çalıştırıp uzuunca bir süre bekledikten sonra,
eğer ki doğru takmışsak, istediğimiz çıktının gelmesini bekliyorduk. Daha sonra
o meşhur delikli kartları keşfettik.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-2.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Delikli kartlardan sonra ihtiyacımız olan şeyleri programlamak çok daha kolay
hale gelmişti fakat yine de bu bilgisayarları kullanabilmek için o alanda uzman
kişilerin bilgisayarı yönetmesi ve yaptığı işlemleri kontrol etmesi gerekiyordu.
Dahası bu devasa bilgisayarlar için çok fazla talep olmaya başlamıştı ve bu
durumu yönetebilmek için  bilgisayar operatörlerinin işleri parçalara bölüp
hesaplamaları ayrı ayrı yapıp, yani aynı anda birden fazla görevi yapıp, sonra
çıktıları birleştirip sonuçları vermesi gerekmişti. Operatörler yine de bu
duruma yetişemediler ve sonuç olarak bilgisayarlar ilk hamlelerini yapıp ilk
mesleğin sonunu getirdiler: bilgisayar operatörleri yerini işletim sistemlerine
bıraktı.
</p>
<p>
	İşletim Sistemleri üniversitelerde başlı başına bir ders olarak anlatılan çok
kapsamlı bir konu olduğu için burada işin magazin kısmına bakacağız.
</p>
<p>
</p>
<p>
	Kısa bilgisayar tarihinden sonra şimdi bir de kısa işletim sistemleri tarihine
bakmamız gerekiyor. İşletim sistemleri basitçe bilgisayarlara bizim istediğimiz
şeyleri yaptırmakla görevli yazılımlardır. Biz ona ne istediğimizi söyleriz ve
işletim sistemi bizi kablolarla, karmaşık kodlarla uğraştırmadan istediğimiz
sonucu tekrar bize gösterir. Tabii ki işletim sistemlerini de uzaylılar yapmadı.
Yıllar süren bilgi birikimi sayesinde şu an kullandığımız modern işletim
sistemleri ortaya çıktı.
</p>
<p>
</p>
<p>
	İlk işletim sistemi 1956 yılında General Motors ve North American Aviation(NAA)
tarafından IBM 704 bilgisayarı için geliştirilmişti. Bu işletim sistemi az önce
bahsettiğimiz operatörlerin görevi olan bir iş bitince diğer işi yapma görevini
üstlenmişti. İlerleyen yıllarda yeni bilgisayarlar, yeni işletim sistemleri de
doğmaya ve her geçen gün de gelişmeye devam etti. Kernel-Shell gibi kavramlar
ile işletim sistemleri çok karmaşık yazılımlar haline gelmeye başladı. Daha
ayrıntılı bilgi için <span style="text-decoration:underline;">“ Linux sistemi,
dağıtımlar”</span> başlıklı yazımızı okuyabilirsiniz.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-6.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
	İlerleyen yıllar ve bilgisayarların ucuzlaması ile birlikte bilgisayar evlere
sığabilen ve ihtiyacı olan herkesin ulaşabileceği bir araç haline gelmeye
başlayınca ortaya hepimizin bildiği Microsoft çıktı ve döneminin efsane işletim
sistemi olan MS-DOS işletim sistemini çıkardı. Şirket bu işletim sistemi ve
sonrasında, ve günümüzde hala, sattığı kopyalar ve işletim sistemlerine özel
çıkardığı yazılımlar,office ve diğer 3. parti yazılımlar gibi, ile dünyanın en
büyük şirketleri arasında yerini koruyor. Fakat büyük bir sorun var. Bu
yazılımların kaynak kodlarını açıp okuyamıyoruz, yani arkada ne işler çevirdiği
hakkında pek bir fikrimiz yok. İşte burada kurtarıcımız olan Açık Kaynak ve
Özgür Yazılım Felsefesi devreye giriyor.
</p>
<h3>Kurtarıcımız: Özgür Yazılım</h3>
<h4>Ne bu açık kaynak?</h4>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-8.png" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Öncelikle açık kaynak ne demek bunu bir açıklayalım. Bir programı geliştirirken
bunu çeşitli programlama dillerini kullanarak yazarız. Bu yazdığımız kodlar,
konuya hakim kişiler tarafından rahatlıkla okunabilir, anlaşılabilir durumdadır.
Sonrasında bu kodlar çeşitli programlar ile, derleyici, interpreter gibi
bilgisayarın anlayabileceği makine koduna dönüştürülür. Bu makine kodunu ise
doğrudan okuyup anlamak neredeyse imkansızdır. Dahası bazı ücretli yazılımlarda
bu kodları daha da karmaşık hale getirip makine kodu halini bile anlamayı
zorlaştırmak için ayrı bir çaba gösterilir.
</p>
<p>
İşte, eğer ki bir yazılım açık kaynak ise, bu yazılımın tüm kodlarını yazan
kişinin gördüğü hali ile görebiliriz.
</p>
<h4>Peki ya Özgür Yazılım?</h4>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-5.jpg" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
	Özgür yazılım ise bir felsefedir, bakış açısıdır, bir kültürdür.
</p>
<p>
Yine “Özgür yazılım nedir?” sorusuna GNU’nun resmi sayfasındaki kısa ve öz
açıklama ile bakalım:
</p>
<p>
	<em>“Özgür yazılım”, kullanıcıların özgürlüğüne ve topluluğa saygı duyan
yazılım demektir. Kabataslak, <strong>kullanıcıların bir yazılımı çalıştırma,
kopyalama, dağıtma, çalışma, değiştirme ve geliştirme özgürlüğüne sahip
olduğu</strong> anlamına gelir. Öyleyse, “özgür yazılım” bir fiyat değil,
özgürlük meselesidir. İngilizcedeki "free" kelimesinden kaynaklı olarak, bu
kavramı anlamak için, “bedava birayı” değil “ifade özgürlüğünü” düşünmek
gerekiyor. Bazı durumlarda, Fransızca ve İspanyolca'dan özgürün karşılığı olarak
libre ödünç alınarak “libre” yazılım kavramı da, yazılımın bedelsiz olduğu değil
özgür olduğunu kastetmek için kullanılıyor.</em>
</p>
<p>
Bu yazıdan da anlaşılacağı gibi özgür yazılım yukarıda bahsettiğimiz “ücret”
için kapalı kaynak ve telif dolu yazılımların insanların özgürlüğünü
kısıtladığını belirterek bunun önüne geçmek için doğmuş bir düşüncedir.
</p>
<p>
Özgür yazılım felsefesi 4 temel ilkeyi benimser ve eğer bir yazılım bu dört
ilkeye de uygunsa o zaman bu yazılım özgür bir yazılımdır der.
</p>

<li>Herhangi bir amaç için, istediğiniz şekilde yazılımı çalıştırma özgürlüğü (0
numaralı özgürlük).
<li>Her ne istiyorsanız onu yaptırmak için programın nasıl çalıştığını ögrenmek
ve onu değiştirme özgürlüğü (1 numaralı özgürlük). Yazılımın kaynak koduna
ulaşmak, bu iş için ön koşuldur.
<li>Kopyaları dağıtma özgürlüğü, böylece başkalarına yardım edebilirsiniz (2
numaralı özgürlük).
<li>Değiştirilmiş sürümlerinizin kopyalarını dağıtma özgürlüğü (3 numaralı
özgürlük). Böylece değişikliklerinizden yararlanması için tüm topluma bir şans
vermiş olursunuz. Kaynak koduna erişmek, bunun için bir ön koşuldur.
</li>

<p>
Okuyunca gerçekten de etkilenmemek elde değil. Peki nerde o zaman bu özgür
yazılımlar?
</p>
<h3>Sonunda GNU/Linux</h3>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/gnu-linux-ozgur-yazilim/2021-03-11-gnu-linux-ozgur-yazilim-3.png" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
	GNU/Linux dendiği zaman hemen iki isim yanında belirir:
</p>
<p>
	Richard Stallman
</p>
<p>
	Linus Torvalds
</p>
<p>
Richard Stallman işletim sistemini geliştirmeye başlamadan önce “UNIX” işletim
sistemini kullanmaktaydı. Bu işletim sisteminin en büyük sorunu ise birçok
lisanslama sorunu ile karşılaşılmasıydı. Bu tarz lisanslama sorunlarını ortadan
kaldırmak ve herkesin özgürce kullanıp geliştirebilmesi için GNU ismini verdiği
işletim sistemini geliştirdi.
</p>
<p>
Fotoğraftaki kişi Richard Stallman. Magazin kısmı işte burada başlıyor. GNU(GNU
is not UNIX, özyinelemeli bir isim) UNIX benzeri bir işletim sistemidir ve bir
işletim sistemi için gereken birçok yazılımı, uygulamalar, kütüphaneler,
geliştirici araçları gibi bulundurur  fakat GNU tam bir işletim sistemi olmaktan
yoksundu çünkü GNU, bir işletim sisteminin kalbi denilebilecek “kernel” dan
mahrumdu.
</p>
<p>
Linus Torvalds ise GNU’dan sonra kendi çekirdeği(kernel) geliştirdi ve buna
Linux ismini verdi. Sonrasında bu iki yazılım birleştirildi ve ortaya GNU/Linux
dediğimiz işletim sistemi ortaya çıktı.
</p>
<p>
Richard Stallman’ın ise rahatsız olduğu bir şey var. Bunu belirtmezsek olmaz.
</p>
<p>
<em>“Çekirdek olarak Linux'u esas alan bir çok işletim sistemi dağıtımı, temel
olarak GNU işletim sisteminin değiştirilmiş sürümleridir. Biz GNU'yu
geliştirmeye, Linus Torvalds'ın çekirdeği yazmaya başlamasından yıllar önce,
1984 yılında başladık. Hedefimiz bütünüyle özgür bir işletim sistemi
geliştirmekti. Tabii ki, bütün parçaları kendimiz geliştirmedik, ama
geliştirilmesine öncülük ettik. Ana bileşenlerin çoğunu geliştirmek suretiyle,
bütün sisteme tek taraflı en büyük katkıyı biz sağladık. Ayrıca temel bakış
açısı da bize aitti.</em>
</p>
<p>
<em>Adil olmak açısından, en azından bizden de eşit derecede bahsedilmeli.”</em>
</p>
<p>
Ve ardından da “Linux” olarak değil de “GNU/Linux” olarak adlandırılmasını,
özgür yazılım ve GNU için verilen emekler için istiyor. Haksız da sayılmaz.
</p>
<h3>Son Sözlerimiz</h3>
<p>
Günümüzde GNU/Linux işletim sistemlerinin binlerce varyasyonu bulunmaktadır.
Bunlardan en popülerleri Ubuntu, Linux Mint, Kali Linux gibi dağıtımlardır ve
her dağıtımın kendine göre iyi olduğu ve kötü olduğu yanları vardır.
</p>
<p>
Günümüzde farkında olmasak da her yerde özgür yazılımları kullanmaktayız ve
bunun en güzel örneği de Android işletim sistemli telefonlardır. Android
telefonlar da Linux Çekirdeğini kullanmaktadır. Linux Çekirdeği tamamen özgür
bir yazılımdır. Hatta github linkine <a
href="https://github.com/torvalds/linux">https://github.com/torvalds/linux</a>
dan ulaşabilirsiniz.
</p>
<p>
Son olarak Richard Stallman’ın bu sözü ile de yazımızı kapatıyorum
</p>
<p>
<em>Yeteneklerini kullanarak başarılı olan insanlarla bir sorunum yok, sadece
başarının en üst hedef olmadığını düşünüyorum. Özgürlük, bilginin paylaşılması -
genişlemesi başarının, kişiselliğin ötesinde şeyler. Kişisel başarı yanlış değil
ama etkisi sınırlanmış, eğer gerektiği kadarını elde ettiyseniz hala bunun için
açlık duymak ayıp, tabii doğruluk, güzellik ve adalet için durum tam tersi.</em>
/ Richard Stallman
</p>
