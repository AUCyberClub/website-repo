---
layout: post
title: PoineTR CTF Çözümleri
date: '2017-12-14 20:51:00 +0300'
categories: blog
---
__poineTR CTF Çözümleri__

8-12 Aralık tarihleri arasında SDU BT ekibi tarafından düzenlenen CTF'in çözümlerini içermektedir. AUCC CTF ekibi olarak bu CTF'e katılım sağlayıp, sorulan tüm soruları çözerek birinci bitirmiş bulunmakyız.

CTF'in sitesine erişim için [şuraya](http://poinetr.com/) tıklamanız yeterli ancak domaine erişilemediği için [şu linki](http://webcache.googleusercontent.com/search?q=cache:poinetr.com) kullanabilirsiniz.  

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/scoreboard.jpg)

__Başlarken__  
__Flag Format & Kurallar__  
İçerikte yarışma kurallarından bahsediliyordu, en altta da flag formatı paylaşılmıştı.

*poinetr_{kolayGelsin}*

**Yarışma Formatı Hakkında**  
Yine yarışmada hızlı olmanın önemini vurgulayan bir bilgilendirmenin ardından aşağıdaki format paylaşılmıştı.

*poinetr_{ekipCalismasi}*

**Osint**  
**Bul Beni Kaybolmuşum**  
"Elimize böyle bir konuşma geçti.
Ne bulabilirsek artık...

( hepsi küçük & boşluklar yerine alt çizgi )" 

soru metni ile bir jpeg dosyası verilmişti. Dosya üzerinden ulaştığımız linkte exif bilgilerinde GeoTag'ine sahip bir fotoğraf vardı. Haritalar üzerinden koordinatları girdiğinizde Cengiz Aytmatov Caddesine ulaşıyordunuz.

*poinetr_{cengiz_aytmatov}*

**Karakterlerle Savaş**  

"017001001005  
021002001037  
021006004013  
127001003026  
127001001035  
036001001010  

Sana bir kitap vermiştim hatırlıyor musun ?

-->>Parolamı Bulur Musun ?"

Parolamı bulur musun? sorusunu bundan önce çözdüğümüz için ne olduğunu idrak etmemiz uzun sürmedi. Elimizde bir PDF vardı ve içinden belirli şeyleri cımbızlayacaktık. Ancak çözüm için farklı yöntemler denesek de(sayfa-satır vs.) doğru yöntemi bulamadığımız için sona bıraktık, ipucu yayınlandıktan sonra denemediğimiz şeyin "paragraf" etkeni olduğunu farkettik. Üçlü gruplamanın ardından *sayfa-paragraf-satır-harf* sırası izlenince "revolt" stringi elde ediliyordu.

*poinetr_{revolt}*

**QRception**  

