---
layout: post
title: Steganografi Nedir
date: '2021-03-29 16:00:00 +0300'
author: Ebubekir Türker
categories: steganografi
index: 1
---

Öncelikle tanımlardan başlayalım:

- **Steganografi** : Görünüşte hiçbir zararı olmayan bir dosyaya, çeşitli yöntemlerle bir mesaj gizleme sanatıdır.
- **Cover**: Gizli mesajı bu dosyaya gömülür.
- **Stego-medium** , **Stego-file** : Gizli mesaj cover'a gömüldükten sonra oluşan dosyaya denir.

Steganografi'yi üçe ayırmak da mümkün, Metin Steganografi, Resim Steganografi ve Ses Steganografi.



### 1 ) Metin Steganografi

Adından da anlaşılacağı gibi metinlere gizleme yöntemidir. Alıcı ve göndericinin yöntemde anlaştıkları sürece pek çok yöntem geliştirilebilir. Örnek olarak

- Baş harfleri kullanmak : After The Theater, All Clients Keep A Tab Down At Wesley’s Nook -> ATTACKATDOWN
- Her kelimenin 3. harfine gizlemek : Fishing freshwater bends and saltwater coasts rewards anyone feeling stressed. Resourceful anglers usually find masterful leapers fun and admit swordfish rank overwhelming anyday. -> Send Lawyers, Guns, and Money.
- Büyük harleri kullanmak : **S**usan sAys **G**aIl Lies. M**A**tt le**T**s **S**usan f**E**el jo**V**ial. **E**lated (or) a**N**gry? -> Sail at seven.

Bu örnekler daha da çoğaltılabilir, CTFlerde  kullanılabilecek toollar ile bu bölümü kapatacağım.

