## [Linux工具快速教程](https://linuxtools-rst.readthedocs.io/zh_CN/latest/index.html#)

### 使用命令的帮助

```shell
# 参考手册全局查询
man -k 关键词
# 类似man -k
apropos 关键词
# man的相关信息
man man

# 命令的简要说明 
whatis 命令
# 命令更详细的介绍
info 命令
# 命令的位置
which 命令
# 命令的二进制文件、源码、手册位置
whereis 命令
whereis -b 	# 只搜索命令的二进制文件位置，类似which
whereis -s
whereis -m 

```

使用举例

```shell
$ whatis whereis
whereis (1)          - locate the binary, source, and manual page files for a command

$ whatis -w "loca*"
local (1)            - bash built-in commands, see bash(1)
local (8)            - Postfix local mail delivery
local.users (5)      - The SELinux local users configuration file
locale (3pm)         - Perl pragma to use or avoid POSIX locales for built-in operations
locale.conf (5)      - Configuration file for locale settings
localectl (1)        - Control the system locale and keyboard layout settings
localtime (5)        - Local timezone configuration file

# whatis会显示具体文档类别
$ whatis printf
printf               (1)  - format and print data
printf               (1p)  - write formatted output
printf               (3)  - formatted output conversion
printf               (3p)  - print formatted output
printf [builtins]    (1)  - bash built-in commands, see bash(1)
$ man 3 printf

# 查找GNOME的config配置工具命令
$ man -k GNOME config | grep 1
bond2team (1)        - Converts bonding configuration to team
cpupower-info (1)    - Shows processor power related kernel or hardware configurations
cpupower-set (1)     - Set processor power related kernel or hardware configurations
grub2-menulst2cfg (1) - Convert a configuration file from GRUB 0.xx to GRUB 2.xx format.
grub2-script-check (1) - Check GRUB configuration file for syntax errors.
grub2-syslinux2cfg (1) - Transform a syslinux config file into a GRUB config.
gsettings (1)        - GSettings configuration tool
p11-kit (8)          - Tool for operating on configured PKCS#11 modules
pkcs11.conf (5)      - Configuration files for PKCS#11 modules
pkcs11.txt (5)       - NSS PKCS #11 module configuration file
pkg-config (1)       - Return metainformation about installed libraries
postconf (1)         - Postfix configuration utility
pwscore (1)          - simple configurable tool for checking quality of a password
systemd-delta (1)    - Find overridden configuration files
```

### 文件及目录管理

```shell
mkdir
rm
mv
cp
cd 
ls

find
locate

cat 
vi
head 
tail
more
less

diff
egrep

chown
chmod

ln

| && >
```



```
Ctl-U   删除光标到行首的所有字符,在某些设置下,删除全行
Ctl-W   删除当前光标到前边的最近一个空格之间的字符
Ctl-H   backspace,删除光标前边的字符
Ctl-R   匹配最相近的一个文件，然后输出
```



### 文本处理

#### find 文件查找

#### grep 文本搜索

#### xargs 命令行参数转换

#### sort 排序

#### uniq 消除重复行

#### 用tr进行转换

#### cut 按列切分文本

#### paste 按列拼接文本

#### wc 统计行和字符的工具

#### sed 文本替换利器

#### awk 数据流处理工具

#### 迭代文件中的行、单词和字符



### 磁盘管理

#### 查看磁盘空间

```shell
$ df -h
文件系统        容量  已用  可用 已用% 挂载点
/dev/vda1        40G  2.5G   35G    7% /
devtmpfs        909M     0  909M    0% /dev
tmpfs           920M     0  920M    0% /dev/shm
tmpfs           920M  440K  919M    1% /run
tmpfs           920M     0  920M    0% /sys/fs/cgroup
tmpfs           184M     0  184M    0% /run/user/0

# 查看当前目录所占空间大小，-s表示只显示整个目录大小类似-d0
$ du -sh
400K	.
```

查看当前目录下所有子文件夹排序后的大小:

```
for i in `ls`; do du -sh $i; done | sort
或者：
du -sh `ls` | sort
```

```shell
$ du -sh `ls` | sort
124K	cloud-init.log
12K	boot.log-20200215
12K	httpd
12K	lastlog
148K	cron-20201227
148K	cron-20210103
148K	cron-20210110
152K	cron-20201220
172K	secure-20210110
176K	secure-20201220
17M	sa
184K	secure-20210103
```

