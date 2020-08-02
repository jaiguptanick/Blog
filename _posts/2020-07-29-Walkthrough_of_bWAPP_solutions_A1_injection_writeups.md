---
layout: post
published: true
title: "A1-Injection | Solutions of bWAPP | Walkthrough of All Levels"
date: 2020-07-29 23:32:20 +0300
description: Solutions of HTML Injection - Reflected (GET), HTML Injection - Reflected (POST), HTML Injection - Reflected (Current URL), HTML Injection - Stored (Blog), iFrame Injection, LDAP Injection (Search), Mail Header Injection (SMTP), OS Command Injection, OS Command Injection - Blind, PHP Code Injection, Server-Side Includes (SSI) Injection, SQL Injection (GET/Search), SQL Injection (GET/Select), SQL Injection (POST/Search), SQL Injection (POST/Select), SQL Injection (AJAX/JSON/jQuery), SQL Injection (CAPTCHA), SQL Injection (Login Form/Hero), SQL Injection (Login Form/User), SQL Injection (SQLite), SQL Injection (Drupal), SQL Injection - Stored (Blog), SQL Injection - Stored (SQLite), SQL Injection - Stored (User-Agent), SQL Injection - Stored (XML), SQL Injection - Blind - Boolean-Based, SQL Injection - Blind - Time-Based, SQL Injection - Blind (SQLite), SQL Injection - Blind (Web Services/SOAP), XML/XPath Injection (Login Form), XML/XPath Injection (Search).
excerpt: "Writeups of all levels in A1-Injection Catagory such as HTML Injection - Reflected GET, POST, OS Command Injection, SQL Injection and XML Injections"
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
Here is a walkthrough and tutorial of the [bWAPP](http://www.itsecgames.com/) which is a vulnerable web application by itsecgames which you can download and test on your local machine. It has a complete list of OWASP vulnerabilities which we can practially test.<b>The best part of using bWAPP is that it is running on our local system so we have access to its source code, so if we got stuck somewhere then we can analyse its source code as it is very neat and describitive having comments wherever necessary. We can see the function being used to restrict or sanatize the input,then can search for its vulnerablity on the web.</b>

>Hello, today we are going to solve all types of injection of buggy web application such as HTML Injection - Reflected (GET), HTML Injection - Reflected (POST), HTML Injection - Reflected (Current URL), HTML Injection - Stored (Blog), iFrame Injection, LDAP Injection (Search), Mail Header Injection (SMTP), OS Command Injection, OS Command Injection - Blind, PHP Code Injection, Server-Side Includes (SSI) Injection, SQL Injection (GET/Search), SQL Injection (GET/Select), SQL Injection (POST/Search), SQL Injection (POST/Select), SQL Injection (AJAX/JSON/jQuery), SQL Injection (CAPTCHA), SQL Injection (Login Form/Hero), SQL Injection (Login Form/User), SQL Injection (SQLite), SQL Injection (Drupal), SQL Injection - Stored (Blog), SQL Injection - Stored (SQLite), SQL Injection - Stored (User-Agent), SQL Injection - Stored (XML), SQL Injection - Blind - Boolean-Based, SQL Injection - Blind - Time-Based, SQL Injection - Blind (SQLite), SQL Injection - Blind (Web Services/SOAP), XML/XPath Injection (Login Form), XML/XPath Injection (Search).

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

```
%3c%75%3e%75%6e%64%65%6c%69%6e%65%3c%2f%75%3e%20
```

![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get5.png)

Now it worked.

## HTML Injection - Reflected (POST)
---
This is as same as GET just the input is not displayed in the URL and is send securely. 

## HTML Injection - Reflected (Current URL)
---





<!--
	j
``` 
1.There is a user name james.
2.The ssh key to login via SSH.
```
Saving the Key to a file and reduce its permission using ```chmod 400 james.key ``` and then connecting via SSH:


<h3>Privilege Escalation</h3>

``` 
```

```

```
## HTML Injection - Reflected (GET)
---
<h3>Security Level: low</h3>

<h3>Security Level: medium</h3>

<h3>Security Level: high</h3>

<h3><u><b>BONUS</b></u></h3>
Finally, We got a connection from the Box as ROOT. It was really a nice room containing many fundamentals, and I enjoyed solving it and writing its walkthrough.
<br>
<br>

<i>Thanks for your patience, I hope you enjoyed reading. Happy Hacking... </i>
![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get1.png)
![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get1.png)
![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get1.png)
![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get1.png)
![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get1.png)
![HTML Injection get]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a1/get1.png)

-->