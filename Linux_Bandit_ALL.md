# Bandit Solutions
https://overthewire.org/wargames/bandit/
Bandit is a chall website. It provides an ssh server, with different users and passwords. 

The users are sequential (bandit0, bandit1, bandit2, ...).

The goal is to find the n+1 password in banditn user. 

Ganesh's chall password are bandits passwords.
-------------------------------------------------------------------------------------------

## Bandit 0 (Ganesh bandit0): 
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

- Host: bandit.labs.overthewire.org
- user: bandit0
- password: bandit0
- port: 2220

Usually SSH connections go by port 22. We need to add an extra option to ssh, which is `ssh user@domain`. So, the solution is:


```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```


### Ganesh bandit0 flag: `bandit0`
-------------------------------------------------------------------------------------------
## Bandit 0->1 (Ganesh bandit1)
The password for the next level is stored in a file called - located in the home directory

Do: 

```
ls
cat readme
```

the file contains the password of bandit1 user. 
### Ganesh bandit1 flag: `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`
-------------------------------------------------------------------------------------------

## Bandit 1->2 (Ganesh bandit2)
The password for the next level is stored in a file called - located in the home directory
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Type password discovered in bandit0->bandit1, `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`.
There will be a file named
```
-
```
on bandit1 user initial folder. It's not possible to do:

```
cat -
```
because `-` is a reserved unix word for parameters. After looking up on stackoverflow, I did

```
cat ./-
```

which worked. The password for bandit2 is:

### Ganesh bandit2 flag: `CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9`
-------------------------------------------------------------------------------------------

## Bandit 2->3 (Ganesh bandit3)
The password for the next level is stored in a file called spaces in this filename located in the home directory

Enter bandit2 user
```
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

cat refeals a file named: 
```
spaces in this filename
```

spaces need to be scaped in order to access file. This can be done easily using `tab <->` key. 

```
cat spaces\ in\ this\ filename
```

### Ganesh bandit3 flag: `UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`
-------------------------------------------------------------------------------------------

## Bandit 3-> 4 (Ganesh bandit4)
The password for the next level is stored in a hidden file in the inhere directory.

Enter bandit3 user
```
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

there's a folder named inhere. Enter it
```
cd inhere/
```

There's a hidden file on the folder. Use 

`ls -a`
to find it. It's named `.hidden`. `Cat` it.

### Ganesh bandit4 flag: `pIwrPrtPN36QITSp3EQaw936yaFoFgAB`

-------------------------------------------------------------------------------------------