"qr.svg" isimli bir dosya linki paylaşılmıştı. Tabii ilk olarak bu karekodu [online bir serviste](https://online-barcode-reader.inliteresearch.com/) decode ettik. Oradan [şu youtube linki geldi](https://www.youtube.com/watch?v=0iyiKI8H-DU) Yorumlarda base64decode edildiğinde *Daha Fazla Yorulma Flag Buralarda Değil.* çıktısını veren bir string vardı. Aranırken sorunun title'ı dikkatimizi çekti. "Qr in here" diyordu. Kaynak koda baktığımızda *image/png* tipinde base64 encode edilmiş farklı bir veri vardı. Bunu çektiğimizde farklı bir karekod geldi. Aynı servisten decode yapınca bayrağı elde ediyordunuz.

*poinetr_{christ0pher_n0lan}*

**Yolumu Çizdim**  
*yolumu-cizdim.kml* isimli bir dosya paylaşılmıştı. KML dosyaları coğrafi verileri XML formatına dayalı şekilde tutmayı sağlayan bir dosya formatı. Öncelikle [online herhangi bir servis üzerinden](http://kmlviewer.nsspot.net/) şansımızı denedik, bazı pathlerin haritada işaretlendiğini ve sanki anlamlı bir kelimeye benzediğini düşündük -Bu arada lokasyon İspanya Barcelona'dandı. Ancak pek de anlamlı görünmeyen bir string geldi. Daha sonra dosyayı raw olarak görüntüleyince aslında yorum satırları barındırdığını farkettik. Bunları kaldırıp tekrar deneyince flag geldi.

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/yolumucizdim.png)

*poinetr_{ciddi_misin}*

**NS**  
"poineTR.com nereye işaret ediyor? Yoksa orda bir Harry Potter karakteri mi var?"

poinetr.com adresinin DNS çözümlemesini yaparak NS kaydını sorgulamamız istenmiş.
```
$ dig ns poinetr.com
```

diyerek *lily.ns.cloudflare.com* sonucunu alıyoruz. Buradan sevgili Lily Potter'a selam olsun.

*poinetr_{lily}*

**Sızıntı**  
Bir FBI personelinin parolası isteniyordu. Elimizde telefon numarası vardı. (205) 279-1457
Numara ile ufak bi araştırmadan sonra "paul.daymond@ic.fbi.gov or (205) 279-1457" bilgisine ulaştık([bkz](https://www.fbi.gov/contact-us/field-offices/birmingham/news/press-releases/beyond-the-bridge-police-and-community-engagement)) buradan sonra parolaya ulaşmak zor olmadı.

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/sizinti.jpg)

*poinetr_{09172jksdf9812}*

**Follow Me**  
"76 yaşında oldukça güzel bir kadın. Bir rivayete göre beyaz tavşanlarla da arası iyiymiş. Yerine geçtiği kadın akarboz almak zorunda olduğundan daha fazla hayata tutunamamış. Sanki ona daha çok yakışıyordu. Sahi kimdi o ?"

Başlarda davşandan ötürü Alice üzerinde çok odaklandık. Hatta konu bi ara Lost'a Fionnula Flanagan'a kadar geldi :) ancak akarboz burada kilit kelime rolü gördü. Kahin ablamızı bağdaştırmak uzun sürmese iyiydi [link](https://tr.wikipedia.org/wiki/Kahin_(Matrix)) (erişemiyorsanız da en azından önbelleği görüntüleyin :D)

*poinetr_{Gloria Foster}*

**Misc**  
**Bunu Duyunca Mors Oldum**  
Verilen mp3 dosyasındaki sesler mors alfabesi ile yazıp daha sonra morse decode yaparak bayrağa kolaylıkla erişebilirdiniz.

*poinetr_{samuel_morse}*

**Her Şey Göründüğü Gibi Olmayabilir**  
"Ya göründüğün gibi ol ya da olduğun gibi görün..."

bir rar arşiv dosyası verilmişti. Açmaya çalıştığınızda parola girmenizi istiyordu. Tecrübe kaynaklı olarak direk dosya adını parola yerine denedik ve başarılı olduk. Buna *rar2john* hashi elde ettikten sonra *john* a vererek de ulaşmak da mümkündü tabii. İçinden 49 adet zip ve bir adet de poinetr02.. diye devam eden rar geldi. Anlaşıldığı üzere bu devam edip giden bir seriydi. Biz de riske atmamak adına ufak bir script yazdık:
```
import os
for i in xrange(1,10):
    command = "unrar e -y poineTR0" + str(i) + ".rar -ppoineTR0" + str(i)
    os.system(command)
```
sadece 8 tane varmış oysa ki :) başlıkta belirtildiği üzere çıkan onca zipin aslında zip olmayacağı aşikardı. Bu yüzden scriptimizde ufak bir değişiklik yapmamız gerekti:
```
import os
for i in xrange(1,10):
    command = "unrar e -y poineTR0" + str(i) + ".rar -ppoineTR0" + str(i)
    os.system(command)

for i in xrange(1000,9999):
    command = "mv " + str(i) + ".zip " + str(i) + ".png"
    os.system(command)
```
ve bizi şaşırtıcı olmayan şekilde bir sürü pokemon kucakladı, özlemiştik kendilerini. Ancak 4 tane farklı resim vardı bunları birleştirince flag geliyordu. 

*poinetr_{s3ni_sect1m}*


**Malware**  
Soruda bir png dosyası verilmişti. Biz başlık "malware" olunca soruya çok farklı baktık, o yüzden online servislere dönmemiz biraz geç oldu. Virustotal üzerinde dosyanın hash ini ararsanız Community sekmesinde *ctfhunter* isimli arkadaşın flag'i paylaşmış olduğunu görürdünüz :)

*poinetr_{analyzing_malware}*

**Don't Click Me**   
"Çift tıklayarak açamazsın beni."

başlangıçta bu soruda çifti geçtik tek tıklayacak bir şey de yoktu :) biz o an bunda derin manalar ararken soru güncellendi, meğer link eksik kalmış :)
Başlık üzerinde yeterince düşündüğümüz için dosyayı komut satırında çalıştırmayı denedik ve meyvesini aldık.

