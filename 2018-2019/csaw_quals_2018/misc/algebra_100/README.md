# Algebra (100): misc

## Information

*CTF*: CSAW Quals 2018

*Category*: Misc

*Point Value*: 100

*Writeup Author*: github.com/nalshihabi


We connect to the port for the challenge and are greeted with this message:
```
  ____                                     __ _           _            ___ ___
 / ___|__ _ _ __     _   _  ___  _   _    / _(_)_ __   __| |  __  __  |__ \__ \
| |   / _` | '_ \   | | | |/ _ \| | | |  | |_| | '_ \ / _` |  \ \/ /    / / / /
| |__| (_| | | | |  | |_| | (_) | |_| |  |  _| | | | | (_| |   >  <    |_| |_|
 \____\__,_|_| |_|   \__, |\___/ \__,_|  |_| |_|_| |_|\__,_|  /_/\_\   (_) (_)
                     |___/
**********************************************************************************
X + 8 = 151
What does X equal?:
```

So, it would seem that to solve this challenge, we need to solve algebraic equations. This can be annoying and difficult to writeup, unless, of course, there happens to be a library already for it. There just so happens to be! Python has a library called SymPy:

https://docs.sympy.org/latest/modules/solvers/solvers.html

So pretty much from here it is straightforward what to do: implement this library to read input from the challenge and solve each equation. Here is the script we hacked up:

```Python
import socket

from sympy import *
from sympy.parsing.sympy_parser import parse_expr

HOST = 'misc.chal.csaw.io'
PORT = 9002

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect((HOST, PORT))


def readuntil(sock, val):
    s = []
    while True:
        v = sock.recv(1)
        if v == val:
            break
        s.append(v)
    return b"".join(s)


def readline(sock, thing=b""):
    if len(thing) == 0:
        s = []
        while True:
            v = sock.recv(1)
            if v == b"\n":
                break
            s.append(v)
        return b"".join(s)
    else:
        return sock.recv(len(thing) + 1).strip()

for i in range(7):
    readline(sock)

x = symbols("X")

while True:
    eq = [_.decode("utf-8") for _ in readline(sock).split(b"=")]
    print(eq)
    string = readuntil(sock, b"?")
    readuntil(sock, b":")
    answer = solveset(Eq(parse_expr(eq[0]), parse_expr(eq[1])), x)
    print(answer)
    my_answer = eval(str(answer)[1:-1])
    print(my_answer)
    sock.send(bytes(str(my_answer), "utf-8") + b"\n")
    print(readline(sock))
    print("\n")
```

We ran this script and then eventually got the flag spat out to us:
```
flag{y0u_s0_60od_aT_tH3_qU1cK_M4tH5}
```
