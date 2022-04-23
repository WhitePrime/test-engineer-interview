# Базовые команды Linux



### **pwd**

Вывести текущую (рабочую) директорию.

```
[user@testhost ~]$ pwd
/home/user
```

### **date**

Вывести текущую дату и время системы.

```
[user@testhost ~]$ date
Mon Dec 16 13:37:07 UTC 2019
[user@testhost ~]$ date +%s
1576503430
```

### **w**

Данная команда показывает, кто залогинен в системе. Помимо этого также на экран выводится uptime и LA (load average).

```
[user@testhost ~]$ w
 05:47:17 up 377 days, 17:57,  1 user,  load average: 0,00, 0,01, 0,05
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
user     pts/0    32.175.94.241    05:47    2.00s  0.01s  0.00s w
```

### **ls**

Вывести содержимое директории. Если не передать путь, то выведется содержимое текущей директории.

```
[user@testhost ~]$ pwd
/home/user
[user@testhost ~]$ ls
qqq
[user@testhost ~]$ ls /home/user
qqq
[user@testhost ~]$ ls /
bin  boot  cgroup  dev  etc  home  lib  lib64  local  lost+found  media  mnt  opt  proc  root  run  sbin  selinux  srv  swap  sys  tmp  usr  var
```

Лично я часто использую опции

* l

(long listing format — вывод в колонку с дополнительной информацией о файлах),

* t

(сортировка по времени изменения файла/директории) и

* r

(обратная сортировка — в сочетании с

* t

наиболее «свежие» файлы будут внизу):

```
[user@testhost ~]$ ls -ltr /
total 4194416
drwxr-xr-x    2 root root       4096 Jan  6  2012 srv
drwxr-xr-x    2 root root       4096 Jan  6  2012 selinux
drwxr-xr-x    2 root root       4096 Jan  6  2012 mnt
drwxr-xr-x    2 root root       4096 Jan  6  2012 media
drwx------    2 root root      16384 Oct  1  2017 lost+found
drwxr-xr-x    2 root root       4096 Oct  1  2017 local
drwxr-xr-x   13 root root       4096 Oct  1  2017 usr
drwxr-xr-x   11 root root       4096 Apr 10  2018 cgroup
drwxr-xr-x    4 root root       4096 Apr 10  2018 run
-rw-------    1 root root 4294967296 Sep 10  2018 swap
dr-xr-xr-x   10 root root       4096 Dec 13  2018 lib
drwxr-xr-x    6 root root       4096 Mar  7  2019 opt
drwxr-xr-x   20 root root       4096 Mar 19  2019 var
dr-xr-xr-x   10 root root      12288 Apr  9  2019 lib64
dr-xr-xr-x    2 root root       4096 Apr  9  2019 bin
dr-xr-xr-x    4 root root       4096 Apr  9  2019 boot
dr-xr-xr-x    2 root root      12288 Apr  9  2019 sbin
dr-xr-xr-x 3229 root root          0 Jul  2 10:19 proc
drwxr-xr-x   34 root root       4096 Oct 28 13:27 home
drwxr-xr-x   93 root root       4096 Oct 30 16:00 etc
dr-xr-x---   11 root root       4096 Nov  1 13:02 root
dr-xr-xr-x   13 root root          0 Nov 13 20:28 sys
drwxr-xr-x   16 root root       2740 Nov 26 08:55 dev
drwxrwxrwt    3 root root       4096 Nov 26 08:57 tmp
```

Есть 2 специальных имени директории: "

_._

" и "

_.._

". Первое означает текущую директорию, второе — родительскую директорию. Их бывает удобно использовать в различных командах, в частности,

_ls_

:

```
[user@testhost home]$ pwd
/home
[user@testhost home]$ ls ..
bin  boot  cgroup  dev  etc  home  lib  lib64  local  lost+found  media  mnt  opt  proc  root  run  sbin  selinux  srv  swap  sys  tmp  usr  var
[user@testhost home]$ ls ../home/user/
qqq
```

