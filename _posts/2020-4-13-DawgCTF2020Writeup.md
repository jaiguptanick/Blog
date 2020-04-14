---
layout: post
published: true
title: "Dawg CTF 2020 Writeup"
date: 2020-04-11 13:32:20 +0300
description: Dawg CTF 2020 Writeup | UMBC Cyber Defense - can it be breached?,.
excerpt: "Dawg CTF 2020 writeups, code snippets, notes, scripts."
image: "/images/dawg/logos.png"
sitemap:
    priority: 0.8
    lastmod: 2020-04-11
    changefreq: monthly
    <style>
/* This stylesheet sets the width of all images to 100%: */
img {
  width: 50%;
}
</style>
---
<style>
/* This stylesheet sets the width of all images to 100%: */
img {
  width: 80%;
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


<!-- ## BruXOR
---
>There is a technique called bruteforce. Message: q{vpln'bH_varHuebcrqxetrHOXEj No key! Just brute .. brute .. brute ... :D

This level again requires brute-forcing XOR. This online [tool](https://gchq.github.io/CyberChef/) can easily do this with the key 17.

<img src="{{ "/images/1_bruXOR_1.png" | absolute_url }}" alt="XOR CTF" />


## Reverse Polarity
---
>I got a new hard drive just to hold my flag, but I'm afraid that it rotted. What do I do? The only thing I could get off of it was this:01000011010101000100011001111011010000100110100101110100010111110100011001101100011010010111000001110000011010010110111001111101


The level can be solved by just converting the Binary to Text.

``` Flag-CTF{Bit_Flippin} ```

## Vigenere Cipher
---
>The vignere cipher is a method of encrypting alphabetic text by using a series of interwoven Caesar ciphers based on the letters of a keyword.I’m not sure what this means, but it left lying around: blorpy
gwox{RgqssihYspOntqpxs}

The given text is Vigenere Cipher and the key is **blorpy**.You can use this online [tool](https://www.boxentriq.com/code-breaking/vigenere-cipher).

![vigenere CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/2_vugenere_1.png)

```Flag-FLAG{CiphersAreAwesome}```

## Morse Code
---
>..-. .-.. .- --. ... .- -- ..- . .-.. -- --- .-. ... . .. ... -.-. --- --- .-.. -... -.-- - .... . .-- .- -.-- .. .-.. .. -.- . -.-. .... . . ...

This representation is morse code. Use this online [tool](https://gchq.github.io/CyberChef/) to decode.

![img]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/3_morse_code.png)


## HyperStream Test #2
---
>I love the smell of bacon in the morning! ABAAAABABAABBABBAABBAABAAAAAABAAAAAAAABAABBABABBAAAAABBABBABABBAABAABABABBAABBABBAABB

The above text is encoded as **Bacon Cipher** which can be decoded by this online [Tool](https://gchq.github.io/CyberChef/)

![img]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/4_HYPER_1.png)

```Flag-ILOUEBACONDONTYOU``` 
-->

<br>
<br>

<i>Thanks for your patience,I hope you enjoyed reading. Happy Hacking... </i>
