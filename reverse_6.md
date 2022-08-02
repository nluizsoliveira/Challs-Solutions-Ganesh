After de-compiling the file, I noticed a function with `flag` in its name:

```

void __stack_chk_fail(void)

{
                    // WARNING: Subroutine does not return
  __stack_chk_fail();
}


void printFlag(void)

{
  long in_FS_OFFSET;
  int local_2c;
  undefined8 local_28;
  undefined8 local_20;
  undefined2 local_18;
  undefined local_16;
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  local_28 = 0x707b6873656e6147;
  local_20 = 0x706d756a5f306730;
  local_18 = 0x7233;
  local_16 = 0x7d;
  for (local_2c = 0; local_2c < 0x13; local_2c = local_2c + 1) {
    putchar((int)*(char *)((long)&local_28 + (long)local_2c));
  }
  putchar(10);
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    // WARNING: Subroutine does not return
    __stack_chk_fail();
  }
  return;
}
```

It's not called by `main()`. I tried calling the function in `main()` and recompiling it, but got **a lot of errors**.

Therefore I tried using gdb, according to https://bestestredteam.com/2020/05/01/calling-functions-with-gdb/:

```
gdb pogo
```

When using `info functions`, I see printFlag there:

```
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  putchar@plt
0x0000000000001040  __stack_chk_fail@plt
0x0000000000001050  printf@plt
0x0000000000001060  _start
0x0000000000001090  deregister_tm_clones
0x00000000000010c0  register_tm_clones
0x0000000000001100  __do_global_dtors_aux
0x0000000000001150  frame_dummy
0x0000000000001159  printFlag
0x00000000000011de  main
0x0000000000001200  __libc_csu_init
0x0000000000001270  __libc_csu_fini
0x0000000000001278  _fini
```

However when I try to call it, either using:

```
print (void) printFlag()
```

or

```
call printFlag()
```

I get an error: You can't do that without a process to debug. According to https://stackoverflow.com/questions/48608134/gdb-calling-a-function-that-is-not-in-main, it turns out I need to:
1-  create a breakpoint in main 
```
break main
```
2- run the program, that will stop at breakpoint
```
run
```
3- finally call the function

```
call (void) printFlag()
```

which prints the flag
