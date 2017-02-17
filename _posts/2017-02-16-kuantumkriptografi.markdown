---
layout: post
title: Genel Hatlarıyla Kriptografi ve Kuantum Kriptografiye Giriş
date: '2017-02-16 22:40:07 +0300'
categories: blog
---

Kriptoloji; kriptografi ve kripto analiz olmak üzere ikiye ayrılır. Kriptografi uygulamalarının ana amacı, gerçekleşen haberleşmenin gizliliğini ve güvenliğini üçüncü kişilere(saldırganlara) karşı korumaktır. Kripto analiz ise, kriptografik algoritmaların analizlerini yapan bilim dalıdır.  
  
Kriptolojinin temel amaçları:  
1) Gizlilik  
2) Bütünlük  
3) Kimlik Denetimi  
4) İnkar edememe  
  
Bu terimleri biraz daha açacak olursak,  
  
**Gizlilik**  
Bilgi istenmeyen kişiler tarafından anlaşılmamalıdır.  
**Bütünlülük**  
Bir bağlantının tamam ya da tek bir veri parçası için , mesajın gönderildiği gibi
olduğu , üzerinde hiç bir değişiklik yapılmadığının garantisidir.  
**Kimlik Denetimi**  
İletimi gerçekleştirilen bir mesajın göndericisinin gerçekten gönderen kişi
olduğu garantisidir.  
**İnkar edememe**  
İletilen mesajının inkar edilememesidir.  
  
  
Klasik Kriptoloma Yöntemleri      
---  
0x00 - Sezar Kripto Algoritması  
0x01 - Afin Kripto Algoritması  
0x02 - Vigenere Kripto Algoritması  
0x03 - RSA Kripto Algoritması  
0x04 - ElGamal Kripto Algoritması  
  
Bu algoritmalara kısaca örnekler ile değinmek istiyorum. Yazının sıkıcı olmaması
adına cebirsel ifadelerden olabildiğince kaçınacağım.  
  
**0x00 - Sezar Kripto Algoritması (Ceasar Cipher)** 
Kısaca yer değiştirme algoritmasıdır.

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/1.png)  
  
Yukarıdaki şekilde de görüleceği üzere her harf, alfabede kendisinden 3 sonraki
harf ile yer değiştirmektedir. Örnek olarak:  
  
AnkaraUniversity kelimesi 3 harflik dönüşüme uğradığında alacağı değer
DqndudXqlyhuvlwb olacaktır. Aynı işlem tersine de çalıştırılabilir. Yeni oluşan
stringdeki her karakter, alfabede kendisinden 3 önceki karakter ile yer
değiştirdiğinde asıl metin tekrar elde edilebilir. Çift yönlü bir algoritmadır.  
  
**0x01 - Afin Kripto Algoritması (Affine Cipher)**  
(Not : A hep 0 olarak kabul edilmektedir.)  

![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/2.png)  
  
c=ap+b (mod m), 1<=a<=m, 1<=b>=m  
p=a^-1(c-b)(mod m)  
Ax=1 (mod m)  
  
Örnek ile açıklamak gerekirse,  
‘AnkaraUniversity’  
burada a=5 b=7 di seçilmiştir.  
‘HufhohDuvibotvyx ’  
  
**0x02 - Vigenere Kripto Algoritması (Vigenére Cipher)**  
Bu şifreleme sisteminde bir tane şifrelenecek metinimiz ve şifreleme için
kullanacağımız key olmalıdır.  
  
![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/3.png)  
  
Burada yapılan işlem şifrelenmesi istenen metinimizdeki sırasıyla her harfin
tablodaki sayısal değerinin üzerine, sırasıyla keydeki her harfin karşılığı olan
sayının eklemesi ve elde edilen son değere karşılık gelen harf yine tablodan
seçilerek dönüşüm sağlanacaktır.  
  
Örnek olarak,    
***Şifrelenecek metin***  
AnkaraUniversity  
***Key***  
AUCC  
  
