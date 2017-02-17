---
layout: post
title: CanYouPwnMe CTF Çözümleri
date: '2017-02-17 16:30:00 +0300'
categories: blog
---
Selam,
17 ocak tarihinde ilk girişimizi yapıp, vakit bulabildikçe soruları çözmeye vakit ayırdığımız [CanYouPwnMe CTF](https://ctf.canyoupwn.me)'de çözüp puan alabildiğimiz tüm soruların olabildiğince ayrıntılı çözümlerini paylaşmak istiyoruz. Toplamda 57 soru çözmüş olup 7540 puanla sıralamada birinciliğimizi sürdürmekteyiz (17 Şubat 2017). Çözümleri hatırlanamayan 2 soru haricinde 55 sorunun cevabını aşağıdaki bulabilirsiniz. CanYouPwnMe ekibine düzenlemiş oldukları CTF için teşekkür ederiz. 

Soruları kategorileri dahilinde düşük puandan yüksek puana gidecek şekilde sıraladık. 

Keyifli okumalar.
[AUCC](https://twitter.com/_aucc)

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/tablo.png)  

**Flag Form 10 # Flag**  
**Soru:** cypwn_{h4ckm3}  
Soru CTF boyunca kullanılacak olan flag formatını belirtmiş. Verilen flag doğrudan girildiğinde soru çözülmüş olacaktır.  
  
Flag : cypwn_{h4ckm3}  
  
  
**Crypto 25 # Hard**  
**Soru:** PCYvKDEAJCdvLSVvLThvLyI=    
Stringin sonundaki eşittir işareti ve 24 karakter uzunluğund olmasından ötürü
önce Base64 ve benzeri decode algoritmalı kullandık ve doğal olarak çözüm
gelmeyecekti. XOR operasyonuna sokulmuş bir metin olduğunu yaptığımız
deneme yanılmalar sonunda anladık.  
  
Çözüm için şu online servis kullanılabilir:  
[http://strelitzia.net/wasXORdecoder/wasXORdecoder.html](http://strelitzia.net/wasXORdecoder/wasXORdecoder.html)  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/1.png)  
  
Ya da python ile yazılmış şu güzel araç da kullanılabilir:  
[https://gist.github.com/revolunet/2412240](https://gist.github.com/revolunet/2412240)  
  
Flag: cypwn_{x0rz0rg0p}  
  
  
**Crypto 50 # OldSchool**  
**Soru:** *Text: cfxdigthdppymtdbqyz*    
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *Key: TBCXRL*  
          
Şifrelenmiş metin ve key birlikte verildiği için Vigenere şifrelemesi kullanıldığı
anlaşılıyor. Yine online hizmet veren araçlar ile encrypted veri kırılabilirdi.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/2.png)  
  
Elde edilen sonuç aşağıdaki string olacaktı.
```  
Jevgrvagbsyntsbezng  
```  
Ceasar Cipher tekniği akla gelecekti ve Rot13 rotasyonu kullanıldığında flag
elde edilecekti.  

```
➜ echo 'Jevgrvagbsyntsbezng' | tr 'A-Za-z' 'N-ZA-Mn-za-m'      
Writeintoflagformat  
```  
  
Flag :cypwn_{Writeintoflagformat}  
  
  
**Crypto 50 # CryptoForBabies**  
**Soru:** *Vm0wd2VHUXhTWGhXV0doV1YwZDRWbFl3WkRSV01WbDNXa1J
TVjAxV2JETlhhMUpUVm14S2MyTkliRmhoTVhCUVZqSjRZV1JIVmtsalJt
UnBWa1ZhU1ZkV1pEUlRNbEpYVW01T2FGSnRVbkJXYTFaaFUxWmtW
MXBJY0d4U2EzQllWakkxUzJGV1NuUmhSemxWVm14YU0xUnNXbUZX
YkdSeVYyeENWMkV3Y0ZSV1ZWcFNaREZDVWxCVU1EMD0*  
  
Bu soruda verilen metin base64 algoritması ile ard arda 9 defa encode edilmiş.  
Metin 9 defa decode edildiğinde flag bulunmuş oluyor.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/3.png)  
  
Bu işlem için faydalandığımız online servis aşağıdadır.  
[https://www.base64decode.org/](https://www.base64decode.org/)  
  
Flag : cypwn{babyFl4g}  
  
  
**Crypto 50 # Hold Your Breath**  
**Soru:** *Hold Your Breath and Count to 27395*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *6e13409111b425a434d1cd9a80743669ec7385f9*  
  
Verilen hash değeri hash-identifier aracı ile analiz edildiğinde SHA1 olduğu
ortaya çıkacaktır.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/4.png)  
  
Online servisler kullanılarak bize verilen SHA1 hash i kırılabilirdi. Bu işlem için
[https://md5hashing.net/hash/sha1](https://md5hashing.net/hash/sha1) sitesini kullandık. Sonuç aşağıdadır.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/5.png)  
  
Flag: cypwn_{26595}  
  
  
**Crypto 50 # Keep Calm**  
**Soru:** *Keep Calm and Discard Powers of 2*    
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *100256105256100256121256111256117256109256105256115256115256109256101*  
  
Verilen soruda ASCII değerleri seçilebilmekte. Ortalığı karıştıran mevzu ise
“256” değerleri. ASCII tablosu 0-255 arasındaki sayılardan oluştuğundan ötürü
doğrudan dönüşüm yapmamızı engellemek adına aralara 256’lar serpiştirildğini
düşünerek 256’ları temizledik. Sonucunda şöyle bir değer elde ettik. 
``` 
100 105 100 121 111 117 109 105 115 115 109 101  
```  
ASCII’den text e dönüşüm işlemi yaptığımızda flag elde edilmiş oldu.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/6.png)  
  
Flag: cypwn_{didyoumissme}  
  
  
**Crypto 50 # Like a Dog**  
**Soru:** *Like a Dog Chasing Cars*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *bcwikraowkqsdvlcvswexhqsfmsxslpvcsdnhsqvbdosgusnijnffidxfo*  
  
Soruda verilen “Like a Dog Chasing Cars” ipucunu arama motorlarında
arattığınız zaman The Dark Knight filminin müziği olduğunu bulabilirsiniz.
Verilen şifreli metin Vigenere ile şifrelenmiş. Metni decode etmemiz için gereken
key ise filmin kötü karakteri ismi “joker”.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/7.png)  
  