## Bandit 4-> 5 (Ganesh bandit5)
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Enter bandit4 user
```
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

There are 9 files in the folder: 
```
ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
```
I searched about doing for loops in bash, printing variables and printing newlines. Than did: 
```bash
for i in $(seq 0 9); do echo "$i ---------------------------"; cat "./-file0$i";echo ""; done
```

which outputed
```bash
0 ---------------------------
�/`2ғ�%��rL~5�g��� �����
1 ---------------------------
��p,k�;��r*��	�.!��C��J	�dx,�
2 ---------------------------
e�)�#��5��
          ��p��V�_���ׯ�mm
3 ---------------------------
������h!TQO�`�4"aל�߂phT��,�A
4 ---------------------------
?�4�ו$����I&������c���ގ.�
5 ---------------------------
�r�l$�?h�9('���!y�e�#�x�O��=��
6 ---------------------------
ly���~��A�f����-E�{���m�����ܗM
7 ---------------------------
koReBOKuIDDepwhWk7jZC0RTdopnAYKh

8 ---------------------------
�T�?�i��j��îP�F�l�n��J����{��@
9 ---------------------------
�e�0$�in=��_b�5FA�P7sz��gNT

```

FIle 7 contains the only readable string, which is the password. 
### Ganesh bandit5 flag: `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`
-------------------------------------------------------------------------------------------

## Bandit 5-> 6 (Ganesh bandit6)
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

    human-readable
    1033 bytes in size
    not executable


Enter bandit5 user
```
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

Step 1: Figuring out a wai to find all files under a directory
- `find .` finds all files under a directory, recursively
Step 2: Finding all non-executable files under a directory
- `find` has a param `-perm` that allows searching for permissions. 
    - `-perm` can be refined through `-` and `/.
           ```

              find -perm -mode:

              In this case the permission bits mentioned must be present for the file. For example, if you do find -perm -666 and if a file has 776, it will be matched. Similarly 666, 777 etc will be matched too, but 665 won't be matched. In summary, the mentioned (three) bits must be a subset of the permission bits.

              find -perm /mode:

              Here any one bit of subset would do. For example, if we do find -perm /666, and if a file has 644, the file will be matched because the user permission bit is 6, and we are looking for a single bit subset. Similarly, 700, 060, 006 etc will be matched, but not e.g. 444, as no bit contains any subset of the required permission bits.
          ```
![](https://danielmiessler.com/images/permissions.png)
     - I started querying **all executable files by user, group or owner: /111**
     - `find . -perm -111`
     - Then **negated** the condition with ! to find not executables.
     - `find . ! -perm -111`
- find can also filtrate by size: 
![](https://i.imgur.com/n12C7kt.png)   
therefore 
```bash
find . -size 1033c ! -perm /111
./maybehere07/.file2
```
was the query utilized. The content of `./maybehere07/.file2` is:



### Ganesh bandit6 flag: `DXjZPULLxYr17uwoI01bNLQbtFemEgo7`

-------------------------------------------------------------------------------------------
## Bandit 6->7
```
find . -type f  -size 33c -user bandit7 -group bandit6
```
returns
```
find: ‘./root’: Permission denied
find: ‘./home/bandit28-git’: Permission denied
find: ‘./home/bandit30-git’: Permission denied
find: ‘./home/bandit5/inhere’: Permission denied
find: ‘./home/bandit27-git’: Permission denied
find: ‘./home/bandit29-git’: Permission denied
find: ‘./home/bandit31-git’: Permission denied
find: ‘./lost+found’: Permission denied
find: ‘./etc/ssl/private’: Permission denied
find: ‘./etc/polkit-1/localauthority’: Permission denied
find: ‘./etc/lvm/archive’: Permission denied
find: ‘./etc/lvm/backup’: Permission denied
find: ‘./sys/fs/pstore’: Permission denied
find: ‘./proc/tty/driver’: Permission denied
find: ‘./proc/17610/task/17610/fdinfo/6’: No such file or directory
find: ‘./proc/17610/fdinfo/5’: No such file or directory
find: ‘./cgroup2/csessions’: Permission denied
find: ‘./boot/lost+found’: Permission denied
find: ‘./tmp’: Permission denied
find: ‘./run/lvm’: Permission denied
find: ‘./run/screen/S-bandit16’: Permission denied
find: ‘./run/screen/S-bandit33’: Permission denied
find: ‘./run/screen/S-bandit5’: Permission denied
find: ‘./run/screen/S-bandit11’: Permission denied
find: ‘./run/screen/S-bandit20’: Permission denied
find: ‘./run/screen/S-bandit13’: Permission denied
find: ‘./run/screen/S-bandit29’: Permission denied
find: ‘./run/screen/S-bandit1’: Permission denied
find: ‘./run/screen/S-bandit25’: Permission denied
find: ‘./run/screen/S-bandit30’: Permission denied
find: ‘./run/screen/S-bandit9’: Permission denied
find: ‘./run/screen/S-bandit28’: Permission denied
find: ‘./run/screen/S-bandit18’: Permission denied
find: ‘./run/screen/S-bandit7’: Permission denied
find: ‘./run/screen/S-bandit26’: Permission denied
find: ‘./run/screen/S-bandit15’: Permission denied
find: ‘./run/screen/S-bandit4’: Permission denied
find: ‘./run/screen/S-bandit19’: Permission denied
find: ‘./run/screen/S-bandit31’: Permission denied
find: ‘./run/screen/S-bandit17’: Permission denied
find: ‘./run/screen/S-bandit22’: Permission denied
find: ‘./run/screen/S-bandit21’: Permission denied
find: ‘./run/screen/S-bandit14’: Permission denied
find: ‘./run/screen/S-bandit24’: Permission denied
find: ‘./run/screen/S-bandit23’: Permission denied
find: ‘./run/shm’: Permission denied
find: ‘./run/lock/lvm’: Permission denied
find: ‘./var/spool/bandit24’: Permission denied
find: ‘./var/spool/cron/crontabs’: Permission denied
find: ‘./var/spool/rsyslog’: Permission denied
find: ‘./var/tmp’: Permission denied
find: ‘./var/lib/apt/lists/partial’: Permission denied
find: ‘./var/lib/polkit-1’: Permission denied
./var/lib/dpkg/info/bandit7.password
find: ‘./var/log’: Permission denied
find: ‘./var/cache/apt/archives/partial’: Permission denied
find: ‘./var/cache/ldconfig’: Permission denied
```

the only file is `./var/lib/dpkg/info/bandit7.password`, which contains: 

### Ganesh Bandit7 flag: HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
----------------------------------------------------------------
