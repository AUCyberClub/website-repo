---
layout: post
title: MetaTwo CTF Write-Up
date: '2022-21-11 13:00:00 +0300'
author: Eren İşlek
categories: cozumler
---

CTF linki: https://app.hackthebox.com/machines/MetaTwo

Hackthebox tarafından sağlanan ip üzerinde çalışan servisleri tespit etmek ve karşı makine hakkında fikir sahibi olmak için hedef makineyi tarıyoruz.

`nmap -sV -sC 10.10.11.186`

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/55d8bbde8c00789008f78880adc5fbf5.png" alt="55d8bbde8c00789008f78880adc5fbf5.png" width="1500" height="auto" >

Karşı tarafın 21. portunda FTP servisi, 22. portunda SSH servisi, 80. portunda ise http servisi yani bir web sitesi çalıştığını görüyoruz.
Ayrıca karşıda bir WordPress web sitesi olduğunu ve bu web sitesinin 5.6.2 sürümünü çalıştırdığını görüyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/7a1f8069e8151dfc5c198839291bb67b.png" alt="7a1f8069e8151dfc5c198839291bb67b.png" width="1500" height="auto" >

Bize verilen IP'yi tarayacımızda açtığımızda "http://metapress.htb/" web adresine yönlendirdiğini görüyoruz. Bizim elimizde bir IP adresi var fakat karşı tarafta bir domain çalışmakta bu IP adresini bilgisayarımızda domain adresine yönlendirmemiz gerekmekte. Bu sebeple "/etc/hosts" dosyasını düzenlememiz gerekiyor.
`sudo nano /etc/host`

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/6dd7d8b73d662ae918b2d9f20be61403.png" alt="6dd7d8b73d662ae918b2d9f20be61403.png" width="1500" height="auto" >

Web sitesine girdiğimizde bu ekranla karşılaşıyoruz ve bu ekranda bir randevu sistemine yönlendiren bir link olduğunu görüyoruz

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/ce832d8ec9f827b508c5e52d55023a69.png" alt="ce832d8ec9f827b508c5e52d55023a69.png" width="1500" height="auto" >

Bu randevu sistemi bir eklenti ile çalışmak zorunda, bu eklentinin sürümünü bularak bu sürümde herhangi bir zafiyet olup olmadığını öğreneceğiz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/f82b8607196691ed56f9b3c674cb55f8.png" alt="f82b8607196691ed56f9b3c674cb55f8.png" width="1500" height="auto" >

Sitenin kaynak koduna bakarak eklenti sürümünü görebiliriz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/c3d2d4dfd43458dba1b7618d174b6a68.png" alt="c3d2d4dfd43458dba1b7618d174b6a68.png" width="1500" height="auto" >

Bu sürümü internette aratarak zafiyet arıyoruz.

https://wpscan.com/vulnerability/388cd42d-b61a-42a4-8604-99b812db2357
<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/5a616b1f0e22a982733f5c7e6d239e49.png" alt="5a616b1f0e22a982733f5c7e6d239e49.png" width="1500" height="auto" >
CVE-2022-0739

Aratınca karşımıza bir SQL Injection zafiyeti çıkıyor. Ve CVE'sini internette aratarak bu zafiyeti sömüren bir python kodunu buluyoruz.

https://github.com/destr4ct/CVE-2022-0739

Bu python kodunu çalıştırmak için nonce bulmamız gerekiyor. Bunun için çalışan servisin yine kaynak kodunda "nonce" aratıyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/26cd298a3e481e1c99d322fa17a96d9b.png" alt="26cd298a3e481e1c99d322fa17a96d9b.png" width="1500" height="auto" >

Kodumuzu çalıştırıyoruz, admin ve manager kullanıcılarının SQL sunucsunda şifrelenmiş olarak depolanan hallerini elde ediyoruz. Bunları kullanmadan önce bruteforce yöntemi ile asıl şifreyi bulmamız gerekiyor.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/2bbc0cbb9a51d12eb70121bfe93b1242.png" alt="2bbc0cbb9a51d12eb70121bfe93b1242.png" width="1500" height="auto" >

Admin kullanıcısı için herhangi bir eşleşme bulamıyoruz fakat manager kullanıcısı için şifreyi bize kullandığımız araç veriyor.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/765b0709340547631192c42c841108a0.png" alt="765b0709340547631192c42c841108a0.png" width="1500" height="auto" >

Elde ettiğimiz şifre ve kullanıcı adını kullanarak sitedeki manager kullanıcısına giriş yapıyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/06c0c4af07f14c67cb31dd14d8d38657.png" alt="06c0c4af07f14c67cb31dd14d8d38657.png" width="1500" height="auto" >

