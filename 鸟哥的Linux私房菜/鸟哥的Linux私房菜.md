#   《鸟哥的Linux私房菜》笔记

2020.2.4再次学习。
### 准备

学习环境：Mac的VMware Fusion虚拟机，CentOS 7 64位

查看IP地址的方法：
`cat /etc/sysconfig/network-scripts/ifcfg-eth0`
`ifconfig`
`ip add`



### 零、计算器概论

#### 计算机硬件的五大单元

![](/Users/andyron/myfield/github/LearnLinux/images/linux-001.jpg)

#### CPU的种类

精简指令集（RISC）

复杂指令集（CISC）

#### 计算单位

1 Byte = 8 bits

![](/Users/andyron/myfield/github/LearnLinux/images/linux-002.jpg)

容量一般是用二进制方式，1GBytes = 1024 *1024 * 1024 Bytes；速度用十进制，1GHz= 1000 * 1000 * 1000 Hz。

#### 操作系统

操作系统核心的功能：

- 系统呼叫接口（System call interface）
- 程序管理（Process control）  cpu有效分配，cpu排程机制
- 内存管理（Memory management）
- 文件系统管理（Filesystem management）
- 装置的驱动（Device drivers）   可加载模块



#### 一些命令

`cat /proc/cpuinfo`

`lspci`   显示系统中所有PCI总线设备或连接到该总线上的所有设备的工具



### 一、Linux是什么

GNU 是 GNU is Not Unix 

GNU C Compiler(gcc)

自由软件基金会(FSF, Free Software Foundation)

GNU的通用公共许可证(General Public License, GPL) --- copyleft(相对于专利软件的copyright！)

POSIX是可携式操作系统接口(Portable Operating System Interface)，重点在规范核心与应用程序之间的接口。

Linux distributions：两大主流 1）使用RPM （Red Hat，Fedora，SuSE），2）使用dpkg(Debian,Ubuntu等)

linux上的图形界面： KDE ， GNOME

**平行运算**是将原本的工作分成多样，然后交给多部主机去运算，最终再将结果收集起来。

*要让linux解决问题*

Linux最强的地方在于**网络**，而Windows是赢在用户接口较为亲善。

*作为一个使用者，人要迁就机器；做为一个开发者，要机器迁就人。*

**TLDP**是 The Linux Documentation Project 。

异步的磁盘/内存数据传输模式。



### 二、Linux如何学习

`/usr/share/doc/`   Linux自己的文档存储位置

`/var/log/`   Linux系统日志

不同环境下，解决问题的方法有很多种，只要行的通，就是好方法。



### 三、主机规划磁盘分区

#### 



#### 磁盘接口与装置文件名

*   IDE接口 /dev/hd[a-d] 
*   SATA接口（目前磁盘，u盘等） /dev/sd\[a-p][1-\] (a-p的顺序是安装磁盘被检测的先后，数字是分隔槽)

![](/Users/andyron/myfield/github/LearnLinux/images/linux-003.jpg)



#### 磁盘分区

##### 磁盘的组成

> sector 扇区，磁区(512字节)。  
> track 磁道。由于磁盘是旋转的，则连续写入的数据是排列在一个圆周上的。所以这个圆周上的所有sector组成一个track。  
> side/head 磁面/磁头。每个磁面都有一个用于读取存储数据的磁头，所以side数与head数相同  
> cylinder 磁柱，柱面(这个翻译貌似不好理解)。

*   磁盘的第一个sector： 1，主要启动记录区(Master Boot Record, MBR)：可以安装开机管理程序的地方，有446 bytes 2，分割表(partition table)：记录整颗硬盘分割的状态，有64 bytes 3，结束标志：2bytes
*   partition table 
    *   最多纪录四条分割信息（开始和结束的磁柱号码，主和延伸分割槽；其中延伸最多一个，可以进行逻辑分割）
    *   分隔槽最小单位是cylinder
    *   延伸分割槽使用额外的扇区来纪录分割信息（在延伸分隔槽中）

##### 开机流程与MBR 

由于**开机管理程序**是操作系统在安装的时候所提供的，所以他会认识硬盘内的文件系统格式。 
1.  BIOS：开机主动执行的韧体（写在硬件上的一个软件程序），会认识第一个可开机的装置；
2.  MBR：第一个可开机装置的第一个扇区内的主要启动记录区块，内含开机管理程序；
3.  开机管理程序(boot loader)：一支可读取 核心档案 来执行的软件；
4.  核心档案：开始操作系统的功能... 

##### 多重引导 

开机管理程序也可以安装在每个分隔槽的**启动扇区**(boot sector)

每个分割槽都拥有自己的启动扇区

实际可开机的核心档案是放置到各分隔槽中

windows安装程序会主动的覆盖掉MBR以及自己所在分割槽的启动扇区 ，所以先安装windows

##### 磁盘分区的选择 

**挂载** 就是利用一个目录当成进入点，将磁盘分隔槽的数据放置在该目录下

SAMBA （与windows文件共享） /home

邮件服务器 /var



### 四、安装CentOS与多重引导小技巧



### 五、首次登入与man page

#### 基础

`date` `cal`

`startx`

`bc`

ctrl-c 中断目前程序 ctrl-z 把程序掉到背景中

ctrl-d 键盘输入结束 (End Of File, EOF 或 End Of Input) 类似于 exit

#### man page

man page 中第一行代号的意义（`man 7 man` 查看）：