Flag: cypwn{sometimesthetruthisnotgoodenoughsometimespeopledeservemore}  
  
  
**Crypto 100 # The secret ot the photo**  
**Soru:** *http://s3.dosya.tc/server10/e49llx/ctf-canyoupwnme.jpg.html*  
  
Sorudaki linkten CanYouPwnMe logosu geliyordu.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/8.png)  
  
Crypto karegorisinde bize verilen bir jpg dosyası için akla gelebilecek
yöntemlerden biri steganografik decode olacaktı. Jpg dosyası decode edilince
base64 ile encode edilmiş şu metin elde ediliyor:  
Bu işlem için önce şu adresten online steganografik decode işlemi yapıyoruz.  
[https://futureboy.us/stegano/decinput.html](https://futureboy.us/stegano/decinput.html)    
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/9.png)  
Uygulamanın jpg dosyamızdan çıkardığı base64 encoded metin şu olacaktı.  
```  
ZmJzenFfe2lvZGpleG94cWd4fQ==  
```  
Elde edilen base64 encoded metin decode edildiğin çile hala bitmemişti bir de Ceasar Cipher rotasyonuna sokmamız gerecekti çünkü base64 decode
işleminden gelen değer şu idi  
```
➜ echo "ZmJzenFfe2lvZGpleG94cWd4fQ==" > base64encoded.txt  
➜ base64 -d base64encoded.txt  
fbszq_{iodjexoxqgx}  
```  
Pek kullanışlı bir Ceasar Cipher rotasyon uygulaması olan [şu](http://theblob.org/rot.cgi?text=fbszq_{iodjexoxqgx}) siteden tüm formatlara yönelik dönüşüm yapıldığında flag rot23 rotasyonunda bulunacaktı.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/10.png)  
  
Flag : cypwn_{flagbulundu}    
  
  
**Crypto 100 # I hate you, ALL !!!**  
**Soru:** *http://pastebin.com/f36XmBGw*  
  
Soruda verilen bağlantı ziyaret edildiğinde uzunca bir base64 encoded text ile karşılaşılıyordu. 1 defa decode işlemine soktuktan sonra [,],!,?,+,(,) karakterlerinden oluşan obfuscated uzunca bir string elde ediliyordu. Deobfuscation işleminden sonra google drive linki elde edilecekti. Bu işlemler için sırasıyla aşağıdaki servisler kullanılmıştır.  
[https://www.base64decode.org/](https://www.base64decode.org/)  
[http://deobfuscatejavascript.com/](http://deobfuscatejavascript.com/)  

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/11.png)   
  
Elde edilen link aşağıdadır  
[https://drive.google.com/file/d/0B5i8WVYofXg6SlAzSFdpVDNqVjQ/view](https://drive.google.com/file/d/0B5i8WVYofXg6SlAzSFdpVDNqVjQ/view)  
  
Bu link ziyaret edildiğinde aşağıdaki jpg dosyası elde edilecekti.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/12.png)   
  
Exiftool aracı ile sempatik teyzemizi analiz ettiğimizde Title alanının karşısında hash benzeri bir değer bulunmaktaydı.  
```
➜ exiftool nefret.jpg  
ExifTool Version Number 		: 10.40  
File Name 						: nefret.jpg  
Directory 						: .  
File Size 						: 16 kB  
File Modification Date/Time 	: 2017:02:16 02:46:52+03:00  
File Access Date/Time 			: 2017:02:16 02:49:56+03:00  
File Inode Change Date/Time 	: 2017:02:16 02:46:56+03:00  
File Permissions				: rw-r--r--  
File Type 						: JPEG  
File Type Extension				: jpg  
MIME Type 						: image/jpeg  
JFIF Version 					: 1.01  
Resolution Unit 				: inches  
X Resolution 					: 96  
Y Resolution 					: 96  
Exif Byte Order 				: Big-endian (Motorola, MM)  
Image Description 				: 718f17b43473d15b74201d9c9e537be6  
XP Title 						: 718f17b43473d15b74201d9c9e537be6  
Padding 						: (Binary data 2060 bytes, use -b option to extract)  
About 							: uuid:faf5bdd5-ba3d-11da-ad31-d33d75182f1b  
Title 							: 718f17b43473d15b74201d9c9e537be6  
Description 					: 718f17b43473d15b74201d9c9e537be6  
Image Width 					: 225  
Image Height 					: 225   
Encoding Process 				: Baseline DCT, Huffman coding  
Bits Per Sample 				: 8  
Color Components 				: 3  
Y Cb Cr Sub Sampling 			: YCbCr4:2:0 (2 2)  
Image Size 						: 225x225  
Megapixels 						: 0.051  
```
  
*718f17b43473d15b74201d9c9e537be6* bu değer google arama motorunda  aratıldığında daha önceden kırılmış bir hash değeri olduğu gelen sonuçlardan
anlaşılıyordu.  
    
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/13.png)  
  
Flag: cypwn_{flag_1}  
  
  
**Crypto 150 # Note**  
**Soru:** *Note: 2E124EA5FCEB1D3EE56BA1205EDF8002*  
  
Soruda NTLM ile şifrelenmiş bir string verilmişti. Metin decode edildiğinde flag
bulunmuş oluyor.  
  
[https://hashkiller.co.uk/ntlm-decrypter.aspx](https://hashkiller.co.uk/ntlm-decrypter.aspx)  
Adresinden online olarak soruda verilen hash kırılıp flag elde edilebilirdi.  
  
Flag : cypwn{78ab12}  
  
  
**Crypto 200 # Önce Karakter**  
**Soru:** *Sabah kalktığımda "zftcqcnftc" diye mesaj gelmişti "anlamadım" diye
yanıtladığımda ise "The quick brown fox jumps over the lazy dog." diye bir
mesaj daha geldi.*  
  
İlk önce The quick brown fox jumps over the lazy dog u google da arattım neden bu cümle bize verilmiş diye "The quick brown fox jumps over the lazy dog" bu cümlenin pangram olduğunu öğrendim yani tüm alfabedeki harfleri barındıran bir cümleymiş.Anladım ki alfabede bir değişiklik yapmamız gerekiyor.Kullanılan algoritma ise Yerine Koyma Şifrelemesi (Substitution Cipher)dir.

Soruda belirtildiği gibi cipher textimiz(mesajımız) = zftcqcnftc 

http://substitution.webmasters.sk/simple-substitution-cipher.php web sayfasını açtım.(online substitution cipher encoding/decoding)

cümlemizdeki harfleri sırasıyla  ['T', 'h', 'e', 'q', 'u', 'i', 'c', 'k', 'b', 'r', 'o', 'w', 'n', 'f', 'x', 'j', 'm', 'p', 's', 'v',  'l', 'a', 'z', 'y', 'd', 'g'] çıkarttım, ve yeni alfabemi oluşturdum bu işlemi gerçekleştirirken ilk harfleri aldıkdan sonra aynı ikinci harfleri atladım .(Yani benim alfabemde A=T, B=H, C=E, ... oldu.) Text kısmınada zftcqcnftc yazdım ve decode ettim flag GIVMEFIVE.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/14.png)
  
Flag : cypwn_{GIVEMEFIVE}  
  
  
**Crypto 300 # Secret Message**  
**Soru:** *http://dosya.co/lvcetyf51u1z/mesajim.html*  
  
Linkte verilen dosya SSL ile şifrelenmişti. Wikipedia’da geçen tüm kelimelerin içinde bulunduğu bir wordlist kullanıldı bu sorunun çözümü için ([Wikipedia Wordlist](http://blog.sebastien.raveau.name/2009/03/cracking-passwords-with-wikipedia.html)). Kaba kuvvet saldırısı için ise [https://github.com/glv2/bruteforce-salted-openssl](https://github.com/glv2/bruteforce-salted-openssl)  aracı kullanıldı. Soruda dikkat edilmesi gereken nokta, salt değerinin “mesajim” olması idi.   
   
Parametreler aşağıdaki gibi olacaktı.  
```
bruteforce-salted-openssl -1 -t 4 -f wordlist.txt -c AES-128-CBC -p 100000
mesajim  
```  
Flag: cypwn_{buralar_eskiden_hep_tarlaydı}  
    
    
**Crypto 500 # I forgot it!**  
**Soru:** *Benim için çok önemli bir dosya vardı ama bulamıyorum nerde acaba?*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *[https://drive.google.com/open?id=0B5i8WVYofXg6ZjdwdmNWSkxEMWM](https://drive.google.com/open?id=0B5i8WVYofXg6ZjdwdmNWSkxEMWM)*  
  
Linkte verilen dosya indirilip analiz edildiğinde TrueCrypt container ı olduğu
anlaşılıyordu (dosyanın adı bile dogrusifreleme idi ama burada soruyu yazan
arkadaşları uyarmamız lazım True-Crypt ikilisinin çevirisinde hata olduğunu
düşünüyoruz, doğrutürbe olarak çevrilebilirdi). Açabilmek için de bir parolaya
ihtiyaç vardı. Bu sebeple rockyou wordlisti ve truecrack aracını kullanarak kaba
kuvvet saldırısı yaptık. Sonuç olarak bir parola elde ettik.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/15.png)  
  
Container açıldığı zaman enteresan bir dosya ile karşılaştık.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/16.png)  
  
Nedir bu ses dosyası diye açtık ki soruyu hazırlayan arkadaşlar bizleri de
düşünmüş olacaklar ki gece gece eğlenmiş olduk. 
   
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/17.png)    
  
Sonuç olarak bir şey elde edemedik. 500 puanlık sorunun böylesine kolay
çözülmesini de beklemiyorduk açıkçası. Hidden container olma ihtimalini
düşünerek yeni bir kaba kuvvet saldırısına başladık. Bu defa tek sonuçta
durmamasını sağladık ve 2 parola elde ettik.  
  
--> john true --show  
dogrusifreleme:789456:normal::::dogrusifreleme  
dogrusifreleme:123123123:hidden::::dogrusifreleme  
  
2 password hashes cracked, 4 left  
  
Hidden container 123123123 parolası ile açıldı. Fakat içinden flag.rar dosyası
çıktı. Sırasıyla hash değerini çekip kaba kuvvet saldırısı yapıldı.  
  
rar2john rarismi.rar > rarhashi.txt  
  
john rarhashi.txt --wordlist=rock.txt  
  
Rar dosyasının içinden md5 özeti elde edildi  
  
c38bcb34ca957809c9a815dbc875d2cf  
  
Online servislerde sorup soruşturulduğunda elde edilen sonuç  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/18.png)  
  