Также есть полезная опция для вывода скрытых файлов (начинаются на "

_._

") —

* a

:

```
[user@testhost ~]$ ls -a
.  ..  1  .bash_history  .bash_logout  .bash_profile  .bashrc  .lesshst  man_signal  man_signal_error_log  .mongorc.js  .ssh  temp  test  .viminfo
```

И еще можно использовать опцию

* h

— вывод в human readable формате (обратите внимание на размеры файлов):

```
[user@testhost ~]$ ls -ltrh
total 16K
-rwxrwx--x 1 user user   31 Nov 26 11:09 temp
-rw-rw-r-- 1 user user 6.0K Dec  3 16:02 1
drwxrwxr-x 2 user user 4.0K Dec  4 10:39 test
```

### **cd**

Изменить текущую директорию.

```
[user@testhost ~]$ pwd
/home/user
[user@testhost ~]$ cd /home/
[user@testhost home]$ pwd
/home
```

Если не передавать имя директории в качестве аргумента, будет использоваться переменная окружения

_$HOME_

, то есть домашняя директория. Также может быть удобно использовать \`

_\~_

\` — специальный символ, означающий

_$HOME_

:

```
[user@testhost etc]$ pwd
/etc
[user@testhost etc]$ cd ~/test/
[user@testhost test]$ pwd
/home/user/test
```

### **mkdir**

Создать директорию.

```
[user@testhost ~]$ mkdir test
[user@testhost ~]$ ls -ltr
total 38184
-rw-rw-r-- 1 user user 39091284 Nov 22 14:14 qqq
drwxrwxr-x 2 user user     4096 Nov 26 10:29 test
```

Иногда нужно создать определенную структуру директорий: например, директорию в директории, которой не существует. Чтобы не вводить несколько раз подряд

_mkdir_

, можно использовать опцию

* p

— она позволяет создать все недостающие директории в иерархии. Также с этой опцией

_mkdir_

не вернет ошибку, если директория существует.

```
[user@testhost ~]$ ls
qqq  test
[user@testhost ~]$ mkdir test2/subtest
mkdir: cannot create directory ‘test2/subtest’: No such file or directory
[user@testhost ~]$ mkdir -p test2/subtest
[user@testhost ~]$ ls
qqq  test  test2
[user@testhost ~]$ ls test2/
subtest
[user@testhost ~]$ mkdir test2/subtest
mkdir: cannot create directory ‘test2/subtest’: File exists
[user@testhost ~]$ mkdir -p test2/subtest
[user@testhost ~]$ ls test2/
subtest
```

### **rm**

Удалить файл.

```
[user@testhost ~]$ ls
qqq  test  test2
[user@testhost ~]$ rm qqq
[user@testhost ~]$ ls
test  test2
```

Опция

* r

позволяет рекурсивно удалять директории со всем их содержимым, опция

* f

позволяет игнорировать ошибки при удалении (например, о несуществующем файле). Эти опции позволяют, грубо говоря, гарантированно удалить всю иерархию файлов и директорий (если на это есть права у пользователя), поэтому, их нужно использовать с осторожностью (классический пример-шутка — "

_rm -rf /_

", при определенных обстоятельствах удалит вам если не всю систему, то очень много важных для её работоспособности файлов).

```
[user@testhost ~]$ ls
test  test2
[user@testhost ~]$ ls -ltr test2/
total 4
-rw-rw-r-- 1 user user    0 Nov 26 10:40 temp
drwxrwxr-x 2 user user 4096 Nov 26 10:40 temp_dir
[user@testhost ~]$ rm -rf test2
[user@testhost ~]$ ls
test
```

### **cp**

Копировать файл или директорию.

```
[user@testhost ~]$ ls
temp  test
[user@testhost ~]$ cp temp temp_clone
[user@testhost ~]$ ls
temp  temp_clone  test
```

У этой команды также есть опции

* r

и

* f

, их можно использовать, чтобы гарантированно скопировать иерархию директорий и папок в другое место.

### **mv**

Переместить или переименовать файл или директорию.

```
[user@testhost ~]$ ls -ltr
total 4
drwxrwxr-x 2 user user 4096 Nov 26 10:29 test
-rw-rw-r-- 1 user user    0 Nov 26 10:45 temp
-rw-rw-r-- 1 user user    0 Nov 26 10:46 temp_clone
[user@testhost ~]$ ls test
[user@testhost ~]$ mv test test_renamed
[user@testhost ~]$ mv temp_clone test_renamed/
[user@testhost ~]$ ls
temp  test_renamed
[user@testhost ~]$ ls test_renamed/
temp_clone
```

### **cat**

Вывести содержимое файла (или файлов).

```
[user@testhost ~]$ cat temp
Content of a file.
Lalalala...
```

Также стоит обратить внимание на команды

_head_

(вывести

_n_

первых строк или байт файла) и

_tail_

(о ней — далее).

### **tail**

Вывести

_n_

последних строк или байт файла.

```
[user@testhost ~]$ tail -1 temp
Lalalala...
```

Очень полезной является опция

* f

— она позволяет выводить новые данные в файле в реальном времени.

### **less**

Иногда текстовый файл слишком большой, и неудобно выводить его командой

_cat_

. Тогда можно открыть его с помощью команды

_less_

: файл будет выводиться по частям, доступна навигация по этим частям, поиск и прочий простой функционал.

```
[user@testhost ~]$ less temp
```

Также может оказаться удобным вариант использования

_less_

с конвейером (

_pipe_

):

```
[user@testhost ~]$ grep "ERROR" /tmp/some.log | less
```

### **ps**

Вывести список процессов.

```
[user@testhost ~]$ ps
    PID TTY          TIME CMD
 761020 pts/2    00:00:00 bash
 809720 pts/2    00:00:00 ps
```

Я сам обычно использую BSD опции "

_aux_

" — вывести все процессы в системе (так как процессов может быть много, я вывел только первые 5 из них, использовав конвейер (

_pipe_

) и команду

_head_

):

```
[user@testhost ~]$ ps aux | head -5
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0  19692  2600 ?        Ss   Jul02   0:10 /sbin/init
root           2  0.0  0.0      0     0 ?        S    Jul02   0:03 [kthreadd]
root           4  0.0  0.0      0     0 ?        I<   Jul02   0:00 [kworker/0:0H]
root           6  0.0  0.0      0     0 ?        I<   Jul02   0:00 [mm_percpu_wq]
```

Многие также используют BSD опции "

_axjf_

", что позволяет вывести дерево процессов (здесь я убрал часть вывода для демонстрации):

```
[user@testhost ~]$ ps axjf
   PPID     PID    PGID     SID TTY        TPGID STAT   UID   TIME COMMAND
      0       2       0       0 ?             -1 S        0   0:03 [kthreadd]
      2       4       0       0 ?             -1 I<       0   0:00  \\_ [kworker/0:0H]
      2       6       0       0 ?             -1 I<       0   0:00  \\_ [mm_percpu_wq]
      2       7       0       0 ?             -1 S        0   4:08  \\_ [ksoftirqd/0]
...
...
...
      1    4293    4293    4293 tty6        4293 Ss+      0   0:00 /sbin/mingetty /dev/tty6
      1  532967  532964  532964 ?             -1 Sl     495   0:00 /opt/td-agent/embedded/bin/ruby /usr/sbin/td-agent --log /var/log/td-agent/td-agent.log --use-v1-config --group td-agent --daemon /var/run/td-agent/td-agent.pid
 532967  532970  532964  532964 ?             -1 Sl     495 803:06  \\_ /opt/td-agent/embedded/bin/ruby /usr/sbin/td-agent --log /var/log/td-agent/td-agent.log --use-v1-config --group td-agent --daemon /var/run/td-agent/td-agent.pid
      1  537162  533357  532322 ?             -1 Sl       0 5067:43 /usr/bin/dockerd --default-ulimit nofile=262144:262144 --dns=172.17.0.1
 537162  537177  537177  537177 ?             -1 Ssl      0 4649:28  \\_ docker-containerd --config /var/run/docker/containerd/containerd.toml
 537177  537579  537579  537177 ?             -1 Sl       0   4:48  |   \\_ docker-containerd-shim -namespace moby -workdir /var/lib/docker/containerd/daemon/io.containerd.runtime.v1.linux/moby/0ee89b20deb3cf08648cd92e1f3e3c661ccffef7a0971
 537579  537642  537642  537642 ?             -1 Ss    1000  32:11  |   |   \\_ /usr/bin/python /usr/bin/supervisord -c /etc/supervisord/api.conf
 537642  539764  539764  537642 ?             -1 S     1000   0:00  |   |       \\_ sh -c echo "READY"; while read -r line; do echo "$line"; supervisorctl shutdown; done
 537642  539767  539767  537642 ?             -1 S     1000   5:09  |   |       \\_ php-fpm: master process (/etc/php73/php-fpm.conf)
 539767  783097  539767  537642 ?             -1 S     1000   0:00  |   |       |   \\_ php-fpm: pool test
 539767  783131  539767  537642 ?             -1 S     1000   0:00  |   |       |   \\_ php-fpm: pool test
 539767  783185  539767  537642 ?             -1 S     1000   0:00  |   |       |   \\_ php-fpm: pool test
...
...
...
```

У этой команды много различных опций, так что при активном использовании рекомендую ознакомиться с документацией. Для большинства же случаев хватит просто знать "

_ps aux_

".

### **kill**

Послать сигнал процессу. По умолчанию посылается сигнал

_SIGTERM_

, который завершает процесс.

```
[user@testhost ~]$ ps ux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
531      1027147  0.0  0.0 119956  4260 ?        S    14:51   0:00 sshd: user@pts/1
531      1027149  0.0  0.0 115408  3396 pts/1    Ss   14:51   0:00 -bash
531      1027170  0.0  0.0 119956  4136 ?        R    14:51   0:00 sshd: user@pts/2
531      1027180  0.0  0.0 115408  3564 pts/2    Ss   14:51   0:00 -bash
531      1033727  0.0  0.0 107960   708 pts/1    S+   15:17   0:00 sleep 300
531      1033752  0.0  0.0 117264  2604 pts/2    R+   15:17   0:00 ps ux
[user@testhost ~]$ kill 1033727
[user@testhost ~]$ ps ux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
531      1027147  0.0  0.0 119956  4260 ?        S    14:51   0:00 sshd: user@pts/1
531      1027149  0.0  0.0 115408  3396 pts/1    Ss+  14:51   0:00 -bash
531      1027170  0.0  0.0 119956  4136 ?        R    14:51   0:00 sshd: user@pts/2
531      1027180  0.0  0.0 115408  3564 pts/2    Ss   14:51   0:00 -bash
531      1033808  0.0  0.0 117268  2492 pts/2    R+   15:17   0:00 ps ux
```

Так как процесс может иметь обработчики сигналов,

_kill_

не всегда приводит к ожидаемому результату — моментальному завершению процесса. Чтобы «убить» процесс наверняка, нужно послать процессу сигнал

_SIGKILL_

. Однако это может привести к потере данных (например, если процесс перед завершением должен сохранить какую-то информацию на диск), так что нужно пользоваться такой командой осторожно. Номер сигнала

_SIGKILL_

— 9, поэтому короткий вариант команды выглядит так:

```
[user@testhost ~]$ ps ux | grep sleep
531      1034930  0.0  0.0 107960   636 pts/1    S+   15:21   0:00 sleep 300
531      1034953  0.0  0.0 110516  2104 pts/2    S+   15:21   0:00 grep --color=auto sleep
[user@testhost ~]$ kill -9 1034930
[user@testhost ~]$ ps ux | grep sleep
531      1035004  0.0  0.0 110516  2092 pts/2    S+   15:22   0:00 grep --color=auto sleep
```

Помимо упомянутых

_SIGTERM_

и

_SIGKILL_

существует еще множество различных сигналов, их список можно легко найти в интернете. И не забывайте, что сигналы

_SIGKILL_

и

_SIGSTOP_

не могут быть перехвачены или проигнорированы.

### **ping**

Послать хосту ICMP пакет

_ECHO\_REQUEST_

.

```
[user@testhost ~]$ ping google.com
PING google.com (172.217.15.78) 56(84) bytes of data.
64 bytes from iad23s63-in-f14.1e100.net (172.217.15.78): icmp_seq=1 ttl=47 time=1.85 ms
64 bytes from iad23s63-in-f14.1e100.net (172.217.15.78): icmp_seq=2 ttl=47 time=1.48 ms
64 bytes from iad23s63-in-f14.1e100.net (172.217.15.78): icmp_seq=3 ttl=47 time=1.45 ms
64 bytes from iad23s63-in-f14.1e100.net (172.217.15.78): icmp_seq=4 ttl=47 time=1.46 ms
64 bytes from iad23s63-in-f14.1e100.net (172.217.15.78): icmp_seq=5 ttl=47 time=1.45 ms
^C
--- google.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 1.453/1.541/1.850/0.156 ms
```

По умолчанию

_ping_

работает, пока его не завершить вручную. Поэтому может быть полезна опция

* c

— количество пакетов, после отправки которых

_ping_

завершится самостоятельно. Ещё одна опция, которую я иногда использую —

* i

, интервал между посылками пакетов.

```
[user@testhost ~]$ ping -c 3 -i 5 google.com
PING google.com (172.217.5.238) 56(84) bytes of data.
64 bytes from iad30s07-in-f238.1e100.net (172.217.5.238): icmp_seq=1 ttl=47 time=1.55 ms
64 bytes from iad30s07-in-f14.1e100.net (172.217.5.238): icmp_seq=2 ttl=47 time=1.17 ms
64 bytes from iad30s07-in-f14.1e100.net (172.217.5.238): icmp_seq=3 ttl=47 time=1.16 ms

--- google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 10006ms
rtt min/avg/max/mdev = 1.162/1.295/1.551/0.181 ms
```

### **ssh**

OpenSSH SSH клиент, позволяет подключаться к удаленному хосту.

```
MacBook-Pro-User:~ user$ ssh user@11.11.22.22
Last login: Tue Nov 26 11:27:39 2019 from another_host
[user@testhost ~]$ hostname
testhost
```

Есть много нюансов в использовании SSH, также этот клиент обладает большим количеством возможностей, поэтому при желании (или необходимости) можно почитать про это

[более подробно](https://habr.com/ru/post/435546/)

.

### **scp**

Копировать файлы между хостами (для этого используется

_ssh_

).

```
[user@testhost ~]$ pwd
/home/user
[user@testhost ~]$ ls
temp  test_renamed
[user@testhost ~]$ exit
logout
Connection to 11.11.22.22 closed.
MacBook-Pro-Aleksandr:~ user$ scp user@11.11.22.22:/home/user/temp Downloads/
temp                                                                                                                                                                                                        100%   31     0.2KB/s   00:00
MacBook-Pro-Aleksandr:~ user$ cat Downloads/temp
Content of a file.
Lalalala...
```

### **rsync**

Также для синхронизации директорий между хостами можно использовать

_rsync_

(

* a

— archive mode, позволяет скопировать полностью всё содержимое директории «как есть»,

* v

— вывод на консоль дополнительной информации):

```
MacBook-Pro-User:~ user$ ls Downloads/user
ls: Downloads/user: No such file or directory
MacBook-Pro-User:~ user$ rsync -av user@testhost:/home/user Downloads
receiving file list ... done
user/
user/.bash_history
user/.bash_logout
user/.bash_profile
user/.bashrc
user/.lesshst
user/.mongorc.js
user/.viminfo
user/1
user/man_signal
user/man_signal_error_log
user/temp
user/.ssh/
user/.ssh/authorized_keys
user/test/
user/test/created_today
user/test/temp_clone

sent 346 bytes  received 29210 bytes  11822.40 bytes/sec
total size is 28079  speedup is 0.95
MacBook-Pro-User:~ user$ ls -a Downloads/user
.                    .bash_history        .bash_profile        .lesshst             .ssh                 1                    man_signal_error_log test
..                   .bash_logout         .bashrc              .mongorc.js          .viminfo             man_signal           temp
```

### **echo**

Вывести на экран строку текста.

```
[user@testhost ~]$ echo "Hello"
Hello
```

Здесь заслуживают внимания опции

* n

— не дополнять строку переносом строки в конце, и

* e

— включить интерпретацию экранирования с помощью "\\".

```
[user@testhost ~]$ echo "\\tHello\\n"
\\tHello\\n
[user@testhost ~]$ echo -n "\\tHello\\n"
\\tHello\\n[user@testhost ~]$
[user@testhost ~]$ echo -ne "\\tHello\\n"
	Hello
```

Также с помощью этой команды можно выводить значения переменных. Например, в Linux exit code последней завершенной команды хранится в специальной переменной

_$?_

, и таким образом можно узнать, какая именно ошибка произошла в последнем запущенном приложении:

```
[user@testhost ~]$ ls    # ошибки не будет
1  man_signal  man_signal_error_log  temp  test
[user@testhost ~]$ echo $?    # получим 0 — ошибки не было
0
[user@testhost ~]$ ls qwerty    # будет ошибка
ls: cannot access qwerty: No such file or directory
[user@testhost ~]$ echo $?    # получим 2 — Misuse of shell builtins (according to Bash documentation)
2
[user@testhost ~]$ echo $?    # последний echo отработал без ошибок, получим 0
0
```

### **telnet**

Клиент для протокола TELNET. Используется для коммуникации с другим хостом.

```
[user@testhost ~]$ telnet example.com 80
Trying 93.184.216.34...
Connected to example.com.
Escape character is '^]'.
GET / HTTP/1.1
Host: example.com

HTTP/1.1 200 OK
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Tue, 26 Nov 2019 11:59:18 GMT
Etag: "3147526947+gzip+ident"
Expires: Tue, 03 Dec 2019 11:59:18 GMT
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Server: ECS (dcb/7F3B)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1256

... здесь было тело ответа, которое я вырезал руками ...
```

Если нужно использовать протокол TLS (напомню, что SSL давно устарел), то

_telnet_

для этих целей не подойдёт. Зато подойдёт клиент

_openssl_

:

**Пример использования openssl с выводом ответа на GET запрос**

## **Решение типовых задач в Linux**

### **Изменить владельца файла**

Изменить владельца файла или директории можно с помощью команды

_**chown**_

:

```
[user@testhost ~]$ chown user:user temp
[user@testhost ~]$ ls -l temp
-rw-rw-r-- 1 user user 31 Nov 26 11:09 temp
```

В параметр этой команде нужно отдать нового владельца и группу (опционально), разделенных двоеточием. Также при изменении владельца директории может быть полезна опция

* R

— тогда владельцы изменятся и у всего содержимого директории.

### **Изменить права доступа файла**

Эта задача решается с помощью команды

_**chmod**_

. В качестве примера приведу установку прав «владельцу разрешено чтение, запись и исполнение, группе разрешено чтение и запись, всем остальным — ничего»:

```
[user@testhost ~]$ ls -l temp
-rw-rw-r-- 1 user user 31 Nov 26 11:09 temp
[user@testhost ~]$ chmod 760 temp
[user@testhost ~]$ ls -l temp
-rwxrw---- 1 user user 31 Nov 26 11:09 temp
```

Первая 7 (это 0b111 в битовом представлении) в параметре означает «все права для владельца», вторая 6 (это 0b110 в битовом представлении) — «чтение и запись», ну и 0 — это ничего для остальных. Битовая маска состоит из трёх битов: самый младший («правый») бит отвечает за исполнение, следующий за ним («средний») — за запись, и самый старший («левый») — за чтение.

Также можно выставлять права с помощью специальных символов (

_мнемонический синтаксис_

). Например, в следующем примере сначала убираются права на исполнение для текущего пользователя, а затем возвращаются обратно:

```
[user@testhost ~]$ ls -l temp
-rwxrw---- 1 user user 31 Nov 26 11:09 temp
[user@testhost ~]$ chmod -x temp
[user@testhost ~]$ ls -l temp
-rw-rw---- 1 user user 31 Nov 26 11:09 temp
[user@testhost ~]$ chmod +x temp
[user@testhost ~]$ ls -l temp
-rwxrwx--x 1 user user 31 Nov 26 11:09 temp
```

У этой команды есть много вариантов использования, поэтому советую прочитать про неё подробнее (особенно про мнемонический синтаксис, например,

[здесь](https://vps.ua/wiki/change-permissions/)

).

### **Вывести содержимое бинарного файла**

Это можно сделать с помощью утилиты

_**hexdump**_

. Ниже приведены примеры её использования.

```
[user@testhost ~]$ cat temp
Content of a file.
Lalalala...
[user@testhost ~]$ hexdump -c temp
0000000   C   o   n   t   e   n   t       o   f       a       f   i   l
0000010   e   .  \\n   L   a   l   a   l   a   l   a   .   .   .  \\n
000001f
[user@testhost ~]$ hexdump -x temp
0000000    6f43    746e    6e65    2074    666f    6120    6620    6c69
0000010    2e65    4c0a    6c61    6c61    6c61    2e61    2e2e    000a
000001f
[user@testhost ~]$ hexdump -C temp
00000000  43 6f 6e 74 65 6e 74 20  6f 66 20 61 20 66 69 6c  |Content of a fil|
00000010  65 2e 0a 4c 61 6c 61 6c  61 6c 61 2e 2e 2e 0a     |e..Lalalala....|
0000001f
```

С помощью этой утилиты можно вывести данные и в других форматах, однако наиболее часто могут пригодиться именно такие варианты её использования.

### **Искать файлы**

Найти файл по части имени в дереве каталогов можно с помощью команды

_**find**_

:

```
[user@testhost ~]$ find test_dir/ -name "*le*"
test_dir/file_1
test_dir/file_2
test_dir/subdir/file_3
```

Также доступны другие опции и фильтры поиска. Например, так можно найти файлы в папке

_test_

, созданные более 5 дней назад:

```
[user@testhost ~]$ ls -ltr test
total 0
-rw-rw-r-- 1 user user 0 Nov 26 10:46 temp_clone
-rw-rw-r-- 1 user user 0 Dec  4 10:39 created_today
[user@testhost ~]$ find test/ -type f -ctime +5
test/temp_clone
```

### **Искать текст в файлах**

Справиться с этой задачей поможет команда

_**grep**_

. У неё есть множество вариантов использования, здесь в качестве примера указан самый простой.

```
[user@testhost ~]$ grep -nr "content" test_dir/
test_dir/file_1:1:test content for file_1
test_dir/file_2:1:test content for file_2
test_dir/subdir/file_3:1:test content for file_3
```

Один из популярных способов использования команды

_grep_

— использование её в конвейере (

_pipe_

):

```
[user@testhost ~]$ sudo tail -f /var/log/test.log | grep "ERROR"
```

Опция

* v

позволяет сделать эффект

_grep_

'а обратным — будут выводиться только строки, не содержащие паттерн, переданный в

_grep_

.

### **Смотреть установленные пакеты**

Универсальной команды нет, потому что всё зависит от дистрибутива Linux и используемого пакетного менеджера. Скорее всего вам поможет одна из следующих команд:

```
yum list installed
apt list --installed
zypper se —installed-only
pacman -Qqe
dpkg -l
rpm -qa
```

### **Посмотреть, сколько места занимает дерево директорий**

Один из вариантов использования команды

_**du**_

:

```
[user@testhost ~]$ du -h -d 1 test_dir/
8,0K test_dir/subdir
20K test_dir/
```

Можно менять значение параметра

* d

, чтобы получать более подробную информацию о дереве директорий. Также можно использовать команду в комбинации с

_sort_

:

```
[user@testhost ~]$ du -h -d 1 test_dir/ | sort -h
8,0K test_dir/subdir
16K test_dir/subdir_2
36K test_dir/
[user@testhost ~]$ du -h -d 1 test_dir/ | sort -h -r
36K test_dir/
16K test_dir/subdir_2
8,0K test_dir/subdir
```

Опция

* h

у команды

_sort_

позволяет сортировать размеры, записанные в human readable формате (например, 1K, 2G), опция

* r

позволяет отсортировать данные в обратном порядке.

### **«Найти и заменить» в файле, в файлах в директории**

Данная операция выполняется с помощью утилиты

_**sed**_

(без флага

_g_

в конце заменится только первое вхождение «old-text» в строке):

```
sed -i 's/old-text/new-text/g' input.txt
```

Можно использовать её для нескольких файлов сразу:

```
[user@testhost ~]$ cat test_dir/file_*
test content for file_1
test content for file_2
[user@testhost ~]$ sed -i 's/test/edited/g' test_dir/file_*
[user@testhost ~]$ cat test_dir/file_*
edited content for file_1
edited content for file_2
```

### **Вывести колонку из вывода**

Справиться с этой задачей поможет

_**awk**_

. В данном примере выводится вторая колонка вывода команды \`

_ps ux_

\`:

```
[user@testhost ~]$ ps ux | awk '{print $2}'
PID
11023
25870
25871
25908
25909
```

При этом надо иметь ввиду, что

_awk_

обладает гораздо более богатым функционалом, так что при необходимости работы с текстом в командной строке стоит почитать об этой команде подробнее.

### **Узнать IP адрес по имени хоста**

С этим поможет одна из следующих команд:

```
[user@testhost ~]$ host ya.ru
ya.ru has address 87.250.250.242
ya.ru has IPv6 address 2a02:6b8::2:242
ya.ru mail is handled by 10 mx.yandex.ru.

[user@testhost ~]$ dig +short ya.ru
87.250.250.242

[user@testhost ~]$ nslookup ya.ru
Server: 8.8.8.8
Address: 8.8.8.8#53

Non-authoritative answer:
Name: ya.ru
Address: 87.250.250.242
```

### **Сетевая информация**

Можно использовать

_**ifconfig**_

:

```
[user@testhost ~]$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 47.89.93.67  netmask 255.255.224.0  broadcast 47.89.95.255
        inet6 fd90::302:57ff:fe79:1  prefixlen 64  scopeid 0x20<link>
        ether 04:01:57:79:00:01  txqueuelen 1000  (Ethernet)
        RX packets 11912135  bytes 9307046034 (8.6 GiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 14696632  bytes 2809191835 (2.6 GiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 0  (Local Loopback)
        RX packets 10  bytes 866 (866.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 10  bytes 866 (866.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

А можно и

_**ip**_

:

```
[user@testhost ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 04:01:57:79:00:01 brd ff:ff:ff:ff:ff:ff
    inet 47.89.93.67/19 brd 47.89.95.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fd90::302:57ff:fe79:1/64 scope link
       valid_lft forever preferred_lft forever
3: ip_vti0: <NOARP> mtu 1500 qdisc noop state DOWN group default
    link/ipip 0.0.0.0 brd 0.0.0.0
```

При этом, если, например, вас интересует только IPv4, то можно добавить опцию

* 4

:

```
[user@testhost ~]$ ip -4 a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    inet 47.89.93.67/19 brd 47.89.95.255 scope global eth0
       valid_lft forever preferred_lft forever
```

### **Посмотреть открытые порты**

Для этого используют утилиту

_**netstat**_

. Например, чтобы посмотреть все слушающие TCP и UDP порты с отображением PID'а процесса, слушающего порт, и с числовым представлением порта, нужно использовать ее со следующими опциями:

```
[user@testhost ~]$ netstat -lptnu
```

### **Информация о системе**

Получить данную информацию можно с помощью команды

_**uname**_

.

```
[user@testhost ~]$ uname -a
Linux alexander 3.10.0-123.8.1.el7.x86_64 #1 SMP Mon Sep 22 19:06:58 UTC 2014 x86_64 x86_64 x86_64 GNU/Linux
```

Чтобы понять, в каком формате производится вывод, можно обратиться к

_help_

'у данной команды:

```
[user@testhost ~]$ uname --help
Использование: uname [КЛЮЧ]…
Печатает определенные сведения о системе.  Если КЛЮЧ не задан,
подразумевается -s.

  -a, --all          напечатать всю информацию, в следующем порядке,
                       кроме -p и -i, если они неизвестны:
  -s, --kernel-name  напечатать имя ядра
  -n, --nodename     напечатать имя машины в сети
  -r, --release      напечатать номер выпуска операционной системы
  -v, --kernel-version     напечатать версию ядра
  -m, --machine            напечатать тип оборудования машины
  -p, --processor          напечатать тип процессора или «неизвестно»
  -i, --hardware-platform  напечатать тип аппаратной платформы или «неизвестно»
  -o, --operating-system   напечатать имя операционной системы
      --help     показать эту справку и выйти
      --version  показать информацию о версии и выйти
```

### **Информация о памяти**

Чтобы понять, сколько оперативной памяти занято или свободно, можно воспользоваться командой

_**free**_

.

```
[user@testhost ~]$ free -h
              total        used        free      shared  buff/cache   available
Mem:           3,9G        555M        143M         56M        3,2G        3,0G
Swap:            0B          0B          0B
```

### **Информация о файловых системах (свободное место на дисках)**

Команда

_**df**_

позволяет посмотреть, сколько места свободно и занято на примонтированных файловых системах.

```
[user@testhost ~]$ df -hT
Файловая система Тип      Размер Использовано  Дост Использовано% Cмонтировано в
/dev/vda1        ext4        79G          21G   55G           27% /
devtmpfs         devtmpfs   2,0G            0  2,0G            0% /dev
tmpfs            tmpfs      2,0G            0  2,0G            0% /dev/shm
tmpfs            tmpfs      2,0G          57M  1,9G            3% /run
tmpfs            tmpfs      2,0G            0  2,0G            0% /sys/fs/cgroup
tmpfs            tmpfs      396M            0  396M            0% /run/user/1001
```

Опция

* T

указывает, что нужно выводить тип файловой системы.

### **Информация о задачах и различной статистике по системе**

Для этого используется команда

_**top**_

. Она способна вывести разную информацию: например, топ процессов по использованию оперативной памяти или топ процессов по использованию процессорного времени. Также она выводит информацию о памяти, CPU, uptime и LA (load average).

```
[user@testhost ~]$ top | head -10
top - 17:19:13 up 154 days,  6:59,  3 users,  load average: 0.21, 0.21, 0.27
Tasks: 2169 total,   2 running, 2080 sleeping,   0 stopped,   0 zombie
Cpu(s):  1.7%us,  0.7%sy,  0.0%ni, 97.5%id,  0.0%wa,  0.0%hi,  0.1%si,  0.0%st
Mem:  125889960k total, 82423048k used, 43466912k free, 16026020k buffers
Swap:        0k total,        0k used,        0k free, 31094516k cached

    PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
  25282 user      20   0 16988 3936 1964 R  7.3  0.0   0:00.04 top
   4264 telegraf  20   0 2740m 240m  22m S  1.8  0.2  23409:39 telegraf
   6718 root      20   0 35404 4768 3024 S  1.8  0.0   0:01.49 redis-server
```

Эта утилита обладает богатым функционалом, так что если вам надо часто ей пользоваться, лучше ознакомиться с её документацией.

### **Дамп сетевого трафика**

Для перехвата сетевого трафика в Linux используется утилита

_**tcpdump**_

. Чтобы сдампить трафик на порте 12345, можно воспользоваться следующей командой:

```
[user@testhost ~]$ sudo tcpdump -i any -A port 12345
```

Опция

* A

говорит о том, что мы ходим видеть вывод в ASCII (поэтому это хорошо для текстовых протоколов),

* i any

указывает, что нас не интересует сетевой интерфейс,

_port_

— трафик какого порта дампить. Вместо

_port_

можно использовать

_host_

, либо комбинацию

_host_

и

_port_

(

_host A and port X_

). И еще полезной может оказаться опция

* n

— не конвертировать адреса в хостнеймы в выводе.

Что если трафик бинарный? Тогда нам поможет опция

* X

— выводить данные в hex и ASCII:

```
[user@testhost ~]$ sudo tcpdump -i any -X port 12345
```

При этом надо учитывать, что в обоих вариантах использования будут выводиться IP пакеты, поэтому в начале каждого из них будут бинарные заголовки IP и TCP. Вот пример вывода для запроса "

_123_

" посланного в сервер, слушающий порт 12345:

```
[user@testhost ~]$ sudo tcpdump -i any -X port 12345
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on any, link-type LINUX_SLL (Linux cooked), capture size 262144 bytes
14:27:13.224762 IP localhost.49794 > localhost.italk: Flags [P.], seq 2262177478:2262177483, ack 3317210845, win 342, options [nop,nop,TS val 3196604972 ecr 3196590131], length 5
    0x0000:  4510 0039 dfb6 4000 4006 5cf6 7f00 0001  E..9..@.@.\\.....
    0x0010:  7f00 0001 c282 3039 86d6 16c6 c5b8 9edd  ......09........
    0x0020:  8018 0156 fe2d 0000 0101 080a be88 522c  ...V.-........R,
    0x0030:  be88 1833 3132 330d 0a00 0000 0000 0000  ...3123.........
    0x0040:  0000 0000 0000 0000 00                   .........
```
