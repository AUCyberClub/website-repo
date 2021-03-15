---
layout: post
title: Linux Dosya Sistemi
date: '2021-03-13 22:26:47 +0300'
author: Kübra Dilara Balcı
categories: linux
index: 4
---
<center><h1><strong>LİNUX DOSYA SİSTEMİ</strong></h1></center>
<p>
</p>
<p>
	Windows işletim sisteminden Linux’a geçerken kullanıcıların en çok yaşadığı
sıkıntılardan biri dosya sistemlerinin farklı olmasıdır. Hatta farkı Linux
dağıtımları için dosya sistem hiyerarşisi de değişebilir. Linux sisteme ilk
geçiş yaptığınızda “Hangi klasör ne işe yarıyor? Hangi klasör neyle ilişkili?”
gibi sorularla karşı karşıya kalmanız çok mümkündür. Bu yazımızda Linux’ta dosya
sistemi hiyerarşisini ve aslında Linux’ta sistemdeki her şeyin bir dosya
olduğundan bahsedeceğiz.
</p>
<h2><strong>Linux Dosya Sistemi Nedir?</strong></h2>
<p>
Bir Linux dosya sistemi, bir disk sürücüsü veya bölümdeki(partition)
yapılandırılmış bir dosya koleksiyonudur. Bir bölüm(partition) hafıza(memory)nın
bir bölümüdür ve bazı özel verileri içerir. Makinemizde hafızanın çeşitli
bölümleri olabilir. Genel olarak, her bölüm bir dosya sistemi içerir.
</p>
<p>
Linux dosya sistemi aşağıdaki bölümleri içerir:
</p>
<ul>
<li>Kök dizin (/)</li>
<li>Belirli bir veri depolama biçimi (EXT3, EXT4, BTRFS, XFS vb.)</li>
<li>Belirli bir dosya sistemine sahip bir bölüm(partition) veya mantıksal
birim(logical volume).
</li>
</ul>
<p>
Linux dosya sistemi, genellikle depolamanın veri yönetimini işlemek için
kullanılan Linux işletim sisteminin yerleşik bir katmanıdır. Dosyayı disk
deposunda düzenlemeye yardımcı olur. Dosya adını, dosya boyutunu, oluşturulma
tarihini ve bir dosya hakkında çok daha fazla bilgiyi yönetir.
</p>
<p>
Dosya sistemimizde desteklenmeyen bir dosya biçimimiz varsa, bununla başa çıkmak
için yazılım indirebilirsiniz.
</p>
<p>
</p>
<h2><strong>Linux Dosya Sistemi Yapısı</strong></h2>
<p>
Linux dosya sistemi, bir kök dizini(/) ve alt dizinlerini içerdiğinden
hiyerarşik bir dosya yapısına sahiptir. Diğer tüm dizinlere kök dizinden(/)
erişilebilir. Bir bölüm(partition) genellikle yalnızca bir dosya sistemine
sahiptir, ancak birden fazla dosya sistemine sahip olabilir.
</p>
<p>
Bir dosya sistemi geçici olmayan depolama verilerini yönetebilecek ve bu veriler
için alan sağlayabilecek şekilde tasarlanmıştır. Tüm dosya sistemleri bir
adlandırma ve organizasyonel metodoloji olan bir ad alanı(namespace)
gerektiriyordu. Ad alanı, adlandırma sürecini, dosya adının uzunluğunu veya
dosya adı için kullanılabilecek bir karakter alt kümesini tanımlar. Ayrıca,
belirli dosyaların düzenlenmesi için dizinlerin kullanılması gibi bir bellek
bölümündeki dosyaların mantıksal yapısını da tanımlar. Bir ad alanı
tanımlandıktan sonra, söz konusu dosya için bir Meta Veri(Metadata) açıklaması
tanımlanmalıdır.
</p>
<p>
Veri yapısının hiyerarşik bir dizin yapısını desteklemesi gerekir. Bu yapı
belirli bir blok ve kullanılan disk alanını tanımlamak için kullanılır. Ayrıca,
dosya boyutu, oluşturulma tarihi ve saati, güncelleme ve son değiştirilme gibi
dosyalar hakkında diğer ayrıntılara da sahiptir. Bölümler(partition) ve
birimler(volume) gibi disk bölümü hakkındaki gelişmiş bilgileri de depolar.
</p>
<p>
Gelişmiş veriler ve temsil ettiği yapılar, sürücüde depolanan dosya sistemi
hakkındaki bilgileri içerir. Dosya sistemi meta verilerinden farklı ve
bağımsızdır.
</p>
<p>
Linux dosya sistemi, iki parçalı dosya sistemi yazılım uygulama mimarisini
içerir. Aşağıdaki tabloda gördüğünüz gibi:
</p>
<p>
    <img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/linux-dosya-sistemi/linux-file-system.png" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Dosya sistemi, dosyalar(files) ve dizinler(directories) gibi dosya sistemi