Matematik problemi çözüp sonucu 0 bulmak gibi olsa da eğlendirdi.  
  
Flag: cypwn_{zaaaa}   
  
  
**Network 100 # Bruto Anthem**  
**Soru:** *Bizim grup 14344393 kişi (adımıza r0ckyou demişler) saldırıyoruz. Ama
nereye?*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *[http://s3.dosya.tc/server10/ih4a60/canyoupwn.rar.html](http://s3.dosya.tc/server10/ih4a60/canyoupwn.rar.html)*  
  
Linkteki dosya indirilip açıldığında bir pcapng dosyası elde edilecekti. Wireshark
aracı ile trafik analizi yapıldığında http protokolünde bir internet sitesi ile
iletişime geçildiği ve login denemelerinde bulunulduğu görülecekti. Bizce
anlamsız bir şekilde flag bu login denemesinin yapıldığı site idi  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/19.png)  
  
Flag: cypwn_{athome.starbucks.com}   
  
  
**Network 200 # WPA2**  
**Soru:**  *Galatasaraylı Emel'in kablosuz ağını ele geçirmek isteyen saldırgan, bir
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; handshake yakaladı. Parolayı bulmasına yardım eder misiniz?*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *NOT: Parola 8 karakterlidir.*   
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *[https://drive.google.com/open?id=0B5i8WVYofXg6Q1NHVTM2Z2toUnc](https://drive.google.com/open?id=0B5i8WVYofXg6Q1NHVTM2Z2toUnc)*  
  
Ilk önce bize verilen cap dosyasını analiz ederek işe başladık,zaten dosya
isminden tahmin edebiliyorduk fakat ESSID'de "AslanCimbom" çıkınca
parolanında galatasaray ile ilgili olduğu kesinleşmiş oldu.Daha sonra bize
verilen ".cap" dosyasını "aircrack-ng" ile ".hccap" dosyasına dönüştürdük. 
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/19.png)
Burdan sonra kendi oluşturmuş olduğumuz içerisinde türkçe
kelimelerle beraber "emel,gs,cimbom,galatasaray,1905" gibi kelimeleri kendi
aralarında crosslayan aşağıdaki script ile kelimeleri çapraz olarak ilk ve son
sıraya gelecek şekilde ekleyerek ortak bir wordlist olan "emelwordlist.txt"
oluşturduk.  
```
#!/bin/bash    
kelimeler=birinci.txt    
sayilar=ikinci.txt    
for k in $(cat $kelimeler):    
    do    
        for s in $(cat $sayilar):    
            do    
                printf "$k$s\n"  
                printf "$s$k\n"  
            done  
    done  
```  
Son olarak,
```
hashcat -m 2500 cimbom.hccap emelwordlist.txt  
```
komutuyla sözlük bazlı kava kuvvet saldırısı başlatarak sonunda "1905emel" olarak parolaya
ulaştık.  
  
