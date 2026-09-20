# Level 0
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. 

**User:** `bandit0`  
**Password:** `bandit0`  
**Command:** `ssh andit0@bandit.labs.overthewire.org -p 2220`

# Level 0 → Level 1
The password for the next level is stored in a file called readme located in the home directory.


**User:** `bandit0`  
**Password:** `bandit0`  
**Command:** `ls , cat  readme`

# Level 1 → Level 2
The password for the next level is stored in a file called - located in the home directory

**User:** `bandit1`  
**Password:** `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR`  
**Command:** `cat ./-`


# Level 2 → Level 3
The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

**User:** `bandit2`  
**Password:** `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`  
**Command:** `cat /home/”--spaces in this filename–”`

# Level 3 → Level 4
The password for the next level is stored in a hidden file in the inhere directory.

**User:** `bandit3`  
**Password:** `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`  
**Command:** `ls -a`

# Level 4 → Level 5
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

**User:** `bandit4`  
**Password:** `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`  
**Command:** `cat ./-file07`


# Level 5 → Level 6
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

**User:** `bandit5`  
**Password:** `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`  
**Command:** `find inhere -type f -size 1033c ! -executable`
`cat inhere/maybehere07/.file2`

# Level 6 → Level 7
The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7
owned by group bandit6
33 bytes in size	

**User:** `bandit6`  
**Password:** `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`  
**Command:** `find / -type f -user bandit7 -group bandit6 2>/dev/null`
`cat  /filepath`

# Level 7 → Level 8
The password for the next level is stored in the file data.txt next to the word millionth

**User:** `bandit7`  
**Password:** `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`  
**Command:** `grep “millionth ” data.txt`

# Level 8 → Level 9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

**User:** `bandit8`  
**Password:** `VR1ljMayciFxbnUokuQmJFw6QC9VKtub`  
**Command:** `sort data.txt | uniq - u`

# Level 9 → Level 10
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

**User:** `bandit9`  
**Password:** `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl`  
**Command:**

# Level 10 → Level 11
The password for the next level is stored in the file data.txt, which contains base64 encoded data

**User:** `bandit10`  
**Password:** `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG`  
**Command:**

# Level 11 → Level 12

# Level 12 → Level 13

# Level 13 → Level 14

# Level 14 → Level 15

# Level 15 → Level 16

# Level 16 → Level 17

# Level 17 → Level 18

# Level 18 → Level 19

# Level 19 → Level 20

# Level 20 → Level 21

# Level 21 → Level 22

# Level 22 → Level 23

# Level 23 → Level 24

# Level 24 → Level 25

# Level 25 → Level 26

# Level 26 → Level 27

# Level 27 → Level 28

# Level 28 → Level 29

# Level 29 → Level 30

# Level 30 → Level 31

# Level 31 → Level 32

# Level 32 → Level 33

# Level 33 → Level 34