*poinetr_{d0nt_d0uble_click}*

**Kupa Kızı Sinek Valesi**  
Bu soru da sinir bozucu sorulardan birisiydi. Daha ilk başlarda ekipten birisi parçanın orjinal klibinin altında soru ile ilgili olduğunu düşündüğümüz bir yorum buldu.
>Artık eskisi kadar kolay yorumu bulamayacaksın😝😝 mesajın diğer bölümlerin, de anlamak için üçlü şifrelemeyi araştır ve bu sayıyı bir yere not et 05077( bu sayınının üçlü şifrelemesiyle alakası yok ama bu da bir bilmece(diğerleriyle birleştir)﻿

ancak bu yol göstermekten ziyade akıl karıştırdı :D biraz süründükten sonra sayı sistemlerine döndük  ama orda daha fazla süründük. Ancak şundan emindik;
>X98 AX5 AA0  X97 AA4 A2A X95 AX9 AX5 X95  AX7 AAA A2A AA5 X97 A2A AXX AX5 AX7

elimizdeki veri buydu. Ortada iki bilinmeyen vardı. 
>CTF'lerin kuralı; ortada iki bilinmeyen varsa bunlar 1 ve 0'dır.

dedik ve elimizde ASCII olması kuvvetle muhtemel bir dizi vardı.
>098 105 110  097 114 121 095 109 105 095  107 111 121 115 097 121 100 105 107

ve [buradan](https://convert.town/ascii-to-text) çevrilmesi ile birlikte flag'e ulaşmış olduk

*poinetr_{binary_mi_koysaydik}*

**Who are you ?**  
"WhoAmI" adlı bir jpeg imiz vardı soruda. Elf gözlü bir arkadaşımız resimde flag gördüğünü iddia etti. Başta inanmasak da dikkatli bakınca doğru olduğu kanaatine vardık :D

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/whoami.png)

*poinetr_{low_mrx}*

**18. yy.**  
"Çook eskiden kullanılan bir karton buldum. Biraz garip. Üzerinde bi şeyler yazıyor ama biraz yıpranmış. Onarabilirsen okutabiliriz ..

(hepsi küçük)"

resmi biraz araştırdığımızda "punch card" kavramına ulaştık. Bu [servisten](http://www.masswerk.at/keypunch/) el ile decode edilebiliyordu.

Önce alfabe oluşturduk;

*WARNING! GRAPHIC CONTENT*

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/18yy.jpg)

Daha sonrasında decode işlemini gerçekleştirdik;

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/18yy-2.jpg)

*poinetr_{muhammedali}*

labirent sorusuna geldiğimizde scoreboard durumu şu şekildeydi:

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/labirentscr.jpg)

**Labirent**  

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/labirent.jpg)

Yarışmada en son çözdüğümüz soruydu. Son etapta yayınlandığında ilk uğraştığımız sorulardandı ancak çözemeyince sona bırakma kararı aldık. O kadar Exif, flow chart, forensics uğraşları sonrasında "Flag bu mu ola ki" edasıyla o çizgileri deneyerek sonuca ulaşmak bizi hakikaten üzdü. Bu flag'i gözlerimiz yaşlı girdik submit alanına...

*poinetr_{node}*

**Forensics**  
**Arama**  
Soruda verilen fotoğrafı öncelikle google üzerinde aradık ancak sadece Elon Musk'a ait olduğu sonucuna vardık. Daha sonra başlık forensics olunca sıradan her şeyi denemeye başladık(foremost, binwalk, header footer bilgileri, strings, exifdata, jpg-markers vs.) derken dosyanın adındaki hashten "elonmusk" çıkınca *steghide* bile denedik. Ancak daha sonra basit bir sorgu ile ulaştığımız [şu adreste](https://www.wikihow.com/Hide-a-File-in-an-Image-File) durum açıklanıyordu. Aklımıza gelmeyişi bizi yordu açıkçası. Dosyanın uzantısını Windows makinede .7z olarak değiştiriyoruz ve çıkartıyoruz arşivden. Parola sorduğu zaman da "elonmusk" bilgisini kullanıyoruz:

>Kurucularından biri olan bu adamın güzel bi servisi vardı.
>Mayıs 2016'da Türkiye'deki faaliyetlerini durdurdular.
>Benim için müşteri hizmetleriyle görüşür müsün ?
>(Hepsi birleşik && özel karakter yok)

buradan hareketle PayPal'ın iletişim numaralarını denemeye başladık ancak bir türlü tutmadı. Araştırmayı bölgesel yapmak yerine küresel olarak yapınca doğru numaraya eriştik.([bkz. paypal customer service number](https://www.google.com.tr/search?q=paypal+customer+service+number&ie=utf-8&oe=utf-8&gws_rd=cr&dcr=0&ei=EwYqWofOKYb4wQKz25noBA))

*poinetr_{0014029352050}*

**SDÜ Bank**  
Yandex.disk üzerinden bir ses dosyası paylaşılmıştı. İçeriğinde kayıt altına alınmış sözde müşteri hizmetleri görüşmesi vardı :) Tuşların sesinden veriyi elde etmemiz gerekiyordu. Bunun için [şurayı](http://dialabc.com/sound/detect/) kullandık ancak servisten kaynaklı olsa gerek tek seferde en fazla 12 haneyi decode edebiliyordu. Bu yüzden ses dosyasını 3 parçaya bölerek decode ettik. *Kart numarası: 2547 8552 2632 4771 Şifre: 4578*

*poinetr_{25478552263247714578}*

**Böyle Parola mı Olur ?**  
Soruda verilen dosya header'ından anlaşılacağı üzere Minidump crash report. Gentilkiwi abimizi özlemiştik biz de zaten. Hemen powershell'imize geçiyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/boyleparolamiolur.png)

*poinetr_{7488e331b8b64e5794da3fa4eb10ad5d}*

**Parolamı Bulur Musun ?**  
"Buralarda bi yerlerde olacaktı :(" 

Dosyayı irdelediğimizde dos/mbr boot sector olduğunu görüyoruz. Ancak imaj partition'a sahip olduğu için ek bir parametreye gerek duymadan mount edebiliyoruz. İçersinde secret.rar adlı arşiv vardı, parola olarak yine "secret" denedik ancak bu defa olmadı. Başka yerlere bakmaya başladık ve çok geçmeden bir txt içersinde "freed0m" u bulduk. Parolanın bu olduğu aşikardı tabii ki. Arşivden doğrudan flag geldi.

*poinetr_{found_pass}*

**Elektrikler Kesildi**  
"En son bi şeyler karalıyordum elektrikler kesildi. Oof of.." 

verilen mem.mem dosyasını elektrikler kesilmeden hemen önce alınmış bellek dökümü olarak kabul ediyoruz ve volatility ile incelemeye başlıyoruz. 
```
$ volatility -f mem.mem imageinfo
```
ile dump için profil belirliyoruz
```
$ volatility -f mem.mem —profile=WinXPSP2x86 pslist
```
ile açık olan processlere bakıyoruz bi umut notepad yerse diye de
```
$ volatility -f mem.mem —profile=WinXPSP2x86 notepad
```
deniyoruz ancak sadece açık bırakılmış, Paintten kaçış yok daha önce Google'ın ctfindekine benzer bir soru anlaşılan diyor ve pslistten mspaint.exe nin PID'sini alıp çekmek için kullanıyoruz
```
$ volatility -f mem.mem —profile=WinXPSP2x86 memdump -D=msdump/ -p 1044
```
Çıkan dosyamız dump olduğu için nasıl okuyacağımız konusunda ufak bir araştırma yardımcı oluyor. Uzantıyı data yaparak GNU Manipulation ile inceleyebiliyoruz. Ancak burası değeri bulana kadar biraz sayısal loto tadında oluyor, ilk bulduğumuz şey buydu ama pek flag'e benzemediği için aramaya devam ettik

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/elektrik-1.jpg)

ancak daha sonra  

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/elektrik-2.jpg)

ve revert edilince de  

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/elektrik-3.jpg)