Flag : cypwn_{1905Emel}  
  
  
**Network 230 # Uptime**  
**Soru:** *Uptime suresini bulabilir misin?*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *SSID: Meryem*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *[https://drive.google.com/open?id=0B5i8WVYofXg6bk9DMTdZanBRZHc](https://drive.google.com/open?id=0B5i8WVYofXg6bk9DMTdZanBRZHc)*  
  
SDUCTF’17 de sorulan sorunun “benzeriydi” diyebiliriz. Soruda bizden "meryem"
SSID'li ağın uptime süresini soruyor.Burda yapılması gereken şey  
```
airodump-ng -r meryem.pcap --uptime  
```
komutunu kullanmak bu komut ile resimde görüldüğü gibi uptime süresi görünüyor açık olarak.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/21.png)  
  
Flag: cypwn_{00:10:54}  
  
  
**Network 250 # ARP**  
**Soru:** *Antivirüs arp dedi saldırı dedi tehlike dedi. Kim bu ya ?*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *[http://dosya.co/1fri373s4q4a/arpctf.pcap.html](http://dosya.co/1fri373s4q4a/arpctf.pcap.html)*  
  
Verilen pcap dosyasını NetworkMiner aracı ile incelediğimizde ağda bi arp
saldırısı olduğu görülüyor,anormalliklerden arp saldırısının yapılmış olduğu MAC
adresiyle eşleşen bilgisayarın hostname'i flag olarak girdiğimizde puanı
alıyoruz.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/22.png)  
  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/23.png)  
  
Flag: cypwn_{ARHC-X}  
  
  
**Network 500 # All day All Night**  
**Soru:** *Sen yazılımcısın, parolaları böyle mi saklarsın?*  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *[http://s8.dosya.tc/server3/ezcean/firmware.rar.html](http://s8.dosya.tc/server3/ezcean/firmware.rar.html)*  
  
Bu soruda bize bir modemin firmware'i veriliyor,internette biraz
araştırdığımızda bu modeme ait bir zaafiyet olduğu ortaya çıkıyor.Daha sonra
"[http://www.routerpwn.com/zynos/](http://www.routerpwn.com/zynos/)" sitesine bize verilmiş olan firmware'i
upload ettiğimizde modemin parolası geliyor direk.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/24.png)  
  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/25.png)  
  
Flag: cypwn_{45278913}  
  
  
**Trivia 20 # Git101**  
**Soru:** *Unutma dökümantasyon önemli.*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *https://github.com/londragecidi/londragecidi*

Bize verilen linkteki github sayfasının Wiki kısmına bakmamız yeterliydi.

Flag:	cypwn_{ben_git_biliom_abi}
  
**Trivia 50 # First Deuce**  
**Soru:** *EE bre deyyus nedir bu ilk DEUCE ??*

Arama motorlarında deuce computer olarak aratınca deuce ile ilgili bir wiki sayfasına ulaşıyoruz. 
[https://en.wikipedia.org/wiki/English_Electric_DEUCE](https://en.wikipedia.org/wiki/English_Electric_DEUCE) linkindeki bilgileri denerken Predecessor Pilot ACE kısmını da denedik ve flag cypwn_{Pilot_ACE}  idi.

Flag:	cypwn_{Pilot_ACE}  
  
**Trivia 50 # Carrot**  
**Soru:** *At boyutunda ördek?*

“At boyutunda ördek” yani ingiliççe haliyle “Horse sized duck” olarak arama motorunda arattığımızda “Dromornithidae” adlı bir dinazor türü karşımıza çıkıyor. Hakkında yazılanları okuduğunuzda ördeklerle ilgili esrarengiz bağlantıları görebilirsiniz. Yine de bu soru için 20 küsür denememiz gitti. Hiç hoş değil eeey yönetim. Google arama motorunun kullanımına yönelik bir soruydu esasen. Bilmediğiniz bir şeyi nasıl aratır onun hakkında bilgi edinebilirsiniz, bunu öğretme niyetinde olduğunu düşünüyoruz.  

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/26.png)

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/27.png)

Çılgın bir ördeğimsi dinozor.

Flag : cypwn_{Dromornithidae}
  
**Trivia 50 # INTELLIGENCE**  
**Soru:** *Bu çocuk müthiş istihbarat tekniği kullandı. :)*

Tabii ki en güzel istihbarat hedefe dokunmadan yapılan istihbarattır değil mi efenim değil mi (bkz: Open Source Intelligence)

Flag: cypwn_{OSINT}  
  