metindeki ilk harfimiz A=0 ‘dır. Keydeki ilk harfimiz de A=0 ‘dır bu yüzden ilk
şifrelenmiş harfimiz A olacaktır. Devam edelim, metindeki 2. Harfimiz ve ona
karşılık gelen sayısal değer N=13’dür. Keyimizdeki 2. Harfimiz ve ona karşılık
gelen sayısal değer ise U=20 ‘dir. N harfine karşılık gelen sayısal değerin
üzerine 20 (U) eklememiz gerekiyor. Bu işlem sonucunda elde edilen değer 33
olacaktır. Alfabemiz [0,25] aralığında olduğundan ötürü mod(26) işlemine
alınan 33 değerinin sonucu sayısal olarak 7, harf karşılığı da H harfidir. Aynı
yöntem ile şifrelenmesi istenen metindeki her harf sırası ile keyimizde bulunan
harflerle aynı işleme sokularak elde edilen sonuçlar doğrultusunda yeni
değerler elde edilir. İşlemin nihai sonucunda elde edilecek metin şu olacaktır:
‘ahmcruwpipgtscva’  
  
“Key 4 harfli, şifrelenmesi istenen metin 16 harfli; 4 harf sonra ne yapıyoruz key
bitti hoca!” diyen arkadaşlar için, keyimizi şifrelenmesi istenen metinle
işlemimiz bitene kadar tekrarlıyoruz.  
  
AnkaraUniversity  
AUCCAUCC...  
Olarak devam ediyor.  
  
**0x03 - RSA Kripto Algoritması (RSA Algorithm)**  
Çalışma mantığı olarak çarpanlara ayırma işleminin zorluğunu temel alır.
Şifreleme ve elektronik imza uygulamalarında kullanılmaktadır. RSA algoritması
anahtar üretimi, şifreleme ve şifre çözme olmak üzere 3 basamaktan
oluşmaktadır.  
  
Rsa nın anahtar oluşturma algoritma işlemleri sırasıyla :  
1- P ve Q olmak üzere çok büyük iki asal sayı belirlenir.  
2- Bu iki asal sayının çarpımı N=P*Q ve bu f(N)=(P-1)(Q-1) hesaplanır.  
3- 1 den büyük f(N)’den küçük f(N) ile aralarında asal bir E tamsayısı seçilir.  
4- E sayısının mod f(N)’de tersi alınır, sonuç D gibi bir tamsayı olur.  
5- E ve N tamsayıları genel anahtarı, D ve N tamsayıları ise özel anahtarı
oluşturur.  
  
Örnek vermek gerekirse,  
P=53 ve Q=59 sayılarımız olsun. Ayrıca küçük bir sayıya ihtiyacımız var.  
Tam sayı için; 1<e< n e=3 olsun.  
     
P*Q=n → 53*59=31272  
  
1. Adım - Private Key Oluşturma  
f(n)=(P-1)(Q-1)  
f(n)=(53-1)(59-1)  
f(n)=3016  
  
2. Adım - Şimdi Private Key hesaplayalım =d  
d=2(f(n))+1/ e;  
2011=(2*(3016)+1)/3;  
  
3. Adım - Public Keyimiz ile Şifremizi Çözelim  
Bildiklerimiz : public için n,e,3127,3;  
Private için d=2011;  
c=89^e mod n  
1394=89^3 mod 3127  
  
4. Adım - Private Key ile Verimizi Çözelim  
c= encrypted data  
d=private key  
n=public key  
  
Decrypted Data = c^d mod n  
89=1394^2011 mod 3127  
8=H 9=I “HI”;   
  
Klasik Bilgisayarlarda Kullanılan Mantık Kapıları   
---  
**NOT**  
Girişindeki mantıksal değeri tersine çevirir. Girişteki işaretin lojik 1 seviyesinde
olması durumunda çıkış lojik 0 seviyesinde; lojik 0 seviyesinde olması
durumunda ise çıkış lojik 1 seviyesinde olur. Tek bitlik bir kapıdır.  
  
