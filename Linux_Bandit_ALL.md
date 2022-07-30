# Bandit Solutions
https://overthewire.org/wargames/bandit/
Bandit is a chall website. 
It provides an ssh server, with different users and passwords. 
The users are sequential (bandit0, bandit1, bandit2, ...).
The goal is to find the n+1 password in banditn user. 

Ganesh's chall password are bandits passwords.

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

## Bandit 0->1 (Ganesh bandit1)
The password for the next level is stored in a file called - located in the home directory

Do: 

```
ls
cat readme
```

the file contains the password of bandit1 user. 
### Ganesh bandit1 flag: `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`

## Bandit 1->2
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

## Bandit 2->3 (Ganesh bandit3)
The password for the next level is stored in a file called spaces in this filename located in the home directory


