---
layout: post
title: DKHOS CTF Çözümleri
date: '2018-02-15 20:10:00 +0300'
categories: blog
---

# DKHOS CTF Çözümleri
## UPDATE

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/update.png)

Kopya tespitlerinden sonra nihai sonuca göre 4 takım öne geçerek **5.** ve **katılım sağlayan üniversite takımları arasında 1.** olduk.

İlgili tweetler: [*AUCC*](https://twitter.com/_aucc/status/965337478541533185) | [*DKHOS*](https://twitter.com/ctfturkey/status/965335027029594112)

---

Merhabalar,
 
Ankara Üniversitesi Siber Güvenlik Topluluğu adına *AUCC* takım ismi ile 4 kişi katıldığımız [**DKHOS CTF**](https://www.dkhos.com)'te şuanda nihai olmayan tabloya göre 9. tamamladık.

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/unofficialscoreboard.png)

35 Sorunun büyük bir yüzdesinde ilerleme kaydetmiş olsak da 16'sında nihayete ulaşabildik.

Yarışma genel anlamda sorunsuz geçti. ([Sistem](https://twitter.com/ctfturkey/status/962444185403035648) çok üst düzey de olsa  bazı ufak aksaklıklar *-[bkz.](https://twitter.com/ctfturkey/status/962456946166165504) tuzluk-* yüzünden anlık krizler geçirmedik değil)

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/prodaft.png)

Çoh iyi oldu çoh da güzel iyi oldu taammı. Şimdi mesela ctf olayını çok karıştırdılar. Aralarında bir fark galdı, o farkda çok güzel oldu. herkesin çözüşüne kimse garışamaz. ha nasıl garışamaz ben bu şekil çözerim, bu bayan şu şekil çözer. şu şekil çözer... amma hiçkimse kimseye garışmaya bi hakkı yok. özgürlüğü bidir. aa ctf kurban olduuum protdafttan gelebilir amma lakin ki öyle değildir. benim yorumlamam bu kadar. hadi hayrılı işler.

Ciddi anlamda kız tarafını benimsemiş olucaz ki aheste aheste çözdük soruları. Pelinsu dedik Mahmut'u hor gördük, şimdi el içine çıkamaz olduk...

---

## Forensics
### Karanlıkta Arayış Başlar
#### 100 (+ 10) Points

> Pelinsu'nun kaybolmasının ardından Mahmut'un hayatı kararmıştı. Hiç zaman kaybetmeden düştüğü bu çaresiz durumda kendine gelmeli ve araştırmalarına başlamalıydı. Kaybedecek tek bir saniyesi yoktu ... 

Ekte baya uzun bir video vardı ve neredeyse tamamı siyah framelerden oluşuyordu. Exiftool ile .mp4 dosyasına baktığımızda :

> IngredientsToPart = time:3984383208960000f254016000000d10160640000f254016000000
>
> IngredientsFilePath = flag.jpg
>
> IngredientsMaskMarkers = None

şeklinde bir çıktı geliyordu. Muhtemelen videonun kısacık bir yerinde flag görünüyordu. OpenCv ve Python kullanarak video’yu frameler şeklinde bir değişkene atayan ve ardından o değişkenin (150,150). pikselini kontrol eden bir kod yardımı ile siyah renkten başka bir renk piksele sahip olan her frame’i dışarı başka bir .jpg dosyası olarak kaydettik.

```
import numpy as np
import cv2

cap = cv2.VideoCapture('26b8351bdd03ce6d1d683bc38786aa3ea2432d45.mp4')

while(cap.isOpened()):
    ret, frame = cap.read()
    if frame[150,150][0] != 0 or frame[150,150][1] != 0 or frame[150,150][2] != 0:
       cv2.imwrite("flag.jpg",frame)
        break
cap.release()
```

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/fikrimin.jpg)

> **DKHOS{f1krim1n_1nc3_gulu}**

### Bildiğim bütün küarlar... Paramparça !
#### 200 (+ 20) Points

> Pelinsu'nun uğradığı birçok lokasyonda kod parçaları bulunmaktaydı. İpucu neydi ?

bir küar'ın parçaları verilmişti. Hepsinin **exif** datasından modify date'ini

```      
    for file in `ls`;do echo $file » test.txt ; exiftool $file|grep "Modify Date"|cut -d ":" -f2-20 » test.txt;done
```

komutu ile test.txt dosyasına çıkardık zaten qr'ın köşeleri belli idi onların tarihindeki dosya sayısı da az olunca **2018:01:28** tarihli resimleri listemizden çıkardık..... gibi saçma sapan şeyler yaptık ama eleyemedik bazı resimlerin dakikaları aynı olduğunu görünce *"herifler zeki çıktı aga"* diyerek başka bişey bulmalıyız başka, başka diyerek Ali Ağaoğlu'na bağlayarak aramaya başladık. Brute atalım desek ordan da gelmez diye düşündük çünkü *"21in 16lı veya 9lu kombinasyonu hiç de az bir sayıya denk gelmiyor"* diyerek vazgeçtik exif datalarının içinden geçtik ancak hiçbir şey beklediğimiz gibi olmadı flag başka bir yerlerde olmalı diyerek. Resimlerin isimlerine odaklandık öyle sapıttık ki teomanın şarkısından bişeyler çıkarmaya çalıştık(gitar tellerine bile baktım ya el insaf) ancak yok, yoktu ulan *"başlarım ama ha"* derken **ipucu neydi?**'nin gereksiz fazlalığı dikkatimizi çekti çünkü ipucu bulamamıştık. İplerin uçlarını not almaya başladık(*bu ne demekse* diyosunuz :D) Soruyu hatırlayalım. Her kelimenin iki "ucu" alındığında gerekli sırayı oluşturuyorduk.

> Pelinsu'nun uğradığı birçok lokasyonda kod parçaları bulunmaktaydı. İpucu neydi ?

Tabii bu aydınlanma ile bir sapıtma durumu oldu ama toparladık ve **pn-uı-bk-la-kd-pı-bı-iu-ni** sırasıyla getirip 3'e 3 lük bir resim oluşturunca(gimp sağolsun ancak ImageMagic'in sağladığı *montage* utility de kullanılabilirdi):

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/quar.jpg)

