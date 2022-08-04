---
layout: post
title: HackKaradeniz Write-up
date: '2022-07-29 13:00:00 +0300'
categories: cozumler
---


# HACKKARADENİZ CTF WRITE-UP
<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/aucc-logo.png" />
</p>



Ankara Üniversitesi Siber Güvenlik Topluluğu (**AUCC**) üyeleri olarak 16.07.2022- 17.07.2022 tarihlerinde katılıp 6. olarak tamamladığımız Hackkaradeniz Yarı Final CTF'inin çözümleri.

**AUCC** yarışmacıları:
- ***canoztas*** | *Can ÖZTAŞ* | *Ankara Üniversitesi*
- ***allesfresser*** | *Mücahit KURTLAR* | *Ankara Üniversitesi*
- ***krypton*** | *Yiğit GÜNDOĞDU* | *Ankara Üniversitesi*
- ***f2u0a0d3v1*** | *Fuad ANZUROV* | *Ankara Üniversitesi*

## NETWORK
### N-T-W-1:

- [A-Packets](https://apackets.com/pcaps?pcap=a311d973e9686a57240228c92979cf6f.pcap&view=flows)

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/n-t-w-1-1.png" />
</p>

- HTTP requestlerine bakıldığında `dvwa` üzerine saldırı yapıldığı gözlemleniyor, örnek bir  payloaddan `sql injection` olduğunu anlıyoruz.

**FLAG:** `Flag{sql_injection}`

### N-T-W-2:

- [A-Packets](https://apackets.com/pcaps?pcap=f6c79bf84ed292eee13a47612fe7a6fc.pcap&view=ftp)

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/n-t-w-2-1.png" />
</p>

- FTP loglarına baktığımızda bir shell dosyası attığını görüyoruz. Dosyanın adı da `bBHk1d.php`

**FLAG:** `Flag{bBHk1d.php}`

### N-T-W-3:

- [A-Packets](https://apackets.com/pcaps?pcap=f6c79bf84ed292eee13a47612fe7a6fc.pcap&view=graph)

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/n-t-w-3-1.png" />
</p>

- Trafiği incelediğimizde en anomali durumun `4444` portu ile konuşma olduğunu fark ediyoruz.

**FLAG:** `Flag{172.16.8.50,4444}`

## WEB
### Interview:

- Domainler şuan kapandığı için screenshot alamıyoruz ve flagi hatırlamıyoruz ama attığımız mailin logları ve mail screenshotu buradadır.
- Siteyi dolanırken kariyer sayfasında mail atmamız gerektiğini anlıyoruz. Ayşe Zonguldak’ın e-mailini Twitter'da buluyoruz. Maili attığımızda bize kullanıcı-adı parola veriyor.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/interview-1.png" />
</p>

- Bu bilgilerle girdiğimiz panelde hatırladığımız kadarıyla `md5` ile şifrelenmiş query stringdeki obje referansları vardı, bunu sırayla denediğimizde flag’e ulaşıyoruz.

## MISC
### Anıt:

- [/robots.txt](https://anit.hackkaradeniz.xyz/robots.txt)
- [/canakkale.jpg](https://anit.hackkaradeniz.xyz/canakkale.jpg)
- [/img](https://anit.hackkaradeniz.xyz/img/)
- Sitedeki bu endpointleri buluyoruz. robots.txt’den çıkan resim’den bozuk bir resim dosyası buluyoruz. Buradan bitlerini jpg jfife çevirince bu resmi buluyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/anit-1.jpg" />
</p>

- Görsel bizi `anit.php`’ye götürüyor. Burada `ascii` ve `hex`’li bir şifreleme olduğunu verilen görsellerden ve sitenin yorumlarıdan tahmin ediyoruz ama biz bu pattern’i tam olarak kestiremesek de...

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/anit-2.png" />
</p>

- ...akıllıca bir brute force atarak `302` dönen yeri buluyoruz. Abide kelimesinin `Adlhh` olduğun bulduğunu buluyoruz.
- Sonra gelen ekranda 2 fotoğrafın lokasyonu bize soruluyor reverse image search ile birinin Ankara Yenimahalle diğerinin Bursa Osmangazi olduğunu buluyoruz. İlgili yerleri girince flage ulaşıyoruz.

**FLAG:** `Flag{4n1tl4r_t4r1ht1r}`

### Fernet:

- [fernet](https://fernet.hackkaradeniz.xyz)
- Sitede kırmızı ile HackKaradeniz yazılmıştı, buraya gidince Method not Allowed dönüyordu, biz de önce OPTIONS atıyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/fernet-1.png" />
</p>

- response’da post atıldığını söylüyor, post atınca bize bir key ve ciphertext dönüyor.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/fernet-2.png" />
</p>

- Sitenin domainin de adından bunun `fernet encryption` olduğunu anlıyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/fernet-3.png" />
</p>

- [class cryptography.fernet.Fernet(key)](https://cryptography.io/en/latest/fernet/)
- `python` kullanarak flag'i buluyoruz.

**FLAG:** `FLAG{H4cK_kar4D3n1z_2o22-T3mMuz}`

## MALWARE
### Forrest Gump:

- Verilen unity ile yapılmış programı dnSpy ile `HKGame_data>Managed>Assemly-CSharp.dll` ile açtığımızda `UnityMovement` classının içinde `DetectTouchingObject` fonksiyonun oyunun amacına göre flagı vereceğini düşündük.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/forrest_gump-1.jpg" />
</p>

- Kodu kendimiz çalıştırdığımızda flagı elde ettik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/forrest_gump-2.jpg" />
</p>

**FLAG:** `FLAG{F1N4L3_DOGRU_4D1M_4D1M}`

### windows.exe:

- Verilen exe dosyasına [VIRUSTOTAL](https://www.virustotal.com/gui/)'a attık VIRUSTOTAL ile dosyayı tarattığımızda içinde farklı dosyaların olduğunu tespit ettik.

- `DirWatch` toolu ile incelediğimiz de `config.json` dosyası 
olduğunu fark ettik. `config.json` dosyasının incelediğimizde `base64` formatında decode ettiğimizde flag karşımıza çıktı.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/windows_exe-1.png" />
</p>

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/windows_exe-2.png" />
</p>

```json
[{"Algo":"","Coin":"","URL":"pool.hashvault.pro:80","User":"46zddr14XunCANLoynmVXxSFZi15Af3qycbEPoH72qrS6dSFHdavYnHb29zTNXqqRHAFBMmWxW5QuKvfYdAQ5SU3GqqRfEA","Pass":"RmxhZ3sweDQ2NkM2MTY3N0I2ODY1NzI3MzY1Nzk3NjM0NzQ2MTZFMzE2MzY5NkU3RH0=","RigID":1,"NiceHash":false,"KeepAlive":false,"Enabled":true,"TLS":false,"TLSFingerprint":"","Daemon":false,"Socks5":"","SelfSelect":"","SubmitToOrigin":false}],"PrintTime":0,"HealthPrintTime":0,"DMI":false,"Retries":0,"RetryPause":0,"Syslog":false,"tls":{"Enabled":false,"Protocols":"","Cert":"","CertKey":"","Ciphers":"","CipherSuites":"","Dhparam":""},"dns":{"IPv6":false,"TTL":0},"UserAgent":"","Verbose":0,"Watch":false,"PauseOnBattery":false,"PauseOnActive":false}
```

- `Pass` key'ine bakarsak:

```json
"Pass":"RmxhZ3sweDQ2NkM2MTY3N0I2ODY1NzI3MzY1Nzk3NjM0NzQ2MTZFMzE2MzY5NkU3RH0="
```

- base64 decode edersek:

`Flag{0x466C61677B686572736579763474616E3163696E7D}`

**FLAG:** `Flag{herseyv4tan1cin}`

### FunctionBomber:

- ELF dosyasını `ida` ve `ghidra` ile incelediğimizde `CreateFlag` fonksiyonlarından 99999 tane olduğunu görüyoruz. Bu fonksiyonlardan sahte olanların yalnızca return 1 olduğunu. Doğru fonksiyonu bulabilmek için `objdump -d` ile fonksiyonlara ait bilgileri çektik. Yazdığımız `python` scripti ile fonksiyonların `assemble` kod kısımlarında 3.satırında `mov eax,1` olmayan fonksiyonu bulduk.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/functionbomber-1.jpg" />
</p>

- çıktısı:

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/functionbomber-2.jpg" />
</p>

- Belirlediğimiz fonksiyonun `assemble` koduna baktık.Daha sonrasında `gdb` asıl `main` kısmının  `return` addresine breakpoint koyarak rip ye bu fonksiyonun adresini koyduk ve fonksiyonu çalıştırdık.Her aşamada rspyi kontrol ettik ve sonucunda `SEt7QzR5ZWxpbmRlbl9PdGV5ZTUzfQ` elde ettik.
`Cybershef` de magic modda cipherı verdiğimizde flagı elde etmiş olduk.

**FLAG:** `HK{C4yelinden_Oteye53}`

### Hesap Makinesi:

- Verilen `elf` dosyasının `go` ile yazılmış olduğunu ve `upx` ile packlendiğini fark ettik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/hesap_makinesi-1.jpg" />
</p>

- `upx -d` ile unpack ettikten sonra file `ida`’da açtık. `main` kısımlarından `main_meh` kısmında gizli bölme olduğunu gördük.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/hesap_makinesi-2.jpg" />
</p>

- Kodun ilerleyen kısımlarında password sorduğunu ve gördük. Password kısmına geçtikten sonra ise encode edilmiş datanın 3 kere `base64` formatında decode edildiğini fark ettik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/hesap_makinesi-3.jpg" />
</p>

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/hesap_makinesi-4.jpg" />
</p>

- Sonrasında flag'i elde ediyoruz.

`Flag{0x466C61677B68617934747434656E68616B696B696D7572736974696C696D6469727D}`

**FLAG:** `Flag{hay4tt4enhakikimursitilimdir}`

### Mixer:
- Verilen exe dosyasını `ida` ile açtığımızda flage ulaşabilmek için `strcmp` yapıyor ancak `strcmp`in öncesinde bir `swap` işlemi yapıyor. Ayrıca `swap` işlemi girilen inputu ortadan ayırıp ters çeviriyor. Karşılaştırma yaptığımız değeri bu `swap` algoritmasına göre düzenleyip exe dosyasında çalıştırdığımızda bize flagi elde ediyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/mixer-1.png" />
</p>

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/mixer-2.png" />
</p>

**FLAG:** `Flag{H3y6!D!_K4R4D3N!2}`

### RansomWare:

- Verilen exe dosyasını `ida` ile açtığımızda encode edilmiş partı keşfettik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/ransomware-1.png" />
</p>

- Encode edilmiş partta tam tersini yapacak bir script yazdık.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/ransomware-2.jpg" />
</p>

- Daha sonrasında flagi elde etmiş olduk.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/ransomware-3.jpg" />
</p>

**FLAG:** `Flag{K4r4d3n!zD3_Ru264r_S3RT_3s3R}`

### Klasik:

- Verilen exe dosyasını çalıştırdığımızda direkt olarak flag karşımıza çıkıyor :)

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/klasik-1.jpg" />
</p>

`Flag{0x466C61677B6D696C347474616E6F6E63653230397D}`

**FLAG:** `Flag{mil4ttanonce209}`

### Dünya Dönüyor:

- Öncelikle verilen dosyayı ida ile açtığımızda `sub_C81320` fonksiyonunun `return` değeri 1 olacak şekilde patchledik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/dunya_donuyor-1.png" />
</p>

- Sonra kodun bu kısmını  eşit değilden eşit olacak şekilde pathcleyip her compare edildiğinde `edx` valuesunu yazdıracak şekilde conditional breakpoint koyduk.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/dunya_donuyor-2.png" />
</p>

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/dunya_donuyor-3.png" />
</p>

- Daha sonrasında inputu orjinal exeye girince flagi elde ettik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/dunya_donuyor-4.png" />
</p>

**FLAG:** `HK{Z0n6uLD4K_y0Lcu5u_K4LM4S1N}`

### ASM:

- Verilen `asm` kodunu `.s` uzantısı ile kaydettikten sonra `g++` ile derledik.Daha sonra `ida` ile açtığımızda okunabilir koda ulaştık.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/asm-1.jpg" />
</p>

- Encode function:

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/asm-2.jpg" />
</p>

- Burda `des` arrayini `ida`’da `hex` kısmından çekip düzenledik ve bu algoritmaya göre her karakter için `brute-force` yapacak scripti yazarak flagi elde ettik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/asm-3.jpg" />
</p>

**FLAG:** `HK{Karadenizin_bir_havasi_bir_yaylasi123}`

### Deep:

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/deep-1.png" />
</p>

- Verilen file `ida`’da açtığımızda ilk başta kodun bu kısmını bakarak yaptık ancak yanlış flag geldiği için diğer fonksiyonlara baktık.`printf`'in ayrı implementasyonunu olduğunu gördük ve  baktığımızda bir şeyi decode ettiğini fark ettik ve bunu `python`'da kodunu yazdık.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/deep-2.jpg" />
</p>

- Register olarak 8-bit register kullandığından burada rotate rightada oluşabilecek maksimum kombinasyon 8 olmalıydı. Bunu da ekleyince `base64` formatında değer geldi.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/deep-3.png" />
</p>

**FLAG:** `HK{K4r4den1z1n_S1ber_Y1ld1zlar1}`

##  OSINT
### GEOINT:

- Görseldeki kapının alt kısmındaki afişe dikkatlice baktığımızd `unterschriften sammelstelle` yazdığını görebiliriz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/geoint-1.png" />
</p>

- Bu kelimeleri `Google Images` üzerinden arattığımızda karşımıza aşağıdaki gibi bir sonuç çıkıyor.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/geoint-2.png" />
</p>

- Benzer afişli sonucun kaynağının `Aachen` merkezli bir bisikletçi aktivist topluluğu olduğunu görüyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/geoint-3.png" />
</p>

- Buradan yola çıkarak Aachen’deki restoranları arıyoruz...

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/geoint-4.png" />
</p>

- ...ve konumun Macaroni olduğunu öğreniyoruz.

- Sonrasında restoranın web sitesi üzerinde iletişim kanallarında bir mail adresi olduğunu görüyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/geoint-5.png" />
</p>

- Mail adresine ilişkin bir leak olup olmadığına baktığımızda ise [123rf](https://123rf.com) üyeliğinin expose olduğunu öğreniyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/geoint-6.png" />
</p>

- [Bu](https://www.bleepingcomputer.com/news/security/popular-stock-photo-service-hit-by-data-breach-83m-records-for-sale/) web sitesindeki habere göre sızan kullanıcı bilgileri arasında parola hash’lerinin de olduğunu öğreniyoruz.

- [Bu](https://breachdirectory.org/) leak sitesinde mail adresini girğimizde ise aşağıdaki gibi bir sonuç karşımıza çıkmakta

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/geoint-7.png" />
</p>

**FLAG:** `Flag{d26fd6a8b28f2c2b3f2cdc3ac1c9d52bb41ca4ce}`

### BlackOnBlack:

- Soru dahilinde verilen siyah görseli [aperi](https://aperisolve.fr) web sitesine upload ettiğimizde çıkan sonuçlardan biri aşağıdaki gibi oluyor.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/blackonblack-1.png" />
</p>

- Okunabilirliği arttırmak adına Gimp üzerinden renk kanalları üzerinden kurcalama yaptıktan sonra aşağıdaki gibi bir görsel elde ettik.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/blackonblack-2.png" />
</p>

```
OBQXG4Z2MU2HG6LQGRZXG5ZQOJSA====
```

- `base64` ile encode edilmiş gibi görünüyor fakat anlamlı bir sonuç çıkmıyor. Base32 ile denediğimizde ise aşağıdaki gibi clean texti elde ediyoruz

```
pass: e4syp4ssw0rd
```

- Password çıktığına göre muhtemelen görselde steghide ile bir dosya saklanmış durumda. Denediğimizde ise haklı olduğumuzu görüyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/blackonblack-3.png" />
</p>

- Text dosyası içinde bahsi geçen BSSID’yi Wigle üzerinden arıyoruz ve flag’i buluyoruz.

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/blackonblack-4.png" />
</p>

**FLAG:** `Flag{bl4ck_ch405}`

### Rotasını Şaşıran Tır - 1:
- Soruda geçen +d0qbfGAndK82YmU0 hash analiz eden programlarca tanınamadı ve pastebin vb. sitelerde directory olarak çıkmadı. Fakat sonuç olarak Telegram invite linki olarak deneyince...

<p align="center">
  <img src="{{ AUCyberClub.github.io }}/assets/img/hackkaradeniz/rotasini-sasiran-tir-1-1.png" />
</p>

**FLAG:** `Flag{M4sm4vi_K4r4d3niz4_H0sg3ldin}`


 ---
 **[Mücahit KURTLAR](https://www.linkedin.com/in/mucahitkurtlar/)**
 **[Yiğit GÜNDOĞDU](https://www.linkedin.com/in/yigit-gundogdu)**
 **[Can ÖZTAŞ](https://www.linkedin.com/in/can-oztas/)**
 **[Fuad ANZUROV](https://www.linkedin.com/in/f2u0a0d3/)**
