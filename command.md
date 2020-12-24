## 常用命令

### 查找、查看系统命令等情况

which

whereis

which ps		搜索ps命令的绝对路径

whereis jobs		搜索命令的文件所在的绝对路径

whereis -b ping 		只搜索命令的二进制文件的绝对路径

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