bileşenleriyle etkileşim kurmak ve işlev çağrılarına(function calls) erişmek
için bir API ((Application programming interface)Uygulama programlama arabirimi)
ihtiyaç duyar. API, dosyaları oluşturma, silme ve kopyalama gibi görevleri
kolaylaştırır. Bir dosya sistemindeki dosyaların düzenlenmesini kolaylaştıran
bir algoritmadır.
</p>
<p>
Verilen dosya sisteminin ilk iki parçası birlikte bir Linux sanal dosya sistemi
olarak adlandırılır. Çekirdek(kernel) ve geliştiricilerin dosya sistemine
erişmesi için tek bir komut seti sağlar. Bu sanal dosya sistemi belirli sistem
sürücüsünün dosya sistemine bir arayüz vermesini gerektirir.
</p>
<h2><strong>Linux Dosya Sistemi Özellikleri</strong></h2>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/linux-dosya-sistemi/Dosya_sistemi.png" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Linux'ta dosya sistemi bir ağaç yapısı oluşturur. Tüm dosyalar bir ağaç ve
dalları olarak düzenlenmiştir. En üstteki dizine kök (/) dizin adı verilir.
Linux'taki diğer tüm dizinlere(directory) kök dizinden erişilebilir.
</p>
<p>
 Linux dosya sisteminin bazı temel özellikleri vardır:
