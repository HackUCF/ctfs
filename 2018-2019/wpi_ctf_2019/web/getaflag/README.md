# **Web Challenge: getaflag**

###### tags: `web` `ctf`

This is a web challenge from WPI CTF. We connect to http://getaflag.wpictf.xyz:31337/ and are prompted to guess a password:

![](https://i.imgur.com/um5F2IB.png)

Usally, the first step I take when figuring out a web challenge is trying to understand what it does. I then snoop around the page basically touching every button and eventually checking the source code of the page. So in this challenge I did those first two steps but nothing really happened, so I eventually went on to check the source code of the page where I was able to find some base64 encoded text:

![](https://i.imgur.com/GAm2zc6.png)

I booted up the terminal and decoded it with `echo <insert encoded b64> | base64 -d` and was able to get a clue: 

![](https://i.imgur.com/L7l5lWe.png)

In the clue Goutham forgot to block `http://getaflag.wpictf.xyz:31337/auth.php` so we go investiagate see what we find: 

![](https://i.imgur.com/LlxCrDq.png)

So we end up with some pseudocode that is telling us basically how to guess the correct password so we can get the flag. If you may have never read much php code like me before you can sort of understand what is going on, but the key thing is recognizing that the `extract($_GET)` is known to be a dangerous method. Sending user input data through the extract function can be manipulated to do other things such as viewing files, listing directories, etc.(https://www.php.net/manual/en/function.extract.php). Eventually after messing with it for a while I managed to get the flag by manipulating the input to `http://getaflag.wpictf.xyz:31337/?input=&passcode=1`: 

![](https://i.imgur.com/vZvgmbW.png)

I immediately clicked on the flag and got trolled with the rick roll, but ended up checking out the source code of the page and managed to find the flag hidden in there:

![](https://i.imgur.com/cqYLzfp.png)

Flag: WPI{1_l0v3_PHP}


