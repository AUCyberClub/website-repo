---
layout: post
title: Siber Güvenlik 101
date: '2021-03-10 22:26:47 +0300'
author: Can Öztaş
categories: intro
index: 3
---


<h1><center><strong>Siber Güvenlik 101</strong></center></h1>

Oxforda göre “hacking”in tanımı:

<a href="https://www.oxfordlearnersdictionaries.com/definition/english/hacking"><i>"Birinin bilgisayar ya da telefonuna izni olmadan erişme işi"</i>

olarak geçmekte. Tabii ki IOT çağında bu işi sadece bilgisayarlarla ya da telefonlarla sınırlamak artık yeterli değil, zira artık her şey internet'e bağlı durumda.

Ama "Peki bu iş teoride adım adım nasıl yapılıyor”sorusu önemli bir soru. Gelin bu işin metodolojisine teorik bir giriş yapalım. Kavramları anladıktan bu işlerin detaylarını diğer yazılarımızda bulabilirsiniz:







A.Gözlem:
Bir sisteme sızma öncelikle bilgi toplamakla başlar. Bilgi toplama işinde arama motorları en büyük yardımcıdır. Sızılmak istenen sisteme ait yetkili kişi/kişilerin bulunması, bu kişiler hakkında e-mail'den tutun da evcil hayvanının adına kadar araştırma, IP adresleri, DNS kayıtları, o yerin varsa eski leak'lerde olup olmaması gibi gibi bir araştırma ilk aşamadır. Araştırma ve gözlem işi google'dan başlayıp darknete kadar adeta bir kazı yapar gibi devam eder.

B.Scanning:
Bu aşamada var olan sistemle ilgili arka planda nelerin çalıştığını anlamaya yönelik süreç başlar. Port taraması veya network-mapping bu aşamada yapılır. İlk aşamadan farklı olarak aslında bu aşamada sistemdeki insanlardan çok, makinelerin gözlemi yapılır kısa ve net bir tanım olabilir. [(yazımız burada)](https://www.aucyberclub.org/hackingfalan/network/2021/03/14/network101.html)

C.Gain Access:
Ve Hacker filmlerinin en havalı sahnesine gelmiş durumdayız. Sisteme yetki sağlamak. İlk iki aşamada doğru bilgiler bulunduktan sonra, sisteme sızıntı sağlamak aslında en çok social-engineering phishing temelli saldırılar yapılır. Filmlerden de aşina olduğumuz email-spoofing yeterli inandırıcılık ile büyük şirketlere ve kurumlara çok büyük dert olabilir. Kullanılan teknolojileri bir şekilde öğrenildikten sonra, buna istinaden hazır malware'ler ya da o teknolojilere özel malware'ler kullanılabilir ve yazılabilir. 

D.Erişimi Devam Ettirme:
Bir şekilde sisteme sızıldıktan sonra, bağlantının kalıcı olması amaçlanabilir. Erişilen sistemde yetki yükseltilmesi , aynı network’deki başka makinelere sıçranması gibi gibi olaylar bu aşamada yapılır.

E.Temizlik:
Tabii ki işin içinde, kali linux’un mottosu’nda olduğu gibi “the quieter you become the more you can hear” [https://www.kali.org](https://www.kali.org), sessizlik önemlidir. İş bittikten sonra aynı sessizlikte ayrılmak gerekebilir, o da bu aşamadır. Kısaca bu aşama server log’ları, temp dosyalar gibi şeyleri temizlemeyi kapsayan aşamadır.

F.Raporlama:
Aslında black/white hat [(hack kültürü)](https://www.aucyberclub.org/hackingfalan/intro/2021/03/11/hack-kulturu.html) kısmının ayrıldığı nokta burasıdır. İki şapka da kabaca bu aşamaya kadar aynı metodolojiyi kullanırken, white hacking’de raporlama vardır. İşten sonra bu rapor sistem sahiplerine, IT’cilere sorumlu kimse onlara teslim edilerek bulunan açıkların kapatılması amaçlanır.

![]({{ AUCyberClub.github.io }}/hackingfalan/assets/siber-101/graph.png)

<h4>NASIL KORUNURUZ ?</h4>

->Account'larda iki adımlı doğrulama sistemi (two-factor authentication) varsa kesinlikle açılsın

->Olabildiğince komplex parolalar seçin, kesinlikle her hesaba farklı parola, hafızam zorlanıyor diyorsanız da en azından ana mail hesabınıza kesinlikle zor bir parola seçin

->Tuhaf linklere tıklamadan önce kontrol edin,[ https://transparencyreport.google.com/safe-browsing/search?hl=en](https://transparencyreport.google.com/safe-browsing/search?hl=en) gibi bir sürü servis var.

**->Crack torrent sorunlu işlerdir, legal değildir ve tavsiye etmiyoruz, ama çok gerekiyorsa belki bir sanal makine açılıp crackli işler orada halledilebilir.**

->Gelen her mailde uyanık olun, zira scam e-mail'ler her mail servisi tarafından bloke edilemiyor.

->Güvenmediğiniz sitelerde tarayıcı ayarlarından javascript çalışmasını kapatabilirsiniz.

->Belirli aralıklarla cache(önbellek) temizlemeyi unutmayın.

->Bilmediğiniz sitelerden dosya indirmeyin, çok da indiresiniz varsa sanal makine, biliyorsunuz.

![]({{ AUCyberClub.github.io }}/hackingfalan/assets/siber-101/polis.png)









 

