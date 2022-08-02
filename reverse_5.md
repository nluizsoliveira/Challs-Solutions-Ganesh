After de-compiling with ghidra, this seems to be the function used to  generate the random key

It uses ascii index 

```
{
  char local_c;
  
  local_c = param_1;
  if (('`' < param_1) && (param_1 < '{')) {
    local_c = param_1 + '\x03';
  }
  return (int)local_c;
}

```
![image](https://user-images.githubusercontent.com/49366837/182269589-e9bee308-dae7-4809-8797-b6af23f45d6e.png)

int scramble(char param_1)

if the character is between  ```(`, {)```, it's shifting character 3 positions. 

the string given by compiling program is: 

jdqhvk{dyh_fdhvdu}

both { and } characters are out of the range. They stay the same. 

the rest of characters is in range and must be shifted 3 positions left. 

Which results in ganesh{ave_caesar}