> **DKHOS{Bunl4r_h3p_M0ntaj}**

### Hadi hoppala vede cuppala
#### 300 (+ 30) Points

> Mahmut Pelinsu'nun eski bozuk harddisklerinden birine analiz çalışması yapar. Disk'in belirli bölümünden elde ettiği veriyi anlamlandırmaya çalışacaktır.

> **Hint:** Acaba disk ile beraber verinin header ve footer'ı da bozulmuş olabilir mi?

Nedense başlarda "diskin bozuk olması" ibaresine dikkat etmeyip verinin XOR'a uğramış olma ihtimali üzerinde durduk. Ancak ipucu ile beraber alet edevatı toplayıp onarıma giriştik. Öncelikle **hexinator** ile hazır **grammer** deneyerek dosyanın tipini anlamaya çalıştık ve hatta **gz** formatına çok benzer olması bizi yanlış yönlendirdi. Ama bir türlü düzelmeyince başka arşiv formatlarına döndük. Sonunda bozuk **header** bizi [buraya](http://www.7-zip.org/recover.html) getirdi. Bağlantı hakkında bir dipnot düşmek gerekirse bir binary dosya onarımı hakkında en kapsamlı anlatımlardan birisi diyebiliriz. 

Bahsedilen **signature** değerinin ilk iki byte'ı değiştirilmişti, ilk olarak onu düzelttik. Daha sonra **footer** konumu yanlış point ediliyor olabilir diye **end header'ın** offset değerini hesapladık ama doğruydu. Bundan sonra düzenlenmesi gereken tek değer **the length of End Header** olarak ifade edilen kısımdı. **Footer** boyutu *0* olarak değiştirildiği için dosya okunamıyordu. *0xb0* offsetinden *0xd5'e* kadar olan kısım 38 byte olduğu için bunun hex dengi olan **26** değerini *0* ile değiştirdiğimizde sağlıklı bir .7z dosyası elde etmiş olduk. Ama dosyanın parola korumalı olması üzdü. 

