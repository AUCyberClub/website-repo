---
layout: post
title: SQL Injection to Shell Web Walkthrough
date: '2017-03-06 10:30:42 +0300'
categories: cozumler
---

Merhabalar,

Bu yazımda **[Pentesterlab](https://pentesterlab.com/exercises/from_sqli_to_shell)** tarafından hazırlanan **[SQLiToShell](https://pentesterlab.com/exercises/from_sqli_to_shell)** zafiyetli sanal makinesini inceleyeceğiz.
Gerçek hayata oldukça yakın hazırlanmış bu challenge'da bir web uygulama üzerindeki **SQL Injection**
zafiyetini istismar ederek hedef sistemde uzaktan kod çalıştırmayı deneyeceğiz.

İlk olarak verilen **ISO** dosyasını **VirtualBOX** sanallaştırma ortamı üzerinde canlandırıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/1.png)  


![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/2.png)  

Web uygulumanın dizinlerini incelediğimde, resimlerin görüntülendiği URL'ler dikkatimi cekiyor **php?id=1**.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/3.png)   

Site bize gerekli fotoğrafları göstermek için **Select * From photos WHERE id=1** gibi bir SQL sorugusu yapiyor.
Bu durumda SQL sorgusuna dışarıdan müdahele edebiliyor muyum görmek için URL'in sonuna bir meta karakter olan
**'** karakterini ekliyorum. Eğer müdahele edebiliyorsam koyduğum **'** karakteri SQL syntax'ını bozucak ve 
bize bir **syntax error** hatası döndürücek.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/4.png)  

Bingo!

Bu sonuç bize gösteriyor ki , bu SQL sorgusuna müdahele edebilir, değiştirebilir ve kendi amaçlarım doğrultusunda kullanabilirim.
Şu anda yapmamız gereken şey veritabanındaki **table** ve **column** isimlerini bulmak ve bunlardan gerekli
bilgileri çekmek.

İlk olarak uygulamada kaç adet **column** olduğunu öğrenmek için , **ORDER BY** sorgusunu kullanıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/5.png)  

İlk olarak 10 sayısını verdim ve bize bir hata döndü. Bu durumda sitede 10 dan daha az **column** var demektir.
Hatasız bir sonuç döndürene kadar sayıyı birer birer azaltıyorum ve sorguyu tekrar deniyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/6.png)  

Sayı 4'e indiğinde hata döndürmeyi bıraktı . Bu durumda sitede 4 column var diyebiliriz. Şimdi hangi columnun
zaafiyetli olduğu bulmak için **union select** sorgusunu kullanıyorum.


![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/7.png)  

``` 1,2,3,4 numaralarını girmemin sebebi 4 column olması```

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/8.png)  

Sorgunun ardından döndürdüğü 2 numarası, zafiyetli columnun 2 numaralı column olduğunu gösteriyor.

Verileri çekeceğimiz column numarasını bulduğumuza göre, artık başlayabiliriz.

Databasedeki **table** isimlerini görmek için **union select 1,concat(table_name),3,4 from information_schema.tables** sorgusunu kullanıyorum.

```Information_schema veritabanlarında default olarak bulunur ve veritabanının bir şeması olarak düşünülebilir.
    2 sayısının yerine concat yazmamın sebebi zaafiyetli column'un 2 numaralı column olması.```

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/9.png)  

Dönen bilgileri incelediğimde bir **users** table'ı görüyorum. Kullanıcı bilgilerini buradan çekeceğiz.

Eğer **column** isimlerinide bulabilirsek, işimiz bitmiş sayiliyor. Bunun içinde önceki yaptığım sorguya
benzer olarak **union select 1,concat(colum_name),3,4 from information_schema.columns** sorgusunu yapiyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/10.png)  

Dönen sonuçları incelediğimde **login** ve **password** column'unu buluyorum.
Şimdi tek yapmam gereken , **users** table'ı altındaki **login** ve **password** column'unu veritabanından çekmek.
Son olarak **union select 1,concat(login," ", password)** sorgusunu kullanıyorum ve veritabanından gerekli bilgileri çekiyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/11.png)  

**username = admin** ama **password** hashlenmiş geliyor. Google'a hash cracker yazarak çıkan ilk siteye giriyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/12.png)  

Ve password bilgisinide elde etmiş oluyoruz.

Buraya kadar yaptığım işlemleri her ne kadar basitleştirmeye çalışsam da manual olarak **SQL injection**
uygulamak oldukça zahmetli ve karışık olabilir.Bu yüzden böyle durumlarda karışıklığı azaltmak için **sqlmap** gibi toollar kullanılır.