**Trivia 100 # Mayası Bozuk Bu Sorunun**  
**Soru:** *. ... .. .*
Soruda Maya alfabesinden sayılar verilmiş. Aşağıdaki tabloya göre verilen
sayıların günümüz karşılığı bulunduğunda flag bulunmuş oluyor.  
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/28.png)  
  
Flag : cypwn_{1321}  
  
  
**Trivia 100 # (D)emand (B)rogress**  
**Soru:** *Lanet olası federaller! Eş kurucu(co-founder) federallerden birşey almış. Ve bu onları kızdırmış olmalı..!*

Demand Progress ile ilgili arama motorları üzerinden araştırmalar yapıldığında kurucusu Aaron Swartz olan ve kar amacı gütmeyen bir kuruluş ile ilgili bilgilere eriştik. Araştırmayı derinleştirdiğinizde (karşınıza çıkan uzun wikipedia yazılarını okuduğunuzda) Aaron Swartz’ın hayatındaki en önemli olaylardan birinin PACER veritabanındaki dökümanları public etmesi yer alıyor. Soruda da sızdırma ile ilgili şeyler yazdığından ötürü en mantıklı gelen keyword PACER oldu ve denediğimizde 100 puan elde etmiş olduk.

Flag : cypwn_{pacer}  
  
  
**Trivia 120 # Mr. Robot**  
**Soru:** *http://dosya.co/kdi5poggcvp3/ctfcypm.html.html*

Bize verilen html dosyasını bir text editör ile açtığımızda gelen sembolleri "Find and Replace" ile her bir sembol için boşlukla değiştiriyoruz.Daha sonra resimdede görüldüğü üzere "matrixhacker" olarak cevap geliyor. 

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/29.png)

Flag:	cypwn_{matrixhacker}

  
**Trivia 150 # Not deleted, Can not be deleted!!!**  
**Soru:** *https://github.com/stolkhomvadisi/rails-mailinglist-activejob*
Verilan github adresinde commitlere bakıldığında yapılan değişiklikler görülebiliyor.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/30.png)

Burda "secret.yml" incelendiğinde içerisinde flag görülüyor.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/31.png)
  
Flag : cypwn_{dikkat_etmek_ve_detayli_incelemek_butun_hersey_bu}  
  
  
**Trivia 200 # Is this love?**  
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6X09ZUUlVT19id00*

Verilen rar dosyasını “love” parolasıyla açtığımızda iki adet qr kod görüyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/32.png)

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/33.png)

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/34.png) 

(Bu işlem için resmin kontrast ayarları ile oynamanız gerekiyor. Gimp önerilir)

İlk QR-Code:ctf
İkinci QR-Code:ypbitrghkrpsgkxehr

Evet flag olarak cypwn_{ypbitrghkrpsgkxehr} denesek de puan alamadık. Önceki sorularda kullanılan yöntemler göz önüne alındığında ve hatta elimizde 2 string değeri olduğu göz önüne alındığında aklımıza ilk gelen vigenere oldu. Decode işleminden sonra flag geldi (CTF öncesi sübliminal içerir

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/35.png)

Flag: cypwn_{wwwgameofpwnerscom}

  
**Trivia 300 # This is LEAK!**  
**Soru:** *http://i.hizliresim.com/qjpR8Q.png*
Link ziyaret edildiğinde 
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/36.png)

Görüntüsü ile karşılaşılacaktı. 

Açıkçası yaptığımız işlem mantık yürütmek oldu. CTF canyoupwn.me tarafından düzenleniyor. Sorunun adında LEAK büyük harflerle yazılmış. Önce internette araştırma yapsak da canyoupwn.me adresine geri döndük ve yakın zamanda yazılmış postları inceledik. Bir konu başlığı adeta "gelin bana!" diye el sallıyordu [https://canyoupwn.me/tr-webrtc-ip-leak/](https://canyoupwn.me/tr-webrtc-ip-leak/). Flag olarak webrtc denediğimizde sonuca ulaşmış olduk.
  
Flag : cypwn_{webrtc}  
  
  
**Trivia 400 # Yeşil Erik**  
**Soru:** *Yeşil eriğin tadı da bir başkadır :)*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *bubirsecret*
SDUCTF’te sorulmuş olan bir soruydu. Çözen olmamıştı o zamanlar. Açıkçası eğlenmedik soruyu çözerken. 400 puan olması ve böylesine bir çözüme sahip olması ironik bir tebessüm bıraktı yüzlerimizde. Sorunun çözümü için nihayetinde izlediğimiz adımlar şu oldu.

Teknik olayları tamamen eledik. Saatlerimiz gitti çünkü. Tamamen sürreel düşüncelere kapılmaya başladık. Ve şu konuşmanın çok benzeri kendi aramızda döndü. 

S: yeşil erik nedir?
C: meyvedir
S: tamam onu sormak istemedim, nasıl bir meyvedir yani?
C: yeşil?
S: başka?
C: ekşidir
S: heh dur orda. Ekşi ne var?
C: meyveler içecekler bla bla bla, anlamıyorum nereye varacaksın ????
S: yok yok bırak meyveyi sebzeyi ekşi diyince aklına gelen şeylerden birini söyler misin
C: sözlük var. Eksisozluk.com
S: tamam çok güzel. Soruda bir string daha verilmiş. bubirsecret. Arama kutucuğunda bir aratır mısın onu
C:   
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/37.png)
Haydaa.. Erikle başladık nereye geldik. (buraya geldik: [https://eksisozluk.com/entry/64566724](https://eksisozluk.com/entry/64566724))
S: Neye benziyor bu?
C: base64? Rot? Hash mi yoksa?
S: soru kalıpları benzer hep. Yine 2 string verilmiş. Vigenere dene bakalım ne gelecek. Ama dikkat et soruda hata var key değeri sözlükteki entryde yazan “sır” değil “sir” olacak :)) 
C:
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/38.png)

Evet.. 400 points.. evet..

Flag:	cypwn_{duysesimikriptoloji}

  
**Reverse 100 # Rev1**  
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6Tzl2R29Ea2hILUU*

Linkten gelecek olan binary, komut satırında strings komutu ile ile okunduğunda içinden flag gelecekti.  

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/39.png)

