---
layout: post
title: Mr-Robot 1  Walkthrough
date: '2017-04-13 14:50:00 +0300'
categories: cozumler
--- 

Bu yazıda [VulnHub](https://www.vulnhub.com/entry/mr-robot-1,151/) üzerinde yayınlanan zafiyetli sanal makinelerden biri olan **Mr-Robot:1** makinesinin tam çözümünü inceleyeceğiz. Makinede toplamda 3 adet flag bulunuyor ve maalesef VM'in herhangi bir hikayesi de yok.

Klasik olarak çözüme bir nmap taraması yaparak başladım.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/1.png)


Açık olan tek port HTTP olarak döndü. Biraz website üzerinde dolandıktan sonra işime yarayabilecek hiçbir şey bulamayınca **nikto** ile tarama yapmaya karar verdim.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/2.png)

Dikkatimi çeken 4 sonuç oldu. İlk olarak **robots.txt** dizinindeki bilgileri göz attım.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/3.png)

İlk key'imiz ve bir adet wordlist.  
**/readme.html** ve **/license.txt** kısımlarında faydalı bir bilgi bulamadım.  
Robots.txt dizinindeki wordlisti gördükten sonra olaylar kafamda şekillenmeye başladı. Elimde bir wordpress sitesi ve bir wordlist var. Yapmam gereken şey **brute force** ile panele giriş yapmaktı.  
Fakat bunun için wordliste ek olarak bir de username bilgisine ihtiyacım vardı. **Wpscan** ile site üzerindeki usernameleri tespit etmeye çalıştım.  

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/4.png)

Maalesef sonuç beklediğim gibi olmadı. İş başa düştü diyerek, login page'ine girdim. Makinenin isminden dolayı ilk olarak **mrrobot** kullanıcı ismi ile giriş yapmayı denedim.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/5.png)

**Invalid Username** hatası döndü. Yani eğer doğru bir username bulursam **Invalid Password** gibi bir hata dönecekti bu durumda bruteforce yapabilirdim. Makinenin esinlendiği diziyi takip etmediğim için Google'da diziyle ilgili biraz araştırma yaptım, ana karakterin isminin **elliot** olduğunu öğrendim ve username olarak **elliot** denediğimde ;

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/6.png)

Bana beklediğim sonucu döndü (aslında bu kadar kolay olmasını beklemiyordum). Önceki username'i çok kolay bulmamdan yakındığımdan olacak ki **wpscan** ile bruteforce işlemini başlattığımda uzunca bir süre beklemem gerekti.

**wpscan --url targetip --wordlist fsociety.dic --username elliot**

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/7.png)

Sabrın zaferi diyerek password bilgisini de elde ettim.  
Şimdi yapmam gereken şey, siteye bir shell yüklemekti. Panel üzerinde biraz gezindikten sonra php kodlarını yapıştırabileceğim bir yer buldum.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/8.png)

Buraya gerekli php kodlarını yapıştırıp kaydedersem, sitede bulunmayan bir dizine girmeye çalıştığımda otomatik olarak kodlar execute edilecek ve site üzerinde oturum açabilecektim.
**msfvenom** ile bir php dosyası oluşturdum.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/9.png)

Php dosyasını **leafpad** ile açıp içindekileri kopyaladım ve panelde bulduğum yere yapıştırdım.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/10.png)

Msfconsole'u açıp dinlemeye başladım.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/11.png)

Sitede bulunmayan bir dizine girmeye çalıştığımda gerekli sinyaller geldi.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/12.png)

Meterpreter'e pek aşina olmadığım için shell oturumuna geçtim.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/13.png)

Biraz içeride dolandıkdan sonra **home** dizinin altında ikinci key'i ve bir hash buldum.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/14.png)

Başta key'i okumaya çalıştığımda permission denied verdi. Ben de hash'e yöneldim.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/15.png)

Online bir decoder ile passwordu decode ettikten sonra robot kullanıcısı olarak yetkilerimi değiştirdim.

**su robot**

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/16.png)

Artık ikinci key'i de okuyabiliyordum ama hala **root** olabilmiş değildim. Bu yetki ile ulaşabileceklerimi görmek için ufak bir tarama yaptım
**find / -perm /6000**


![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/17.png)

Tarama sonuçlarını incelerken alışılmadık bir şey gözüme çarptı. **NMAP** default olarak gelmeyen bir uygulamaydı, yani buraya dikkat etmemiz için koyulmuştu. Bir şekilde root yetkisi elde edeceksem bu uygulama üzerinden etmem gerekiyordu.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/18.png))

Biraz Google'da arama yaptıktan sonra nmap'in 3.8 ve 4.0 sürümlerinde uygulamayı yetkiden bağımsız olmaksızın herkesin root olarak çalıştırabildiğini öğrendim. **--interactive**  parametresini kullanarak istediğimiz komutları **root** olarak çalıştırabiliyorduk.

![]({{ AUCyberClub.github.io }}/assets/img/mrrobot/19.png)

Bu özellikten faydalanarak **/root** dizini altındaki son keyi okuyabildim.

---
**[Engin Demirbilek](https://twitter.com/Hyal0id)**
---
