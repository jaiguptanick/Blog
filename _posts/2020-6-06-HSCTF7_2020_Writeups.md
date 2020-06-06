---
layout: post
published: true
title: "HSCTF7 2020 Writeup | Web"
date: 2020-06-06 13:32:20 +0300
description: HSCTH 7 Writeup | Blurry Eyes,Debt Simulator,Inspector Gadget,Broken Tokens,Traffic Lights W
excerpt: "HSCTF 2020 writeups for web catagory."
image: "/images/hsctf/logos.png"
sitemap:
    priority: 0.8
---

<style>
img {
  width: 90%;
}
</style>
These are all the writeup of web challanges in HSCTF7.<br />
## Blurry Eyes
---
>I can't see :( 
 https://blurry-eyes.web.hsctf.com

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_1.png)


The webpage contain information about CTF's. But there is flag in the bottom which seems blurred!!
The source page also does not have anything interesting, moving to inspect element.

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_2.png)


Deleting the name blur from the span tag shows the flag.

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_3.png)

Also you can get the flag by clicking on the "span class="poefKuKjNPojzLDf" as this class stores the flag in the css file.


![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_4.png)


``` Flag- flag{glasses_are_useful} ```

## Debt Simulator
---
>https://debt-simulator.web.hsctf.com/

The webpage shows a strange game which says "Very Realistic" as everytime we loose in the game.


![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf2_1.png)


Moving to source page didn't showed anything interesting so intersepting request using Burp Suite.


![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf2_2.png)

It seems that it is calling some function everytime we create a move in the game.<br>Now we need to find out or gess the correct function to display the flag. Now again searching the .js files in the source code gives a link "https://debt-simulator-login-backend.web.hsctf.com/yolo_0000000000001" from where it is fetching the function.

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf2_3.png)

Opening the link gives us all the three functions that the site is calling.

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf2_4.png)

Replacing the function in the burp by "getgetgetgetgetgetgetgetgetFlag" gives us the flag..


![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf2_5.png)


```Flag- flag{y0u_f0uND_m3333333_123123123555554322221} ```


## Inspector Gadget
---
>https://inspector-gadget.web.hsctf.com/

This was the easiest as opening the source code directly gives us the flag.

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf3_1.png)


```Flag- flag{n1ce_j0b_0p3n1nG_th3_1nsp3ct0r_g4dg3t} ```

<!--
##  Broken Tokens
---
>I made a login page, is it really secure?
  https://broken-tokens.web.hsctf.com/
  Note: If you receive an "Internal Server Error" (HTTP Status Code 500), that means that your cookie is incorrect.


![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_3.png)


![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_3.png)


Decoding the Vigenere Cipher using this online [tool](https://www.boxentriq.com/code-breaking/vigenere-cipher) 
<br />

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_3.png)

Gives us the text but the flag is not accurate though we get the automatic generated key.Using the same key on the [CyberChef Tool](https://gchq.github.io/CyberChef/)  
gives the proper flag format..


![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf1_3.png)


``` Flag- ```                 -->

##  Traffic Lights W
---
>Can you figure out what's going on with this shady company?
    https://traffic-light-w.web.hsctf.com/
 

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf5_1.png)

This challange is simply XXE vernerable if we move to upload firmware option there it asks to upload a XML.
A example file is also given as :
```
<?xml version="1.0" encoding="ISO-8859-1"?>
<root>
  <content>Red</content>
</root>
```

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf5_2.png)

I tried to upload a XXE payload to check if it is vernerable.
```
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<root>
  <content>&xxe;</content>
</root>
```

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf5_3.png)

The website seems XXE(XML External Entity) vernerable.

now we need it to display the flag.On the homepage it shows some docker hostname in which only two are active.

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf5_3_1.png)

Using the hostname "traffic-light-1001" in our xml payload shows noting then using "traffic-light-1004" as :
```
<?xml version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "http://traffic-light-1004"> ]>
<root>
  <content>&xxe;</content>
</root>
```

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf5_4.png)

This payload works and gives us the flag..

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf5_5.png)


``` Flag- flag{shh_im_mining_bitcoin} ```

##  Very Safe Login
---
>Bet you can't log in.
 https://very-safe-login.web.hsctf.com/very-safe-login

The page shows the login page, opening the source code shows the function used logging in the form.
![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf6_1.png)

Logging in using the username and password given gives the flag.

![HSCTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/hsctf/hsctf6_2.png)


``` Flag- flag{cl13nt_51de_5uck5_135313531} ```


<br>
<br>

<i>Thanks for your patience,I hope you enjoyed reading. Happy Hacking... </i>
