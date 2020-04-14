---
layout: post
published: true
title: "VirSecCon CTF 2020 Writeup - Web "
date: 2020-04-11 13:32:20 +0300
description: VirSecCon CTF 2020 Writeup for Web Catagory | Countdown,.
excerpt: "VirSecCon CTF 2020 writeups, code snippets, notes, scripts for beginners Web.."
image: "/images/virsecConCTF/virssecon_logo.png"
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

## Countdown
---
>We hear something beeping... is there something in the oven?
 Connect here: http://jh2i.com:50036.

Beep reminds time which is stored in the cookies. <br /> Cheking cookies gives us detonate time, increase its value and click link on the page.


![Countdown CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/virsecConCTF/virsec1.png)


Boom!! It gives the flag

``` Flag- LLS{saving_lives_with_cookies} ```

## Hot Access
---
>Access to all the latest modules, hot off the press! What can you access?
Connect here: http://jh2i.com:50016


Finally the link to flag-http://jh2i.com:50016/sshh_dont_tell_i_hid_the_flag_here/flag.txt 

```Flag- LLS{htaccess_can_control_what_you_access} ```

<!--

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
-->

<br>
<br>

<i>Thanks for your patience,I hope you enjoyed reading. Happy Hacking... </i>