Bu kadar nezaket yeter diyerek vurduk ağzına. [Şu repo](https://bitbucket.org/dhiru/pylzma-ng.git)daki 7z2john.py ile hashi çıkartıp **john**'dan **rockyou** ile vurduk. Wordlistlerin Tarkanı'ndan gelmezse *"Heijan - Gene mi Amcalar Lyrics"* deneyecektik ama çok şükür böyle bi şey yaşanmadı. Çok sürmeden parolayı **piggies** olarak elde edip flagı öğrendik.

> **DKHOS_{4l_G1rd1n_g1rd1n}**

### Hafıza kaybı
#### 400 (+ 40) Points

> Pelinsu'nun odasında kilitli dolabı açan Mahmut sonunda Pelinsu'nun makinasına erişmiştir. Makina açıkken aldığı imaj üzerinde yeni ipuçları bulmak için çalışmaya koyulacaktır.

***mobilden bağlanan yürek yemiş arkadaşın isyanı:** Eyy ctf yönetimi mega.nz üyelik müyelik dedi 2GB'ımı yedi hala sinirliyim.*

Kilitli dolabın içine uzatma çekilmiş olmasını normal kabul ederek rolümüze devam ettik. Soru isimlerinin özenle seçildiğini farkettikten sonra kafamızda deli sorular dönmeye başladı ama imajlarla yakın dostuz neyse ki.

İlk olarak **volatility** aracı ile verilen imaj üzerinde standart prosedür olan profilleme kısmını yaptık.

```
$ volatility -f for400.img imageinfo
```

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/imageinfo.png)

ardından

```
$ volatility -f for400.img --profile=Win7SP1x86 pslist
```

böyle durumlarda eğer doğrudan şüphelendiğiniz bir process yoksa bunu son seçenek olarak almakta fayda var. **cmd.exe** gördüğümüz için konsolda neler döndüğünü merak ettik:

```
$ volatility -f for400.img --profile=Win7SP1x86 consoles
```

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/consoles.png)

ve gizemli bir string'e ulaştık. **OaX81_Nlrn** tabii bu değerle ileride **clipboard'a** göz atınca da karşılaşacaktık. Aslında sırf biz bulabilelim diye bir de konsola yapıştırılmış, selamlar burdan :) Ya flag buysa diye **Caesar** vb. denemelerimiz boşa çıkınca bunu tekrar dönmek üzere bi kenara not alıp devam ettik. **filescan** pek iç acıcı sonuçlar vermeyince processlere dönmek farz olmuştu. Parent pid'si **explorer.exe'yi** işaret eden **form.exe** (tıhlanmış olduğunu düşündüğümüz için) şüphe uyandırdı ve bu processte karar kıldık:

```
$ volatility -f for400.img --profile=Win7SP1x86 procdump -p 2420 -D .
```

**strings** çıktısı ortamı ısıtmaya yetti. **Foremost** yahut **binwalk** ile içerideki arşiv kolayca elde edilebilirdi. Bu feature örneklemesi hoşumuza gitti açıkçası :)

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/unrar.png)

> **DKHOS{its_N0t_A_BuG_it_is_a_feature}**

### Son parça
#### 500 (+ 50) Point

> İşte bellek işte fidye.
>
> Ya atarsın ya çözersin.
>
> Baktın olmaz vazgeçersin.
>
> Zordur almak bizden kızı.

elimizde bariz şekilde bir şifreli dosya, bir de muhtemelen fidye yazılımı bulaşmış olan imaj dosyası vardı. 

Durum açıktı, standart işlemleri bu imaj üzerinde de gerçekleştirdik ama ilk izlediğimiz yol gizli/enjekte edilmiş zararlı kod var mı bunu kontrol etmekti **malfind** ile:

```
$ volatility -f for500.img --profile=Win7SP1x86 malfind
```

**MZ** header'ı ile **system.exe** üzerinde bir executable izine rastladık. Bu çıktıyı kullanmak çok mantıklı olmayacağı için doğrudan **system.exe** processini dump edip [virustotal](https://www.virustotal.com/) üzerinde bilgi edinmeye çalıştık. 

```
$ volatility -f for500.img --profile=Win7SP1x86 procdump -p 3108 -D ~
```

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/razy.png)

virustotal bunun **Razy** varyantı olduğunu söylese de bunun hakkında güzel bir dokümantasyon bulamamak bizi başka şeylere yönlendirdi. Basit düşünüp imajda **strings** ile decrypt gibi bir string'i arayınca meşhur ransomware bildirimlerinden birinin içeriğini gördük

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/putin.jpg)

capslock açık olarak yazılması **grep** ile çekerken çıktıları elemek açısından işimize geldi. Dolayısıyla ransom adını bulmak umuduyla bi kaç deneme sonunda headshot attık:

