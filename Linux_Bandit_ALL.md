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

There are 9 files in the folder: 
```
ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
```
I searched about doing a for in bash, printing variables and printing newlines. Than did: 

```bash
for i in $(seq 0 9); do echo "$i ----------"; cat "./-file0$i";echo ""; done
```
Enter bandit4 user
```bash
for i in $(seq 0 9); do echo "$i ---------------------------"; cat "./-file0$i";echo ""; done
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
### Ganesh bandit4 flag: `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`