**AND**  
2 bitlik bir kapıdır. Giriş değerlerinin çarpımını alır ve sadece girilen iki değerde
1 olduğunda 1 sonucunu verir.  
  
**OR**  
Girilen 2 ya da daha çok değerin toplamını alan kapıdır. Girilen değerlerden biri
1 olduğunda 1 sonucunu verir.  
  
**NAND**  
Girilen değerlerin çarpımını alıp sonucun tersini çıktı olarak veren kapıdır. Bu
anlamda AND kapısını tersidir. Sadece girilen iki değerde 1 olduğunda 0
değerini verir.  
  
**NOR**  
Girilen iki ya da daha fazla değerin toplamını alıp tersini çıktı olarak veren
kapıdır. Bu anlamda OR kapısının tersidir. Sadece girilen tüm değerler 0
olduğunda 1 sonucunu verir.  
  
**XOR**  
Girişteki değerler farklı olduğunda 1 sonucu verir. Geriye kalan her durumda 0
sonucunu verecektir.  
  
**XNOR**  
Girişteki değerler aynı olduğunda 1 sonucunu verir bunun dışındaki her
durumda 0 sonucunu verecektir.    
&nbsp; &nbsp; &nbsp; &nbsp;     
  
Yazının bu kısmına kadar kriptografi ile ilgili bilinen terimlerin üzerinden geçmek
istedim ve bilindiği üzere şu ana kadar çözülemeyen şifreleme algoritması
bulunmamaktadır.  
Peki durum gerçekten böyle mi? Bu kısmı biraz soru-cevap şeklinde ilerletmek
niyetindeyim.  
   
**Kuantum nedir?**  
En temel tanımı ile kuantum; mikro dünyadaki atomları ve atom-altı
parçacıkların davranışlarını açıklamayı amaçlayan doğrulanmış bir fizik
kuramıdır.  
  
**Kuantum bilgisayar nedir?**  
Klasik bir bilgisayar tüm işlemlerini 1 ve 0 değerini alabilen klasik bit ‘lerle yapar.
Kuantum bilgisayarlar ise kuantum bitlerini yani q-bit ‘leri kullanırlar. Bunlar
aynı anda hem 1 hem de 0 değerini alabilirler. Kuantum bilgisayarlar işlem
gücünü bu q-bit ‘lerden alırlar. Q-bit olarak kullanılabilecek bir dizi fiziksel nesne
vardır; bunlar foton, atom çekirdeği veya elektron olabilir.  
  
**Kuantum kriptografi neyi ifade ediyor?**  
Kuantum kriptografide temel prensip; tek kullanımlık anahtarlı kriptografi tekniğinin kullanılmasıdır.
Kuantum kriptografiyi diğer kriptografi
sistemlerinden farklı kılan şey güvenli ve devamlı anahtar dağıtımının
garantilenmesidir. Kuantum anahtar dağıtımında optik hat Heisenberg
belirsizlik kuramından faydalanılarak dinlenilmesi imkansız kılınır ve normal
yollardan gönderilecek verilerin kodlanmasında kullanılacak şifre anahtarları bu
optik hat üzerinden iletilir. Bu sayede en gizli seviyedeki bilgiler kırılması
imkansız şekilde kriptolanarak rahatça her türlü iletişim hattından gönderilir.  
  
  
KUANTUM MANTIK KAPILARI    
---
**Hadamard kapısı**  
Tek kübitin |0 > ve |1 > durumlarını dolanık hale getirmek için kullanır.  
  
Hadamard kapısının matrisi :  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/4.png)  

**Pauli-X kapısı**  
Klasik kapılardaki , değil kapısının kuantum halidir. Girişi tersine döndüren
kapıdır.  
  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/5.png)  

**Pauli-Y kapısı**  
Tek kübitlik bir kapıdır.Gösterimi Y ‘dir. Y ekseni üzerinde döndürme işlemi yapılır.  
  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |0 >→ i|1 > |1 >→ −i|0 >  
  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/6.png)  