![](/Users/andyron/myfield/github/LearnLinux/images/linux-004.jpg)

man page中每个部分的含义：

![](/Users/andyron/myfield/github/LearnLinux/images/linux-005.jpg)



`man -f command` 查看某个命令的所有相关说明文件， 类似于 `whatis` （需要有whatis数据库） 

 `man -k`(比-f更全,相关的) 类似于 `apropos` 

#### info page

类似man page，不过info page将文件数据拆成一个一个的段落。

#### 其它有用的文件


`/etc/man.config`中定义了man到哪寻找参考文件  
MANPATH /usr/man 
MANPATH /usr/share/man  
MANPATH /usr/local/man  
MANPATH /usr/local/share/man  
MANPATH /usr/X11R6/man

`info` /usr/share/info/

`/usr/share/doc/` 下有很多重要的文档 `/usr/share/doc/centos-release-notes-5.5/`  
`/usr/share/doc/bash-3.2/`

#### 其它命令

`nano` 文本编辑器

`sync` 将数据同步写入磁盘

`shutdown`

`reboot`,`halt`,`poweroff`

`init 0` 关机，`init 5` 类似 `startx`

`/etc/issue`中是开机显示信息，通过`man issue`(配置文件的档案内容格式，man page的代号为5) > `man mingetty`查看/etc/issue中变量的意义



#### 忘记root密码



 ### 六、linux的档案权限与目录配置

#### 1 使用者与群组

####2 Linux文件权限

##### Linux文件属性

![](/Users/andyron/myfield/github/LearnLinux/images/linux-006.jpg)

##### 改变文件属性与权限

`# chgrp [-R] group dirname/filename`

`# chown [-R] user[:group] dirname/filename`

`# chmod [-R] xyz dirname/filename`

`# chmod u=rwx,go=rx .bashrc`  通过符号类型改变权限

##### 目录与文件的权限意义

文件的rwx， 主要针对『文件的内容』而言的

目录的r表示可以查询该目录下的文件名数据，即可以用`ls` 目录的w很重要，表示可以改变目录下的结构，即 1)建立新的档案与目录； 删除已经存在的档案与目录(不论该档案的权限为何！) 将已存在的档案或目录进行更名； 搬移该目录内的档案、目录位置。

目录的x表示能否进入目录使之成为工作目录，即可以`cd`

sudo -s

last /var/log/wtmp btmp



##### 文件种类与扩展名



#### 3 Linux目录配置

![](/Users/andyron/myfield/github/LearnLinux/images/linux-007.jpg)

![](/Users/andyron/myfield/github/LearnLinux/images/linux-008.jpg)

![image-20200204212546837](/Users/andyron/myfield/github/LearnLinux/images/linux-009.jpg)



![image-20200204212704073](/Users/andyron/myfield/github/LearnLinux/images/linux-010.jpg)

![image-20200204212734454](/Users/andyron/myfield/github/LearnLinux/images/linux-011.jpg)

![](/Users/andyron/myfield/github/LearnLinux/images/linux-012.jpg)



目录树

![](/Users/andyron/myfield/github/LearnLinux/images/linux-013.jpg)



### 七、Linux文件和目录管理

`$PATH`

`cd`  `pwd`  `mkdir`  `rmdir`



`ls`

`cp`   `rm`   `mv`



#### 文件内容查阅

`cat `  `tac`  `nl`

`more`  `less`

`head`  `tail`

`od`

`touch`

#### 文件和目录的默认权限、隐藏权限

`umask`

`chattr`  `lsattr`

文件的特殊权限： SUID，SGID，SBIT

`file` 

#### 命令和文件的搜索

`which`

`whereis`  `locate`  `find`

#### 权限和命令间的关系



### 八、Linux磁盘与文件系统管理

#### 1 EXT2



#### 2 简单操作

`df`  `du`

`ln`



#### 3 磁盘的分割、格式化、检验与挂载

`fdisk`  `partprobe`

`mkfs`  `mke2fs`

`fsck`  `badblocks`

`mount`  `umount`

`mknod`  `e2label`  `tune2fs`  `hdparm`



#### 4 设定开机挂载

`/etc/fstab`   `/etc/mtab`



### 九、压缩与打包



#### 常用压缩命令

`compress`

`gzip`  `zcat`

`bzip2`  `bzcat`



#### 打包命令

`tar`



#### 完整备份工具

`dump`

`restore`



#### 光盘写入工具

`mkisofs`

`cdrecord`



### 十、Vim



### 十一、Bash



### 十二、正则与文件格式化处理



#### 文件的格式化与相关处理

`printf`

`awk`

`diff`  `cmp`  `patch`

`pr`



### 十三、Shell脚本



### 十四、Linux账号管理与ACL权限设定



### 十五、磁盘配额（Quota）与进阶文件系统管理



### 十六、crontab



### 十七、程序管理与SELinux牛膝初探



### 十八、系统服务（daemons）



### 十九、认识、分析登录档

`syslog`

`/etc/syslog.conf`



`logrotate`

`/etc/logrotate.conf`

`/etc/logrotate.d/`



#### 分析登录档

`logwatch`



### 二十、开机流程、模块管理与Loader



### 二十一、系统设定工具（网络与打印机）与硬件侦测



### 二十二、软件安装：原始码与Tarball



### 二十三、软件安装：RPM、SRPM、YUM



### 二十四、X Window设定介绍



### 二十五、Linux备份策略



### 二十六、Linux核心编译与管理



