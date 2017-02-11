---
layout: post
title: Pelican ile GitHub Üzerinde Blog Oluşturma
date: '2017-02-11 22:39:47 +0300'
categories: blog
---

  Merhabalar,

  Bu yazıda pelican ile github üzerinde nasıl blog oluşturabileceğinizi anlatacağım. Öncelikle kısaca pelican nedir sorusuna bir yanıt verelim. Pelican, veritabanı veya sunucu tarafı mantığı gerektirmeyen, Python ile yazılmış statik bir site oluşturucusudur. Aynı zamanda pelican'ın kaynak kodu GitHub'da barındırılmaktadır. Peki GitHub nedir ve ne için kullanılır?

                              Git + Hub = GitHub

  GitHub'daki "Git", Linux'u yaratan kişi olan Linus Trovalds tarafından başlatılan bir açık kaynaklı sürüm kontrol sistemidir. "Sürüm kontrolü" nedir derseniz: Sürüm kontrolü, belirli bir sürüme daha sonra geri ulaşabilmeniz için, bir dosyaya veya dosya grubuna zamanla yapılan değişiklikleri kaydeden bir sistemdir.

  "Hub" ise, GitHub'da çalışmayı daha kolay bir hale getirmek için Git'i sarıp, ek özellik ve komutlarla genişleten bir komut satırı aracıdır.


  Pelican ve GitHub hakkında ufak bir bilgi edindiğimize göre bu dosyaları kuralım.

  GitHub'a [buradan](https://github.com/) üye olabilirsiniz. Daha sonra aşağıda gördüğünüz komutları takip ederek GitHub'ı kurabilirsiniz.

    $ sudo apt-get install git git-doc
    $ git config --global user.name KULLANICIADI
    $ git config --global user.email KULLANICIADI.EMAIL@örnek.com
  
  Sisteminize Pelican'ı kurmak için ise:

    $ pip install Markdown
    $ pip install typogrify
    $ pip install pelican


  Pelican, kurduğunuz şekliyle reStructuredText'i destekler. Ben bu anlatımda tercihen yazılarımı markdown formatında oluşturacağım için, Markdown dosyasını da makineme kurdum.

  Blogunuz için ayrı bir dizin oluşturmanızı tavsiye ederim. Aksi taktirde çalışacağınız alan karışabilir. Artık sitemizi oluşturmaya başlayabiliriz:

    $ pelican-quickstart

  Bu komutu çalıştırdıktan sonra karşınıza çıkan soruları kendinize göre yanıtlayın.

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog1.png)

  "**$ pelican-quickstart**" komutundan sonra, dizininiz şu şekilde bi görünüme sahip olacaktır.

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog2.png)

  Burada bulunan dosyalardan bahsedecek olursak;  
  
  > **Makefile**, "make" komutununa hangi işlemleri yapması gerektiğini söyler. Örneğin, "make devserver" gibi komutları tanımlar. ( Burada "make devserver" komutu, size ait olan development sunucusunu localhost'ta çalıştırmanızı sağlar. )
  
  > **content**, oluşturacağınız tüm Markdown dosyalarınızın bulunması gerektiği dizindir. Pelican, gönderilerinizin bu dizinde olacağını varsayar.Tercihen content'i, yazılarınızı ve bu yazıların içerisinde bulunacak resimleri birbirinden ayıracak şekilde aşağıdaki gibi iki ayrı dizine bölebilirsiniz:  
    $ mkdir content/pages   
    $ mkdir content/images  
  Pelican, oluşturduğumuz bu pages dizininin içinde, blog veya sizi tanıtan, iletişim bilgilerinizi kapsayan yazılarınızın ; images dizininin içinde ise, yazılarınızın içeriğinde bulunan resimlerin olduğunu bilecek şekilde yapılandırılmıştır.
  
  > **develop_server.sh** ise, blogunuza yazdığınız yazıların, eklediğiniz resimlerin ve temanızın üzerinde yaptığınız değişikliklerin, GitHub Pages'e tekrar aktarma gerekmeksizin, "localhost:8000" üzerinden görmenizi sağlayan bir bash komut dosyasıdır.
  
  > **fabfile.py**, fab komutunu kullanarak sitenizi oluşturmanıza izin veren Fabric için bir yapılandırma dosyasıdır. Bunu kullanmak isterseniz, "$ pip install fabric" komutu ile dosyayı indirmeniz gerekmektedir. Alternatif olarak sadece "make" komutunu da kullanabilirsiniz.
  
  > **output**, sunucunuzu çalıştırdığınız zaman content dosyanızın içerisinde bulunan bilgilerin, HTML dosyalarında saklanacağı yerdir.
  
  > **pelicanconf.py**, Pelican yapılandırma ayarlarınızı içerir.
  
  > **publishconf.py**, Pelican yapılandırma ayarlarını barındırdığı için pelicanconf.py gibidir, ancak onun aksine "$ make devserver" komutu işlem görürken publishconf.py'e başvurulmaz.
  
  
  Şimdi blog oluşturma kısmına geri dönelim. Blogda yer almasını istediğiniz tüm yazılar ve resimler content (içerik) klasörünüzün içerisinde bulunmalıdır. O zaman hadi dizinimizi content'teki pages klasörüne geçirelim :

    $ cd content/pages

  Benim oluşturduğum dosyanın adı deneme.md ve aşağıdaki gibi bir görünüme sahip :

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog3.png)

  Dosyanızın içinde sadece başlık, tarih ve kategori bilgilerinin bulunması yeterli. Bu bilgilerden sonra gelecek satırda da paylaşmak istediğiniz yazıyı eklemelisiniz. Bu yazının reStructuredText hali ise aşağıdaki gibi olacaktır :

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog4.png)

  Bu işlemlerden sonra projects dizini aşağıdaki gibi bir görünüme sahip olacaktır:
![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog5.png)

  Şimdi projects dizininize geri dönüp, "**$ make devserver**" komutunu kullanarak development sunucusunu başlatın. Komutun çalışması tamamlandıktan sonra eklediğiniz yazıyı veya yazıları, tarayıcınızın URL kısmından "[http://localhost:8000](http://localhost:8000)" adresine giderek görebilirsiniz :

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog6.png)

  "**$ make stopserver**" komutuyla ise sunucunuzun çalışmasını durdurabilirsiniz.  

  **Pelican Blogu GitHub'a Aktarmak**
  Blog içeriklerini hazırladıktan sonra, bunları GitHub'a aktarıp herkes tarafından görüntülenebilecek ufak bir platforma dönüştürebilirsiniz. Bunun için ise öncelikle bir GitHub hesabınız olmalı. Eğer GitHub'a üye değilseniz [bu linke tıklayarak](https://github.com/) üye olabilirsiniz.

  Hesabınızı oluşturup , ona giriş yapınız.

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog7.png)

  Blogunuz için oluşturduğunuz dosyaları taşıyacak bir repository yani bir depo oluşturmadan önce , hesabınıza SSH (Secure Shell) anahtarı eklemelisiniz. SSH anahtarı, SSH protokolünde kimlik doğrulaması için kullanılan bir şifreleme anahtarıdır. SSH protokolü, güvenli ağ iletişiminin daha basit ve ucuz uygulanması için tasarlanmış bir protokoldür. SSH anahtarları ise, kullanıcı adı ve parola ikilisine benzer bir şekilde erişim izni almanızı sağlar. 

  Terminalinize "**ls -al ~/.ssh**" komutunu girerek elinizde bulunan SSH anahtarlarını görebilirsiniz:

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog8.png)

  Public anahtarların dosya isimleri, varsayılan olarak aşağıdakilerden biri olacaktır: 
  > id_dsa.pub  
  > id_ecdsa.pub  
  > id_ed25519.pub  
  > id_rsa.pub  
  
  Eğer public ve private olmak üzere bir anahtar çiftine sahip değilseniz veya yeni bir çift anahtar oluşturmak istiyorsanız;

    $ ssh-keygen -t rsa -b 4096 -C "KULLANICIADI.EMAIL@örnek.com" 

  Bu komut, e-postanızı bir etiket olarak kullanarak sizin için yeni bir ssh anahtarı oluşturur:

  > $ ssh-keygen -t rsa1 -b 4096 -C "KULLANICIADI.EMAIL@örnek.com"  
  > Generating public/private rsa key pair.  
  > Enter file in which to save the key (/home/user/.ssh/rsa): [Entera tıklarsanız public anahtarı belirtilen yere yerleştirir.]  
  > Enter passphrase (empty for no passphrase): [Public anahtarınız için bir parola oluşturun.]  
  > Enter same passphrase again: [Parolanızı tekrar girin.]  
  
  Burada, "Enter file in which to save the key (/home/user/.ssh/rsa): " satırında oluşturduğunuz public anahtarın nerede tutulmasını istediğinizi full-path ile gösterebilirsiniz.

  Oluşturduğunuz SSH anahtarı daha sonra ssh-agent denilen hizmete eklemeniz gerekmektedir. Sisteminizde ssh-agent'ın etkinleştirildiğinden emin olun:  
  
  > ssh-agent'ı arkaplanda çalıştırın  
  > $ eval "$(ssh-agent -s)"  
  > Agent pid 12345  
  
  SSH anahtarınızı , ssh-agent'a ekleyin:

    $ ssh-add ~/.ssh/id_rsa

  Şimdi de ssh anahtarını , github hesabınıza ekleyin:
  
  1. GitHub'da sağ üst köşede bulunan profil resminize tıklayıp, ayarlar (settings) seçeneğine gidin.
  ![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog9.png)
  2. Sol tarafta çıkan kullanıcı ayarları çubuğunda "SSH ve GPG anahtarları (SSH and GPG Keys)" kısmını seçtikten sonra karşınıza çıkan sayfanın sağ üstünde bulunan "Yeni SSH Anahtarı (New SSH key)" seçeneğine tıklayın.
  3. Altta açılan bölümde "Başlık (Title)" kısmına bilgisayarınızı anlatacak bir bilgi girin. "Key (Anahtar)" kısmına ise public anahtarınızın bulunduğu dosyanın çıktısını kopyalayıp-yapıştırın ("**cat id_rsa.pub**"). Ve "SSH Anahtarını Ekle (Add SSH Key)" seçeneğine tıklayın.
  ![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog10.png)
  
  
  SSH anahtarını hesabınıza eklediğinize göre bir depo (repository) açıp, blogunuz için oluşturduğunuz dosyaları bu depoya ekleyebilirsiniz. Git'te herhangi bir şey yapmak için bir Git deponuz olmalıdır. Kaydettiğiniz verilerin saklandığı yer burasıdır..