```
$ strings for500.img | grep ENCRYPTED
```

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/4.png)

demek ki *strings'i küçümsemiycen* hatta:

> intext:ransomware system.exe

gibi bir Google dorku kullansak da çıkıyor muydu la yoksa dedik... neyse hepsi tecrübe bunların. Fidye yazılımı hakkındaki [analiz](https://blog.malwarebytes.com/threat-analysis/2016/05/7ev3n-ransomware/) ve [@hasherezade](https://twitter.com/hasherezade) tarafından yazılmış [recover-script](https://github.com/hasherezade/malware_analysis/tree/master/7ev3n)'leri son noktayı koyacaktı. Birinci scriptle dosyamıza kavuştuk. 

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/Chrysanthemum.jpg)
 
> **DKHOS{R4nsomWARe_so_h0t_now}**

Böylece forensicste "son parça"yı da yerine koymuş olduk. Sorularda böyle gerçekçi senaryolar işlenmesini ayrıca takdir ediyoruz.

---

## Reversing
### Tamirci Pala Remzi
#### 100 (+ 10) Points 

> Pelinsu'nun eski ipad'ini uzun uğraşlar sonucunda telefon tamircisinden geri alan mahmut cihazı yeniden başlatır. 
>
> Ekran açılır. Youtube'dan video oynamaya başlar. https://www.youtube.com/watch?v=o_TKIM1vUEs
>
> Acaba Pelinsu burada olabilir mi ? diye düşünür Mahmuıt.
>
> Video sonunda bir anda Mahmut'un önünden sayılar akıp gitmeye başlar.

Linkteki videodan zaten manchesterlı bi şey olduğu netti, yorumlara bakmak gereği bile duymadık ancak manchester codingi biraz geç bulduk(soruların üzerinden 4-5 kere geçtikten sonra) ve dururmuyuz yapıştırdık cevabı çılgınlar gibi (şuraya)[https://www.dcode.fr/manchester-code]

> 0010101001011111001111110100111001101001010100110110100101001101010111110111001001101001010110100110
> 0001010010000101111101110010011011110111100101101001011011000101001101100001010000100101111100101010

iddiaya göre decode edilmiş haliydi.

onu da (binary to texte)[https://www.rapidtables.com/convert/number/binary-to-ascii.html] verdik ve

> \*_?NiSiM_riZaH_royilSaB_\*

bunu flag olarak denesek de yemedi. Ama tokadı yeyince nevri döndü:

```
$ echo -n "*_?NiSiM_riZaH_royilSaB_*" | rev
```

> **DKHOS{\*_BaSliyor_HaZir_MiSiN?_\*}**

---

## Crypto

Sıra Türkiye'de genelde en sevilmeyen/zorlanılan kategoride.

### Sevgili günlük
#### 100 (+ 10) Points

> Mahmut Pelinsu'nun gizli mesajlarını içeren günlüğünü elde etmişti. İlk sayfalarda Pelinsu'nun amatörce kullandığı şifreleme algoritmaları hemen dikkatini çekti. İşe koyulmuştu.

verilen dosya **file** denetiminden geçirildiğinde **tar** arşivi olduğu anlaşılıyordu. İçerisinde iki dosya vardı. RSA sorusu olarak kabul edip devam ettik.

```
$ openssl rsa -text -pubin -modulus -in public.key
```

yaptık ama olmadı. Dosya içeriğine baktığımızda normalde var olması gereken şu blokların kaldırıldığını farkettik:

> -----BEGIN PUBLIC KEY-----
> 
> -----END PUBLIC KEY-----

tekrar deneyince

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/5.png)

**exponent** ve **modulus** değerlerini elde ettik ancak bize modulusun onluk değeri lazım o yüzden bi kaç çalım atıyoruz:

```
$ python -c "Modulus='C9BC6E819D316A23A75EA29AA7428634617C09A6E77A25C8884CD405DFB7CAA3705D8FD5C7DBD1930EADB3FB4D4601E330ADD121F4F7CC515253B101D310D9DBB3A72ECA36A1DE62A6F4D573F5FB71CADB017579DCE149E9'; print int(Modulus, 16)"
```

> 6632244363219241539342517741426140435091338047212321402880722352853794811833079890571413882419715376524737
> 9054455347435534039717825091371646535671796379604222638975797104335872803093974396756169372117357815745001

sonra bunun hangi **p** ve **q** değerleri ile elde edilebileceğini bulmak için [factordb](http://factordb.com/) üzerinden sorguluyoruz:

> 8143859259110045265727809126284429335877899002167627883200914172429324360133004116702003240828777970252499

bunun karesi olarak oluşturulabiliyormuş. Şuan gerekli tüm değerleri elde ettik, [rsatool](https://github.com/ius/rsatool) ile **private key** dosyasını oluşturabiliriz:

```
$ rsatool.py -p 8143859259110045265727809126284429335877899002167627883200914172429324360133004116702003240828777970252499 -q 8143859259110045265727809126284429335877899002167627883200914172429324360133004116702003240828777970252499 -e 65537 -o key.pem
```

ve flag'e son adım

```
$ openssl rsautl -decrypt -inkey key.pem -in flag.txt.enc
```

> **DKHOS_{b4by_h3ll0_w0rld_crypt0_b4by}**

> ***not:** Kripto çözdük diye sevinecektik de flag metni gerçeği yüzümüze vurdu, sal da sevinelim ya*

---

## Trivia
### Seç bakalım, şimdi sayı söyle
#### 100 (+ 10) Points

>Mahmut ile Pelin küçükken hep bu oyunu oynarlardı...

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/tuzluk.png)

kategori trivia olunca resmi [googleladık](images.google.com) ama o bize *мобильные телефоны сертификат соответствия*'yı verdi.

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/nigga.gif)

durum öyle olunca ne varsa normal Google'da var diyerek bir iki sorguyla tuzluk oyununu bulduk. Hiç de yabancı değilmişiz meğer:

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/kara.jpg)

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/mela.jpg)

