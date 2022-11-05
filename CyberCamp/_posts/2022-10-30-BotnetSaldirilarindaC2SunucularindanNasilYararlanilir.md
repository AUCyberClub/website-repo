---
layout: Botnet Saldırılarında C2 Sunucularından Nasıl Yararlanılır?
title: Siber Güvenlik 101
date: '2022-10-30 22:26:47 +0300'
author: İsmail Başaran
categories: intro
index: 4
---

Komut ve kontrol (Command and Control/C2) saldırısı, ele geçirilmiş ana bilgisayar ile saldırganın sunucusu arasında gizli bir kanal oluşturmak için kullanılan kötü amaçlı yazılım saldırılarının bir bileşenidir. Bu tür saldırılarda saldırganın sunucusuna genellikle Komut ve Kontrol Sunucusu, C2 sunucusu veya C&C sunucusu denir. Daha fazla bilgi için “Komut ve Kontrol Sunucusu (Command and Control Server/C2) Nedir?” yazımızı inceleyebilirsiniz.

**C2 Saldırılarında Kullanılan Modeller**

C2 saldırılarında virüslü sitemlere komut göndermek için kullanılan çeşitli modeller vardır. Farklı komuta yöntemleri kullanılmasın ardındaki neden, komutların geldiği yerin tespit edilmesini zorlaştırmaktır.

**Merkezi Model:** Merkezi model istemci-sunucu işlem modeline oldukça benzerdir. Bu yöntemde virüs bulaşmış ana bilgisayar, yürütülecek işlemlerle ilgili komutlar talep etmek için C2 sunucusunu sorgulayabilir.

Bu modelin algılanması ve engellenmesi genellikle kolaydır, çünkü komutlar hızlı bir şekilde algılanabilen ve engellenebilen IP'ye sahip tek bir kaynaktan gelir. Ancak bazı saldırganlar, C2 sunucu kurulumlarında proxy’ler, yönlendiriciler ve yük dengeleyiciler kullanarak algılama işlemini zorlaştırır.

**Eşler Arası (peer-to-peer/P2P) Model:** Eşler Arası Model, botnet üyelerinin bir düğümden diğerine mesaj ilettiği merkezi olmayan bir yapıyı benimser. Merkezi bir sunucu bulunmadığından düğümleri tespit nispeten zordur.

Düğümler tespit edilse dahi tek seferde yalnızca bir düğüm etkisiz hale getirilebilir. Bu model genellikle merkezi modelle birlikte karışık şekilde kullanılır. Bu karma senaryoda, P2P iletişimi, merkezi sunucu kapatıldığında geri dönüşe ve kaybedilen cihazları/sistemleri tekrar ele geçirmeye imkân tanır.

**Randomize Model:** Randomize Model siber güvenlik uzmanlarının bir botnet'in komuta zincirini tespit edememesini veya C2 sunucusunu izleyip kapatamamasını sağlamak için geliştirilmiştir. Takibi zorlaştırma işlemi, virüs bulaşmış ana bilgisayara veya botnet'e rastgele kaynaklardan komutlar gönderilerek gerçekleştirilir. Bu kaynaklar sosyal medya yorumları, içerik dağıtım ağları (CDN’ler), Gmail, internet aktarımlı sohbet (IRC) odaları ve daha birçok ortamdaki bağlantılar olabilir. Saldırganların bu kaynaklarda aradığı ortak özelliklerden bazıları, insanların çoğunlukla onlara güvenmesi ve sık kullanmasıdır.

**C&C Sunucuları Kurbanları Sömürmek İçin Nasıl Kullanılır?**

**Veri Hırsızlığı:** C2 kanalının yaygın kullanım amaçlarında biri veri hırsızlığıdır. Saldırganlar, oluşturulan arka kapıyı kullanarak bir kuruluşun sisteminden kritik verileri toplayabilirler. Çalınan veriler finansal kayıtlar, ticari sırlar, kullanıcı verileri olabileceği gibi darkweb’de yüksek meblağlara satılabilecek daha detaylı ve gizli veriler de olabilir.

**Devam Eden İşlemleri Sekteye Uğratma:** Saldırganlar, önemli bir görev devam ederken virüslü sistem aracılığıyla bu görevi diledikleri gibi durdurabilir veya kendi istedikleri biçimde yeniden başlatabilirler. Örneğin muhtemel kayıplara karşı tüm verilerini yedekleyen bir şirketteki yedekleme işlemi, düzenli yeniden başlatmalarla asla bitmeyecek bir hale getirilebilir.

