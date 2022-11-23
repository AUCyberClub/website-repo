---
layout: post
title: Komut ve Kontrol Sunucusu (Command and Control Server/C2) Nedir?
date: '2022-10-30 22:26:47 +0300'
author: İsmail Başaran
categories: intro
index: 5
---
Komut ve kontrol (Command and Control/C2) saldırısı, ele geçirilmiş ana bilgisayar ile saldırganın sunucusu arasında gizli bir kanal oluşturmak için kullanılan kötü amaçlı yazılım saldırılarının bir bileşenidir. Bu tür saldırılarda saldırganın sunucusuna genellikle Komut ve Kontrol Sunucusu, C2 sunucusu veya C&C sunucusu denir. Saldırı sunucusu, kurbanın bilgisayarında farklı türde kötü amaçlı faaliyetler gerçekleştirmek için oluşturulan arka kapıdan yararlanır. DNS (alan isimlendirme sistemi) tünellemesi ile veri sızdırma bu faaliyetlere örnek verilebilir.

Yeterli süre tanındığında kötü amaçlı yazılım, ağdaki daha savunmasız ana bilgisayarları tanımlayabilir ve bu bilgisayarlara yayılabilir. Bu işlem “pivoting” olarak da bilinir. Daha fazla sistem ele geçirildiğinde zombi sistemlerden oluşan botnet oluşturulmuş olur. Sonrasında bu botnet’ler, DDoS (Dağıtık Hizmet Engelleme) saldırıları yapmak gibi daha zararlı etkinlikleri gerçekleştirmek için komutlar alır.

![]({{AUCyberClub.github.io}}/CyberCamp/assets/KomutveKontrolSunucusuNedir/1.png)

C2 oldukça tehlikeli bir saldırı yöntemidir çünkü yalnızca bir enfekte bilgisayar tüm ağı çökertebilir. Kötü amaçlı yazılım hedef makinede kendini bir kez çalıştırdığında C2 sunucusu onu çoğaltmak ve yaymak için komut verebilir —bu, ağ güvenlik duvarı çoktan geçildiği için kolayca gerçekleşebilir.

Virüs bir kez ağa bulaştığında saldırgan, kullanıcıları saf dışı bırakmak için ağı kapatabilir veya enfekte olan cihazları şifreleyebilir. 2017’deki WannaCry fidye saldırıları, hastaneler gibi kritik kurumlardaki bilgisayarlara bulaşarak, onları kilitleyerek ve Bitcoin cinsinden fidye talep ederek tam olarak bunu yaptı.

![]({{AUCyberClub.github.io}}/CyberCamp/assets/KomutveKontrolSunucusuNedir/2.png)

### **Komut ve Kontrol (C2) sunucuları nasıl çalışır?**

Siber güvenlik alanında zincirin en zayıf halkası insanlardır. Bu nedenle çoğu durumda saldırganlar kişiyi panik yapmaya itecek, bilinçsizce hareket etmesini sağlayacak e-postalar ve dosyalar göndererek insanların zayıflıklarına saldırır. Kurban kötü amaçlı dosyayı indirip çalıştırdığında zararlı yazılım güvenlik duvarını aşarak ağı ve bilgisayarı tehlikeye atar.

C2 saldırıları, aşağıdaki gibi kanallardan meydana gelebilecek ilk bulaşmalarla başlar:

- kötü amaçlı web sitesi bağlantıları veya kötü amaçlı ekler içeren “phishing” e-postalarıyla
- bazı tarayıcı eklentilerindeki güvenlik açıklarıyla
- zararsız görünen virüslü yazılımlarla veya yazılım güncellemeleriyle
- güvenilir sitelere yüklenmiş (örneğin Play Store) uygulamaların gerçekleştireceği iç güncellemelerde yüklenen yazılımlarla

Örnek bir Command & Control saldırısı, aşağıda açıklanan bir dizi adımda gerçekleştirilebilir:

1. Adım:

   Saldırgan, kullanıcının sistemine veya bir kuruluş içindeki -genellikle güvenlik duvarının arkasındaki- bir sisteme kötü amaçlı yazılımı bulaştırır. Bulaştırma işlemi; “phishing” e-postaları, güvenlik açığı barındıran tarayıcı eklentileri, depolama birimleri, yüklenebilir programlar, kötü amaçlı reklamlar vb. farklı yollarla gerçekleştirilebilir.

   ![]({{AUCyberClub.github.io}}/assets/img/KomutveKontrolSunucusuNedir/3.png)
2. Adım:

   Ana bilgisayara virüs bulaştığında C2 kanalı oluşturulur ve ele geçirilen sistem, komutları almaya hazır olduğunu belirtmek için C2 sunucusuna bir bildirim gönderir. Bu iletişim çoğunlukla DNS gibi güvenilir trafik üzerinden yapılır.

   ![]({{AUCyberClub.github.io}}/CyberCamp/assets/KomutveKontrolSunucusuNedir/4.png)
3. Adım:

   C2 kanalı hazır hale geldiğinde kötü amaçlı yazılım tespit edilmediği sürece virüslü sistem C2 sunucusundan komutlar alabilir. C2 sunucusu, yüklenecek daha fazla yazılım göndermek, verileri şifrelemek ve hatta virüslü ana bilgisayardan tekrar tekrar veri ayıklamak için bu kanalı kullanabilir.

   ![]({{AUCyberClub.github.io}}/CyberCamp/assets/KomutveKontrolSunucusuNedir/5.png)

C2 sunucusu, ağ üzerinden geçiş yapmak için ağdaki diğer sistemlerdeki güvenlik açıklarını aramayı başlatacak komutlar da verebilir. Bu, bir kuruluşun BT (Bilgi Teknolojileri) altyapısını tamamen tehlikeye atabilir ve botnet olarak bilinen ele geçirilmiş bilgisayarlar ağının oluşturulmasına yol açabilir. Tüm bu zombi makineler ordusunun tek amacı, koordine saldırılar gerçekleştirmek için C2 sunucusundan komut almaktır.

### **C2 Sunucu Yapıları**

Saldırganlar C2 sunucularını birkaç farklı yapıya veya topolojiye göre yapılandırılabilir:

- Yıldız topolojisi: Botlar tek bir merkezi sunucu etrafında düzenlenir.
- Çoklu sunucu topolojisi: Karışıklık yaratmak için birden fazla C2 sunucusu kullanılır.
- Hiyerarşik topoloji: Birden çok C2 sunucusu, bir hiyerarşi içinde düzenlenir.
- Rastgele topoloji: Virüslü bilgisayarlar eşler arası “botnet” (peer-to-peer botnet/P2P botnet) olarak iletişim kurar.

2017'ye kadar bilgisayar korsanları, Telegram gibi uygulamaları kötü amaçlı yazılımlar için komut ve kontrol merkezleri olarak kullanıyorlardı. Sadece bu yıl 130 vakada bilinçsiz insanlardan veri çalabilen ve kişileri bilgisayarları aracılığıyla izleyip kaydedebilen ToxicEye adlı bir program bulundu.

#### Kaynaklar:

- https://www.howtogeek.com/726136/what-is-a-command-and-control-server-for-malware/
- https://www.paloaltonetworks.com/blog/security-operations/from-the-hunter-diaries-detecting-c2-servers/
- https://www.feroot.com/education-center/what-is-a-command-and-control-c2-server/
- https://vvelitkn.com

---

**[İsmail Başaran](https://www.linkedin.com/in/ismail-ba%C5%9Faran-063000256/)**