> **KARAMELA**

### Geçmişe yolculuk
#### 200 (+ 20) Points

> Camın üzeri buğuluydu. Şimdilik resmini çekerim, sonra daha detaylı incelerim diye düşünmüştü Mahmut. Pelinsu'nun izlerini geçmişte de birileri aynı yöntemlerle araştırmış olabilir miydi.

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/noktalar.png)

Bazı çabalarımızdan sonra (exiftool, binwalk), resim üzerinde oynamalar yapmamızı sağlayan bir [site](%28https://29a.ch/photo-forensics/#forensic-magnifier%29) bulup şansımızı orada denemeye karar verdik. Component Analysis kısmında oynama yapınca:

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/6.png)

> ***not:** Sorunun triviadan çok steganografi kapsamında olduğunu düşünüyoruz ama başlığında ve açıklamasındaki "geçmişe" yapılan atıflara bir anlam yükleyemediğimiz için trivia kısmına vakıf olamamış olabiliriz de pek tabii.*

> **DKHOS{UNSTOPPABLE}**

### Bana olasılıkları asla söyleme
#### 300 (+ 30) Points

> Pelinsu Mahmut'a kaybolmadan önce bu traş bıçağını gönderdi. Kargo paketinin içindeki ufak bir notta ise; "bunukullananadamınyanınagidiyorumbenioradabul" yazmaktaydı.
> Mahmut bu kargonun gerçekten Pelinsu'dan geldiğinden emin olamasa bile araştırmaya koyuldu ... Ayrıca Pelinsu'nun yazdığı yazının boşluksuz, arada çizgi olmadan ve hepsi küçük harf olması da bir anlam ifade etmekteydi...

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/gilette.jpg)

*Seç bakalım, şimdi sayı söyle* faciasından sonra Google Images'a bir şans daha verdik. Sonuçları ilk bakışta alakasız bulsak da değerlendirmeye aldık. Şu resim üzerindeki ismi denediğimizde puanı aldık:

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/filette.jpg)

> **DKHOS{quigonjinn}**

### Kişi faizi
#### 400 (+ 40) Points

>  Pelinsu son aramalarında amcası ile uzun uzun konuşmuştu. Pelinsu'nun amcası Frank Stephens'ın öldüğünü bildiren belgenin tarihi Mahmut için önemli olabilirdi. 