#### 打包+压缩

两步

先打包：

```shell
$ tar -cvf log.tar boot.log yum.log
```

后压缩：（生成类似log.tar.gz）

```shell
$ gzip log.tar
```

#### 解压缩+解包

先解压缩：

```shell
$ gunzip log.tar.gz
```

后解包：

```shell
$ tar -xvf log.tar
```



### 进程管理工具

#### 查询进程

```shell
# 查询正在运行的进程信息
ps -ef
# 查询归属于用户colin115的进程
ps -ef | grep colin115
ps -lu colin115
# 以完整的格式显示所有的进程
ps -ajx

# 查询进程名中含有re的进程
pgrep -l re
2 kthreadd
400 xfs-reclaim/dm-
555 xfs-reclaim/sda
18950 firewalld
19589 dockerd-current

# 显示进程信息，并实时更新
top

# 查看端口占用的进程状态
lsof -i:3306
# 查看用户username的进程所打开的文件
lsof -u username
# 查询init进程当前打开的文件
lsof -c init
# 查询指定的进程ID(23295)打开的文件
lsof -p 2323
# 查询指定目录下被进程开启的文件（使用+D 递归目录）
lsof +d mydir/
```

#### 终止进程

```shell
# 杀死指定PID的进程 
kill PID
# 杀死相关进程
kill -9 3434
```

#### 进程监控

查看系统中使用CPU、使用内存最多的进程；

```shell
top
```

输入top命令后，进入到交互界面；接着输入字符命令后显示相应的进程状态：

```
P：根据CPU使用百分比大小进行排序。
M：根据驻留内存大小进行排序。
i：使top不显示任何闲置或者僵死进程。
```

#### 分析线程栈

命令pmap，来输出进程内存的状况，可以用来分析线程堆栈：

```shell
$ ps -fe| grep redis
weber    13508 13070  0 08:14 pts/0    00:00:00 grep --color=auto redis
weber    29515     1  0  2013 ?        02:55:59 ./redis-server redis.conf
$ pmap 29515
29515:   ./redis-server redis.conf
08048000    768K r-x--  /home/weber/soft/redis-2.6.16/src/redis-server
08108000      4K r----  /home/weber/soft/redis-2.6.16/src/redis-server
08109000     12K rw---  /home/weber/soft/redis-2.6.16/src/redis-server
```



```shell
# 将用户colin115下的所有进程名以av_开头的进程终止:
ps -u colin115 |  awk '/av_/ {print "kill -9 " $1}' | sh

# 将用户colin115下所有进程名中包含HOST的进程终止:
ps -fe| grep colin115|grep HOST |awk '{print $2}' | xargs kill -9;
```

### 性能监控

```shell
sar -u
sar -u 1 2

sar -q 1 2

sar -r 1 2
free -m

sar -W 1 3

df -h

watch
```



### 网络工具

```shell
netstat -a
netstat -at
netstat -l
netstat -antp | grep 6397

route -n
ping IP
traceroute IP
host domain
host IP

wget

ssh
ftp
sftp
lftp

scp
```

### 用户管理工具

```shell
useradd -m username
passwd username

userdel -r username
su userB

groups
usermod -G groupName username
usermod -g groupName username

/etc/passwd
/etc/group


```

### 系统管理及IPC资源管理

```shell
uname -a
lsb_release -a

sar -u 5 10
cat /proc/cpuinfo
cat /proc/cpuinfo | grep processor | wc -l
cat /proc/meminfo

pagesize
arch

date
tzselect
clock

ipcs

ulimit – a
ulimit – c unlimited
```











## 常用命令

### 查找、查看系统命令等情况



users 显示当前登录系统地用户

who 登录在本机的用户与来源

w 登录在本机的用户及其运行的程序

last 查看用户的登陆日志

lastlog 查看每个用户最后的登陆时间

hostname 查看主机名

uname -r 		显示当前系统的内核版本和操作系统位数

uname -a

cat /etc/redhat-release   查看CentOS版本

cat /etc/issue	同上

id [username] | 查看用户相关的id信息，还可以用来判断用户是否存在

chfn 修改个人信息??

set 显示环境变量和普通变量 


