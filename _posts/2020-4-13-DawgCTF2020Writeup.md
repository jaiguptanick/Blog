---
layout: post
published: true
title: "Dawg CTF 2020 Writeup | Solutions"
date: 2020-04-11 13:32:20 +0300
description: Dawg CTF 2020 Writeup | UMBC Cyber Defense - can it be breached?, Tracking, let her eat cake, Another Pcap,.
excerpt: "Dawg CTF 2020 writeups, solution, code snippets, notes, scripts."
image: "/images/dawg/logos.png"
sitemap:
    priority: 0.8
    lastmod: 2020-04-11
    changefreq: monthly
---

<style>
/* This stylesheet sets the width of all images to 100%: */
img {
  width: 90%;
}
</style>
## UMBC Cyber Defense - can it be breached?
---
>Is the shield for keeping things in or keeping things out?
 https://clearedge.ctf.umbccd.io/


The website has a shield image as given in the challenge description as a hint. 


![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/1.png)


Downloading and opening the image on the stegsolve tool give us the flag.

![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/0.png)


``` Flag- DawgCTF{ClearEdge_hiddenImage} ```

## Tracking
---
>Connect here: https://clearedge.ctf.umbccd.io/


![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/4.png)


The red box in the source page looks strange,they are actually ASCII value of some text. <br />
On convering them gives the flag.


![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/5.png)



```Flag- DawgCTF{ClearEdge_uni} ```


## let her eat cake
---
>Yet again, we begin on a journey to conquer: She's hungry! https://clearedge.ctf.umbccd.io/. Our
 only hint, she’s hungry!


![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/2.png)


Decoding the Vigenere Cipher using this online [tool](https://www.boxentriq.com/code-breaking/vigenere-cipher) 
<br />

![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/6.png)

Gives us the text but the flag is not accurate though we get the automatic generated key.Using the same key on the [CyberChef Tool](https://gchq.github.io/CyberChef/)  
gives the proper flag format..

![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/3.png)


```Flag- DawgCTF{ClearEdge_crypto}```


##  Another Pcap
---
>The flag must be somewhere around here...

we are given a .pcap file lets open it in wireshark.
<br /> Exporting HTTP requests we got 2 files 


![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/9.png)


One of the file contain flag.txt which have flag in base64


![dawgCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/dawg/10.png)


``` Flag-DawgCTF{3xtr4ct1ng_f1l35_1s_fun} ```


<br>
<br>

<i>Thanks for your patience,I hope you enjoyed reading. Happy Hacking... </i>