Manager kullanıcısının sitede çok yetkisinin olmadığını görüyoruz. Ama siteye dosya yükleyebiliyoruz, en başta bulduğumuz wordpress sürümünün eski olduğu için zafiyetli olabileceğini düşenerek bu sürümle alakalı zafiyetleri internette aratıyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/25cd62d725bf1bb1c4860d439677691f.png" alt="25cd62d725bf1bb1c4860d439677691f.png" width="1500" height="auto" >

https://blog.wpsec.com/wordpress-xxe-in-media-library-cve-2021-29447/

Sitede verilen yönergeleri takip ederek evil.dtd ve payload.wav dosyalarını oluşturuyoruz. Daha sonra php sunucusu başlatıp wav dosyamızı karşı tarafa yüklüyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/72d46dc40aaa4e995daba3bf81818647.png" alt="72d46dc40aaa4e995daba3bf81818647.png" width="1500" height="auto" > <img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/c75a8564a3b899a2c66103680f128df3.png" alt="c75a8564a3b899a2c66103680f128df3.png" width="1500" height="auto" >

Elde ettiğimiz veri base64 formatında olduğu için decode ediyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/f7def063623f9af9c4f8dcb460a08586.png" alt="f7def063623f9af9c4f8dcb460a08586.png" width="1500" height="auto" >

Karşı tarafta dosya okuyabiliyoruz, o zaman wordpress web sitelerinin önemli bilgilerini tutan "wp-config" dosyasını okuyarak kayıtlı kullanıcıların giriş bilgilerini elde edebilriz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/a4b0c8239d45304c06db27f75d1d290d.png" alt="a4b0c8239d45304c06db27f75d1d290d.png" width="1500" height="auto" >

Kodumuzu tekrar çalıştırıp decode ettiğmizde FTP sunucusu için giriş bilgilerini buluyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/8f9d64b86ef8ca155f13451aea433a71.png" alt="8f9d64b86ef8ca155f13451aea433a71.png" width="1500" height="auto" >

FTP sunucusna giriş yapıp içinde bilgiler barındırabilecek dosyayı kendi bilgisayarımıza indiriyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/5dfa6eba4ab6a6a314349f4be794d0cb.png" alt="5dfa6eba4ab6a6a314349f4be794d0cb.png" width="1500" height="auto" >

Bu dosyaya baktığımızda SSH giriş bilgileri elde ediyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/00785069dcc6240e788f1a624fda101f.png" alt="00785069dcc6240e788f1a624fda101f.png" width="1500" height="auto" >

Bilgileri kullanıp giriş yaptığımızda ilk flagimizi buluyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/cf083896af4842b95720873f9ba7e87f.png" alt="cf083896af4842b95720873f9ba7e87f.png" width="1500" height="auto" >

Daha sonra home klasörümüze baktığımızda .passpie isimli bir klasör buluyoruz. Passpie isimli bir şifre yöneticisi uygulamasının karşı tarafta kurulu olduğunu görüyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/f3ef1c1fa96960d46b27d8567a0f6c2f.png" alt="f3ef1c1fa96960d46b27d8567a0f6c2f.png" width="1500" height="auto" >

".keys" dosyasındaki PGP anahtarını alıp bilgisayarımızda key adlı dosyaya kaydediyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/329a38dad80dca20eceba09cbf89864b.png" alt="329a38dad80dca20eceba09cbf89864b.png" width="1500" height="auto" > <img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/0a12771fcbfaaa41ee88d44f0c327e90.png" alt="0a12771fcbfaaa41ee88d44f0c327e90.png" width="1500" height="auto" >

Önce gpg2john adlı aracı kullanarak bu private keyi hash formatına çeviriyoruz. Ve john ile bruteforce yöntemiyle şifreyi elde ediyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/c969425d78cb4394be101dddb7f84a43.png" alt="c969425d78cb4394be101dddb7f84a43.png" width="1500" height="auto" >

Bu elde ettiğimiz şifre passpie'ın şifresi. Bu şifreyi kullanarak passpie'daki kayıtlı kullanıcı giriş bilgilerini elde ediyoruz. Sonra bu şifreyi kullanarak root kullanıcısına giriş yapıp root flagimizi alıyoruz.

<img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/378902ba001aca78892db89b2be2f4cc.png" alt="378902ba001aca78892db89b2be2f4cc.png" width="1500" height="auto" > <img src="/assets/img/MetaTwoHackTheBoxCTFWriteup/6e99989eb38bec4b03e93749f03b07c8.png" alt="6e99989eb38bec4b03e93749f03b07c8.png" width="1500" height="auto" >