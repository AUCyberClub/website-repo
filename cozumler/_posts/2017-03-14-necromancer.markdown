---
layout: post
title: The Necromancer:1 Walkthrough
date: '2017-03-14 15:00:00 +0300'
categories: cozumler
---  

Merhabalar,   
Bu yazıda oldukça keyif alarak yaptığım **The Necromancer: 1** sanal makinesinin tam çözümünü inceleyeceğiz.  
Sanal makine hakkında ayrıntılı bilgi için [şurayı](https://www.vulnhub.com/entry/the-necromancer-1,154/) ziyaret edebilirsiniz.  
Makinede toplam 11 adet flag bulunuyor. Flaglerden bazıları hikayeyi devamı için gerekli, bazıları ise random sayılar. Bu yüzden gereksiz flagler üzerinde çok durmadan hikayeyi ilerletmeye çalıştım. Daha keyifli bir okuma için lütfen fotoğraflarda ki hikaye parçalarını da okuyun.
İlk olarak hedef makinenin IP adresini bulmak için nmap taraması yaptım.


![]({{ AUCyberClub.github.io }}/assets/img/necro/1.png)


Adresi buluyoruz bulmasına ama port sonuçları **filtered** dönüyor.Belki bakmamız gereken yer daha yüksek numaralı portlar ya da **TCP** portları değildir de **UDP** portlarıdır diyerek kapsamlı bir tarama yaptım.

 ```
 nmap -n -sT 192.168.102 -p1-65535  --open
 ```  
 
 ```
 nmap -n -sU 192.168.1.102 -p1-65535 --open
 ```

Ama maalesef sonuç yine hüsran.Bir kahve molası verip acaba ağ yapılandırmasında mı sorun var  diye içimden geçirirken bu taraflarla pek ilgisi olmayan, tıp fakültesi öğrencisi bir arkadaşıma
"Elimde bağlanmam/incelemem ve/veya bir şeyler göndermem gereken bir port var ama ne tarama yaptıysam bunu göremedim , aklına herhangi bir şey geliyor mu?" diye sordum
ve aldığım cevap dahiceydi !
"Belki oda sana bağlanmaya yada bir şey göndermeye çalışıyordur ? Bunları izlemek için bir toolunuz yok mu? "
Brilliant arkadaşımdan aldığım ipucu ile  soluğu **wireshark**'da aldım.
Biraz ağı dinledikden sonra gözüme bir şey çarpıyor **4444** numaralı Port ,Bingo !


![]({{ AUCyberClub.github.io }}/assets/img/necro/3.png)


Hemen **netcat** ile 4444 portunu dinlemeye başlıyorum


![]({{ AUCyberClub.github.io }}/assets/img/necro/4.png)

Ve ilk bilgimiz geliyor, bu mesaj **base64**'e benziyor. Online bir decoder ile  decode ediyorum ve hikayemiz burada başlıyor.


![]({{ AUCyberClub.github.io }}/assets/img/necro/5.png)


Ilk flag'i bulmanın ve hikayenin rehavetiyle ilk başta alttaki **u666** bilgisini gözden kaçırıyorum ama flag i decode ettikten sonra adeta burdayım gör beni diye parlıyor.
 
**Flag 1 =  opensesame**

Netcat ile 666 numaralı UDP portuna bağlandım.Başta herhangi bir şey olmasa da ilk flag'i gönderdiğimde hikayemiz kaldığı yerden devam ediyor.


![]({{ AUCyberClub.github.io }}/assets/img/necro/6.png)


Yeni bir flag ve bir ipucu! **Numeral 80** ibaresinden acaba 80 numaralı port mu açıldı diye düşünüyorum ve nmap ile tarama yaptığımda


![]({{ AUCyberClub.github.io }}/assets/img/necro/7.png)


**HTTP(80)** portunun açıldığını gördüm.

Siteye bağlandığımda heyecanlı hikayemiz devam ediyor 


![]({{ AUCyberClub.github.io }}/assets/img/necro/8.png)


![]({{ AUCyberClub.github.io }}/assets/img/necro/9.png)


Hikayenin dışında sitedeki resim dikkatimi çekti. Daha önce karşılaştığım durumlardan edindiğim tecrübeler doğrultusunda hemen resmi indirip içine herhangi bir bilgi gizlenmiş mi araştırmaya başladım.
Binwalk komutuyla içine baktığımda mini mini bir zip bana gülümsüyordu.

![]({{ AUCyberClub.github.io }}/assets/img/necro/10.png)


![]({{ AUCyberClub.github.io }}/assets/img/necro/11.png)


Yine base64 ile encode edilmiş bir mesaj . Decode ettiğimde ise beni bir flag ve bir dizin ismi karşıladı.


![]({{ AUCyberClub.github.io }}/assets/img/necro/12.png)


Dizine gittiğimde hikayenin devamına ulaştığımı gördüm.

![]({{ AUCyberClub.github.io }}/assets/img/necro/13.png)

Hikayeye ek olarak yine bir resim dosyası gözüme çarptı. Ilk resmin içindeki bilgiyi
kolayca çıkarabilmiş olmanın verdiği özgüvenle resmi indirip incelemeye başlıyorum. Fakat ne  denediysem içinden herhangi bir bilgi çıkmadı (binwalk,steghide,hexeditor,strings). Başka bir çarem kalmadığından umutsuzca source kodu açıp incelemeye başladım.


![]({{ AUCyberClub.github.io }}/assets/img/necro/14.png)


Direkt olarak bana bir bilgi vermese de source koddaki **../pics** ibaresinden ilham alarak belki bulmam gereken bir dizin vardır diye düşündüm ve bir kahve molası verip brute force'u başlattım.



![]({{ AUCyberClub.github.io }}/assets/img/necro/15.png)


Tam "bu sabaha kadar sürer ohoooo bari kitap okuyayım derken" **talisman** isimli bir dizin bulundu.Brute force devam ederken dizine bir göz atayım diyorum ve dizine gider gitmez **talisman** isim bir program iniyor.
Daha programı incelemeden köşe bucak öğrenmekten kaçındığım reverse-engineering konusunun şuan karşıma çıkacağını sezdim.Belki gerek yoktur çalışır diyerek programı çalıştırmayı denedim.

![]({{ AUCyberClub.github.io }}/assets/img/necro/16.png)

Ve tabiki girdiğim inputtan bağımsız olarak ne girersem gireyim bana **Nothing Happens** döndürdü.
Teorik olarak ne yapmam gerektiğini aslında biliyordum. Programın içinde çalıştırılmayan bazı fonksiyon/fonksiyonlar var ve bunları bulup çalıştırmam gerek.Nasıl yapacağım konusunda herhangi bir fikrim yoktu ben de  yardım aramaya başladım ve sınıf arkadaşım **[Tevfik](https://twitter.com/tsdorgut)** imdadıma yetişti. Aldığım ipucu ile  **objdump** kullanarak programı incelemeye başladım.

![]({{ AUCyberClub.github.io }}/assets/img/necro/17.png)

Ilk gözüme çarpan şey **wearTalisman** dışında tuhaf isimli bir fonksiyon daha olmasıydı **chantToBreakSpell**. Isminden yola çıkarak çalıştırmam gereken fonksiyonun bu olduğuna karar kıldım.

GDB ile programı çalıştırıp bana herhangi işe yarar bir sonuç dönmeyen **wearTalisman** fonksiyonuna bir breakpoint koydum. Tekrar run  işlemler breakpoint noktasına gelincede **jump** komutuyla **chantToBreakSpell** fonksiyonuna atladım ve hikayenin devamına ulaştım.

![]({{ AUCyberClub.github.io }}/assets/img/necro/18.png)

Flag'i decode ettiğimde **blackmagic** sonucunu buldum. Ayrıca **Chant these words at u31337** ipucundan yola çıkarak netcat ile **31337** numaralı **UDP** portuna baglanmaya calıştım.

**echo blackmagic | nc -u 192.168.1.2 31337**

![]({{ AUCyberClub.github.io }}/assets/img/necro/19.png)

Bağlandım bağlanmasına ama uzun süredır pc başında olmaktan ve hikayeye kendimi fazla kaptırdığımdan olacak yarasalar saldırıya geciyor kısmını okuduğumda refleks olarak terminali kapadım.Elimi yüzümü yıkayıp tekrar pc başına oturdukdan sonra sakin bir kafa ile tekrar porta bağladım. Saldırgan yarasalar dışında en altta beni iki önemli bilgi karşıladı. Ilkı bir dizin ikincisi ise bir flag. Hikayede bazı flagler sayı değerleri olarak verilmiş buda onlardan biri. Sayı değerindeki flaglere hikayeyi devam ettirmek için ihtiyacım yok.
Dizine gittim  ve sonunda hikayemizin kötü karakteri **Necromancer**'a ulaştım.


![]({{ AUCyberClub.github.io }}/assets/img/necro/20.png)


![]({{ AUCyberClub.github.io }}/assets/img/necro/21.png)


En alttaki **u161** ipucunun dışında **necromancer!** kısmının tıklanabilir olduğunu farkettim ve tıkladığımda **necromancer** isimli bir b2zip inmeye başladı. 
Dosyayı **bzip2 -d** komutuyla extract ettiğimde içinden bir tar dosyası onuda çıkardığımda içinden bir **pcap** dosyası çıktı.


![]({{ AUCyberClub.github.io }}/assets/img/necro/22.png)


Wireshark ile dosyayı biraz inceledim ve işime yarayabilecek bir **BSSID** bilgisi buldum.


![]({{ AUCyberClub.github.io }}/assets/img/necro/23.png)

Bu bilgiyi elde ettiğime göre içindeki şifreyi çıkartmak için **Aircrack** kullanabilirdim.Tam bruteforce'a bırakayım da artık kaç saat sürerse sürsün deyip işlemi başlattım ve daha 5 saniye geçmeden 

![]({{ AUCyberClub.github.io }}/assets/img/necro/24.png)

KEY FOUND !! **death2all**

Bulduğum keyle 161 numaralı UDP portuna girmeyi denedim.Ilk başta **echo death2all | nc -u 192.168.1.102 161** komutunu kullandım ama bana herhangi bir sonuç dönmedi.
Daha ayrıntılı bilgi için **-v(verbose)** parametresini ekledim yine beklediğim sonucu dönmedi ama **snmp** protokolüyle ilgili bir bilgi döndü.
 

![]({{ AUCyberClub.github.io }}/assets/img/necro/25.png)


Bu sonucu görür görmez bir kaç ay önce başka bir testte kullandığım **snmp_enum** axuiliary'si aklıma geldi ve hemen metasploit'i açtım.


![]({{ AUCyberClub.github.io }}/assets/img/necro/26.png)


Dönen sonuçta ilk dikkatimi çeken şey **Locked - death2allrw** oldu. Özellikle sondaki **rw** kısmından yola çıkarak **Locked** parametresini değiştirmem gerektiğini anladım.

![]({{ AUCyberClub.github.io }}/assets/img/necro/27.png)

Terminal üzerinden girdiğim birkaç komut ile **Locked** stringini **Unlocked** olarak değiştirdim ve tekrar kontrol ettiğimde bir flag ve bir ipucu geldi **t22**. Flag'i decode ettiğimde çıkan sonuç **demonslayer** oldu. **t22** ipucundan yola çıkarak acaba **ssh** portu mu açıldı diye kontrol ettim.


![]({{ AUCyberClub.github.io }}/assets/img/necro/28.png)


Ve evet port açıktı.Bu durumda **demonslayer**'i password olarak düşündüm ve porta bağlanmayı denedim.


![]({{ AUCyberClub.github.io }}/assets/img/necro/29.png)


Ama bu doğru password değildi.Bu durumda **demonslayer**'i username olarak kullanmaya karar verdim ve **hydra** ile bruteforce saldırısı yaptım.


![]({{ AUCyberClub.github.io }}/assets/img/necro/30.png)

Bulduğum password ile ssh portuna bağlandım ve kendimi necromancer'ın ininde buldum.

![]({{ AUCyberClub.github.io }}/assets/img/necro/31.png)

Bulunduğum dizindeki flag dosyasını açtım ve hikaye devam etti

![]({{ AUCyberClub.github.io }}/assets/img/necro/32.png)

Kendimizi savunmamız için 777 numaralı udp portuna bağlanmamızı istiyordu bir an gaza gelip yeni terminal açtım ve

![]({{ AUCyberClub.github.io }}/assets/img/necro/33.png)

Ikinci bir yarasa vakası yaşadım ve 5-10 dakika boyunca doğru kelimeyi girmeyi denedim.Yaklaşık 20-30 kelime sonra yanlış yerden bağlanmaya çalıştığımı
anladım ve ssh baglantısı üzerinde porta girmeyi akıl edebildim.

![]({{ AUCyberClub.github.io }}/assets/img/necro/34.png)

3 canım kalmıştı **necromancer** acımasızca saldırıyordu.Hemen soruyu google'da arattım ve çıkan cevabı girdim !

![]({{ AUCyberClub.github.io }}/assets/img/necro/35.png)

Ilk saldırıyı başarıyla dodgelamıştım.

Durmuyordu necro, atmaya devam ediyordu şeytani büyülerini

![]({{ AUCyberClub.github.io }}/assets/img/necro/36.png)

Ama yer mi anadolu çocuğu diyerek bir sağa bir sola ninja misali dodgeliyordum.

![]({{ AUCyberClub.github.io }}/assets/img/necro/37.png)

Son atağı dodgelediğimde , ayağım kaymış olucak ki bir anda gözüme flashbang atılmışcasına beyaz flashlar çaktı.
Bir kaç saniyelik geçiçi körlüğün ardından, **Necromancer**'e doğru bakmaya çalıştım ama tek görebildiğim şey kalın siyah bir toz tabakası oldu.
Daha sonra toz bulutu, ayağımın kayması sonucunda hayatta kalabilmesinin verdiği mutlulukla odadan echo yapan bir sesle gülerek kayboldu.
Sessizliğe bürünen odada, **Necromancer**'in daha önce durduğu yere doğru yavaşca yürüdüm yerde belli belirsiz kutumsu bir şey vardı.

![]({{ AUCyberClub.github.io }}/assets/img/necro/38.png)

![]({{ AUCyberClub.github.io }}/assets/img/necro/39.png)

İçini açtım ,  bu da neydi böyle adete **sihirli annem** dizisindeki Dudu'nun kazanından fırlamış yeşil bir iksir.
Ölmeden zor bela buraya kadar gelmiştim artık ne olursa olsun dedim ve iksiri kafaya dikledim ! Kendimi bir anda yüzlerce ml **anabolik steroid** almış gibi güçlü ve tuhaf hissettim.
Ne yani artık yeni **Necromancer** ben miydim ?

![]({{ AUCyberClub.github.io }}/assets/img/necro/40.png)


![]({{ AUCyberClub.github.io }}/assets/img/necro/41.png)

Ahh... Yine kendimi fazla kaptırmışım... 

---  
**[Engin Demirbilek](https://twitter.com/Hyal0id)**

