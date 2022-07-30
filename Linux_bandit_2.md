Enter bandit1 user with
```
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Type password discovered in bandit_1
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

```
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