Soruya bakar bakmaz hemen bunun Person Of Interest adlı dizinin birinci sezon üçüncü bölümünde ki Frank Stephens’den bahsettiğini...
.
.
.
öhöm
.
.
.
soru başlığındaki Türkçe katliamı bizi çok işkillendirdi. Öyle ki ilk gün daha ipin ucu falan ortalarda yokken translate üzerinden İngilizce'ye çevirmeyi denedik ama translate'in azizliğine (individual interest!!!) uğradığımız için çözemedik bi süre. İpucunun ardından parlak(bunu da çevirin) bir arkadaşımız kastın **Person of Interest** olduğunu anladı.

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/kisi.png)

Şükür ki bir diğerimiz de diziyi izlemiş, -kendisi çok öneriyor bu arada-. Birkaç [aşamadan](http://personofinterest.wikia.com/wiki/Stacey_Miles) sonra 

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/kisifaizi.jpg)

> **DKHOS{2006MAY30}**

### Av mevsimi
####  500 (+ 50) Points 

>  Pelinsu'nun kamerasını inceleyen Mahmut en son bu video'ya ulaştı. Defalarca izledi ancak ne anlama geldiğini çözememişti... 

şöyle bir ss koyalım videodan:

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/avmevsimi.jpg)

Önceki ctf tecrübelerimizden de bildiğimiz gibi saçma sapan pek çok alfabe var, bunun da onlardan biri olduğuna hepimiz yemin edecek düzeydeydik. Başta bu alfabeyi yüzüklerin efendisinden sanıp yorumlamaya çalışsak da

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/yuzuk.jpg)

Burada kitlenip kaldık sonra ipucunun(görselin)

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/asa.jpg)

ve yine soru adının yardımıyla alfabenin "alien vs predators" filmine ait olduğunu hatırlayıp

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/alf.jpg)

Yautja isimli saçma alfabeyle

> **DKHOS{AZTEC}**

---

## Mobile
### Ayrılığın hediyesi
####  100 (+ 10) Points 

> Pelinsu'nun uzun zamandır kullandığı bir cep telefonunu en yakın arkadaşlarından biri Cansu'ya vermişti. Pelinsu'nun kaybolduğunu öğrenen Cansu ise telefonu hızlıca 
> Mahmut'a ulaştırmış ve analiz etmesini istemişti. Yakın zamanda bir adresten gelen eposta içerisindeki bir .apk Mahmut'un dikkatini çekmişti. 

Verilen apk dosyası üzerinde klasik işlemlerden sonra (bkz.strings,emulator) dosyayı extract ettik(bu klasik değil gibi). Velhasılıkelam, Androguard'ın kapısını çaldık:

```
$ androlyze -s
```

dosyamızı açtık

```
$ a,d,dx = AnalyzeAPK("20d0e07e19a3c91b8259afe0c591319e22af6cee.apk", decompiler="dad")
```

stringlerin gücüne inanmamız gerektiğini hatırlayarak

```
$ d.get_strings()
```

gelen çıktının en üst kısmında şekil bir font bizi karşıladı

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/imdat.png)

> ***not:** fontun adını bilen varsa şaaparsa mesud eder bizi*

> **DKHOS{IMDAT}**

---

## Cyber Intelligence

Bu sorulardan sonra nerde Hollanda dense sizi hatırlıycaz. Gitmeden sokaklarında süründük ne de olsa

### Sokaklarda ne ararsın beni kimden sorarsın
####  200 (+ 20) Points 

> Mahmut ulaştığı kayıtları incelediğinde Pelinsu'nun lokasyonunun çocuğun çantasında gizli olduğunu düşünmekteydi. 

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/sokak.jpg)

Elimizde bir adet resim ve bir adet video mevcuttu. Video’da, yerde "maak je foto vanaf hier" şekilde bir yazı görünüyordu. Bu yazıyı Google’da aratınca şu [siteyi](https://abandowest.wordpress.com/tag/maak-je-foto-vanaf-hier/) buluyor, buradan da translate yardımı ile bu yerin **Bastiaansplein, Delft** denen bir yerde olduğunu buluyoruz. Karşıdaki **Jumbo** tabelasını da bunlarla birleştirince Google Street View kullanarak biraz bölgede takılıp keşif yaptıktan sonra soruda verilen resimde ensesi görülen çocuğa denk geliyoruz. Cevaptan korktuğumuz için ensesine yanaşıp *Sarıların Sülo sen misin?* demiyoruz. Onun yerine [ön açıdan](https://www.google.com.tr/maps/@52.008904,4.3638221,3a,15y,10.9h,79.73t/data=!3m7!1e1!3m5!1sbjj9h-6CBWVieMUIY_8_YA!2e0!6s//geo1.ggpht.com/cbk?panoid=bjj9h-6CBWVieMUIY_8_YA&output=thumbnail&cb_client=maps_sv.tactile.gps&thumb=2&w=203&h=100&yaw=310.40805&pitch=0&thumbfov=100!7i13312!8i6656) bakıp çanta kolundaki yazıyı flag olarak giriyoruz:

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/dakine.png)

