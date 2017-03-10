---
layout: post
title: Wallaby's: Nightmare (v1.0.2) Walktrough
date: '2017-03-10 16:30:42 +0300'
categories: blog
---    
  
Selam,
Wallaby's: Nightmare (v1.0.2) sanal makinesinin tam çözümünü yaptık, sizlerle paylaşmak istedik. Keyifli okumalar.

__Wallaby's: Nightmare (v1.0.2)__

VM hakkında ayrıntılı bilgi alabileceğiniz ve indirme bağlantısını bulabileceğiniz link aşağıdadır

[VulnHub](https://www.vulnhub.com/entry/wallabys-nightmare-v102,176/)

__VM çözümü__

İşe her zamanki gibi maksimum özgüvenle, hedef tespiti ve port tarama ile başlıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/01.png)


ve hedef sistemimizin **192.168.1.22** IP adresinde ve **SSH(22) , HTTP(80) TCP** portlarının açık ve **IRC(6667)** portununda filtreli bir şekilde hizmet verdiğini görüyoruz. **IRC** ile uğraşmak bana göre bir dert olduğu için hiç denemeden **HTTP**ye yöneliyoruz. Default portunda hizmet verdiği için port belirtmeden, doğrudan IP adresini tarayıcımıza yazarak bağlanabiliyoruz ve bir kullanıcı adı ile üye oluyoruz (**aucc**). Bizi, başımıza geleceklerden haberdar eden şu ekran karşılıyor.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/02.png)


**Start the CTF!** diyerek insanlık için küçük, akıl sağlığımız için büyük bir adım atıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/03.png)


gelen sayfa gözümüzü korkutmuyor bile, yukarıdaki **?page=** i farkedince "Hadi canım!" diyip **passwd** dosyasını görmeye çalışıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/04.png)


bikaç deneme daha yapalım derken ensemizden bizi yakaladığı gibi "Nereye? Kolay mı geldi?" diye bir yazı gösteriyor.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/05.png)


başa dönelim demeye kalmadan sayfanın yerinde olmadığını görüyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/06.png)


hemen panikle **nmap**in kapısına tekrar gelip.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/07.png)


**60080 TCP** portunda **http**yi görünce


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/malkocoglu_firar.png)


gibi bir sitemle tarayıcımıza tekrar dönüyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/08.png)


Sayfamız değişmiş ama sorgu hala çalışıyor mu diye denememizle "bu muydu güvenlik" dememiz bir oluyor.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/09.png)


ilk sayfada neden **Fuzzing is your friend.** dediğiyle ilgili kafamızda şimşekler çakıp,

```
dirb http://192.168.1.22:60080/?page= /usr/share/dirb/wordlists/common.txt
```

ile sayfaya hazır bir wordlist ile dictionary based attack başlatıyoruz


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/10.png)


bu çıkan adresleri denediğimizde **?page=index**te ilk kayıt olduğumuz sayfayı, **?page=home**da da varsayılan olarak açılan sayfayı görüyoruz. **?page=.git/HEAD**'den bir şey çıkacak diye ümitlensek de bu ümidimiz çok sürmüyor. **?page=contact**'ta önemli bir şeyler bulamayıp **?page=mailer** da ipucunu alıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/11.png)


ipucundan hareketle, adresimizi komut verebilecek hale getiriyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/12.png)


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/13.png)


hatta bir ara abartıp:


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/14.png)


kendimize güldürtüp, demek başkalarıda deniyormuş ki bunu yazmışlar diyerek teselli bulmaya çalışıyoruz. O depresyonla IRC'ye razı olsak bile **Irssi** 'den

```
irssi -c 192.168.1.22 -p 6667
```

ile bağlanmayı denediğimizde **Connection Timed Out** hatasıyla o bize razı olmuyor. Damarımıza bastıklarından olsa gerek [pentestmonkey](http://pentestmonkey.net/)'den reverse shell beğenip python'u görünce


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/15.png)


Kali Linux'tan