Flag : cypwn_{BATLAMYUS}
  
  
**Reverse 200 # Rev2**  
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6Q3RrdkVCQTZVNVU*

Bu soruda elimizde 32-bit ELF dosyamız mevcut. Bu bilgiyi file komutu kullanarak elde ettik.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/40.png)

Sonrasında çalıştırıp baktığımızda program bizden bir girdi bekliyor ve doğruluğuna göre sonuç
Veriyor.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/41.png)

Doğru pincode kullanadığımızda “Access Granted!” yazacağını strings le bakarak gördüğümüz değerlerden tahmin edebiliriz.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/42.png)

Programımızı şuana kadar yüzeysel olarak analiz ettik ve elimizde şunlar var; program bizden bir pincode istiyor ve bunu bir değerle karşılaştırıp doğruluğunu test ediyor. GDB kullanarak programın biraz daha derinlerine girelim.
Programımızı gdb rev200 komutu ile çalıştırıp main fonksiyonuna breakpoint koyduk.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/43.png)

Sonra run komutu ile çalıştırdık. Bizim programdan beklentimiz bizden girdi aldıktan sonra bir karşılaştırma yapmasıdır. Girdiyi alacağı kısımda “scanf” fonksiyonu çağırıyor olacak ve hemen sonrasında bizden aldığı girdiyi olması gereken değerle “cmp” ile karşılaştırıyor olacak. Çalıştırdıktan sonra next komutu kullanarak tek tek ilerliyoruz ve scanf fonksiyonun çağrıldığı kısıma geldik.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/44.png)

Scanf’in çağrılmasının ardından “cmp eax, 0x58f” in geldiğini görmekteyiz. Burda bizden istediği değerin “0x58f” olduğunu bulduk, ancak bu hexadecimal(16lık tabanda) halinde, bunun decimal(10luk tabanda) halindeki değeri bizi sonuca ulaştıracaktır.
0x58f -> 1423

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/45.png)

Flag:	cypwn_{1423}
  
  
**Reverse 300 # Rev3**  
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6R3pmOF9yYXkzY00*

rev200 sorusundaki adımları tekrarladığımızda sorunun aynı mantıkta olduğunu görüyoruz. Bu sefer karşımıza “cmp eax, d7e” çıkıyor.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/46.png)

Bu değeri onluk tabana çevirdiğimizde 0xd7e -> 3454 değerini buluyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/47.png)

Flag:	cypwn_{3454} 

  
**Forensics 25 # Flog**   
**Soru:** *Flag'ı bul*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *http://s3.dosya.tc/server10/ol4jyx/canyoupwnme.rar.html*

