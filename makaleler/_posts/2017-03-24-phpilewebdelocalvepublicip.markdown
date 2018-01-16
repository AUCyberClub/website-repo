---
layout: post
title: PHP ile İstemcinin Public ve Local IP Adreslerinin Tespit Edilmesi
Date: '2017-3-24 00:42 +0300'
categories: makaleler
---

&nbsp; Merhabalar,  
  
&nbsp; Bu yazıda "**Bir siteyi ziyaret eden kişinin IP adresini nasıl elde edebiliriz ve bu IP adresini site üzerinde nasıl gösterebiliriz?**" sorusuna yazdığım ufak bir PHP kodu ile cevap vermeye çalışacağım. Öncelikle PHP ile ilgili kısa bir bilgi edinelim.  
  
<h3> &nbsp; Nedir bu PHP? </h3>

&nbsp; PHP, 1994 yılında Rasmus Lerdorf tarafından geliştirilmiştir. HTML içine gömülebilen ve [açık kaynak](https://tr.wikipedia.org/wiki/A%C3%A7%C4%B1k_kaynak) kodlu bir [betik dilidir](https://tr.wikipedia.org/wiki/Betik_dili). Sözdiziminin çoğunu C, Java ve Perl'den almış olsa da betiği bu dillerden daha farklı bir yapıdadır. Sunucu tarafında çalıştırılan bir dildir. Yani, içinde PHP kodu barındıran bir siteye bağlanan kullanıcılar buradaki koda erişemez ve müdahale edemezler, yalnızca kodlar sonucu ortaya çıkan görseli görürler.    
  
  &nbsp;  PHP kodu başlangıç etiketi olan `<?php*` ve bitiş etiketi olan `?>` etiketleri arasına yazılır. Bu etiketler bir HTML dosyasının içinde "PHP kipine" geçişi sağlar. Buna bir örnek verecek olursak;  
  
```
<!DOCTYPE HTML>
<html>
    <head>
        ...Burada bazı HTML kodları bulunuyor...
    </head>

    <body>
        <?php 
            echo "Merhaba, ben bir PHP betiğiyim!";
        ?>
        ...Burada da HTML kodları bulunuyor...
    </body>
</html>

```
  
&nbsp; Burada sayfa yüklenirken `<?php` başlangıç etiketi görüldüğü anda PHP kipine geçiş yapılır ve `?>` bitiş etiketini okuyana kadar gördüğü tüm kodları PHP kodu olarak ele alır. Sonuç olarak bu kod ekrana "Merhaba, ben bir PHP betiğiyim!" yazısını bastıracaktır.  
  
<h3>Peki PHP kullanarak siteyi ziyaret eden kişinin IP adresine nasıl ulaşıyoruz?</h3>
&nbsp; Ziyaretçinin IP adresine ulaşmaya genellikle güvenlik, doğrulama, spamları önleme gibi nedenlerle ihtiyaç duyabiliriz.  
&nbsp; PHP'de bunu elde etmek için başvurabileceğiniz iki farklı yol bulunmaktadır. Bu iki yol, değerlerin nasıl ve nereden alındığı konusundaki farkları dışında birbirleriyle aynı işlevi yerine getirirler. Bunlardan ilki olan **getenv()** PHP'deki ortam değişkenleri yardımıyla girilen parametrenin değerini döndürür ve ikincisi olan **$_SERVER** parametrenin değerini web sunucusundan çeker.  
<fieldset>
&nbsp; "$_SERVER" başlıklar, yollar(path) ve betiklerin yerleri gibi bilgileri içeren bir dizidir ve bir web sunucusu (örneğin, Apache) tarafından oluşturulur. Bu dizideki girdiler HTTP sunucusu tarafından atanır. Kullanımı "$_SERVER['parametre']" şeklindedir.  
&nbsp; "getenv()" belirtilen bir ortam değişkeninin değerini döndürür. Kullanımı "getenv ('parametre')" şeklindedir.  
</fieldset>  
&nbsp; Proxy sunucusunu algılamaması için parametrenin olduğu kısma **REMOTE_ADDR** yazmalısınız. **REMOTE_ADDR** geçerli sayfayı görüntüleyen kullanıcının IP adresidir.  
&nbsp; Proxy sunucusunu algılaması için ise **HTTP_CLIENT_IP, HTTP_X_FORWARDED_FOR, HTTP_X_FORWARDED, HTTP_FORWARDED_FOR, HTTP_FORWARDED** parametrelerini yazmalısınız. Bunlar, bu proxy sunucusuna bağlanan kullanıcının IP adresini veren parametrelerdir.  
  
&nbsp; Benim yazdığım HTML içine gömülmüş olan örnek PHP kodu şu şekilde:  
```
<!DOCTYPE html>
<html>

    <head>
        ...
    </head>

    <body>
        ...
        <?php
            $publicip= 0;

            if (getenv('HTTP_CLIENT_IP')) {
                $localip = getenv('REMOTE_ADDR');
                $publicip = getenv('HTTP_CLIENT_IP'); 
            } else if(getenv('HTTP_X_FORWARDED_FOR')) {
                $localip = getenv('REMOTE_ADDR');
                $publicip = getenv('HTTP_X_FORWARDED_FOR');
            } else if(getenv('HTTP_X_FORWARDED')) {
                $localip = getenv('REMOTE_ADDR');
                $publicip = getenv('HTTP_X_FORWARDED');
            } else if(getenv('HTTP_FORWARDED_FOR')) {
                $localip = getenv('REMOTE_ADDR');
                $publicip = getenv('HTTP_FORWARDED_FOR');
            } else if(getenv('HTTP_FORWARDED')) {
                $localip = getenv('REMOTE_ADDR');
                $publicip = getenv('HTTP_FORWARDED');
            } else {
                $localip = getenv('REMOTE_ADDR');
            }
                
            if ($publicip != 0) {
                echo "<h3>Public IP'niz : $publicip </h3>" ;
                echo "<h3>Local IP'niz : $localip </h3>" ; 
            } else {
                echo "<h3>Local IP'niz : $localip </h3>" ;                    
            }
        ?>   
        ...   
    </body>

</html>
```
&nbsp; Burada gerçekleşen işlemlerden kısaca bahsedecek olursak, siteye giren ziyaretçinin bir internet servis sağlayıcının atadığı public IP üzerinden girip girmediği kontrol edilecektir.  
  
&nbsp; Eğer public IP üzerinden girmişse ortam değişkenleri yardımıyla local ve public IP adreslerinin değerlerini döndürüp, bu değerleri sırasıyla aynı isimli değişkenlere atayacaktır. Burada "$publicip" değişkenine ziyaretçinin public IP adresi atanacağı için değeri değişecek ve "0" olmayacaktır. Buna bağlı olarak altta bulunan "if" koşulu sağlanacağı için ekrana şu çıktıyı verecektir:  
<center>
    "Public IP'niz : ..."  <p></p>  
    "Local IP'niz : ..."  <p></p> 
</center>  
  
&nbsp; Eğer public IP üzerinden girmemişse direkt olarak local IP adresini değişkene atayacaktır. Bu durumda "$publicip" değişkeninin değeri "0" olarak kalacak, "if" koşulu sağlanmayacağı için "else"e geçiş yapılacaktır. Buna bağlı olarak ekranda sadece aşağıdaki çıktı görünecektir:    
<center>
    "Local IP'niz : ..."  <p></p>
</center>  

Sonuç olarak bu şekilde siteyi ziyaret eden kullanıcının IP adresine ulaşmış oluyorsunuz.  
  
Bu kodun tamamına ulaşmak için [tıklayın!](https://github.com/elifipekuysal/My-PHP-Codes/blob/master/publicandlocalip.php)
    
---    
      
PHP ile ilgili daha fazla bilgi edinmek isterseniz aşağıdaki kaynaklardan yararlanabilirsiniz:  
[PHP Nedir?](http://php.net/manual/tr/intro-whatis.php)  
[PHP Neler Yapabilir?](http://php.net/manual/tr/intro-whatcando.php)  
[PHP'nin Tarihçesi](http://php.net/manual/tr/history.php)  
[PHP'nin Kurulumu](http://php.net/manual/tr/install.php)  
[PHP'nin Önemli Özellikleri](http://php.net/manual/tr/funcref.php)  
[PHP Dil Başvuru Kılavuzu](http://php.net/manual/tr/langref.php)  
[PHP Kılavuzu](http://php.net/manual/tr/features.php)  
     
---   
  
**[Elif İpek Uysal](https://twitter.com/elifipekuysal)**  
*Yazıya [bu adresten de](https://elifipekuysal.github.io/php-ile-istemcinin-public-ve-local-ip-adreslerinin-tespit-edilmesi.html) erişebilirsiniz.*