*poinetr_{ram_an4liz}*

**Ahengi Bozan Bir Şeyler Var**  
Parçayı dinlemeye başlıyoruz ancak başlıkta denildiği gibi araya tam 02:06 dolaylarında bir cızırtı giriyor. Önce Audacity ile inceledik, ancak string'in netleştirilmesi konusunda çok tatmin olamayıp, Sonic Visualizer'a geçtik. Spectogram katmanını Mixed channel için ekleyip belirtilen dakikaya geldiğinizde flag net şekilde görülüyordu.

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/ahenk.png)

*poinetr_{ritmi_hisset}*

**Web**  
**Meta Refresh**  
Lynx ile adrese erişim sağladığımızda flag'i buluyorduk. Lynx <3

*poinetr_{s0urce_cod3}*

**Sen poineTR Değilsin**  
Soruda poinetr olarak istek atmamız bekleniyordu. Bunun için Burpsuite ya da zap proxy benzeri araçlar ile user-agent bilgisi düzenlenip istek atılması yeterli idi.

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/poinetrdegilsin.jpg)

*poinetr_{user_4g3nt_forever}*

**No Database**  
Adresin kaynak kodunda 
```
<!-- not using any database system. crentials is harcoded. -->
```
bulunuyordu. Buradan hareketle nosql inj. olabileceğini düşündük. Ve burp üzerinden parametrelerin sonuna *[$ne]* ekleyerek veriyi gönderdik. 

*poinetr_{vuln3rabl3_functi0n}*

**Analiz**  
[Ödüllü Soru]

"Buralarda bir yerde diyor. Nerde hani ?"

Sayfada biraz gezindik Inspect Element ile sayfayı incelerken console sekmesine geldiğimizde flag bizi karşıladı. Böyle olmasını beklemiyorduk :)

*poinetr_{l0g_analyz3r}*

**İçeri Al**  
Yine kaynak kodda bir ipucu vardı.
```
<!-- S3cret file in ac1ac95caeada6a929fde9dbc33f810b -->
```
URL'deki "file=" parametresi yolu girilen dosyayı include ediyordu büyük ihtimalle. Başta yorum satırında verilen yolu bir üst dizinde aradık ancak olmayınca bulunduğumuz dizinde aradık. Parametre olarak *ac1ac95caeada6a929fde9dbc33f810b/S3cret* vermek yeterli idi.

*poinetr_{l0c4lfile_inc}*

**Login**  
Bu soru kolay bir soruydu ancak Wargame kategorisinde anlık bir durgunluk yaşayana kadar bakma fırsatımız olmadı. Soruda adresi yine F12 ile incelemeye başlayınca form olduğunu farkettik ancak *display:none* atanmıştı. Onu kaldırdıktan sonra bir iki denemede gördük ki form boş alana izin vermiyor. Sıkıysa Burpte söyle bunu dedik ve kullanıcı adı kısmında standart blind sql injection uygulayıp parola alanını boş olarak gönderdiğimizde flag bize Set-Cookie değeri ile döndü.

*poinetr_{l0gin_byp4ssTR}*

**Reverse**  
**Güç Değişkende Gizlidir**  
Executable ilspy ile incelendiğinde flag cleartext olarak karşımıza çıkıyor.

*poinetr_{w0lf_4l0n3}*

**Kırmızı Başlıklı Exe**  
Verilen dosyanın executable olmasını bekliyoruz ancak bi kaç ufak sorun farkediliyor. Hemen bir "hello world" executable ı oluşturup header kıyası yapıyoruz ve değiştirildiği ortaya çıkıyor. Düzeltmenin ardından program çalıştırıldığında flag değerine ulaşıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/poinetrctfcozumler/kirmizi.jpg)

*poinetr_{!r3v3rs3}*

**Crypto**  
**13 & Base**  
"Mzj0Ml10AT0gZTj0pwEeYJW1"

ROT13 sonrası base64 decode işlemi

```
echo 'Mzj0Ml10AT0gZTj0pwEeYJW1' | tr 'A-Za-z' 'N-ZA-Mn-za-m' | base64 -d
```
*poinetr_{fl4g-t4m-0l4r4k-bu}*

