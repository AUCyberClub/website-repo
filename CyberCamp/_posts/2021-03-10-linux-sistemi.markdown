---
layout: post
title: Linux Sistemi ve Temel Komutlar
date: '2021-03-10 22:26:47 +0300'
author: Can Öztaş
categories: linux
index: 3
---


<center> <h1>Linux Sistemi ve Temel Komutlar</h1> </center>





Çok temel anlamda Linux kerneli kullanan her sistem Linux olarak adlandırılır. Unix işletim sistemi modeli üzerine yazılan Linux kerneli aslında “Von Neumann mimarisi” kavramından beri varolan CPU,Memory sonrasında ise storage’ı yöneten yazılımdır. Burada sadece bilgisayar (PC) gibi düşünülmemeli, akıllı her ev aletleri, router, gömülü elektronik herhangi bir sistem de Linux olabilir. Linux kerneli 1991’de Linus Torvalds tarafından açık kaynak kodlu olarak C temelli tasarlanmıştır. 


![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/220px-NewTux.svg.png)

Kernelin kodlarına açık kaynak kodlu olduğu için[ bu ](https://github.com/torvalds/linux) linkden bakabile biliriz !  Günümüzde Linux’un PC’de bir sürü distrosu olmasına rağmen pazarda Apple ve Microsoft’un gerisinde olmasına karşın, Linux kerneli; serverlar, android telefonlar, akıllı herhangi bir şey’de en çok kullanan yazılımlardan birisidir.

_PC için işletim sistemi kullanımları 2019:_


*   _Windows: 45.3%_
*   _macOS: 29.2%_
*   _Linux: 25.3%_
*   _BSD/Unix: 0.1%_

_Ama PC olmayan diğer ortamlar için tabii ki Linux başı çekiyor, örnek olarak mobil:_


![](https://upload.wikimedia.org/wikipedia/commons/8/83/World_Wide_Smartphone_Sales.png)

[https://en.wikipedia.org/wiki/Usage_share_of_operating_systems](https://en.wikipedia.org/wiki/Usage_share_of_operating_systems)
<br>
<br>

***

<br>

**Bir Linux Sistemin Bileşenleri, Terminoloji ve Ufaktan Bir Giriş**


![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/linuxuxuxuxuxu.jpg)

_Boot Loader:_ Bir bilgisayar ya da gömülü sistemde ilk çalışan kısımdır. Kabaca Storage’daki OS’i yani bu durumda Linux kernelini memory’e getirip çalıştıran programdır.


![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/Untitled-Diagram-215-1.jpg)

_Linux Kernel:_ Yukarıda da bahsettiğimiz gibi bir bilgisayarda CPU ve memory ile ilişkiyi sağlayan kısımdır. OS kısmının iyice detayına girmek isteyenler için:[ https://en.wikipedia.org/wiki/Linux_kernel https://cse.yeditepe.edu.tr/~kserdaroglu/spring2014/cse331/termproject/BOOKS/ProfessionalLinuxKernelArchitecture-WolfgangMauerer.pdf](https://en.wikipedia.org/wiki/Linux_kernel) buraları önerebiliriz fakat pratikte bakarsak en çok kullanılan işletim sistemi Windows’tan farkları, OS’in source kodlarına erişim (bknz:özgür yazılım) ve daha az GUI son kullanıcı için bir takım farklılıktır. Bunun dışında yaklaşım olarak Windows Hybrid kernel kullanırken Linux hatta UNIX-Like sistemler Monolithic yaklaşım kullanırlar, bu fark basitçe Hybrid ya da Microkernel sistemlerde Memory belirli bölgelere ayrılmışken, ki buna user services, kernel services diyebiliriz, adından da anlaşılacağı gibi Monolithic yaklaşımda böyle bir bölünme yapılmaz. ([https://stackoverflow.com/questions/4537850/what-is-difference-between-monolithic-and-micro-kernel](https://stackoverflow.com/questions/4537850/what-is-difference-between-monolithic-and-micro-kernel))

Başka bir farklılık da sisteme herhangi bir device(donanımsal aygıt) eklendiğinde bu bir dizindir. Bilinen tabir ile linux’larda “everything is a file”dır. [EVERYTHING IS A FILE!](https://tldp.org/LDP/Linux-Filesystem-Hierarchy/html/dev.html)

hatta bu device’lar ‘/dev’ dizininde tutulur.
![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/7b4a617ac4836902a9986ef5a073221b.png)


_Daemon:_ Daemon’lar arkada sessizce çalışan background process’lerdir. Tabii ki OS’in her katmanına erişimimiz olduğu için Linux’da daemon yazıp, bunları düzenleyebiliriz. [ detaylar için burası](https://man7.org/linux/man-pages/man7/daemon.7.html)

_Fun-fact: Daemon’lar demon yani şeytan kelimesinin köken olarak eski halidir. Buna karşın insanların Linux veya UNIX’ı satanik dünyayla ilişkilendirmelerinin yanılgı olduğu söylenir [(ki Satanic Ubuntu var)](https://archiveos.org/ubuntu-satanic/). Buna karşın daemon kavramının pagan inanışlarındaki karşılığı tam olarak demon değildir. Ki ironik olarak demon kavramının tam karşılığı Türkçe’deki şeytan da değildir. Bizdeki şeytan kavramı tek ve cehennemin yöneticisi gibi bir şey iken, Batı’da demon aslında yine o “underworld”de yaşayan kötü olan bir topluluktur. Bu kavram karışıklıklarına karşın[ https://en.wikipedia.org/wiki/Daemon_(computing)](https://en.wikipedia.org/wiki/Daemon_(computing)) da okunabileceği gibi  Daemon aslında eksi pagan inanışlarında kötü olarak değil, kişinin kendi özelliğine göre şekillenen bir yapıya sahiptir ve insana hizmet eder. Tam da isimlendirme bu yüzden olacak ki daemon’lar arka planda çalışan OS’in dolayısıyla kullanıcının hizmetkârları gibi tanımla karşımıza çıkıyor._
![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/8eaa02a76c32418db83462f6caf1a075.png)

<br>

_Shell_: Kullanıcının komut girdiği ve buna bağlı bir output dönen yapıdır. Adından da anlaşılacağı gibi aslında işletim sisteminin kabuğudur, yani kullanıcı ile iletişim için dıştaki bir katmandır. Günümüzde çoğu Linux bash kullanır. (Bourne Again Shell - okunurken born again’e benzemesi de küçük bir şaka). Burada kavram olarak terminal ile karıştırmamamız gerekir. Linux OS’lerde sıkça kullandığımız terminal aslında shell çalıştıran bir GUI’dir.[ ](https://fossbytes.com/difference-between-shell-console-terminal/)


[https://fossbytes.com/difference-between-shell-console-terminal/](https://fossbytes.com/difference-between-shell-console-terminal/)

_Window Manager:_Bulunduğumuz yılda bilgisayarlar artık tabii ki sadece komut satırından oluşan siyah ekranlar değil. Yazıda sıklıkla kısaltmasını kullandığımız GUI (Graphical User Interface)’lere sahipler. OS’lerin GUI’lerine Window Manager diye tanım yaparbiliriz. X11 Tüm UNIX-Like sistemlerde karşımıza çıkarken, PC’den en çok kullanılan Ubuntu ve dolayıslya debian ailesi, Red Hat, CentOS gibi distribüsyonlarda GNOME, Android’de ise firmaya göre farklı Window Manager yazılımları görmekteyiz.



**Distro falan dediniz o nedir ki?**

Özgür yazılım ve GNU kavramlarından bahsettik. Bu durum tabii ki işletim sisteminin kendisi için de geçerli.

Linux kerneli üzerine herhangi bir geliştirici/geliştiriciler kendi OS’lerini yazabilir. Linux üzerine yazılmış ve paylaşılmış her türlü[ https://distrowatch.com](https://distrowatch.com/) distro’lar buradan bakılabilir. Tabii ki bu iş o kadar da kolay olmadığı için çekirdeğin üzerine yazılan distribition’ların üzerine başka işletim sistemleri de yazılabilir. Temel olarak sınıflandırma, “paket dağıtımı” na göre yapılır.

En ünlüler debian, rpm, pacman olarak örnek verilebilir.

Debian tarafında Ubuntu ve Ubuntu türevleri (Xubuntu,Lubuntu gibi değişik donanımlar için değişik versiyonlar),MX,Mint,Parrot ve siber güvenlik 101 için de tavsiye edebileceğimiz Kali ünlü debian distribitionlarıdır. Bunun dışında TUBITAK’ın PARDUS’u da debian tabanlıdır.

_Fun-fact: Debian ismi kurucusu Ian’ın kız arkadaşı Debra ile isimlerinin birleşmesiyle oluşmuştur. Computer-science dünyasında isimlendirmelerde hem tuhaf şakalı isimler, hem de kız mevzuları fazlasıyla karşımıza çıkıyor. En basitinden Zuckerberg Facebook’u okulun en güzel kızını seçmek için kurmuştu._

Pacman tarafında Arch Linux ve türevleri göze batarken, rpm tarafında CentOS, Fedeora, SUSE, Red Hat ve yine bu Linuxların türevleri en çok kullanılan Linux dağıtımlarıdır.

**Birkaç Öneri**

Bu yazıda herhangi bir linux’u nasıl kuracağınızın tutorial’ı olmayacak, fakat bu dünyalara girmek isteyen arkadaşlar için bir iki öneri yazabilirim. Öncelikle distribüsyon seçmek önemli bir başlangıç, debian ailesiyle girişmek güzel bir başlangıç olabilir özellikle Ubuntu bu dünyalara uzak insanlar için gayet başarılı. Bunu seçtikten sonra öncelike sanal-makine (virtual machine) olarak bir Linux kurup veya ikinci bir işletim sistemi olarak (dual-boot) kurmak iyi bir başlangıç stratejisi olabilir.

** **

**Basit Terminal Komutları**

Yazının başında shell ve terminalin ne olduğu anlattık. Sonlara doğru ise en çok kullanılan terminal komutları ve yanlarına gerektiğinde küçük teorik bilgiler ile bir bitiriş yapalım.

$ Öncelikle genel olarak tüm Linuxlarda söyle bir syntax vardır.

$ komut -parametre kısaltması parametre

$ Bir komuttan sonra parametreler “-“ yanına tek harf ile yazılabilir. Veya “--“ ile parametrenin uzun hali yazılabilir. Sonrasında ise parametrenin değeri yazılır.

$ Her komut için, isterseniz OS’in kendi içinde gelsin, isterseniz siz bir şekilde ekleyin/kurun “-h” veya “--help“ o komut hakkında bilgi verir.

->Bu genel kurallar dahilinde en çok kullanılan komutlara bakalım:

_#directory kavramı:_

_Dizin olarak çeviribileceğimiz bu kavram bir dosya sistemidir. Bildiğimiz gibi Linux’da her şey bir dosyadır, dolayısıyla dizindir ve biz bu dizinlerde istediğimizi yapabiliriz. Kullanıcı yetkisi dahilinde OS’in tüm directory’lerini değiştirebilir, gezinebilir, yenisini ekleyebilir._

**pwd (Print Working Directory)**

```shell
pwd
```


Açtığımız o komut satırı penceresinin olduğu dizini döndürür.

![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/pwd.png)



**cd (Change Directory)**

```shell
cd ..
```


Yine olduğumuz o terminalde dizinler arası dolaşmamızı sağlar, cd .. ile bir üst dizine gidebiliriz.


![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/cd.png)


**mkdir (Make Directory)**

```shell
mkdir yeniDizin
```


Yetkimiz olan yerlerdeki ki aşağıda biraz değineceğiz, yeni dizinler oluşturmamızı sağlar.

![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/mkdir.png)


**dir** ve **ls**

```shell
dir
ls -C -b
```


İkisi de açılan terminalin olduğu dizindeki dosyaları ve dizinleri göstermek için kullanılır. dir aslında ls -C -b ‘dir (listele, Column(colon olarak), özel karakterleri “backslash escape” ile göster).

![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/diririr.png)



**tree**

```shell
tree
```


Dizinleri computer-science’dan aşina olduğumu veri yapısı ‘tree’ olarak gösterir.
![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/treee.png)

**rm (remove)**

```shell
rm silinecekDosya
```


Bir dosyayı kaldırmak için kullanılır. Dizinleri kaldırmak içinse rm -r (recursive) komutu kullanılabilir.
![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/rmm.png)


_#root kavramı:_

_Bir linux sistemde birden fazla kullanıcı olabilir, bu kullanıcıların yine bildiğimiz kavramlar olan read write yetkisi dizin ve dosyalara göre değişebilir. Bir de tüm bunların üstünde her dizine erişimi olan ‘root’ kullanıcı vardır. Root’a OS ilk kurulurken verilen şifre ile standart kullanıcı iken geçiş yapılabilir._

**sudo (super user do)**

```shell
sudo -i
```

Herhangi bir komuttan önce bazen o komutu yapmaya o kullanıcının yetkisi olmayabilir. Bu noktada komutu root olarak kullanmak için başına sudo eklenir. Ya da var olan terminalde sudo -i yazılarak root session’a geçilebilir.

![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/sudo.png)

**ps (process)**

```shell
ps
```

Bilgisayarda çalışan process'leri gösterir.
![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/ps.png)

**pstree (process tree)**

```shell
pstree -Au
```

![]({{ AUCyberClub.github.io }}/CyberCamp/assets/linux-sistemi/pstree.png)


Processleri ve birbirleri ile olan ilişkilerini gösterir.