</p>
<ul>
<li><strong>Yolların belirtilmesi(Specifying paths):</strong> Linux’ta
bileşenleri ayırmak için Windows gibi ters eğik çizgiyi (\) kullanmaz;
alternatif olarak eğik çizgi (/) kullanır. Örneğin, Windows'ta olduğu gibi,
veriler C: \Belgelerim\Ornek konumunda depolanabilirken, Linux'ta
/home/belgelerim/ornek konumunda depolanabilir.</li>
<li><strong>Bölüm, Dizinler ve Sürücüler(Partition, Directories, and
Drives):</strong> Linuxta sürücüler düzenlemek için Windows gibi harfler
kullanılmaz(Windows->C sürücüsü, D süsürüsü gibi). Linux'ta bir bölüme(patition)
mi, ağ aygıtına mı yoksa "sıradan" bir dizine ve bir Sürücüye mi hitap
ettiğimizi söyleyemeyiz.</li>
<li><strong>Büyük / Küçük Harfe Duyarlılık(Case Sensitivity):</strong> Linux
dosya sistemi büyük/küçük harfe duyarlıdır. Küçük ve büyük dosya adlarını
birbirinden ayırır. Örneğin, Linux'ta test.txt ile Test.txt farklıdır. Bu kural
aynı zamanda dizinler ve Linux komutları için de geçerlidir.</li>
<li><strong>Dosya Uzantıları(File Extensions):</strong> Linux'ta bir dosya
'.txt' uzantısına sahip olabilir, ancak bir dosyanın dosya uzantısına sahip
olması gerekli değildir. Yeni başlayanlar shell(terminal) ile çalışırken, dosya
ve dizinleri ayırt etmekte bazı sorunlar yaşayabilir. Grafik dosya yöneticisini
kullanırsak, bu dosya ve klasörleri sembolize eder.</li>
<li><strong>Gizli dosyalar(Hidden files):</strong> Linux standart dosyalar ile
gizli dosyalar arasında ayrım yapar, çoğunlukla yapılandırma(configuration)
dosyaları Linux işletim sisteminde gizlidir. Genellikle gizli dosyalara
erişmemize veya okumamıza gerek yoktur. Linux'taki gizli dosyalar, dosya adından
(örneğin; .ignore) önce bir nokta (.) ile gösterilir. Dosyalara erişmek için
dosya yöneticisindeki görünümü değiştirmemiz veya shellde bazı komutlar
kullanmamız gerekir.
</li>
</ul>
<h2><strong>Linux Dosya Sistemi Türleri</strong></h2>
<p>
Linux işletim sistemini kurduğunuz zaman size Ext, Ext2, Ext3, Ext4, JFS,
ReiserFS, XFS, btrfs ve swap gibi birçok dosya sistemi sunar.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/linux-dosya-sistemi/linux-file-system2.png" width="" alt="alt_text" title="image_tooltip">
</p>
<p>
Bu dosya sistemlerini birlikte inceleyelim.
</p>
<li><strong>Ext, Ext2, Ext3 and Ext4</strong>
</li>
<p>
Dosya sistemi <strong>Ext(Extended File System)</strong> Genişletilmiş Dosya
Sistemi anlamına gelir. Öncelikle <strong>MINIX OS</strong> için
geliştirilmiştir. Ext dosya sistemi daha eski bir sürümdür ve bazı sınırlamalar
nedeniyle artık kullanılmamaktadır.
</p>
<p>
<strong>Ext2</strong> iki terabytelık veriyi yönetmeye izin veren ilk Linux
dosya sistemidir. <strong>Ext3</strong>, Ext2 aracılığıyla geliştirilmiş,
Ext2'nin yükseltilmiş bir sürümüdür ve geriye dönük uyumluluk içerir.
<strong>Ext3</strong>'ün en büyük dezavantajı dosya kurtarmayı ve disk anlık
görüntüsünü desteklemediği için sunucuları desteklememesidir.
</p>
<p>
<strong>Ext4</strong> dosya sistemi, tüm Ext dosya sistemleri arasında daha
hızlı dosya sistemidir. SSD (solid-state drive) diskleri için çok uyumlu bir
seçenektir ve Linux dağıtımında varsayılan dosya sistemidir.
</p>
<li><strong>JFS </strong>
</li>
<p>
JFS(Journaled File System) IBM tarafından AIX Unix için geliştirilmiştir. Ext
dosya sistemine bir alternatiftir. Az kaynakla stabilitenin gerekli olduğu Ext4
yerine de kullanılabilir. CPU gücü sınırlı olduğunda kullanışlı bir dosya
sistemidir.
</p>
<li><strong>ReiserFS</strong>
</li>
<p>
ReiserFS Ext3 dosya sistemine bir alternatiftir. İyileştirilmiş performansa ve
geliştirilmiş özelliklere sahiptir. Önceden, ReiserFS SUSE Linux'ta varsayılan
dosya sistemi olarak kullanılıyordu ama daha sonra bazı politikaları değiştirdi.
Bu nedenle SUSE Ext3'e geri döndü. Bu dosya sistemi, dosya uzantısını dinamik
olarak destekler ama performansta bazı dezavantajlara sahiptir.
</p>
<li><strong>XFS</strong>
</li>
<p>
XFS dosya sistemi paralel I/O işleme için geliştirilen yüksek hızlı JFS olarak
kabul edildi. NASA yüksek depolama sunucusuyla (300+ Terabyte sunucusu) bu dosya
sistemini hala kullanıyor.
</p>
<li><strong>Btrfs</strong>
</li>
<p>
Btrfs B ağacı dosya sistemini ifade eder. Hata toleransı, onarım sistemi,
eğlence yönetimi, kapsamlı depolama yapılandırması ve daha fazlası için
kullanılır. Üretim sistemi için uygun değildir.
</p>
<li><strong>Swap</strong>
</li>
<p>
Takas(swap) dosya sistemi, sistem hazırda bekletme(hibernation)
sırasındayken Linux işletim sisteminde bellek sayfalama(memory paging) için
kullanılır. Hiçbir zaman hazırda bekletme durumuna geçmeyen bir sistemin RAM
boyutuna eşit takas(swap) alanına sahip olması gerekir.
</p>
<h2><strong>Linux Dosya Sistemi Dizinleri</strong></h2>
<p>
Dizinlerin belirli amaçları vardır ve dosyaları kolayca bulmak için genellikle
aynı tür bilgileri tutarlar. Unix'in ana sürümlerinde bulunan dizinler
aşağıdadır:
</p>
<p>
<strong>/</strong>
</p>
<p>
/, yalnızca dosya yapısının en üst seviyesinde ihtiyaç duyulan dizinleri
içermesi gereken kök dizindir.
</p>
<p>
<strong>/bin</strong>
</p>
<p>
/bin, ikili(binary) içeren dizindir. Yani çalıştırabileceğiniz bazı uygulama ve
programları içeren dizindir. Bu dizinde ls programını ve dosya ve dizinleri
oluşturmak ve kaldırmak, onları taşımak vb. için diğer temel araçları
bulabilirsiniz. Dosya sistemi ağacının diğer bölümlerinde daha fazla bin dizini
var.
</p>
<p>
<strong>/boot</strong>
</p>
<p>
/boot dizini sisteminizi başlatmak için gerekli dosyaları içerir. Bunu
söylemeden geçemeyeceğim. Sakın DOKUNMAYIN! Buradaki dosyalardan birini
karıştırırsanız Linux'unuzu çalıştıramayabilirsiniz ve bunu düzeltmek biraz acı
verici olabilir. Öte yandan, sisteminizi kazara yok etme konusunda çok fazla
endişelenmeyin. Bunu yapmak için süper kullanıcı(superuser) ayrıcalıklarına
sahip olmanız gerekir.
</p>
<p>
<strong>/etc</strong>
</p>
<p>
/etc isimlerin kafa karıştırmaya başladığı dizindir. /etc adını en eski
Unix'lerden alır ve kelimenin tam anlamıyla "et cetera" dir çünkü sistem dosya
yöneticileri nereye koyacaklarından emin olamadıkları için çöplük(dumping) alanı
oldu.
</p>
<p>
Günümüzde, etc'nin "Yapılandırılacak(configure) her şey" anlamına geldiğini
söylemek daha doğru olacaktır, çünkü tüm sistem genelindeki yapılandırma
dosyalarını olmasa da çoğunu içerir. Örneğin; sisteminizin adını, kullanıcıları
ve parolalarını, ağınızdaki makinelerin adlarını ve hard diskinizdeki
bölümlerin(patition) ne zaman ve nereye bağlanacağını(mount) içeren dosyalar
burada yer almaktadır. Yani Linux'ta yeniyseniz, işlerin nasıl yürüdüğünü daha
iyi anlayana kadar buraya çok fazla dokunmamanız sizin için daha iyi olabilir.
</p>
<p>
<strong>/home</strong>
</p>
<p>
/home kullanıcılarınızın kişisel dizinlerini bulacağınız yerdir. Benim
bilgisayarımda, /home altında iki dizin var: /home/kdb, tüm dosyalarımı içeren
ve /home/guest da herhangi birinin bilgisayarımı ödünç alması gerekmesi
durumunda.
</p>
<p>
<strong>/lib</strong>
</p>
<p>
/ lib kitaplıkların(libraries) bulunduğuı yerdir. Libraryler uygulamalarınızın
kullanabileceği kodu içeren dosyalardır. Uygulamaların masaüstünüze pencere
çizmek, çevre birimlerini(peripherals) kontrol etmek veya dosyaları sabit
diskinize göndermek için kullandığı kod parçacıkları içerirler.
</p>
<p>
Dosya sistemi etrafına dağılmış çok fazla library dizini vardır ama bu, doğrudan
asılı olan <strong>/</strong> diğer şeylerin yanı sıra tüm önemli
çekirdek(kernel) modüllerini içerdiği için özeldir. Çekirdek(kernel) modülleri
ekran kartınız, ses kartınız, WiFi, yazıcınız ve benzeri şeyleri çalıştıran
sürücülerdir.
</p>
<p>
<strong>/media </strong>
</p>
<p>
/media dizini takıp erişmeye çalıştığınızda harici depolamanın
otomatik olarak bağlanacağı(mounted) yerdir.Bu listedeki diğer
öğelerin çoğunun aksine, /media 1970'lere geri dönmüyor, bunun başlıca nedeni,
bir bilgisayar çalışırken anında eklenen ve saptalan depolama (pendrives, USB
sabit diskler, SD kartlar, harici SSD'ler vb.) nispeten yeni bir şey.
</p>
<p>
<strong>/mnt</strong>
</p>
<p>
/mnt dizini biraz eskide kalmıştır. Depolama aygıtlarını veya
bölümleri(partition) manuel olarak bağlayabileceğiniz(mount) yer burasıdır.
Günümüzde çok sık kullanılmamaktadır.
</p>
<p>
<strong>/opt</strong>
</p>
<p>
/opt dizini genellikle derlediğiniz(compile) yazılımların (yani, kendi kaynak
kodunuzu oluşturduğunuz ve dağıtım havuzlarınızdan(distribution repo)
yüklemediğiniz) bazen bulunduğu yerdir. Uygulamalar /opt/bin dizininde ve
/opt/lib dizinindeki librarylerinde sona erecektir.
</p>
<p>
Küçük bir özet: uygulamaların ve librarylerinin bittiği bir başka yer
/usr/local’dır. Yazılım buraya yüklendiğinde /usr/local/bin ve /usr/local/lib
dizinleri de olacaktır. Hangi yazılımın nereye gideceğini belirleyen şey,
geliştiricilerin derleme(compilation) ve yükleme(installation) sürecini kontrol
eden dosyaları nasıl yapılandırdığına bağlıdır.
</p>
<p>
<strong>/proc</strong>
</p>
<p>
/proc, /dev gibi sanal bir dizindir. Bilgisayarınız hakkında CPU'nuz ve Linux
sisteminizin çalıştırdığı çekirdek(kernel) hakkında bilgiler içerir. /dev'de
olduğu gibi, dosyalar ve dizinler bilgisayarınız başladığında veya sisteminiz
çalışırken ve işlemler değiştikçe anında oluşturulur.
</p>
<p>
<strong>/root</strong>
</p>
<p>
/root, sistemin (superuser)süper kullanıcısının ("Yönetici" olarak da bilinir.
Yani en yetkili kullanıcıdır.) ana dizinidir. Kullanıcıların home dizinlerinin
geri kalanından ayrıdır ama buna dokunabileceğiniz anlamına gelmiyor tabi. Kendi
dosyalarınızı kendi dizinlerinde tutsanız iyi olur. /root ile şaka olmaz.
</p>
<p>
<strong>/run</strong>
</p>
<p>
/run sistem süreçlerinin(process) geçici verileri depolamak için kullanılan bir
dizindir. Bu da DOKUNMAMANIZ gereken bir diğer klasördür(folder).
</p>
<p>
<strong>/sbin</strong>
</p>
<p>
/sbin, /bin'e benzer ama yalnızca süper kullanıcının (bu yüzden s ile başlar)
ihtiyaç duyacağı uygulamaları içerir. Bu uygulamaları geçici olarak size süper
kullanıcı(superuser) güçlerini birçok dağıtımda kabul eden <strong>sudo</strong>
komutuyla kullanabilirsiniz. /sbin genellikle bir şeyler yükleyebilen, öğeleri
silebilen ve öğeleri biçimlendirebilen araçlar içerir. Tahmin edebileceğiniz
gibi bu talimatlardan bazıları yanlış kullanırsanız sıkıntı yaşayabilirsiniz, bu
yüzden dikkatli olun.
</p>
<p>
<strong>/usr</strong>
</p>
<p>
/usr dizini UNIX'in ilk zamanlarında kullanıcıların home dizinlerinin tutulduğu
yerdi. Ancak, şimdi /home, yukarıda bahsettiğimiz gibi kullanıcıların kişisel
şeylerini sakladıkları yerdir. Bugünlerde /usr sırayla uygulamaları, librayleri,
belgeleri, duvar kağıtlarını, simgeleri ve uygulamalar ve hizmetler tarafından
paylaşılması gereken diğer şeylerin uzun bir listesini içeren birçok dizin
içerir.
</p>
<p>
Ayrıca /usr içinde bin, sbin ve lib dizinlerini de bulacaksınız. Peki kök salmış
kuzenleriyle farkı nedir? Aslında son zamanlarda pek farklı değil. Başlangıçta
/bin dizini (kökten asılı) <strong>ls</strong>, <strong>mv</strong> ve
<strong>rm</strong> gibi çok temel komutları içerir(daha önceki yazılarımızda
bahsetmiştik). Tüm UNIX/Linux kurulumlarında önceden yüklenmiş olarak gelen bir
sistemi çalıştırmak ve sürdürmek için minimum düzeyde olabilecek türden
komutlar. Öte yandan /usr/bin, kullanıcıların sistemi bir iş istasyonu olarak
kullanmak için yükleyeceği ve çalıştıracağı tıpkı kelime işlemciler, web
tarayıcıları ve diğer uygulamalar gibi şeyler içerir.
</p>
<p>
Ancak birçok modern Linux dağıtımı her şeyi /usr/bin içine koyar ve /bin'i
/usr/bin'i işaret eder ve tam olarak silmek bir şeyi bozabilir. Debian, Ubuntu
ve Mint hala /bin ve /usr/bin (ve /sbin ve /usr/sbin) 'i ayrı tutarken; Arch ve
türevleri gibi diğerleri, ikili(binaries) dosyalar için sadece bir "gerçek"
dizine sahiptir, /usr/bin ve geri kalanı veya *bins /usr/bin'i işaret eden
"sahte" dizinlerdir.
</p>
<p>
<strong>/srv</strong>
</p>
<p>
/srv dizini sunucular için veri içerir. Linux’ta bir web sunucusu
çalıştırıyorsanız siteleriniz için HTML dosyalarınız /srv/http (veya /srv/www)
içine gider. Bir FTP sunucusu çalıştırıyorsanız dosyalarınız /srv/ftp içine
gider.
</p>
<p>
	Bazı durumlarda bu cihazları da değiştirebilirsiniz. Örneğin,
/sys/devices/pci0000:00/0000:00:02.0/drm/card1/card1-eDP-1/intel_backlight/brightness
içinde depolanan değeri değiştirerek laptopunuzun ekran parlaklığını
değiştirebilen dosyadır (makinenizde muhtemelen farklı bir dosyanız olacaktır).
Ama bunu yapmak için süper kullanıcı(root) olmalısın. Bunun nedeni, diğer pek
çok sanal dizinde olduğu gibi, /sys içindeki içerik ve dosyalarla uğraşmak
tehlikeli olabilir ve sisteminizi bozabilirsiniz. Ne yaptığınızı bildiğinizden
emin olana kadar DOKUNMAYIN.
</p>
<p>
	<strong>/tmp</strong>
</p>
<p>
<strong>	</strong>/tmp genellikle çalıştırdığınız uygulamalar tarafından oraya
yerleştirilen geçici(temporary) dosyalar içerir. Dosyalar ve dizinler genellikle
(her zaman değil) bir uygulamanın şu anda ihtiyaç duymadığı, ancak daha sonra
ihtiyaç duyabileceği verileri içerir.
</p>
<p>
Kendi geçici dosyalarınızı saklamak için /tmp kullanabilirsiniz.  - /tmp asılı
duran <strong>/</strong> süper kullanıcı(root) olmadan gerçekten etkileşim
kurabileceğiniz birkaç dizinden biridir.
</p>
<p>
<strong>/var</strong>
</p>
<p>
/var içeriği değişken kabul edildiğinden (sık sık değiştiği için) orijinal
olarak bu ad verildi. Artık bu biraz yanlış bir adlandırma oluyor çünkü sık sık
değişen veriler içeren başka birçok dizin var, özellikle yukarıda gördüğünüz
sanal dizinler.
</p>
<p>
Her ne olursa olsun, /var, /var/log alt dizinlerindeki loglar gibi şeyler
içerir. Loglar, sistemde meydana gelen olayları kaydeden dosyalardır.
Çekirdekte(kernel) bir şey başarısız olursa /var/log içindeki bir dosyaya
kaydedilir. Birisi dışarıdan bilgisayarınıza girmeye çalışırsa, güvenlik
duvarınız da girişimi buraya kaydeder. Ayrıca görevler için makaralar(spool)
içerir. Bu “görevler” paylaşılan bir yazıcıya gönderdiğiniz işler başka bir
kullanıcı uzun bir belge yazdırdığı için beklemeniz gerektiğinde ya da
sistemdeki kullanıcılara teslim edilmeyi bekleyen postalar olabilir.
</p>
<p>
Sisteminizde yukarıda bahsetmediğimiz başka dizinler de olabilir. Örneğin ekran
görüntüsü için /snap dizini gibi. Bunun nedeni, ekran görüntüsünün bir Ubuntu
sisteminde çekilmiş olmasıdır. Ubuntu, yakın zamanda yazılım dağıtmanın bir yolu
olarak snap paketleri dahil etti. /snap dizini, snap'lerden yüklenen tüm
dosyaları ve yazılımı içerir.
</p>
<p>

<img src="{{ AUCyberClub.github.io }}/CyberCamp/assets/linux-dosya-sistemi/standard-unix-filesystem-hierarchy.png" width="" alt="alt_text" title="image_tooltip">
</p>
<h2><strong>Son Sözler</strong></h2>
<p>
</p>
<p>
	Görmüş olduğunuz gibi Linux sistemlerde her şey bir dosyadır. Ve en önemli
şeylerden biri de Linux’ta henüz yeniyseniz dokunmamanız gereken dizinleri iyi
bilmelisiniz. Yeterince bilgisi olmayanlar için root(en yetkili kullanıcı)
tehlikeli olabilir. Ama merak etmeyin alıştıkça daha çok sevmeye
başlayacaksınız.
</p>
