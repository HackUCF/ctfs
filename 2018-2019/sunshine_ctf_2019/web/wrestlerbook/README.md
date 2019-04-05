
# **Web Challenge: WrestlerBook**

This was a Web Challenge from Sunshine CTF 2019. So we load the website and we are prompted with a login page:

![](https://i.imgur.com/814w35X.jpg)

I immediately check to see if we can attack the login page with any SQLi:

![](https://i.imgur.com/iEae04m.png)

Now that we are aware that there is SQL injection on the page I proceed to give it the typical injection: `admin' or 1=1 -- `

![](https://i.imgur.com/SbkuXON.jpg)

Andddd....we manage to login: ![](https://i.imgur.com/m4XC8Mf.png)

but no flag :( :-1:. So we know that we can login using SQL injection and we logged in with Hulk Hogan, so there may be other users and if you know how a database works. We can use other attacks in our SQL injection to test that as well.

![](https://i.imgur.com/Pu2N58O.jpg)
 
 I proceed to logout and check my theory: `admin' or 1=1 limit 1 offset 1 -- ` which essentially we are checking the next row in the database to prove that the theory is true. And voilaaaa it works:
 
 ![](https://i.imgur.com/qMg0vku.png)

we logged into the Nature boy's profile but no flag.....hmmmmmm. So if its not in his profile it may be in another profile, but I'm not too sure which one it is so I decide to boot up Burpsuite and catch the POST request:

![](https://i.imgur.com/NjkYKnx.png)

I send it to intruder and we will run a sniper attack, and essentially what intruder does is that it's a tool for automating customized attacks against web app and we will take advantage of the POST request and iterate through all the profiles which there were only like 100 so that shouldn't take too long....

![](https://i.imgur.com/JdaGgYi.png)


We set the payload to every digit 1 - 100 and start the attack: 

![](https://i.imgur.com/FzoCwpo.png)

And evidently after a minute or so we got the flag:

![](https://i.imgur.com/856jq6t.png)

FLAG: sun{ju57_4n07h3r_5ql1_ch411}


 



