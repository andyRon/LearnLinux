### 《Linux系统命令及Shell脚本实践指南》笔记



```shell
at now + 30 minutes
/sbin/shutdown -h now
<EOT>
```



#### 3.2 文件和目录权限



`chown`

`chgrp`



`umask`

`file`



#### 3.3 查找文件

##### 普通查找

`find PATH -name FILENAME`     例如：`find . -name index.html`

##### 数据库查找 locate

`locate httpd.conf`

`updatedb`

##### 查找执行文件：which/whereis

which用于从系统的PATH变量所定义的目录中查找可执行文件的绝对路径。



### 4.4 硬链接和软连接



硬链接 :  就是文件名指向同一个node。

`ln  weekly.out weekly-hard.out`

软连接和Windows中快捷方式差不多，文件内容是另一个文件路径名。

`ln -s weekly.out weekly-s.out`

```shell
$ ll -i weekly.out weekly-hard.out weekly-s.out
8654478528 -rw-r--r--  2 andyron  staff   180B  2 20 18:40 weekly-hard.out
8654485341 lrwxr-xr-x  1 andyron  staff    10B  2 20 20:21 weekly-s.out -> weekly.out
8654478528 -rw-r--r--  2 andyron  staff   180B  2 20 18:40 weekly.out
```



### 5 字符处理

`grep`是Linux下非常强大的基于**行**的**文本搜索**工具。

`sort`

`cut`  截取。以行为基本单位。

`cat /etc/passwd | cut -f 1 -d ':'`     打印系统的所有用户名。-f 指定列，-d表示分隔符。

```shell
$ cat /etc/passwd | cut -f 1,6 -d ':'
nobody:/var/empty
root:/var/root
daemon:/var/root
_uucp:/var/spool/uucp
_taskgated:/var/empty
_networkd:/var/networkd
```

`cat /etc/passwd | cut -c 1-5`     

`tr`   文本替换

```shell
$ cat /etc/passwd | tr '[a-z]' '[A-Z]'  # 小写换成大写
NOBODY:*:-2:-2:UNPRIVILEGED USER:/VAR/EMPTY:/USR/BIN/FALSE
ROOT:*:0:0:SYSTEM ADMINISTRATOR:/VAR/ROOT:/BIN/SH
DAEMON:*:1:1:SYSTEM SERVICES:/VAR/ROOT:/USR/BIN/FALSE
```

```shell
$ cat /etc/passwd | tr -d ':'   # 删除冒号
nobody*-2-2Unprivileged User/var/empty/usr/bin/false
root*00System Administrator/var/root/bin/sh
```

`paste`  文本合并

`split` 分割大文件

`split -l 500 big_file.txt small_file_`   大文件分割成许多小文件，-l指定500行分割一次。

### 6 网络管理



路由表

`/etc/resolv.conf`   DNS

### 7 进程管理

`ps`

`top`

`kill`

`killall`

`lsof`   查看文件被那些进程打开

```shell
# lsof /var/log/messages
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF   NODE NAME
rsyslogd 794 root    7w   REG  253,1   383286 397894 /var/log/messages
```

进程优先级调整：`nice`、`renice`



### 8 软件安装



`rpm -qf /etc/audit`   查询某个文件属于哪个包

查询某个已安装软件所包含的所有文件

```shell
# rpm -ql less
/etc/profile.d/less.csh
/etc/profile.d/less.sh
/usr/bin/less
/usr/bin/lessecho
/usr/bin/lesskey
/usr/bin/lesspipe.sh
/usr/share/doc/less-458
/usr/share/doc/less-458/LICENSE
/usr/share/man/man1/less.1.gz
/usr/share/man/man1/lessecho.1.gz
/usr/share/man/man1/lesskey.1.gz
```



### 10 正则表达式



#### 10.3 文本处理工具 sed

sed(stream editor)

Sed.txt:

```
this is line 1, this is First line
this is line 2, the Second line, Empty line followd

this is line 4, this is Third line
this is line 5, this is Fifth line
```

`sed -e 's/this/That/g' -e 's/line/Line/g' Sed.txt` ：

```
That is Line 1, That is First Line
That is Line 2, the Second Line, Empty Line followd

That is Line 4, That is Third Line
That is Line 5, That is Fifth Line
```



### 10.4 文本处理工具 awk





### 18 脚本例子





这本书适合入门和温习Linux基础知识，有点像《鸟哥的Linux私房菜》+《Linux命令行与shell脚本编程大全》的非常简化的破产版本😀，这两部很有优秀，但实在太长了。Linux知识真是不用就忘🤦‍♀️。

PS：非常不好的一点，应该是微信读书排版的问题，好多命令间的空格符没了，熟悉的人还好，完全不知道的，影响太大了。😖