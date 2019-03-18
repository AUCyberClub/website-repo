---
layout: post
title: Frida ile Mobil Uygulama Analizi
date: '2019-03-18 15:50:00 +0300'
categories: makaleler
---

Merhaba, bu yazıda çoğu platformda kullanılabilen reverse engineering aracı *"Dynamic instrumentation toolkit"* **Frida**
hakkında konuşacağız. 

### Peki Neye Yarar Frida?
Frida IOS, Android, Windows, Linux vs çoğu platformda çalıştırılabiliyor olsa da bu yazıda daha çok **Android** ile ilgileceğiz. Frida ile, uygulamada bulunan herhangi bir fonksiyonu hooklayıp istediğimiz şekilde manipüle edebiliyoruz. Fonksiyona parametre olarak gönderilen veya fonksiyondan döndürülen değeri okuyabiliyoruz, hatta etkisiz hale bile getirebiliyoruz.

### Dynamic Binary Instrumentation nedir?
DBI (Dinamik İkili Enstrümantasyon) çalışan işlemleri analiz etmek için kullanılan bir tekniktir. Kod enjeksiyonu ve modül yükleme de dahil olmak üzere birçok farklı yöntem kullanır ve oldukça başarılı olduğu kanıtlanmıştır.
Her ne kadar DBI işlevselliğinin çoğu geleneksel bir hata ayıklayıcı ile elde edilebilse de, hafifliği ve esnekliği DBI'yi üstün bir yöntem haline getirir.


### Kurulum
Bilgisayarınızda python, **adb** ve **jadx** kurulu olduğunu varsayarak kuruluma geçiyorum.
Öncelikle fridayı kullanabilmeniz için Android cihazınızda **frida-server** çalışıyor olması gerekiyor. <a href="https://github.com/frida/frida/releases">Şuradan</a> android için olan en güncel frida-server'ı indirebilirsiniz. Eğer **Android emulator** veya **Genymotion** üzerinde çalışacaksanız, x86 sürümünü indirmeniz gerekiyor. Sonra da "adb push frida /data/local/tmp" ile cihaza aktarıyoruz. Server'a execute iznini verdikten sonra, "/data/local/tmp/frida &" diyerek frida-server'ı arkaplanda başlatıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/frida101/1.png)


Ardından da "pip install frida-tools frida" ile frida client'ını çalıştığımız bilgisayara yüklüyoruz.<br>
Daha ayrıntılı kurulum için https://www.frida.re/docs/quickstart/ adresini ziyaret edebilirsiniz.

### Başlayalım?
Frida, uygulamadaki fonksiyonları hooklayabilmeniz için bir **JavaScript API** sunuyor. Yazılan JS kodları da frida-server tarafından runtime'da çalışan process'e enjekte ediliyor. Yani apk'yı decompile ettikten sonra, hooklamak istediğiniz fonksiyonu oluşturduğunuz JS dosyasında belirtiyorsunuz. Daha iyi anlatabilmek için, <a href="https://github.com/OWASP/owasp-mstg/tree/master/Crackmes/Android/Level_01">OWASP'ın Uncrackable1</a> **reverse engineering** sorusu üzerinden örnek göstereceğim. Soru bizden uygulama içerisine hashlenip gizlenmiş bir string'i ortaya çıkarmamızı istiyor.

![]({{ AUCyberClub.github.io }}/assets/img/frida101/2.png)

Uygulamayı başlattığımız anda bir sorunla karşılaşıyoruz. Cihazımız **root** erişimine sahip olduğu için uyarı şeklinde bir dialog gösteriliyor. Dialog'u onayladığımızda ise, uygulamadan tamamen çıkıyor. APK dosyasını indirip jadx ile decompile ettiğimizde, MainActivity.java dosyasının OnCreate metodu içinde root erişimini tespit eden 3 farklı fonksiyon kullanılmış olduğunu görüyoruz. Fonksiyonun içeriği bizi pek de ilgilendirmiyor aslında. Ne döndürürlerse, ne olur bilsek yeterli.	