GitHub'ın sayfasında , ekranın sağ üsttarafında bulunan profil resminizin solundaki "**+**" kısmından "**New repository**" seçeneğine tıklayın.

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog11.png)

  Karşınıza çıkan sayfada "Repository" kısmına blogunuza ulaşılmasını istediğiniz başlığı "github.io" eki ile birlikte yazınız.

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog12.png)

  Bir projede biriyle işbirliği yapmanız gerekiyorsa veya kodunuzu tekrar incelemek ve kullanmak istiyorsanız, URL'yi klonlamalısınız (burada klonlamaktan kasıt kopyalamaktır.) . Deponuzu oluşturduktan sonra karşınıza çıkan sayfadan aşağıdaki komut blokunu kopyalayıp terminal üzerinde çalıştırın. Komutun tamamlanması için kullanıcı adınızı ve parolanızı girmelisiniz.

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog13.png)

  Böylece deponuzu, dizininizde bulunan dosyaları eklemek için aktif hale getirmiş oldunuz. Son olarak yapmanız gereken şey "**output**" dizininizin içinde bulunan her şeyi bu depoya aktarmak. Bunun için ilk önce terminalden "**output**" dizininize geçiş yapın ve aşağıdaki komutları kullanarak bu dizinin içindekileri deponuza yerleştirin:

    $ cd output
    $ git add -A
    $ git commit -m "commit mesajı"
    $ git push origin master

  Artık blogunuz başka kişiler tarafından görüntülenmeye açık hale getirilmiş oldu. Blogunuza, deponuzu oluştururken "Repository Name" kısmına yazdığınız adresinden ulaşabilirsiniz.

![]({{ www.aucyberclub.org }}/assets/img/pelicangithubblog14.png)

---
**[Elif İpek Uysal](https://twitter.com/elifipekuysal)**  
*Yazıya [elifipekuysal.github.io](https://elifipekuysal.github.io/) adresinden de erişebilirsiniz.*
  