**Sistemleri veya Ağları Kapatma:** Kötü amaçları yazılımın bir kuruluş içindeki sistemlerin bazı bölümlerinde veya tamamında geçiş yapabildiği durumlarda saldırganlar iş operasyonlarını sonlandırmak için tüm sistemi kapatabilir. Saldırganlar, şirket yöneticilerini talepleri karşılanana kadar sistemi kapalı tutmakla tehdit edebilir. Bu yöntem, şifrelemeye ihtiyaç duyulmayan fidye saldırılarından biridir.

**DDoS (Dağıtık Hizmet Engelleme) Saldırıları:** Bazen virüslü sistemler asıl hedef değildir ve yalnızca farklı bir kuruluşa veya hizmete saldırı başlatmak için piyon olarak kullanılırlar. Saldırganlar, C2 sunucusu üzerinden zombi sistemlere bir hedefin hizmet kapasitesini tüketecek ve hizmet veren sunucuyu işlevsiz hale getirecek komutlar verebilirler.

**Verileri Şifreleme veya Tahrip Etme:** C2 sunucularının kurban bilgisayarlara zarar vermek için gerçekleştirebileceği etkinliklerden bir diğeri de verileri şifrelemek veya kullanılamaz hale getirmektir. Bu işlemler, veriler yayınlanmadan önce fidye istemek veya bir kuruluşun faaliyetlerini sabote etmek için kullanılabilir.

Yukarıdakiler, bir C2 sunucusu aracılığıyla gerçekleştirilebilecek yaygın saldırılara yalnızca birkaç örnektir. C2 kanalları, virüslü bilgisayara veya ağa açılan bir arka kapıdır ve hasar potansiyelleri yalnızca saldırganın hayal gücüyle sınırlıdır.

**C&C Saldırıları Nasıl Algılanır ve Önlenir**

**Tüm Trafiği Tarayın ve Filtreleyin:** Tarama ve filtreleme işlemi, bir kuruluşun C2 saldırılarını tespit etmek ve önlemek için alması gereken önlemlerin başında gelmektedir. Ağ trafiğinin yetkisiz şekilde şifrelenmesi (DNS tünelleme işlemlerinde yaygın olarak kullanılır), tanınmayan sunucularla veri transferlerinin gerçekleştirilmesi vb. şüpheli etkinlikleri tespit etmek için hem gelen hem de giden trafiğin izlenmesi gerekir.

**Sisteme Yüklenecek Her Tür Uygulama İçin Yönetici Onayını Zorunlu Kılın:** C2 saldırılarından korunmak için bilgisayarınız yalnızca belirli uygulamaların yüklenmesi için değil, kaynağı bilinmeyen her uygulama için yöneticiden onay talep etmesi gerekmektedir. Bu sayede tehdit aktörlerine hizmet eden uygulamaların yüklenmesi zorlaşacak ve sisteminiz daha güvenli hale gelecektir.

Virüs bulaşmış ana bilgisayarları ağdaki diğer ana bilgisayarlardan ayırın: Virüs bulaşmış bir bilgisayar algılandığında, onu diğer ana bilgisayarlardan ayırmak için hemen ağdan kaldırın. Bu, kötü amaçlı yazılımın dönmesini ve ağın kontrolünü ele geçirmesini önler.

**Sisteminizi Antivirüs Yazılımlarıyla Sürekli Tarayın:** Kötü amaçlı yazılımların algılanıp kaldırıldığından emin olmak için, güvenirliği test edilmiş virüsten koruma yazılımı kullanarak sistemlerinizi sürekli tarayabilirsiniz. Bu şekilde, C2 sunucularıyla iletişimde kullanılan kötü amaçlı yazılımlar kaldırılır ve gizli kanal sonlandırılır.

**Sonuç**

C&C saldırıları, saldırganların kötü niyetli faaliyetlerin engellenmelerini ve kuruluşların hasarları azaltmaları önlemek için gizli bir şekilde gerçekleştirilir. Bu nedenle, saldırı sonrasındaki iyileştirici çözümler kullanmak yerine saldırı öncesinde tedbirler almak çok daha önemlidir.

Kaynaklar:

- https://medium.com/dnsfilterofficial/how-a-c2-server-is-leveraged-in-a-botnet-command-and-control-attack-42d03da1e5f5

---
**[İsmail Başaran](https://www.linkedin.com/in/ismail-ba%C5%9Faran-063000256/)**