env 显示环境变量 export 把普通变量变成环境变量 


unset 删除一个环境变量

df [选项] [文件] | 显示指定磁盘文件的可用空间,如果没有文件名被指定，则所有当前被挂载的文件系统的可用空间将被显示

```
-a  显示全部文件系统
-h  文件大小友好显示
-l  只显示本地文件系统
-i  显示inode信息
-T  显示文件系统类型
```

du [选项] [文件] | 显示每个文件和目录的磁盘使用空间
```
-h  方便阅读的方式
-s  只显示总和的大小
```
ps 列出当前进程的快照

```
a   显示所有的进程
-a  显示同一终端下的所有程序
e   显示环境变量
f   显示进程间的关系
-H  显示树状结构
r   显示当前终端的程序
T   显示当前终端的所有程序
-au 显示更详细的信息
-aux    显示所有包含其他使用者的行程 
-u  指定用户的所有进程
```

top 

free [参数] | 显示linux系统中空闲的、已用的物理内存及swap内存,及被内核使用的buffer

locate

find

`man -f`

`info ls`

`groups`  当前用户所属的所有组

```shell
$ finger andyron
Login: andyron        			Name: Andy Ron
Directory: /Users/andyron           	Shell: /bin/zsh
On since 四  2 13 00:34 (CST) on console, idle 7 days 17:08 (messages off)
On since 四  2 13 17:07 (CST) on ttys000, idle 0:30
On since 四  2 20 12:46 (CST) on ttys001, idle 0:01
On since 三  2 19 18:24 (CST) on ttys002
No Mail.
No Plan.

```

### 账号管理

`useradd andy`

`passwd andy`

`useradd -u 555 user1`   指定UID

`useradd -g user1 user2`  创建用户user2，指定其Group是user1

`/etc/passwd`

`userdel`

`groupadd`

`groupdel`

su



### 文件、目录、文件系统

tree -L 1 /  # 使用tree 命令查看根目录下的一层的目录结构

ls -d /*    根目录下的所有的目录和文件

cat -n /root/.bashrc		查看文件内容并列出行号

head /etc/services	默认查看文件前十行内容

 tail -f /var/log/messages		查看文件动态更新的内容

df -h

mount



### 包管理

rpm -qa | grep mysql  	查看当前系统安装关于"mysql"的rpm包名



### 网络管理



### 服务

chkconfig sshd on   使ssh服务开机自启动

pstree   查看正在运行的状态

service --status-all   查看当前服务器所有服务

service --status-all | grep running

systemctl | grep running   查看正在运行的服务

systemctl命令是系统服务管理器指令，主要负责控制systemd系统和服务管理器，它实际上将 service 和 chkconfig 这两个命令组合到一起。

　　CentOS 7.x开始，CentOS开始使用systemd服务来代替daemon，原来管理系统启动和管理系统服务的相关命令全部由systemctl命令来代替。

　　Systemd是一个系统管理守护进程、工具和库的集合，用于取代System V初始进程。Systemd的功能是用于集中管理和配置类UNIX系统。

　　在Linux生态系统中，Systemd被部署到了大多数的标准Linux发行版中，只有为数不多的几个发行版尚未部署。Systemd通常是所有其它守护进程的父进程，但并非全是如此。

### 更多

history

runlevel 		查看当前系统的运行级别

N 3

查看当前系统的运行级别

init 5 			切换当前系统的运行级别



#### shutdown

```shell
sudo shutdown [-h | -r | -s] [time]
```

`-h` ：关机（halt）

`-r` ：重启（reboot）

`-s` ：休眠（sleep）

`time` ：执行操作的时间

- yymmddhhmm ：指定年月日时分，如 17022318 表示2017年2月23日18时
- now ：现在
- +n ：n分钟后
- hh:mm ：今天某时某分



```shell
在 2017年2月23日18时 关机
sudo shutdown -h 1702231800

sudo shutdown -h now 

立刻重启
sudo shutdown -r now

今晚 20 点休眠
sudo shutdown -s 20:00

30分钟休眠
sudo shutdown -s +30
```



##### 其它关机重启命令


立刻关机：`sudo halt`
立刻重启：`sudo reboot`



## 快捷键

`ctrl + a`   跳到命令最前面

`ctrl + e`  跳到命令最后面

----------








