---
layout: post
published: true
title: "ctflearn writeup cryptography - easy "
date: 2020-03-12 13:32:20 +0300
description: ctflearn writeups cryptography (easy) | Character Encoding, Hextroadinary, Base 2 2 the 6, BruXOR, Reverse Polarity, Vigenere Cipher, Morse Code, HyperStream Test.
excerpt: "CTFlearn (Capture The Flag) writeups, code snippets, notes, scripts for beginners cryptography-easy.."
image: "/images/crypt(easy).jpg"
sitemap:
    priority: 0.8
    lastmod: 2020-03-12
    changefreq: monthly
---

## Character Encoding
---
>In the computing industry, standards are established to facilitate information interchanges among American coders. Unfortunately, I've made communication a little bit more difficult. Can you figure this one out? 41 42 43 54 46 7B 34 35 43 31 31 5F 31 35 5F 55 35 33 46 55 4C 7D.

This level is pretty simple; the flag is just converted into hex.

``` Flag- ABCTF{45C1115U53FUL} ```

## Hextroadinary
---
>Meet ROXy, a coder obsessed with being exclusively the worlds best hacker. She specializes in short cryptic hard to decipher secret codes. The below hex values for example, she did something with them to generate a secret code, can you figure out what? Your answer should start with 0x.
0xc4115 0x4cf8

ROX indicates XOR i.e perform XOR operation on these two strings to get the flag.
Use this [tool](https://xor.pw/) to perform XOR on the strings.

```Flag- c0ded ```

## Base 2 2 the 6
---
>There are so many different ways of encoding and decoding information nowadays... One of them will work! Q1RGe0ZsYWdneVdhZ2d5UmFnZ3l9

As the challange name suggest it is converted into base64 encoding.

```Flag- CTF{FlaggyWaggyRaggy}```
## BruXOR
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

The given text is Vigenere Cipher and the key is **blorpy**.You can use this online [tool](https://www.dcode.fr/vigenere-cipher).

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

<br>
<br>

<i>Thanks for your patience,I hope you enjoyed reading. Happy Hacking... </i>
