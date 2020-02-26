---
layout: post
title: Buffer OverFlow 101
date: '2020-02-26 17:00:00 +0300'
categories: makaleler
---


# BUFFER OVERFLOW
Bir program çalıştırılmak istenildiği zaman program kodu makine diline çevrilerek RAM (Random Access Memory) denilen geçici hafıza bölgesine yüklenir.RAM içerisinde belirli kısımlara ayrılır:

  - STACK →Yerel hafıza değişkenleri ,fonksiyonların dönüş adresi ve eski EBP değeri burada saklanır. LIFO mantığı çalışır.Yüksek adresten düşük adrese göre yerleşim gerçekleşir. ESP stack bölgesinin en üst noktasını gösteren kaydedicidir.
  - HEAP →int *ptr;ptr=malloc(10*sizeof(int)); malloc realloc gibi dinamik hafıza alanı ayırmak için kullanılan komutlar ile ayrılan bölge.
  - .BSS →İçerisine herhangi bir değer atanmamış(uninitilized)global ve static değişkenler burada saklanır.
- .DATA →İçerisine herhangi bir değer atanmış (initilized)global ve static değişkenler burada saklanır.
- CODE(.TEXT) →Program kodlarının binary yani makine diline çevrilmiş halleri burada tutulur.

## Kaydediciler(REGISTERS)
  →DATA REGİSTERS
  - 1.AX:akümülatör resgisteri,Dört işlem operasyonlarında kullanılmaktadır.
  - 2.BX:Base Registeri,Bellek lokasyonlarında baz adres göstericisi olarak kullanılır.
  - 3.CX:counter Registeri ,Döngü işlemlerinde sayaç olarak kullanılır.
- 4.DX:Data Registeri,Donanım ile yapılan giriş çıkış işlemlerinde kullanılır.

→INDEX REGISTERS
- 1.ESI(Extended Destination Indicator)Karakter ya da döngü işlemleri sırasında okuma işlemi yapılacak olan yerini adresini gösterir.
- 2.EDI (Extended Destination Indicator ) Karakter ya da döngü işlemleri sırasında yazma işlemi yapılacak olan yerin adresini gösterir.


→SEGMENT REGISTERS
- 1.CS(Code Segment )Program kodlarının makine dilindeki halleri kod segmentde saklanır.Çalıştırılacak tüm komutlar buradadır.CS register kod segmentin başlangıç adresini saklar.
- 2.DS( Data Segment)ilk değer atılmış (initilazed)global ve statik değişkenler data segmentte saklanır.DS kaydedici data segmentin başlangıç adresini tutar.
- 3.SS( Stack Segment )Dönüş adresleri yerel fonksiyon değişkenleri ve eski ebp değerleri stack içerisinde tutulur.SS register stack başlangıç adresini saklar.

→POINTER REGISTERS
- 1.EIP : Bir sonraki çalışacak olan komutun adresini saklar.
- 2.EBP :Stackte referans noktası oluşturur.
- 3.ESP : Stack bölgesinin en üst noktasını gösterir.
Kullanıcı hafızası| EIP | ESP
PROCESS →Süreç dediğimizde “çalışan program” diyoruz.
## BUFFER OVERFLOW
![]({{ AUCyberClub.github.io }}/assets/img/bof101/1.png)

C ve türevleri ile yazılan programlarda hafıza kontrolü kullanıcıya bırakıldığı için kodlamada yapılan bazı hatalardan dolayı bellek için ayrılmış bir yere daha fazla veri yazılması sonucunda bellekte taşma oluşabilmektedir.Bu taşma sonucunda programın çökmesine veya akışının değişmesine neden olan bu açıklıklara bellek tabanlı stack taşma açıklıkları denmektedir.EIP değeri üzerinde taşma olacağından dolayı program çökecektir.Bu açıklık BOF açıklığıdır.Eğer EIP program içerisinde uygun bir yere yönlendirilebilirse STACK içerisinde SHELLCODE çalıştırılarak exploit yazılabilir.
## TAZMANYA 🤪

![]({{ AUCyberClub.github.io }}/assets/img/bof101/2.png)
![]({{ AUCyberClub.github.io }}/assets/img/bof101/3.png)
## Hijackthis😎
![]({{ AUCyberClub.github.io }}/assets/img/bof101/4.png)
![]({{ AUCyberClub.github.io }}/assets/img/bof101/5.png)
Gdb ile de programın hata verip vermediğine bakılabilir.
![]({{ AUCyberClub.github.io }}/assets/img/bof101/6.png)
![]({{ AUCyberClub.github.io }}/assets/img/bof101/7.png)
![]({{ AUCyberClub.github.io }}/assets/img/bof101/8.png)
eip 41414141😱
![]({{ AUCyberClub.github.io }}/assets/img/bof101/9.png)
![]({{ AUCyberClub.github.io }}/assets/img/bof101/10.png)
eip 45444342 boşluk olmadığını anlıyoruz.
![]({{ AUCyberClub.github.io }}/assets/img/bof101/11.png)
IDA dan diğer fonksiyonun adresi için inceleme yapıyoruz. Eip ye bu adresi yazdığımızda artık programımız bu adresten devam edecektir.
![]({{ AUCyberClub.github.io }}/assets/img/bof101/12.png)
Tebrikler beni çağırabildin :)
[Sinem Şahin](https://twitter.com/sinemsahi_) | [Medium](https://medium.com/@wsinemsahin)