> **DKHOS{dakine}**

### Naber?
####  300 (+ 30) Points 

> Pelinsu zamanında en yakın arkadaşı hipster_koder ile görüşmekteydi. Mahmut hipster_koder'ın Pelinsu'ya platonik aşık olduğunu bilmekteydi. Her ihtimalde Pelinsu hakkında yeni bilgilere ulaşmak için araştırması gerekecekti. 

hipster_koder denen arkadaşı sosyal medyayı tararken Instagram'da [bulduk.](https://www.instagram.com/hipster_koder/) Ekran kasmak doğamızda olduğu için GitHub hesabı gözden kaçmadı tabii. *Çok büyük proje'nin* geçmişine göz gezdirirken ilginç bir commit ile iki satırın kaldırıldığını gördük. 

> Username = 'haker_hater'
> Password = 'Pasw0Rth123'

nerede kullanacağımıza karar verememişken bir de [fork](https://github.com/n3cr0l1c/ElCabukluguMarifet/commit/711726537426dbd81cd6cc085f78eb9438bae1f2) gördük. Pastebin üzerinden login kısmı başarısız olunca url üzerinden **/u/** ile belirtilen bağlantıya ulaştık. Araba Sevdası'nın özetini pastebin'e yapıştıran psikopat heçkır kardeşimiz şunu paylaşmayı unutmamış neyse ki:

> Çok Gizli İletişim Kanalı:
>
> 9CAKIJXEOCiBWnvYuEQRoI

sorunun başlığı her ne kadar *Whatsapp??* diye bağırsa da "Heykır adam Whatsapp grup linki mi paylaşacak? İlla paylaşacaksa Telegram linki paylaşırdı" diye ısrarla telegram, IRC falan denedik. Sonunda dönüp dolaşıp inadımızı kırdık, Whatsapp link örneğine bizimkini [iliştirdik](http://chat.whatsapp.com/9CAKIJXEOCiBWnvYuEQRoI).

> **DKHOS{b3nims1n_p3lin5u}**

### Arap saçına döndüm, çöz beni arap saçı
####  400 (+ 40) Points 

> Pelinsu acaba Hollanda'dan kalkıp savaş bölgesine doğru gitmiş olabilir miydi ? Buraları iyi bilen birilerini araştırmak gerekecek ...
> 
> joinchat/AAAAAESbwxmZjRyggLlfqA

önceki sorudan sonra bu ilaç gibi geldi. Telegram kanalına dahil olduk, bu noktada insan kendini ejan moduna sokuyor aman sakin. Orada gerekli talimatlar verilmişti.

![]({{ AUCyberClub.github.io }}/assets/img/dkhosctfcozumler/arap.png)

İpucu ile [liveuamap](https://isis.liveuamap.com) üzerinden belirtilen konuma gittik ama orada bi mevzu yoktu. Kanala tekrar dönüp Hicri/Miladî dönüşümü ile tarihi filtre olarak ekleyince habere ulaştık. Haberin kaynağını bile incelesek de o an çözemedik çünkü sitede dil olarak Türkçe set edilmişti bizim için. Dolayısıyla hiç yorum yapılmamış görünüyordu. Sonradan ingilizce yaptığımızda doğru yerde olduğumuzu anladık. Bizimle ilgili olabilecek yorumları/kişileri inceleyerek aşağı indik. **Abdüddar** flag bende diye haykırıyordu.

> ***not:** Bu ismin de diğer her şey gibi özellikle seçildiğini düşünüyoruz, atmosferi güzel sorulardan birisiydi.*

> **DKHOS{b4rbuny4}**

---
**[Mahmut Sami Karaca](https://twitter.com/msamikaraca_)** | **[Behçet Şentürk](https://twitter.com/BehetSenturk)** | **[Engin Demirbilek](https://twitter.com/hyal0id)** | **[Hüseyin Erdem](https://twitter.com/rootofarch)**
