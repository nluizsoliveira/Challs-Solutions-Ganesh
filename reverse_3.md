I first ran `entenda-me` program, which printed: 

```
printf("Ganesh{%d_eh_a_resposta}", func(10));
```

then, I used `Ghidra` to analize the program, which showed eventually: 

```
int func(int param_1)

{
  int iVar1;
  int iVar2;
  
  if (param_1 == 1) {
    iVar2 = 1;
  }
  else if (param_1 == 2) {
    iVar2 = 1;
  }
  else {
    iVar1 = func(param_1 + -1);
    iVar2 = func(param_1 + -2);
    iVar2 = iVar2 + iVar1;
  }
  return iVar2;
}

```

I compiled the program, ran it with 10, which resulted 55.
