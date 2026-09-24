# Level 0
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. 

**Status:** `IncComplet`  
**User:** `bandit0`  
**Password:** `bandit0`  
**Command:** `ssh bandit0@bandit.labs.overthewire.org -p 2220`

# Level 0 → Level 1
The password for the next level is stored in a file called readme located in the home directory.

**Status:** `Completed`  
**User:** `bandit0`  
**Password:** `bandit0`  
**Command:** `ls , cat  readme`

# Level 1 → Level 2
The password for the next level is stored in a file called - located in the home directory

**Status:** `Completed`  
**User:** `bandit1`  
**Command:** `cat ./-`


# Level 2 → Level 3
The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

**Status:** `Completed`  
**User:** `bandit2`  
**Command:** `cat /home/”--spaces in this filename–”`

# Level 3 → Level 4
The password for the next level is stored in a hidden file in the inhere directory.

**Status:** `Completed`  
**User:** `bandit3`  
**Command:** `ls -a`

# Level 4 → Level 5
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

**Status:** `Completed`  
**User:** `bandit4`  
**Command:** `cat ./-file07`


# Level 5 → Level 6
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

**Status:** `Completed`  
**User:** `bandit5`  
**Command:** `find inhere -type f -size 1033c ! -executable`
`cat inhere/maybehere07/.file2`

# Level 6 → Level 7
The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7
owned by group bandit6
33 bytes in size	

**Status:** `Completed`  
**User:** `bandit6`  
**Command:** `find / -type f -user bandit7 -group bandit6 2>/dev/null`
`cat  /filepath`

# Level 7 → Level 8
The password for the next level is stored in the file data.txt next to the word millionth

**Status:** `Completed`  
**User:** `bandit7`  
**Command:** `grep “millionth ” data.txt`

# Level 8 → Level 9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

**Status:** `Completed`  
**User:** `bandit8`  
**Command:** `sort data.txt | uniq - u`

# Level 9 → Level 10
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

**Status:** `Completed`  
**User:** `bandit9`  
**Command:** `strings data.txt | grep "======="`

# Level 10 → Level 11
The password for the next level is stored in the file data.txt, which contains base64 encoded data

**Status:** `Completed`  
**User:** `bandit10`  
**Command:** `base64 -d data.txt`


# Level 11 → Level 12
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

**Status:** `Completed`  
**User:** `bandit11`  
**Command:** `cat data.txt |tr "N-ZA-Mn-za-m" "A-Za-z" `


# Level 12 → Level 13
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

**Status:** `Completed`  
**User:** `bandit12`  
**Command:** `mktemp -d , cp ~/data.txt . ,xxd -r data.txt data ,file data`

# Level 13 → Level 14
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
If you need help with this level: a hint file can be found in the home directory.
Make sure to read the error messages as they are informative.

**Status:** `Completed`  
**User:** `bandit1`  
**Command:**

# Level 14 → Level 15


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 15 → Level 16


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 16 → Level 17


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 17 → Level 18


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 18 → Level 19


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 19 → Level 20


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 20 → Level 21


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 21 → Level 22


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 22 → Level 23


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 23 → Level 24


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 24 → Level 25


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 25 → Level 26


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 26 → Level 27


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 27 → Level 28


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 28 → Level 29


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 29 → Level 30


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 30 → Level 31


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 31 → Level 32


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 32 → Level 33


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**

# Level 33 → Level 34


**Status:** `IncComplet`  
**User:** `bandit1`  
**Command:**