Şimdi ayni bilgileri **sqlmap** kullanarak databaseden çekelim.

__SQLMAP To Shell__

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/13.png)  

```-u(url), -batch(herhangi bir soruya default cevap ver)```

Dönen sonuçlarda site üzerinde çalışan bir kaç SQL Injection payload'ı gösteriliyor. Yani, harici SQL sorgu komutları site üzerinde çalıştırabiliyor.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/14.png)  

 Şimdi veritabanlarını çekelim 

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/15.png)  

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/16.png)  

İşlem tamamlandığında iki adet veritabanı geliyor.**Information schema** ve **photoblog**.

**Photoblog** veritabanından gerekli bilgileri çekmek için elle yaptığım işlemlerin aynısını
sadece paremetreleri değiştirerek sırayla uyguluyorum;

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/17.png)  

Tabloları görmek için **--tables** parametresi.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/18.png)  

**Users** tablosundaki columnları görmek için **--column** parametresi.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/19.png)  


![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/20.png)  

Ve son olarak columnda ki **login** ve **password** bilgisini çekmek için **--dump** parametresi.  

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/21.png)  

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/22.png)  

Elle yaptığımıza oranla çok daha kısa sürede ve sadece bir kaç parametre değiştirerek aynı bilgiyi
veritabanından aldık.

Admin bilgilerini ele geçirdiğimize göre , şimdi ikinci görevimiz siteye bir **shell** dosyası yüklemek. 

``` 
shell kelimesi ile başka yerlerde de karşılaşabilirsiniz. Genel anlamı, hedef sistem üzerinde uzaktan sistem komutu çalıştırmanızı sağlayan erişim dosyalarıdır. 
```

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/23.png)  

Admin panelini biraz inceliyorum ve **add new picture** kısmını görüyorum.
Burdan siteye bir **shell** dosyası yüklemeyi denememiz gerekiyor.

Çok ufak bir kodlama ile kendimize bir **shell** dosyası oluşturabiliriz.  

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/24.png)  

Daha büyük shell dosyaları internette oldukça fazla bulunuyor ama burada bu dosyada işimizi görmeye yeter.

> BlackArch'ın [webshell'lerini](https://github.com/BlackArch/webshells) kullanabilirsiniz.

Eğer bu dosyayı siteye yükleyebilirsek, bize sitede bir komut satırı açmamızı sağlayacak.
Dosyayı yüklemeyi deniyorum ama **NO PHP** korumasıyla karşılaşıyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/25.png)  

Bir şekilde bu korumayı bypass edip bu dosyayı siteye yüklememiz gerekiyor.Bunun için bildigim bir kaç yöntem var ilk olarak **Tamper Data** kullanarak bypass etmeyi deniyorum.

Bir önceki yazımda Tamper Data'dan biraz bahsetmiştik. 

Dosyanın ismini **shell.php.jpg** olarak değiştiriyorum.Tabiki bu isimle siteye yükleyebilsem bile işime yaramaz.Ama bu isimle yüklerken gönderdiğim **POST** isteğini tekrar editleyip **jpg** kısmını silersem
belki korumayı bypass edebilirim.


![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/26.png)  


Fakat sonuç yine ;

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/25.png)  

Bu durumda deneyebileceğimiz bir kaç bypass yöntemi daha var. Bunlardan birisi dosyanın sonuna **.test** eklemek.Bu php dosyaları için oldukça basit bir bypass yöntemi, ismi her ne kadar **shell.php.test** olsada
eğer yükleyebilirsek, dosya hedef sunucu tarafından php olarak render edilecek.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/27.png)  

Bingo!

Dosyayı siteye yüklemeyi başardık , şimdi dosyamızı kullanmak için nereye yüklendiğini bulmamız gerekiyor.
Default olarak çoğu durumda kullanılan **uploads** dizinine bakiyorum (eğer sonuç dönmeseydi directory fuzzing işlemi yapacaktım)

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/28.png)  

ve dosyamız burda.
Dosyanın bize sağlaması gereken komut satırına ulaşmak için dosyanın üzerine tıklıyorum ve
komut satırını açmak için **?cmd=** komutunu kullanıyorum.
Test etmek için bir kaç komut çalıştırmayı deniyorum.

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/29.png)  

![]({{ AUCyberClub.github.io }}/assets/img/sqlitoshell/30.png)  

Ve bu challenge'mız da burada bitmiş oluyor.

---
**[Engin Demirbilek](https://twitter.com/Hyal0id)**
