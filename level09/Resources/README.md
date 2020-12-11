<<<<<<< Updated upstream
=======
```bash
level09@SnowCrash:~$ ./level09 0000000000000000000000000000000000
0123456789:;<=>?@ABCDEFGHIJKLMNOPQ
level09@SnowCrash:~$ 
```


```bash
level09@SnowCrash:~$ hexdump -C token 
00000000  66 34 6b 6d 6d 36 70 7c  3d 82 7f 70 82 6e 83 82  |f4kmm6p|=..p.n..|
00000010  44 42 83 44 75 7b 7f 8c  89 0a                    |DB.Du{....|
```

```bash
level09@SnowCrash:/tmp$ cat main.c
#include <stdlib.h>
#include <stdio.h>

int main(int argc, char const *argv[])
{
    char lol[] = { 
        0x66, 0x34, 0x6b, 0x6d, 0x6d, 0x36, 0x70, 0x7c, 0x3d, 0x82,
        0x7f, 0x70, 0x82, 0x6e, 0x83, 0x82, 0x44, 0x42, 0x83, 0x44, 
        0x75, 0x7b, 0x7f, 0x8c, 0x89, 0x0a, 0x0
    };
    int i = 0;
    while(lol[i] != '\0') {
        printf("%c",lol[i] - i);
        i++;
    }
    printf("\n");
    return 0;
}

level09@SnowCrash:/tmp$ gcc -o prog  main.c
level09@SnowCrash:/tmp$ ./prog
f3iji1ju5yuevaus41q1afiuq
level09@SnowCrash:~$ su flag09
Password: 
Don't forget to launch getflag !
flag09@SnowCrash:~$ getflag
Check flag.Here is your token : s5cAJpM8ev6XHw998pRWG728z
```
>>>>>>> Stashed changes
