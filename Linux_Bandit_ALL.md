# Bandit Solutions

Bandit is a chall website. 
It provides an ssh server, with different users and passwords. 
The users are sequential (bandit0, bandit1, bandit2, ...).
The goal is to find the n+1 password in banditn user. 

## Bandit 0: 
Bandit starts at user **bandit0**, whose passowrd is also **bandit0**. This is public on bandit site. The challange is to connect to bandit0 user to progress using ssh.

### Ganesh bandit0 flag: `bandit0`

## Bandit 1
bandit1 password is inside bandit0 user, which is accesible through ssh, using following credentials: 
- Host: bandit.labs.overthewire.org
- user: bandit0
- password: bandit0
- port: 2220
- 

Usually SSH connections go by port 22. We need to add an extra option to ssh, which is `ssh user@domain`. So, the solution is:


```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

ssh will ask for password (bandit0). You'll start at a folder with an `readme` file. 

Do: 

```
cat readme
```

the file contains the password of bandit1 user. 
### Ganesh bandit1 flag: `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`

## Bandit 2
Enter bandit1 user with
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Type password discovered in bandit_1, `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`.
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

## Bandit 3


