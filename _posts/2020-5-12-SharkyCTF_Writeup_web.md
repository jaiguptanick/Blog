---
layout: post
published: true
title: "Sharky CTF Writeup | Web "
date: 2020-05-12 13:32:20 +0300
description: Sharky CTF Writeup | .
excerpt: "Sharky CTF writeups, solution, code snippets, notes, scripts."
image: "/images/sharkyctf/logo.png"
sitemap:
    priority: 0.8
    lastmod: 2020-05-12
    changefreq: monthly
---

<style>
/* This stylesheet sets the width of all images to 100%: */
img {
  width: 90%;
}
</style>
## XXExternalXX
---
>One of your customer all proud of his new platform asked you to audit it. To show him that you can get information on his server, he hid a file "flag.txt" at the server's root.
xxexternalxx.sharkyctf.xyz

The name of the challenge clearly suggest that the challenge is related to XXL injection, to find out the content of file /flag.txt

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/1.png)

Stored data look strange, and it shows requesting some XML file in the URL.
If we add some garbage to the query string, like ?xml=jhvhjvvvkvkj, a bunch of errors is spat out of the application showing some of the functions used in web apps.

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2.png)

Now finding some XXE payload that can show the content of flag.txt
Here is the Sample..

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///flag.txt"> ]>
<root>
    <data>&xxe;</data>
</root>

```
Now since there is no submit option to upload our payload to the server, we need to create a link that can be used to forward the code to this website server.
Here I have used Pastebin.com to upload the code.
Use that link in the URL to get the flag..

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/last.png)

``` Flag- shkCTF{G3T_XX3D_f5ba4f9f9c9e0f41dd9df266b391447a} ```

## Logs In ! Part 1
---
>Data printed on one of our dev application has been altered, after questioning the team responsible of its development, it doesn't seem to be their doing. The H4XX0R that changed the front seems to be a meme fan and enjoyed setting the front.
We've already closed the RCE he used, there is a sensitive database running behind it. If anyone could access it we'll be in trouble. Can you please audit this version of the application and tell us if you find anything compromising, you shouldn't be able to find the admin session.
The application is hosted at [logs_in](http://logs_in.sharkyctf.xyz/)

The description tells of finding the admin section on the page.
This was really an easy challenge if you navigate to the correct link. The link to the admin section or say the flag lies at the footer of the page. Clicking on MainController::index in the Request/Response screen revealed some routes:

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_1.png)

The route is highlighted on the debug page.  

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_2.png)

Opening the link http://logs_in.sharkyctf.xyz/e48e13207341b6bffb7fb1622282247b/debug
takes us to the admin page or the flag.

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_3.png)

```Flag- shkCTF{0h_N0_Y0U_H4V3_4N_0P3N_SYNF0NY_D3V_M0D3_1787a60ce7970e2273f7df8d11618475} ```

<!--
## Containment Forever
---
>Hello, welcome on "Containment Forever"! There are 2 categories of posts, only the first is available, get access to the posts on the flag category to retrieve the flag.
containment-forever.sharkyctf.xyz

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_3.png)


Decoding the Vigenere Cipher using this online [tool](https://www.boxentriq.com/code-breaking/vigenere-cipher) 
<br />

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_3.png)

Gives us the text but the flag is not accurate though we get the automatic generated key.Using the same key on the [CyberChef Tool](https://gchq.github.io/CyberChef/)  
gives the proper flag format..

![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_3.png)


```Flag- ```


##  WebFugu
---
>A new site listing the different species of fugu fish has appeared on the net. Used by many researchers, it is nevertheless vulnerable. Find the vulnerability and exploit it to recover some of the website configuration.
Creator: MasterFox
http://webfugu.sharkyctf.xyz




![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_3.png) 
-->


One of the file contain flag.txt which have flag in base64


![Sharky CTF]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/sharkyctf/2_3.png)


``` Flag-   ```


<br>
<br>

<i>Thanks for your patience,I hope you enjoyed reading. Happy Hacking... </i>