- Eğer **snow** ile ilgili bir şey geçiyor ise çok büyük ölçüde **stegsnow** tool'u kullanılmıştır. Bu tool basitçe boşlukları ve tabları kullanarak bir şifreleme yapıyor. `stegsnow -C file.txt` komutu ile şifreyi çözebilirsiniz. Ayrıca [spammimic](https://www.spammimic.com/) toolu da bu işi yapmakta.
- Bazı toollar unicode karakterleri kullanarak gizleme yapıyor, örnek olarak [Unicode Text Steganography](https://www.irongeek.com/i.php?page=security/unicode-steganography-homoglyph-encoder). Bazı unicode karekterlerin yazılabilir(printable) olmamasını kullanarak oluşturulmuş yöntemdir kendileri.

### 2 ) Resim Steganografi

Eveet geldik en çok kullanılan yöntemlere. Burda mesaj bir resmin içine gizlenmekte ve bir çok yolu var.  Şimdilik sadece LSB'yi detaylı anlatıp CTF'lerde size yardımcı olacak toolları listeleyeceğim.

- **LSB**: 
  Bildiğiniz üzere resimler RGB değerlerden oluşmakta (ve bazı diğer değerlerden).  Bu değerlerinin birleşmiş haline piksel diyoruz. Kısaca `piksel = R.G.B..` diyebiliriz. Burdaki RGB değerleri 0 ile 255 arasında değişiyor ve bu RGB değerleri bir araya gelip farklı renkleri oluşturmamızı sağlıyor. Örnek olarak aşağıdaki resme bakabiliriz.![]({{ AUCyberClub.github.io }}/CyberCamp/assets/steganografi-nedir/01-color-table.png) 
  Gördüğünüz gibi Kırmızı rengi oluşturmak için R'dan 255 G'den 0 B'den 0 alınmış.
  Bilgisayar dilinde konuşursak bu değerler binary olarak **00000000** yani 0'dan **11111111** yani 255'e kadar değişiyor. LSB yöntemi ise bu binary değerlerin sadece belirli indexteki kısmını değiştirerek, rengi çok bozmadan içine mesaj gizlemektir. Örneğin 255 sayısının binary değerini düşünün **11111111**, sondaki **1**'i **0** yaparsak 254 olacaktır. Bu renki o kadar da çok etkilemeyecektir. Sondaki bitleri istediğimiz gibi manipule edebiliriz yani. Mantığını anladıysanız sadece sondaki biti değil, sondaki iki biti de manipule edebiliriz çok farketmeyecektir yine. Hadi aucc logomuzun içine [stegano](https://stegano.readthedocs.io/en/latest/installation/) toolu ile bir mesaj gizleyelim.

  ![]({{ AUCyberClub.github.io }}/CyberCamp/assets/steganografi-nedir/AUCC-LSB.png)

  `pipenv install Stegano` komutuyla Stegano toolunu kurduk, ardından `pipenv shell` komutu ile environment'i etkinleştiridik.  `stegano-lsb hide -i AUCC-logo.png  -m AUCyberClub -o AUCC-logo-stego-medium.png` komutuyla `AUCC-logo-stego-medium.png` 'a `AUCyberClub ` mesajını gizledik. Eğer iki resme  de bakacak olursanız aralarında gözle görülür bir fark yok. Gizlediğimiz mesajı açığa çıkarmak için ise `stegano-lsb reveal -i AUCC-logo-stego-medium.png` komutunu kullandık. Başka bir sürü tool kullanılabilir ama mantık genelde böyle işlemekte.

  İncelemek isteyenler için dosyalar burada -> [AUCC-logo.png]({{ AUCyberClub.github.io }}/CyberCamp/assets/steganografi-nedir/AUCC-logo.png) ,  [AUCC-logo-stego-medium.png]({{ AUCyberClub.github.io }}/CyberCamp/assets/steganografi-nedir/AUCC-logo-stego-medium.png)

- #### Diğer Toollar

  - [Aperisolve](https://aperisolve.fr/) bu site bir sürü toolu aynı anda çalıştırmanızı sağlıyor, ctflerde çok iş yapıyor. 
    İçerisinde barındırdığı toollardan biraz bahsetmem gerekirse 
    
    **View** kısmında resmin renk kanallarıyla oynayarak eğer varsa gizlenmiş mesajı çıkarmaya çalışıyor.
    
    [**Zsteg**](https://github.com/zed-0xff/zsteg) toolu ruby ile yazılmış bir stego toolu. PNG ve BMP  dosyalarındaki gizlenmiş datayı bulmaya yarıyor.
    
    [**Steghide**](http://manpages.ubuntu.com/manpages/xenial/man1/steghide.1.html) toolu ise resim ve ses dosyalarına mesaj gizlemek için kullanılıyor ve genelde bir parola ile gizlendiğinden eğer elinizde parola ve resim varsa bu tool tam size göre.
    
    [**Outguess**](http://manpages.ubuntu.com/manpages/xenial/man1/outguess.1.html) , [**Foremost**](http://manpages.ubuntu.com/manpages/bionic/man8/foremost.8.html) , [**Binwalk**](http://manpages.org/binwalk) toolları ise genelde magic bytelara bakarak gizlenmiş bir dosya var mı diye bakıyor. Burada bir **Not** bırakmak istiyorum, kendimden biliyorum png dosyalarında her zaman **zlib** türünde bir dosya vardır, sorular genelde bunlarla ilgili değildir, o yüzden zlibten uzak durun :)

    [**ExifTool**](https://linux.die.net/man/1/exiftool) ise resimlerin metadatasını görmenizi sağlar, burada genelde lokasyon , fotoğrafın sahibi gibi bilgiler olur.

    [**Strings**](https://linux.die.net/man/1/strings) bu kısım ise dosyadan çıkarabildiği yazılabilir yazıları gösterir, sadece resim dosyaları için değil ses dosyalarında da işe yarar
  - [stegsolve.jar](https://github.com/eugenekolo/sec-tools/tree/master/stego/stegsolve/stegsolve) bu tool da offline olarak bir sürü tool barındırıyor.
  - [Steganography](https://github.com/ragibson/Steganography) bu tool ise içinde WavSteg LSBSteg StegDetect araçlarını barındırıyor ki, ctflerde çok işe yarıyorlar.

  ### 3 ) Ses Steganografi

  Her dosya türüne olduğu gibi ses dosyalarına da mesaj gizlenebilir. CTF'lerde en çok karşımıza çıkan ses dosyası türü wav olmakta. Kullanabileceğiniz toollara bakalım.

  - [WavSteg](https://github.com/ragibson/Steganography#WavSteg) LSB yöntemi sadece resimlerde değil ses dosyalarında da kullanılıyor. Ses datasının son bitleriyle oynamak biraz gürültülü bir ses oluştursada mesaj gizlemek için birebir.

  - [Sonic Visualizer](https://www.sonicvisualiser.org/) Bazen mesaj ses dosyalarının kanallarına gizleniyor ve gizleme işlemi için [Coagula](https://www.abc.se/~re/Coagula/Coagula.html) toolu kullanılıyor. Eğer bize verilen ses dosyasını sonic visualizer de açıp  `Layer-> Add Spectrogram` yolunu izleyerek spectogram eklersek müzikteki gizli mesajı buluruz.  

    Merak edenler için aşağıdaki ses dosyası ->  [AUCC-spectrogram.wav]({{ AUCyberClub.github.io }}/CyberCamp/assets/steganografi-nedir/AUCC-spectrogram.wav)

    ![]({{ AUCyberClub.github.io }}/CyberCamp/assets/steganografi-nedir/AUCC-spectrogram.png)

## Yararlı linkler

Buradaki makalelere de göz atmanızı şiddetle tavsiye ederim.

- [steganografi ,mdisec/topluluk-makale](https://github.com/mdisec/topluluk-makale/blob/master/Steganografi/steganografi.md)
- [0xrick.github.io , stego](https://0xrick.github.io/lists/stego/)
- [hacktricks, stego](https://book.hacktricks.xyz/stego/stego-tricks)
- [ctf-katana, steganography](https://github.com/JohnHammond/ctf-katana#steganography)



Ve yazımızın sonuna geldik. Teorik bilgiden çok bildiğim ve karşılaştığım kadarıyla öğrendiklerimi anlattım.  Sağlıcakla kalın.