**Base32**  
"MRQWQYK7NZSWYZLSL53GC4S7NZSWYZLS"
```
echo 'MRQWQYK7NZSWYZLSL53GC4S7NZSWYZLS' | base32 -d
```
*poinetr_{daha_neler_var_neler}*

**Base64**  
"YnVfZGFoYV9iYXNsYW5naWM="
```
echo 'YnVfZGFoYV9iYXNsYW5naWM=' | base64 -d
```
*poinetr_{bu_daha_baslangic}*

**MD5**  
"63a9f0ea7bb98050796b649e85481845"

hashi google da aratmak yeterli

*poinetr_{root}*

**Sen de mi Brütüs**  
"vhcdu_zdv_khuh" [şurada](https://www.dcode.fr/caesar-cipher) caesar bruteforce yapıyoruz

*poinetr_{sezar_was_here}*

**Vigenere**  
”wolem_bxgn”
– poınetr

yine [buradan](https://www.dcode.fr/vigenere-cipher) key olarak "poınetr" kullanıp çözüyoruz

*poinetr_{hayat_kisa}*

**To Be Or Not To Be**  
Bu soruda script yazmak zevkli olabilirdi. Ancak sürenin öneminin daha da arttığı bir zamanda Notepad++ ile replace yapmak en hızlısı idi. SDU ve BT'lerin ikili gösterimi temsil ettiği çok açıktı ama aradaki farklı harfler akıl karıştırıyordu. Bu yüzden önce bi onları kaldırıp şansımızı deneyelim dedik. SDU = 1 ve BT = 0 olacak şekilde replace yapınca elde ettiğimiz binary oldukça anlamlıydı ama bir flag değildi.
```
110001001011000001101110011100110110000101101110001000000110010001101111110001001001111101100001011100111100010010110001001000000110011101100101011100100110010111000100100111110110100100100000011110100110111101110010011000010010000001100100110000111011110011000101100111110110110101100101011001000110100101101011110000111010011101100101001011000010000001111001011001010111010001100101011011100110010101101011011011000110010101110010011010010110111001101001001000000111001101101111011011100111010101101110011000010010000001101011011000010110010001100001011100100010000001101011011101010110110001101100011000010110111001101101011000010111101000101110
```
>İnsan doğası gereği zora düşmedikçe, yeteneklerini sonuna kadar kullanmaz.

biraz denemeden sonra cevabın sözün sahibi olduğunu bulduk.

*poinetr_{sun_tzu}*

**WARGAME**  
Bu soruların içeriği uzak bir makinede barındırılıyor ve SSH bağlantısı üzerinden görülebiliyor. 5 adım var ve geçebilmek için sıralı gitmek zorundasınız. Her bir makinanın SSH parolası bir önceki level'de bulunan flag oluyor.

**Level1**  
SSH 178.211.57.190
level1 = wargame

Bağlantıyı gerçekleştirdikten sonra kullanıcının home dizinine düşüyoruz haliyle. Gözümüze çarpan şey flag.zip dosyası. Dosyayı kendi bilgisayarımıza çekmek için;
```
$ scp level1@178.211.57.190:flag.zip
```
Daha sonra flag.zip'i araştırıyoruz ancak flag bulamıyoruz. En son binwalk ile baktığımız zaman bir resim dosyası görüyoruz. Resim dosyasını çıkartmak için foremost tool'unu kullanıyoruz. Flag resimde yazıyor

*poinetr_{h4ck3rc3m4l}*

**Level2**  

Level1'den aldığımız flag'i kullanarak ikinci makineye bağlanıyoruz. Dosyaları listeliyoruz ve bilgilendirmeyi inceliyoruz.
```
$ cat info
Ne olacak bu halimiz bilmiyorum.
Ayrımız gayrımız yoktu hani.
Neden fark yaratmak istedin ki?
```
buradan anlaşılan yeni.sifreler ve eski.sifreler dosyalarını diff komutu ile karşılaştırmamız gerektiği.
```
$ diff yeni.sifreler eski.sifreler
```
Tek farklılık; *8c76fe7c5849a8571bc60e48de1f26c0*  bu satır. Bu satırın MD5 olduğunu düşünerek kırmaya çalışıyoruz ancak kıramıyoruz. Bu noktada sanırım herkes aynı şekilde düşündüğü için o an herkes takıldı. Biz de bu arada login sorusuna dönüp onu çözdük. Daha sonra farkettik ki bu stringin kendisi flag imiş.

*poinetr_{8c76fe7c5849a8571bc60e48de1f26c0}*

**Level3**  
En zor level buydu açıkcası, fazlasıyla uğraştırdı ve hatta çıldırttı. İçeri girdikten sonra infoyu bastırıyoruz.
         
>Ahhhh Ahhhh....
 
>Flag elimden düştü mağaraya girdi...
 
>26 karakter bişeydi nasıl bulacağım ben onu şimdi...
 
>Fransız şifreci Blaise'e çok ayıp olacak.

"magara" isimli klasore gittikten sonra içerisinde bir çok klasör olduğunu ve her bir klasörde yine bir o kadar daha klasör olduğunu farkediyoruz. Klasörlerden birini scp ile kendi cihazımıza çekip içerisinde bulunan tüm dosya parçalarını
```
$ cat * > deneme
```
komutu ile deneme dosyasında birleştirip bir rar elde ediyoruz rar'ın içerisinde bir debian iso'su görünüyor ve ismi de *debian-8.6.0-amd64-netinst* bu ismin 26 hane olması bizi biraz oyaladı açıkçası. Yönelmemiz gereken yerin bu olmadığına emin olana kadar uğraştık. Artık emin olunca tekrar makineye bağlanıp dosyalar içersinde 26 meselesinin üzerine tekrar gitmeye karar verdik
```
$  find . -type f -size +26c -exec ls -lh {} \;
``` 
bu komutu çalıştırıyoruz. Bu komut ile 26 byte'den büyük olan her dosyayı ekrana bastırıyoruz. Ve böylece sadece bir dosyanın farklı olduğunu görüyoruz. Bu dosyanın içerisinde
> yamaiapat_fcas_cokznoa_hee

yazıyor. Vigenere kullanmamız gerektiğini biliyorduk ancak key olarak Blaise veya dizin adı gibi şeyler denedik. Uzunca uğraşlardan sonra bunun üst diznin adı olan "magara" key'i ile şifrelenmiş bir vigenere çıktısı olduğunu anlıyoruz.

*poinetr_{magaradan_flag_cikinca_ben}*

**Level4**  
Bu seviyenin bilgisi;

>Bekirin dosyaları içinde bir şifre var.
Bu şifreye ulaşman gerek.
Bekir 7 yaşındadır.
ASCII karakterlerini ötelemekten çok hoşlanıyor.
             
>Bekir dosyalarını açarken bir anahtar kullanıyor.
 
>unGxUbvbfLbykx
 
>Bekir sizin onu hacklediğinizi anlamaması için bulduğunuz gibi bırakınız.

parola rot7 ile hemen çıkıyor. Bununla yine makinede bulunan FLAG.zip dosyasının içerisinde ki flag.cap dosyasını çıkartıyoruz. Her ne kadar .cap uzantısı ile bitsede bir .cap dosyası değil sadece metin dosyası. cat komutu ile okumak yeterli olacaktı.

*poinetr_{uzantilar_aldatir_seni_yegen}*

**Level5**  
Info'yu okuyoruz yine;
>Güvercinin boynundaki o kırmızımtırak tüyler vardır ya,
Bir kere taktı mı güvercin o tasmayı boynuna başka birisini sevemezmiş,
Ama bazen fazla sevgiden güvercinler birbirlerini de öldürürlermiş,
Birbirlerinin gırtlağını deşerlermiş fazla sevgiden,
O yüzden o kızıl tasmaya da güvercin gerdanlığı derlermiş.
Madem bu kadar çok sevdiniz birbirinizi bakalım kim takacak o gerdanlığı boynuna...
Madem ikiniz de hasmımsınız artık geldik sınavın son sorusuna.
Biriniz ölürse diğeriniz sağ çıkacak buradan,
Bakalım kim daha çok seviyor diğerini...
Kim takacak o gerdanlığı boynuna...
             
             
>ramizkaraeski

İçeride bulunan .zip'i cihazımıza çekip "ramizkaraeski" parolası ile çıkartıyoruz. "dayi.dat" dosyası yine bir metin belgesi. Bir önceki seviyeden farkı yoktu aslında. Flag da içerisinde:

*poinetr_{gectin_sinavi_yegen_gectin}*
