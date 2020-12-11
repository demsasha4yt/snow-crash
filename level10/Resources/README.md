```bash
level10@SnowCrash:~$ ltrace ./level10 token localhost
__libc_start_main(0x80486d4, 3, 0xbffff7e4, 0x8048970, 0x80489e0 <unfinished ...>
access("token", 4)                                                                                                                             = -1
printf("You don't have access to %s\n", "token"You don't have access to token
)   
```
