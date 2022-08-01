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
## bandit7 -> bandit8
The password for the next level is stored in the file data.txt next to the word millionth.

The command **grep** can find a string in a file, with the following sintax:

grep 'string' file_path

so

```
grep 'millionth' data.txt
```

returns 

### Ganesh bandit8 password: cvX2JJa4CFALtqS87jk27qwqGhBM9plV
---------------------------------------------------------------
## bandit8 -> bandit9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

As found in https://stackoverflow.com/questions/13778273/find-unique-lines, 

```
sort data.txt | uniq -u 
```

finds the unique line, which is

### Gansh bandit9 password: UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

---------------------------------------------------------------
## bandit9 -> bandit10
A senha para o próximo nível está armazenada no arquivo "data.txt:" em uma das poucas linhas legíveis para humanos (human-readable), é precedida por vários caracteres de ‘=’

according to https://unix.stackexchange.com/questions/217936/equivalent-command-to-grep-binary-files, using strings is better for handling binary data before passing it to grep. Therefore: 

```
strings data.txt | grep '='
```

finds
```
========== the*2i"4
=:G e
========== password
<I=zsGi
Z)========== is
A=|t&E
Zdb=
c^ LAh=3G
*SF=s
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
S=A.H&^
```
### Ganesh bandit10 password: truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

---------------------------------------------------------------
## bandit10 -> bandit11
The password for the next level is stored in the file data.txt, which contains base64 encoded data

According to https://linuxhint.com/bash_base64_encode_decode/, it's possible to use `base64` script with flag `--decode` to decode a file. Simply redirect `cat` output to decode. 

```bash
cat data.txt | base64 --decode
```
### Ganesh bandit11 password: IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

---------------------------------------------------------------
## bandit11 -> bandit12
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

according to the wiki article, the command **tr** replaces a letter for other. Therefore, using de regex range sintax it's possible to generate two alphabets, the second one shifted 13 positions, and pass it to tr. THerefore, 
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
### Ganesh bandit12 password: 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

---------------------------------------------------------------
## bandit12 -> bandit13
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

It's not possible to write files in current folder. Before everything, we need to copy data.txt to /tmp/bingo

```
mkdir /tmp/bingo
cp data.txt /tmp/bingo
cd /tmp/bingo
```

According to https://www.systutorials.com/docs/linux/man/1-xxd/, to reverse a hexdump we need to:

```
xxd -r data.txt
```

this will result in: 

```
P�^data2.bin=��BZh91AY&SY�O����ڞOv���}?��}��^���������ߣ��;�����4���h�F�F��4LM
                                                                             @��z��FM��C�hF�C@�4@f��h
4hh��=C%�>X�,�k���1��GY��hPh�Mh
�J�쌑Oϊ��{RBp�Qix�Y�Z!d��j�(�搿ݳ��/��A�#�A�F��0P��v��`�"3�

                                          ��d�bX?��z��2��<��A �n}
5(3A��
      wO�R����6�XS{�
��9?L�P�yB��=z�m?�L�Nt*�7{qP��̜�%"�w9�qm4�� N3�6���K��H䋑[��}!
                                                             d��3A4$�M~�\ɠJ�C�kUƦ\���\�FSN��&=�[��q	\)�$:��H�t&/�(����]��BB9<s ��h=
```

According to https://stackoverflow.com/questions/19120676/how-to-detect-type-of-compression-used-on-the-file-if-no-file-extension-is-spe, it's possible to discover the kind of compression used over a binary filing using `file` command. Before doing that, we need to save the return of reverse-dumping into a file:

```
xxd -r data.txt > bin
file bin
```

That results in: 
```
bin: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```

According to https://linuxize.com/post/how-to-unzip-gz-file/, ```gzip -d file.gz``` decompresses a file. 

if we try: 

```
gzip -d bin
```

error `gzip: bin: unknown suffix -- ignored` is thrown. According to [ https://www.linuxquestions.org/questions/linux-software-2/gunzip-unknown-suffix-ignored-940698/, using --force forces the decompression. ](https://superuser.com/questions/544153/when-using-gzip-decompress-the-result-is-gzip-myfile-zip-unknown-suffix), gzip only works if file has a `gz` extension. 

We need to rename it first.

```
mv bin bin.gz
gzip -d bin.gz
```

This will make `bin.gz` become a `bin` file. We can use `file` on `bin` again:

```
file bin
```
which results in `bin: bzip2 compressed data, block size = 900k`

According to https://superuser.com/questions/480950/how-to-decompress-a-bz2-file, `bzip2 -d filename.bz2` decompresses a bzip2 compresses file. We need to rename bin again before doing that: 

```
mv bin bin.bz2
bzip2 -d bin.bz2
```
This will again make `bin.bz2` become a decompressed `bin` file. Using `file` on it reveals:

```
file bin
```

```
bin: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```

Doing again: 
```
mv bin bin.gz
gzip -d bin.gz
```

results in another `bin` file, which is:

```
file bin
```

`bin: POSIX tar archive (GNU)`. 

According to https://stackoverflow.com/questions/15744023/how-to-extract-filename-tar-gz-file, `tar xvf filename.tar` decompresses a .tar file. 

```
mv bin bin.tar
tar xvf bin.tar
```

This will generate a `data5.bin` file. 
using `file` on it: 

```
file data5.bin
```
results in data5.bin: POSIX tar archive (GNU). Renaming and decompressing it again: 

```
mv data5.bin data5.tar
tar xvf data5.tar
```

Results in a `data6.bin` file. Using `file`:

```
data6.bin: bzip2 compressed data, block size = 900k
```

Renaming and De-compressing (again!!!!!):

```
mv data6 data6.bz2
bzip2 -d data6.bz2
```

will result in a `data6` file. Using `file` on it: 

```
file data6
```
returns `data6: POSIX tar archive (GNU)`. Renaming to tar and decompressint (again!!!!!!!!!!!!):

```
mv data6 data6.tar
tar xvf data6.tar
```

results in a `data8` file. Using file on it: 

```
data8.bin: gzip compressed data, was "data9.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
```

re-naming and decompressing again: 

```
mv data8 data8.gz
gzip -d data8.gz
```

will result in `data8` file. Using file:

```
file data8
data8: ASCII text
```

finally!!!!:
```
cat data8
```

### Ganesh bandit12->13 password: 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
--------------------------------------------------------------------------
## bandit13 -> bandit14
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on


There is a `ssh.private` file on bandit13 home. If we try to `cat  /etc/bandit_pass/bandit14 `, we receive an error, as bandit13 user has no reading permissions for the file. We need to log into `bandit14` user using the `ssh.private`file. 

According to https://unix.stackexchange.com/questions/23291/how-to-ssh-to-remote-server-using-a-private-key, we need to use the `-i` flag on ssh command and pass the private key file. For instance:

```
ssh -i sshkey.private bandit14@localhost
```

This will long into `bandit14`. After that, simplye 

```
cat  /etc/bandit_pass/bandit14
```
### bandit13->14 password: 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
--------------------------------------------------------------------------
## bandit14 -> bandit15
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

According to https://stackoverflow.com/questions/11564841/send-data-to-a-port-via-linux-command, NC program allows submiting data to a port

According to https://linuxhint.com/send-receive-messages-nc-linux/, we can send text data to a host/port using:

```
echo [text] | netcat host port```
```

therefore, 
```
echo 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e | nc localhost 30000
```
This returns the password:
### bandit 14->15 password: BfMYroe26WYalil77FoDi9qh59eK5xNr