![]({{ AUCyberClub.github.io }}/assets/img/frida101/3.png)

Burada karşımıza birden fazla seçenek geliyor. Root'u tespit eden fonksiyonları hooklayıp hepsinin direkt olarak false değer döndürmesini sağlayabiliriz, veya uygulamadan çıkmak için kullanılan **System.exit()** fonksiyonunu hooklayıp etkisiz hale getirebiliriz. İkinci seneçek daha az zahmetli görünüyor.

```
	Java.perform(function() {
	  console.log("started")

	  var systemClass = Java.use("java.lang.System")

	  systemClass.exit.overload("int").implementation = function(var_0) {
	    send("java.lang.System.exit(I)")
	  }
	})
```

Kullanacağımız JS kodları bu şekilde. Kodda Java.perform ile runtime'ı çağırdık ve callback fonksiyonu içerisinde hooklamak istediğimiz fonksiyonun bulunduğu class'ı hookladık. Artık uygulama içerisinde herhangi bir yerden System.exit() fonksiyonu çağırıldığında, orijinali yerine JS dosyamızda yazdığımız implementasyon çalıştırılacak.
Ardından ```frida -U -l script.js owasp.mstg.uncrackable1``` komutunu çalıştırıp işlemi başlatıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/frida101/4.png)
![]({{ AUCyberClub.github.io }}/assets/img/frida101/5.png | height=300)

Bu aşamayı geçtik. Peki gizli string'e nasıl ulaşacağız? MainActivity.class dosyasına biraz daha göz gezdirdiğimizde, butona tıklandığında verify() adında bir fonksiyonun çalıştırıldığını görüyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/frida101/6.png)

Bu fonksiyon da **sg.vantagepoint.uncrackable1.a** classında bulunan başka bir **a** fonksiyon ile kontrol yapıp bir sonuç döndürüyor.

![]({{ AUCyberClub.github.io }}/assets/img/frida101/7.png)

Bu fonksiyonu da incelediğimizde, **sg.vantagepoint.a.a** class'ında bulunan başka bir **a** fonksiyonuna input'a yazdığımız değeri gönderip bir sonuç aldığını ve karşılaştırmayı da bu sonuçla yaptığını görüyoruz. İşimize yarayacak olan değer bu sonuçtan geliyor gibi görünüyor. Fonksiyonu hooklayıp return edilen değeri okumamız gerekiyor. Ancak return edilen değer ayrıca byte data olarak geldiği için bir de string'e çevirmemiz gerekiyor.

```
	Java.perform(function() {
	  console.log("started")

	  var systemClass = Java.use("java.lang.System");

	  systemClass.exit.overload("int").implementation = function(var_0) {
	    send("java.lang.System.exit(I)");
	  };


	  var aClass = Java.use("sg.vantagepoint.a.a")

	  aClass.a.implementation = function(arg1, arg2) {
	      var legit = this.a(arg1, arg2)

	      var s = ""  
	      console.log("legit: " + JSON.stringify(legit))
	      for (i=0; i&#60;legit.length; i++) {
	        s+= String.fromCharCode(legit[i])
	      }
	      console.log(s)

	      return legit
	  }
	})
```

Çalıştırdığımızda da sonuca ulaşıyoruz.

![]({{ AUCyberClub.github.io }}/assets/img/frida101/8.png)

### Kapanış
Genel olarak Frida'nın JS API ve Android ile kullanımı en basit hali ile bu şekilde, ancak Frida çok güçlü bir tool ve ben de henüz gücünü keşfetme aşamasındayım. Eğer Frida ile daha fazla deneyim kazanmak isterseniz, OWASP'ın Android ve IOS için 2'şer sorusu daha bulunuyor, onlara da <a href="https://github.com/OWASP/owasp-mstg/tree/master/Crackmes">https://github.com/OWASP/owasp-mstg/tree/master/Crackmes</a> şuradan ulaşıp çözmeye çalışabilirsiniz.