Çeşitli denemelerden sonra komut satırında 
````
cat canyoupwnme.log | grep pwn 
```
komutunu çalıştırdığımızda aşağıdaki sonuç geliyor.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/48.png)

Flag: cypwn_{canyoupwnme_log}  
  
**Forensics 50 # Is Empty?**  
**Soru:** *Daha dün baktım burdaydı ama şimdi bulamıyorum?*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *https://drive.google.com/open?id=0B5i8WVYofXg6QWxVNUQyTkRfRW8*

demorepo.zip dosyasını açmaya çalıştığımızda bizden bir parola istedi. Zip uzantılı ve parola korumalı dosyaları açmak için kaba kuvvet saldırısı yapabileceğimiz(zip2john) aracını kullandık. zip2john aracını ekran görüntüsündeki parametreler ile çalıştırdığımız .zip dosyasının parolasını bulduk.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/49.png)

Bulunan parola ile zip dosyası extract edilir ve config dosyasında github URL’i görülecektir.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/50.png)

[https://github.com/stolera/demorepo](https://github.com/stolera/demorepo)

Girdiğiniz github adresinde relavent commiti altında "flag.txt" dosyasının içerisinde flag görülüyor.

Flag:	cypwn_{easy_peasy_lemon_squeezy}
  
**Forensics 50 # Attack IP**  
**Soru:** *pcap dosyasında bir saldırı gerçekleşmektedir.Saldırganın IP sini bulmamıza yardım etmelisin.*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *http://s3.dosya.tc/server10/2wb2fj/atack.rar.html*

Linkten gelen pcap dosyası wireshark aracı ile açılıp, trafik analiz edildiğinde ilk paketlerde 192.168.237.141 olan kaynak IP adresinin, yapılan saldırıdan sonra 192.168.237.128 olarak değiştiği gözlemlenebilmekte. 

Flag:	cypwn_{192.168.237.128}  
  
**Forensics 50 # Miyav**  
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6aWRtX1FYRXZwdlE*

Bize verilen dosyanın uzantısının dogru olup olmadığını "file" komutuyla kontrol ettikten sonra,uzantısını ".jpeg" olarak değiştiriyoruz.Resim açılıyor fakat herhangi bir flag yok görünürde. Daha sonra binwalk aracı ile kontrol ettiğimizde içerisinde bazı dosyalar olduğu görülüyor.Burda "binwalk -e miyav.jpeg" komutuyla dosyaları çıkarıyoruz.Içerisinden bir "zip" ve "txt" dosyası çıkıyor.Hem zipin içerisindeki "txt" dosyasında hemde ilk çıkmış olan "txt" dosyasının içerisinde "ameno" olarak flag geliyor.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/51.png)

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/52.png)

Flag:	cypwn_{ameno}  
  
**Forensics 75 # Change is good
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6d0dDTlgzMGE4amc*

Soruda verilen dosyayı hexeditle açtık. İlk sıra 0 ile başlıyor yani null ayrıca soru adı da “Change is good” yani değişiklik iyidir. Soru adı aslında bir şeyleri değiştirmemiz için ipucu niteliğindeydi.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/53.png)

Ardından dosyayı strings komutu ile incelediğimizde “pdf” ve “word” keywordleri geçtiğini gördük. Ayrıca headerda tanımlama eksikti yani dosyanın formatı bilinmiyordu.
![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/54.png)
Hexedit aracı ile düzenleme yapıldığında ki bu düzenlemeyi deneme yanılmaya göre yapmış olduk ya pdf çıkacaktı ya da word ve pdf doğru çıktı. Değişiklik için hexedit ya da benzeri bir araç kullanabilirsiniz. Yeni değerleri girdikten sonra CTRL+X ile kaydedip çıkabilirsiniz.
(Kalın beyaz karakterler yeni header değeridir. Bu değerlere şu adresten ulaşabilirsiniz. http://www.garykessler.net/library/file_sigs.html)

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/55.png)

Header ını düzelttiğimiz pdf dosyasını açtığımızda yazan tek şey “interesting” idi. 

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/56.png)

Flag:	cypwn_{interesting}


**Forensics 100 # Imaj Tools**  
**Soru:** *Ram Imajı alınırken hangi araç kullanıldığını bulmamıza yardım et !*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *http://s3.dosya.tc/server10/x7antf/canyoupwnme.rar.html*

Kullanılacak aracın adı RamCapture idi. 

Flag:	cypwn_{RamCapture}

  
**Forensics 150 # Attack Type**  
**Soru:** *Pcap dosyasında bir saldırı gerçekleşmektedir.Hangi zafiyet exploit edilmeye çalışılmıştır?*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *http://s3.dosya.tc/server10/2wb2fj/atack.rar.html*

Linkten gelen dosyayı Wireshark aracı ile açtık. TCP streamlerini incelediğimizde SMB üzerinden bir şeyler dönmüş olduğunu anladık. SMB servisi üzerinden gerçekleştirilebilen saldırıları araştırdık. Bize verilen dosyayı pcapng'den pcap'e çevirdik ardından Networkminer aracı ile biraz daha ayrıntılı baktık ve sömürülen zafiyetin MS08-067 olduğunu anladık(şaka şaka direk anlamadık tabi çok fazla SMB zafiyetinin adını denedik flag olarak).

Flag:	cypwn_{MS08-067}
  
**Forensics 150 # L-P**  
**Soru:** *Parolayı bul*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *http://s8.dosya.tc/server3/9xksqw/findpassword.rar.html*
Verilen dump dosyasından parola çekilmesi gerektiği aşikar. File komutu ile incelendiğinde Minidump dosyası olduğu da görülmekte.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/57.png)

Aklımıza gelen ilk araç mimikatz oldu (https://github.com/gentilkiwi/mimikatz/releases). Sanal bir windows makine üzerinde sırasıyla aşağıdaki komutları çalıştırdığımızda dump dosyasında bulunan Ahmet Gürel kullanıcısının parolası flag olacaktı.

Flag: 	cypwn_{canyoupwnmectf}  
  
**Forensics 200 # Memory Dump**  
**Soru:** *Ram Imajından flag ı çıkart.*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *http://s3.dosya.tc/server10/x7antf/canyoupwnme.rar.html*

Ram imajlarını analiz etmede kullanılabilen Volatility aracı ile soru çözülebilirdi. Komut satırında 

volatility -f canyoupwnme.mem –profile WinXPSP2x86 notepad 

komutunu çalıştırdığımızda aşağıdaki çıktıyı alacaktık.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/58.png)

Çıktının en altında FLG değerinin yanında bir base64 encoded string görüyoruz. Decode işleminden sonra cevap gelecekti.

Flag:	cypwn_{memo_flag_bulundu}
  
**Forensics 250 # Crypto Die**  
**Soru:** *Rardaki dosyayı açarak dosyayı incelememize yardımcı olmalısın.*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *http://s3.dosya.tc/server10/o86dns/ctf_canyoupwnme.rar.html*

Verilen rar dosyası açıldığında içinden 2 yeni dosya daha çıktı. Bunlardan biri parola korumalı bir rar, diğeri ise password.txt dosyası idi. Password.txt dosyasını okuduğumuzda bir hash değeri ile karşılaştık.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/59.png)

Karşılaştığımız hash i online servisler üzerinden arattığımızda karşılığının eHh4eHh4 olduğunu bulduk. Gülücüklü bir değer gibi görünse de toplam 8 karakter olması base64 encoded olabileceği yönünde şüphe uyandırmadı değil hani. Base64 decode ettiğimizde ise xxxxxx değerini elde ettik. 

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/60.png)

İlk açılan rar’dan çıkan canyoupwnme.rar sıkıştırılmış dosyasını açmak için son elde ettiğimiz değeri kullandık. “dosya” adında executable elde etmiş olduk. Çalıştırma yetkisi verdikten sonra çalıştırdığımızda bize flag i vermiş oldu.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/61.png)

Flag:	cypwn_{ctf_akiyor_masallah}  
  
**OSINT 10 # NS**  
**Soru:** *canyoupwn.me 'nin nameserverlarından birisi?*

[http://dnscheck.pingdom.com/](http://dnscheck.pingdom.com/) sitesinde canyoupwn.me yi test ettiğimizde, Advanced View görünümünde kullandığı name server'lar görünüyor.Burada cypwn_{ada.ns.cloudflare.com} olarak denediğimizde kabul ediyordu.

Flag: cypwn_{ada.ns.cloudflare.com}  
  
**OSINT 25 # Mail**  
**Soru:** *Bu canyoupwn.me mailleri nerede barındırıyor acaba?*

Mail server'ını bulmak için 

dig canyoupwn.me mx 

komutunu çalıştırdık ve aşağıda yanıt olarak mx.yandex.net 'i aldık.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/62.png)

Flag:	 cypwn_{mx.yandex.net} idi. 
  
**OSINT 50 # xCyberx**  
**Soru:** *Siber suçlular gizli ağlardan erişim sağlayarak orjinal Mona Lisa tablosunun taranmış digital kopyasını ele geçirdiler. Bu orjinal resmin yerine ise başka bir resim bırakmışlar. Siber suçluları takibe hazır mısın? Bıraktıkları resim dosyası aşağıdadır.*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *https://drive.google.com/open?id=0B5i8WVYofXg6c29VYlg2MUZTQkk*

Öncelikle bir script yazılarak resim rockyou wordlist'i ile steghide'a sokuldu ve cyberx parolasıyla açıldı. Buradan hint.txt adında bir dosya geldi. Dosyanın içindeki linkten bir qr kod geldi. Bu qr kodu okuttuğumuzda 
```
DoÄ ru yoldasÄ±n dostum devam et.. go go go!!! flag : aWV2Y3Rfe20wMGpfcDBIX0h4MF9lMGFfQHgzX0BfbkBpcTNYfQ== 
```
yazısıyla karşılaştık. Burada verilen stringi base64 decode işlemine soktuğumuzda 
```
ievct_{m00j_p0H_Hx0_e0a_@x3_@_n@iq3X} 
```
Değeri geldi. Bunu da rot decoder'dan geçirdiğimizde cypwn_{g00d_j0B_Br0_y0u_@r3_@_h@ck3R} olarak flag'i elde etmiş olduk.

Flag:	cypwn_{g00d_j0B_Br0_y0u_@r3_@_h@ck3R}  
  
**OSINT 100 # Secret**  
**Soru:** *secret.canyoupwn.me*

[http://viewdns.info/dnsrecord](http://viewdns.info/dnsrecord) sitesinde bize verilen secret.canyoupwn.me adresini arattığımızda doğrudan flag'a ulaşıyorduk.

Flag:	cypwn_{kks271723jjjasd9asd771239}  
  
**OSINT 100 # Nerd**  
**Soru:** *I need a source code for a domain. But I don't know what is the domain name!*
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; *search " canyoupwn.me "*

Enteresan bir şekilde Türkçe açıklaması yoktu bu sorunun. Soru adından yola çıkarak [https://nerdydata.com/search](https://nerdydata.com/search) sitesinde canyoupwn.me'yi arattığımızda erdemoflaz.com sitesine ait bir source code ile karşılaşıyoruz. Buradan da flag'ı cypwn_{erdemoflaz.com} olarak buluyoruz.

Flag:	cypwn_{erdemoflaz.com}  
  
**OSINT 125 # Social Media**  
**Soru:** *Stalker olma vakti!! nick:c0mrad3ctf heryerde ara !!*

Soruda bizden stalker olmamız isteniyor. Verilen kullanıcı adı Snapchat uygulamasında bulunduğunda hesabın bir QR kod paylaştığı görülüyor. QR kod okutulduğu zaman flag elde ediliyordu.

Flag : cypwn_{T@m_b1R_sT@lk3Rs1N_d0sTuM}  
    
**OSINT 150 # This is Anonymous job!**  
-,-
çözümü chat historylerden çıkarabilirsek ekleyeceğiz buraya
sevgilerimizle.  
  
**OSINT 200 # TV?**  
**Soru:** *Hacı geçen canyoupwnme diye bir kanal gördün onion pi den bahsediyordu, "bin"li bişeler vardı sanki..*

Öncelikle canyoupwn.me 'nin telegram kanalına girip Onion Pi ile ilgili yazısını buluyoruz(https://canyoupwn.me/tr-onion-pi-kurulum/). Yazının en sonunda yazıyla alakası olmayan bir string paylaşılmış.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/63.png)

Soruda “bin'li bir şeyler vardı” dediği için aklımıza pastebin geliyor (şaka şaka hemen gelmedi tabi. Binary ne olabilir burdan ne gelebilir diye tartışmalar çıktı) ve pastebin.com/xvtMaBkU URL’ine gidiyoruz. Flag böylece gelecekti. 

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/64.png)

Flag:	cypwn_{h4ckm3}  
  
**Malware Analysis 50 # Ava Giden Avlanır**  
**Soru:** *http://s2.dosya.tc/server4/xrmwno/analiz.rar.html*

“analiz.rar” isimli indirilen sıkıştırılmış dosyanın içinden 
```
unrar e analiz.rar
```
komutu ile “skype stelaeri” isimli bir dosya çıkarttık. Bu dosyayı strings komutu ile incelediğimizde karşımıza komutun çıktısının sonunda şöyle bir bölüm gelmektedir.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/65.png)

Flag:	cypwn_{capkin_hacker}  
  
**Malware Analysis 100 # Bir türüjan yazmışım moruk**  
**Soru:** *http://dosya.co/5cey302ghfs9/server.rar.html*

İndirilen “server.rar” isimli sıkıştırılmış dosyadan “server.exe” isimli bi PE32 executable dosya çıkmaktaydı. Bu dosyayı https://www.virustotal.com adresine yükleyip analiz ettirdiğimizde, bu dosya için atılmış yorumlar sekmesinde şöyle bir yorumun olduğunu farkettik.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/66.png)

FLAG: cypwn_{capkinhacker.zapto.org}  
  
**Malware Analysis 200 # Backdoor is OPEN**  
-,-
çözümü chat historylerden çıkarabilirsek ekleyeceğiz buraya
sevgilerimizle.  
  
**Misc 50 # ssh**  
**Soru:** *Ssh sunucu yapılandırdım. Ancak bağlantı çok uzun sürüyor. Config dosyasına hangi satırı eklemeliyim?*

Config dosyasına “UseDNS no” satırının eklenmesi gerekiyor.

Flag : cypwn_{UseDNS_no}  
    
**Misc 50 # O zaman dans!**  
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6NVVtT0wzUmt2V1k*

Verilen linkte link yönlendirmesini kaldırıp html dosyasındaki div'ler arasına # karakteri koyduktan sonra tarayıcıda açıldığında ekrana bir QR kod basılıyor.

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/67.png)

Flag:	cypwn_{oha_lan_çok_zormuş}  
  
  
**Misc 100 # Sub**  
**Soru:** *192.168.20.0 networkunde toplam 36 ip olsun istiyorim subnetini kac ayarlamaliyim?*

Verilen networkte toplam 36 ip olması için subnetin 26 olması gerekmektedir

Flag: cypwn_{26}    
  
**Stego 50 # There is not exist easier than this**  
**Soru:** *https://drive.google.com/open?id=0B5i8WVYofXg6MmdWejRnU2hrYXc*

Sorunun başlığı “There is not exist easier than this” olunca direk kontrastla oynadık; parlaklığı low, kontrastı high yapınca flag görünüyordu. (çok yakından kazın üstüne bakmanız gerekiyor.)

![]({{ AUCyberClub.github.io }}/assets/img/cypmctfcozumler/68.png)

Flag:	cypwn_{cok_gizli}