```
nc -lvp 1234
```

ile **1234** portunu dinlerken, kodu kali makinemizin IP adresine göre düzenleyip acımadan kullanıyoruz ve bilgi toplamaya başlıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/16.png)


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/17.png)


yine bir zaafiyetli makine olduğu için tüm kullanıcılara verilmiş iptables'ı yönetme iznini kullanarak *irc* ye dışarıdan yolladığımız paketlerin drop edildiğini görüyoruz ve drop eden bu kuralı siliyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/18.png)


```
irssi -c 192.168.1.22 -p 6667
```

ile yeniden bağlanmayı denediğimizde bağlanıyoruz ve

```
/list
```

ile kanalları listeleyip,

```
/join #wallabyschat
```

ile wallabyschat kanalına katılıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/19.png)


```
.help
```

ile seçeneklerimizi listeleyip


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/20.png)


bize özelden gönderdiğini söyleyince

```
/window 3
```

ile yolladığı seçeneklere bakıyoruz


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/21.png)


bunların hangisi bizim işimize yarar diye baktığımızda **run** dikkatimizi çekiyor.

```
/window 2
```

ile yeniden kanala dönüp **run** diyerek çalıştırmak istediğimizde hiçbir tepki almıyoruz ve **/run** ile **.run** 'ı da deniyoruz. Yalnızca **.run** 'da bize *Waldo* olmadığımızı söylüyor. "Oluruz canım dertettiğin şeye bak" deyip

```
/nick waldo
```

dediğimizde tepki dahi vermiyor çünkü zaten kanalda bir **waldo** var. Onu atmayı denediğimizde de yetkimizin olmadığını söylüyor.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/22.png)


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/hiyar.jpg)


işler burada geriye dönmemiz gerektiğini söylüyormuş. yeniden *python reverse shell* 'i ile bağlandığımız terminale gelirsek ve

```
sudo --list
```

yaparsak *vim* ile bir dosyanın *waldo* adına "parola sormadan" açılabildiğini görmüş oluruz:


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/23.png)


ile vim editörü üzerinden **bash** 'e **sh** 'a kısacası yeniden shelle çıkabiliriz. Zaten herhangi bir metin editörünü, böylesine gerçek olmayan bir terminalde kullanmamız malesef mümkün değil. Ben bireysel seçimim olarak yeni bir sayfa açmayı tercih ederek yeni bir reverse shell ile başka porttan(**2017**) devam ediyorum.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/24.png)


ve şuan waldonun nasıl olup da IRC kanalına bağlı olduğunu öğrenmek için

```
who
```

ile login olmuş kullanıcıları ve neler yaptıklarını listeliyoruz.

```
pkill tmux
```

ile de waldo hesabında bulunduğumuz için bu çalışan *tmux* işlemini durduruyorum.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/25.png)


*irssi* 'ye döndüğümde waldonun çıktığını belirtiyor.

```
/nick waldo
```

ile nickname'imizi waldo yapıp **.run** 'ı çalıştırmaya çalıştığımızda beklediğimiz cevabı alıyoruz. Sürekli .run yazmamak için yine bir **reverse shell** ile mide bulandırarak bağlantımı bu sefer **1996** portundan sağlıyorum.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/26.png)


bütün bıkkınlığımızla wallaby kullanıcısında

```
sudo --list
```
    
çıktısını gördüğümüzde sonda olduğumuzu anlıyoruz çünkü hiçbir sudo parolası istemiyor. En mantıklısını yapıp,

```
sudo su -
```
    
ile *root* oluyoruz,

```
find / -name "flag.txt"
```

ile flag'ımızı **/root** dizininde bulup **cat** ile bastırıyoruz.


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/27.png)


**FLAG**


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/flag.png)


**BU CTFDEN ÇIKAN SONUÇ**


![]({{ AUCyberClub.github.io }}/assets/img/wallaby_v1/shell.png)


      
 ---
 **[Hüseyin Erdem](https://twitter.com/rootofarch)**