**Pauli-Z kapısı**  
Tek kübitlik kapıdır. Gösterimi Z’dir. Z ekseni üzerinde döndürme işlemi
yapar.  
  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; |0 >→ |0 > |1 >→ −|1 >  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/7.png)  
  
**Faz Kaydırma Kapısı**  
Bu kapının özelliği ,0, 01 ve 10 için değişiklik yapmamak ama 11 durumu için
|1> girdisinin ei Θ |1> girdisine dönüştürmesidir. Yani |1> için, Θ derece
döndürme işlemi yapılmaktadır.  
  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/8.png)  
  
**Swap Kapısı**  
İki kübitlik bir kapıdır. Giren iki kübitin değerlerini birbirleriyle değiştirir.  
  
**Kontrol Kapıları**  
2 ,3 kübitlik kapılardır. Kendi aralarında alt dallara ayrılırlar.  
(CNOT,CSWAP ,CCNOT gibi ) Her birinin farklı işleyişi vardır.  
  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/9.png)  
  
**Asimetrik Sistem**   
Göndericinin ve alıcının farklı anahtarlar kullandığı kriptosistemlere, asimetrik
veya açık anahtarlı sistemler denir.  
  
**Simetrik Sistemler**  
Simetrik kriptosistemlerde yani gizli anahtarlı kripto sistemlerde hem şifreleme
hemde şifre çözme için aynı anahtar kullanılır.  
  
**BB84 protokolü**  
BB84, Charless Bennet ve Gilles Brassard tarafından 1984 yıllında geliştrilen
bir kuantum anahtar dağıtımı yöntemidir. İlk kuantum kriptografi yöntemidir.Bu
protokol kuantum parçalarının birbirine dik olmamasına dayanan bir güvenliğe
sahiptir.BB84 protokol un un mantığını spini ( 1/2) olan parçacıklar ile
örneklendirebiliriz.Spin ya +(1/2) ya da -(1/2) olacaktır.Bu protokolü uygularken
farklı iki yön yani bize dört farklı kubit durumu verir.  
  
![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/10.png)  

1-![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/11.png)  
   
2-![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/12.png)  
  
3-![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/13.png)  
  
4-![]({{ AUCyberClub.github.io }}/assets/img/kuantumkriptografi/14.png)   
  
ai ve bi ,a ve b nin i numaralı bitleridir.  
  
İletişimde fiber optik kablo kullanıldığı varsayılmaktadır.  
  
Uygulama sırasında, şifreleme için kullanılacak bir anahtar elde etmek icin
gönderici farklı iki bazdan herhangi birinde hazırlanmıs bir kubiti (kuantum biti)
alıcıya gönderir. Fakat bilginin hangi bazda hazırlandığını gizli tutar. Alıcı ise
bazlardan birini seçer ve ölçüm yapar. Eğer aynı bazı kullanırlarsa alıcı ve
gönderici sonuçlar uyumlu olacaktır. Farklı bazları kullanmışlarsa veriler
silinecektir.  

**Sonuç olarak**  
Gizli bilgileri ele geçirmeye çalışan birisinin önce araya giriği daha sonra alıcıya
elde ettiği sonuçlara uygun bilgiler gönderdiği durumda neler olabileceğini
inceleyecek olursak;  
Eğer dinleyici doğru bazı kullanırsa , alıcının kübite yüklediği bilgiyi doğru olarak
öğrenecek ve bu doğru bilgiyi alıcıya da gönderecektir.Fakat bu
imkansızdır.Binlerce kübitten oluşan bir anahtardaki tüm bitleri şans eseri doğru
bazda ölçmek gerçekten imkansız bir durum gibi görünüyor.  
   
---  
**[Kaan Ezder](https://github.com/kezder)**  
*Aynı konu ile ilgili daha önce yazmış olduğu yazıyı [şuradan](https://canyoupwn.me/tr-quantum-cryptography/) okuyabilirsiniz.*



















