Bandit is a chall website. 
It provides an ssh server, with different users and passwords. 
The users are sequential (bandit0, bandit1, bandit2, ...).
The goal is to find the n+1 password in banditn user. 

For example, the first challange is to connect to bandit0 through SSH, using following credentials: 
- Host: bandit.labs.overthewire.org
- user: bandit0
- password: bandit0
- port: 2220

Usually SSH connections go by port 22. We need to add an extra option to ssh, which is `ssh user@domain`. So, the solution is:


```
ssh bandit0@bandit.labs.overthewire.org -p 22
```

ssh will ask for password (bandit0). You'll start at a folder with an `readme` file. 

Do: 

```
cat readme
```

the file contains boJ9jbbUNNfktd78OOpsqOltutMc3MY1, which is the password for bandit1 user. 