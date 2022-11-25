---
layout: post
title: DLL Injection Nedir?
date: '2022-11-25 22:26:47 +0300'
author: İsmail Başaran
categories: malware
index: 2
---
DLL injection, kötü amaçlı etkinliği meşru bir Windows işleminin altına enjekte ederek kendini kullanıcıdan ve sistemden gizleme yöntemidir. Kötü amaçlı yazılım, kurban cihazı kendi DLL'ini yüklemeye zorlar ve onu meşru, tamamen doğal görünen bir işlemin alt işlemi haline getirir. Kendisini gizlemesi için kullanacağı bu işlem svchost.exe veya explorer.exe gibi herhangi bir işlem olabilir.

Artık, kötü amaçlı yazılımların normal bir process’in altına bir subprocess enjekte edeceğini ve etkinliğini gizleyerek yakalanmaktan kaçınmaya çalışacağını biliyoruz. Ancak konuyu kavrayabilmek için öncelikle DLL’nin tam olarak ne olduğunu ve ne işe yaradığını anlamamız gerekir. Dynamic-Link Library’nin (Dinamik Bağlantı Kütüphanesi) kısaltması olan DLL, Windows uygulamalarının birden çok uygulama arasında kod paylaşması için Windows tarafından sunulan kütüphanelerdir.

Windows’taki her büyük program bazı temel işlemlere ihtiyaç duyar ve DLL tarafından sağlanan, önceden tanımlamış, daha küçük işlevleri kullanır. Bu açıdan bakıldığında, Windows’taki programların kullandığı DLL’ler, kodlamada kullanılan ve yazılımcının işini kolaylaştıran hazır kütüphanelere benzemektedir.

Hepimiz Windows API’ı (Uygulama Programlama Arayüzü) daha önce duymuşuzdur. İşte bu DLL’leri Windows API’ın en temel bloğu olarak düşünebilirsiniz. Örneğin:

- kernel32.dll — dosya ve klasörlere erişir ve
  bunlar üzerinde değişiklik yapar.
- gdi32.dll — grafikleri görüntülemek ve işlemek
  için kullanılır.
- wsock32.dll — internet ve ağ uygulamaları
  tarafından ağ bağlantılarını işlemek için kullanılır.

**Daha derine inersek:**

Kötü amaçlı yazılımlar, Windows API işlevlerini kullanarak DLL oluşturur veya kötü amaçlı DLL dosyasının yolunu bir process içine yazar. target.exe yürütüldüğünde, "target.exe" önceden tanımlanmış yollardan gerekli DLL'leri çağırır ve yükler. Bu sayede normal bir uygulama mal.dll’i çalıştıracak ve tamamen normal olan uygulamanın zararsız bir subprocess’i olarak gösterecektir.

![](/CyberCamp/assets/dll-injection-nedir/image1.png)

Yukarıdaki resimde gösterildiği gibi, target.exe içine kötü amaçlı DLL enjeksiyonunu gerçekleştirmekten sorumlu olacak bir *başlatıcı* dosyamız var. target.exe her yürütüldüğünde, mal.dll de yürütülür. Bu teknik, meşru bir işlem (bizim senaryomuzda target.exe) içerisine kötü amaçlı etkinlikleri gizlemek için kullanılan bir tekniktir.

**Nasıl yapılır?**

İşleme özel güvenlik duvarını atlamak ve target.exe’ye erişmek için belirli adımlar vardır.

**-Zararlı DLL’in yolunu hazırlama**

![](/CyberCamp/assets/dll-injection-nedir/image2.png)

İlk olarak, başlatıcı olarak adlandıracağımız kötü amaçlı yazılım, mevcut çalışma dizinini almak için [GetCurrentDirectory](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-getcurrentdirectoryhttps:/)’yi ve mal.dll’in yolunu hazırlamak için [lstrcatA](https://learn.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-lstrcatahttps:/)’i kullanır.

**-Hedef işlemin PID’sini (işlem kimliğini) alma**

![](/CyberCamp/assets/dll-injection-nedir/image3.png)

Bir sonraki adım target.exe’nin process ID’sini almaktır. [EnumProcesses](https://learn.microsoft.com/en-us/windows/win32/api/psapi/nf-psapi-enumprocesseshttps:/) isimli fonksiyon sistemde her bir process objesinin process tanımlayıcısını alıp bunları bir dizide depolar, daha sonra *launcher* bu listede gezip “target.exe”yi bulana kadar karşılaştırma yapar ve “target.exe”ye atanmış doğru PID’yi bulana kadar döngüyü tekrar eder.

**-target.exe’ye ulaşmak için tanıtıcı edinme**

PID alındıktan sonra, bu PID, target.exe’ye bir tanıtıcı elde etmek için [OpenProcess](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-openprocess) işlevine parametre olarak kullanılabilir.

**-target.exe [sanal adres alanı](https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/virtual-address-spaceshttps:/) içinde bellek ayırma**

![](/CyberCamp/assets/dll-injection-nedir/image4.png)

[VirtualAllocEx](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualallocexhttps:/)- Bu işlev, önceki adımdan alınan tanıtıcı kullanarak target.exe içindeki belleği ayırır.

**-Yeni oluşturulan belleğe mal.dll’in tam yolunu yazma**

![](/CyberCamp/assets/dll-injection-nedir/image5.png)

Bu kodda, “Buffer” parametresi, mal.dll’in tam yolunu içeren bir dizeye işaret eder. lpBaseAddress yeni oluşturulan belleğin başlangıç noktasıdır ve hProcess, target.exe için bir tanıtıcı içerir. Buffer’ı lpBaseAddress‘e yazmak için [WriteProcessMemory](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-writeprocessmemory) işlevi çağırılır. Bu da mal.dll’in yolunun target.exe içine yazıldığı anlamına gelir. DLL dosyasını çalıştırmak için kernel32.dll’den [LoadLibraryA](https://docs.microsoft.com/en-us/windows/win32/api/libloaderapi/nf-libloaderapi-loadlibrarya) işlevi gereklidir, bu nedenle [LoadLibraryA](https://docs.microsoft.com/en-us/windows/win32/api/libloaderapi/nf-libloaderapi-loadlibrarya)‘in adresini manuel olarak çözer ve bir değişkene depolar.

**-Çalıştırma**

Son olarak, [CreateRemoteThread](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createremotethread) sanal adres alanında çalışan iş parçacığı oluşturucu çağrılır. Böylece target.exe ile mal.dll de çalıştırılmış olur.

Yukarıdaki örnek, DLL injection yöntemlerinden biridir ancak enjeksiyon farklı yollarla da gerçekleştirilebilmektedir.

### Sources:

* [Whatis DLL Injection?](https://vvelitkn.com/malware%20analysis/What-is-DLL-Injection/)
* [Preet Kamal’s DLL Injection Article](https://medium.com/malware-autopsy/dll-injection-f4b512cacaf4)
* [Windows API Documantation](https://learn.microsoft.com/en-us/windows/win32/api/)
* [Further Information of DLL Injection by cocomelonc](https://cocomelonc.github.io/tutorial/2021/09/20/malware-injection-2.html)
