---
layout:     post
title:      Shell Fundamental
author:     BonBon
tags: 		Shell
subtitle:  	Some basics while learning shell
category:  project1
---
<!-- Start Writing Below in Markdown -->
# Table of Contents

* TOC
{:toc}

# Resources

[Linux 命令行与 Shell 脚本教程](https://archlinuxstudio.github.io/ShellTutorial/#/shellBasic/shell_basic)
<embed src="https://archlinuxstudio.github.io/ShellTutorial/#/shellBasic/shell_basic" height="500px" width="100%">

[WashingtonU: Using vi, the Unix Visual Editor][1]
<embed src="https://staff.washington.edu/rells/R110/#basics4" height="500px" width="100%">

[Runoob: linux教程][2]
<embed src="https://www.runoob.com/linux/linux-file-content-manage.html" height="500px" width="100%">

[Github: linux Intro][5]

[1]:https://staff.washington.edu/rells/R110/#basics4
[2]:https://www.runoob.com/linux/linux-file-content-manage.html
[5]:https://github.com/BoobooWei/booboo_linux_base


# Linux基础命令
## 命令提示符

* \# root 用户
* $ 一般用户
* [ 用户的身份 @ 主机名 当前位置 ]

当前位置显示的是目录名

## 常用的命令

### ls

| 常用参数 | 含义及用法                                    |
| :--- | :--------------------------------------- |
| -l   | long 的缩写 详细列出当前目录下的所有文件属性 	七列 文件名 <=255 个字符 |
| -d   | directory 的缩写 查看当前目录本身的信息                |
| -h   | 以人性化的方式显示文件大小,录的大小并不代表目录内所有文件的大小 du -sh /etc<== 查看 etc 目录真正的大小 |
| -a   | 查看隐藏文件 以 . 开头的文件                         |
| -R   | 查看多层目录                                   |
| -b   | 特殊字符将以 \ 分割 ls 查看有特殊字符的文件                |

### cd

| cd   | change directory 切换工作目录                  |
| :--- | :--------------------------------------- |
| 绝对路径 | 以根为起始的路径                                 |
| 相对路径 | ~当前用户的家目录 ;. 当前目录 ;.. 上一层用户 ;- 回到上一次所在位置 |

### pwd

pwd: print working directory 显示当前所在位置的绝对路径

##  符号

### 通配符 *

匹配任意多个字符

例如：a* 包括aa\*、ab\*、ac\* 等等 
寻找包含a的文件名：ls -lrt \*a\*

### 通配符 ?

匹配任意单个字符
例如： a? 可以是ab、ac、ad、a1、a9、a#等等

### | 管道

output | input

对某些命令执行的结果去作操作,会用到管道；用于命令与命令之间的连接，前一个命令的输出是后一个命令的输入

#### | 管道实验

详细列出 /tmp 目录下的文件,并截取以空格为分割的第三列

```shell
[tom@rhel7 ~]$ ls -l /tmp|cut -d" " -f3
tom
tom
root
root
root
详细列出 /tmp 目录下的文件,截取含有关键字 tom 的行,再截取以空格为分割的第一列内容
[tom@rhel7 ~]$ ls -l /tmp|grep tom|cut -d" " -f1
drwxrwxr-x.
-rw-rw-r--.
```

### rm

| rm   |      [filename] remove 删除文件,对 root 用户有提示,普通用户没有提示 |
| :---: | :--------------------------------------- |
| -f   | force 强制删除, root 无提示                     |
| -i   | 普通用户有提示的删除                               |
| -r   | 递归删除,慎重使用 -rf                            |

### mkdir

mkdir:make directory 创建目录

`mkdir -p /test/test1`

递归创建目录

`mkdir {a..e}`

创建 a-e 的目录

`touch {a..e}/file{1..4}`

 在 a-e 的目录下新建 file1-file4 文件
 
### rmdir

rmdir:remove directory 删除目录

只能删除空目录,出于安全性的考虑

`rm -rf [d_name]`

可以删除非空目录

### cp
cp: copy 复制文件
| cp   | cp 源文件 目的地(目录) |
| :---: | :------------------------ |
| -p   | 保留文件原属性             |
| -r   | 复制目录                  |


| rm   |      [filename] remove 删除文件,对 root 用户有提示,普通用户没有提示 |
| :---: | :---------------------------------------: |
| -f   | force 强制删除, root 无提示                     |
| -i   | 普通用户有提示的删除                               |
| -r   | 递归删除,慎重使用 -rf                            |

### mv

mv: move 移动 移动和重命名

mv 源文件 目的地(目录)

## 针对文件内容的基本操作

### 文件的查看

| 文件   | 命令   | 解释                                       |
| :---: | :---: | :--------------------------------------- |
| 小文件  | cat  | 以正序查看 调用内存比较多 -n 显示行号                    |
|      | tac  | 以倒序查看 调用内存比较多                            |
| 大文件  | head | 查看文件首部，默认10行 ，-n 指定行号                    |
|      | tail | 查看文件尾部，默认10行，-n指定行号                      |
|      | more | 按空格 space 下一页 b 向上翻页 enter 下一行           |
|      | less | 比 more 多了一个搜索功能 /[ 需搜索的子段 ]N 向上查找 n 向下查 q 退出 |

### 文件的修改

| 软件          | 解释                                       |
| :---------- | :--------------------------------------- |
| LibreOffice | .odt 结尾 类似于 windows office               |
| gedit       | 类似于 windows 记事本                          |
| vim         | 插入模式 后面会专门讲到 vim 编辑器的使用 退出模式 命令模式        |
| echo        | 本身代表回显 echo xxx > file 将 xxx 写入 file 文件,并覆盖原有内容 echo xxx >> file 在 file 文件追加 |

#### echo实验

```shell
[booboo@rhel7 ~]$ echo hi > file1
[booboo@rhel7 ~]$ cat file1
hi
[booboo@rhel7 ~]$ echo booboo > file1
[booboo@rhel7 ~]$ cat file1
booboo
[booboo@rhel7 ~]$ echo hihihihi >> file1
[booboo@rhel7 ~]$ cat file1
booboo
hihihihi
```

### 文件的过滤

grep: 截取行

```shell
grep [OPTIONS] PATTERN [FILE...]
过滤带有 [ 字符串 ] 的行
grep [ 字符串 ] [ 文件 ]	
过滤以 [ 字符串 ] 为开始的行
grep [^ 字符串 ] [ 文件 ]
过滤以 [ 字符串 ] 为结尾的行
grep [ 字符串 $] [ 文件 ]
过滤反选
grep -v [ 字符串 ] [ 文件 ]

eg.
过滤以 root 为开始的行
 grep ^root /etc/passwd
过滤以 bash 为结尾的行
grep bash$ /etc/passwd 
```

cut: 截取列

```shell
cut -d" 分割符 "( 以什么为分隔符 ) -fn( 第几列 ) [ 文件 ]
eg. cut -d":" -f2 /etc/resolv.conf
```

wc: 统计

```shell
wc 行数 单词数 字符数 文件名
-l 只显示行数
-w, --words 显示单词数
-c, -m,--bytes 显示字节
eg.
[root@stu15 ~]# wc /etc/resolv.conf 、
4 11 98 /etc/resolv.conf
```

sort: 排序

```shell
默认按照首字母 ACII 码
-n 按照数字大小排序
-u 剔除重复的行
-r 降序排列
-k 指定某一列
-t 分隔符
eg.sort -n -k 2 -t : file1 
将 file1 以第二列的数字排序,列以:分割
```

uniq: 剔除重复行

`uniq [file_name]`


#### 文件过滤实验

```shell

grep

[booboo@rhel7 ~]$ grep root passwd
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
[booboo@rhel7 ~]$ grep ^booboo passwd
booboo:x:1001:1001::/home/booboo:/bin/bash
[booboo@rhel7 ~]$ grep ^root passwd
root:x:0:0:root:/root:/bin/bash
[booboo@rhel7 ~]$ grep bash$ passwd
root:x:0:0:root:/root:/bin/bash
student:x:1000:1000:student:/home/student:/bin/bash
booboo:x:1001:1001::/home/booboo:/bin/bash
[booboo@rhel7 ~]$ grep -v nologin passwd
root:x:0:0:root:/root:/bin/bash
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
student:x:1000:1000:student:/home/student:/bin/bash
booboo:x:1001:1001::/home/booboo:/bin/bash

cut

[booboo@rhel7 ~]$ cut -d":" -f1 passwd
root
bin
daemon
adm
lp
sync
shutdown
halt
mail


wc

[booboo@rhel7 ~]$ wc passwd
  42   72 2121 passwd
[booboo@rhel7 ~]$ wc -l passwd
42 passwd
[booboo@rhel7 ~]$ wc -w passwd
72 passwd
[booboo@rhel7 ~]$ wc -c passwd
2121 passwd

sort

[booboo@rhel7 ~]$ vi num
[booboo@rhel7 ~]$ cat num
booboo 20 100
tom 21 100
tom 21 100
kevin 19 200
booboo 20 100
mark 20 200
[booboo@rhel7 ~]$ sort num
booboo 20 100
booboo 20 100
kevin 19 200
mark 20 200
tom 21 100
tom 21 100
[booboo@rhel7 ~]$ sort -r num
tom 21 100
tom 21 100
mark 20 200
kevin 19 200
booboo 20 100
booboo 20 100
[booboo@rhel7 ~]$ sort -u num
booboo 20 100
kevin 19 200
mark 20 200
tom 21 100
[booboo@rhel7 ~]$ sort -n -k 2 -t " " num |sort -u
booboo 20 100
kevin 19 200
mark 20 200
tom 21 100

uniq

[booboo@rhel7 ~]$ uniq num
booboo 20 100
tom 21 100
kevin 19 200
booboo 20 100
mark 20 200
```

## 帮助命令

| 命令             | 解释                                       |
| :------------- | :--------------------------------------- |
| type [ 命令 ]    | 判断是内部命令 or 外部命令                          |
| --help         | 外部命令                                     |
| help           | 只针对系统内部命令                                |
| man []         | 内容清晰、详细,在线文档,支持搜索( /name ) `man [ 章节 ] [name]` |
| info []        | 太详细                                      |
| /usr/share/doc | 存放帮助文档,在与软件同名的目录下有所有软件的使用文档              |

**man和—help以及help的区别**

_man命令_

系统中会有单独的man文件，就是说，如果系统没有安装对应man文件，哪怕命令完全正常，man都没结果（同样，只要安装了man文件，哪怕没命令，也可以得到一大堆东西）。

_--help参数_

将会显示可执行程序自带的信息，这些信息是嵌入到程序本身的，所以--help信息较简短。

_help命令_

是选项帮助命令，顾名思义  你可以把单独某个命令的某个选项列出来，方便快捷很多，省去了man当中查找的繁琐，但是help只支持shell的内部命令。内部命令即存储在shell内部可以直接调用的一些简单命令，比如说echo，cd，pwd等。

### --help 参数

--help参数是大所数命令自带的选项，用于查看使用帮助。

```shell
[booboo@rhel7 ~]$ ls --help
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      scale sizes by SIZE before printing them; e.g.,
                               '--block-size=M' prints sizes in units of
                               1,048,576 bytes; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
  -C                         list entries by columns
      --color[=WHEN]         colorize the output; WHEN can be 'never', 'auto',
                               or 'always' (the default); more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs' dired mode
  -f                         do not sort, enable -aU, disable -ls --color
```

### help

help只支持shell的内部命令。内部命令即存储在shell内部可以直接调用的一些简单命令,例如cd,echo,help等。

help(选项)(参数)
-s：输出短格式的帮助信息。仅包括命令格式。

```shell
[booboo@rhel7 ~]$ type cd
cd is a shell builtin
[booboo@rhel7 ~]$ help cd
cd: cd [-L|[-P [-e]]] [dir]
    Change the shell working directory.

    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.

    The variable CDPATH defines the search path for the directory containing
    DIR.  Alternative directory names in CDPATH are separated by a colon (:).
    A null directory name is the same as the current directory.  If DIR begins
    with a slash (/), then CDPATH is not used.

    If the directory is not found, and the shell option `cdable_vars' is set,
    the word is assumed to be  a variable name.  If that variable has a value,
    its value is used for DIR.

    Options:
        -L	force symbolic links to be followed
        -P	use the physical directory structure without following symbolic
    	links
        -e	if the -P option is supplied, and the current working directory
    	cannot be determined successfully, exit with a non-zero status

    The default is to follow symbolic links, as if `-L' were specified.

    Exit Status:
    Returns 0 if the directory is changed, and if $PWD is set successfully when
    -P is used; non-zero otherwise.
[booboo@rhel7 ~]$ type touch
touch is hashed (/bin/touch)
[booboo@rhel7 ~]$ type echo
echo is a shell builtin
[booboo@rhel7 ~]$ help echo
echo: echo [-neE] [arg ...]
```

### man
man命令是Linux下的帮助指令，通过man指令可以查看Linux中的指令帮助、配置文件帮助和编程帮助等信息。

```config
语法
man(选项)(参数)
选项
-a：在所有的man帮助手册中搜索；
-f：等价于whatis指令，显示给定关键字的简短描述信息；
-P：指定内容时使用分页程序；
-M：指定man手册搜索的路径。
参数
数字：指定从哪本man手册中搜索帮助
关键字：指定要搜索帮助的关键字
```

例如输入man ls，它会在左上角显示“ECHO(1)”“ECHO”代表手册名称；“(1)”代表 表示该手册位于第一节章1）”表示该手册位于第一节章，同样，我们输man ifconfig它会在最左上角显示“IFCONFIG（8）”。也可以这样输入命令：“man [章节号] 手册名称”。 man是按照手册的章节号的顺序进行搜索的，比如： man sleep 只会显示sleep命令的手册,如果想查看库函数sleep，就要输入: man 3 sleep

```shell
[booboo@rhel7 ~]$ man echo|cat
ECHO(1)                         User Commands                         ECHO(1)
#此处“ECHO”代表手册名称；“（1）”代表 表示该手册位于第一节章



NAME
       echo - display a line of text

SYNOPSIS
       echo [SHORT-OPTION]... [STRING]...
       echo LONG-OPTION

DESCRIPTION
       Echo the STRING(s) to standard output.

       -n     do not output the trailing newline

       -e     enable interpretation of backslash escapes

       -E     disable interpretation of backslash escapes (default)

       --help display this help and exit

       --version
              output version information and exit

       If -e is in effect, the following sequences are recognized:

       \\     backslash

       \a     alert (BEL)

       \b     backspace

       \c     produce no further output

       \e     escape

       \f     form feed

       \n     new line

       \r     carriage return

       \t     horizontal tab

       \v     vertical tab

       \0NNN  byte with octal value NNN (1 to 3 digits)

       \xHH   byte with hexadecimal value HH (1 to 2 digits)

       NOTE:  your  shell  may  have  its  own version of echo, which usually
       supersedes the version described here.  Please refer to  your  shell's
       documentation for details about the options it supports.

       GNU  coreutils  online  help: <http://www.gnu.org/software/coreutils/>
       Report echo translation bugs to <http://translationproject.org/team/>
AUTHOR
       Written by Brian Fox and Chet Ramey.
COPYRIGHT
       Copyright © 2013 Free Software Foundation, Inc.  License  GPLv3+:  GNU
       GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
       This  is  free  software:  you are free to change and redistribute it.
       There is NO WARRANTY, to the extent permitted by law.
SEE ALSO
       The full documentation for echo is maintained as a Texinfo manual.  If
       the  info  and  echo programs are properly installed at your site, the
       command
             info coreutils 'echo invocation'
      should give you access to the complete manual.

GNU coreutils 8.22               January 2014                         ECHO(1)
```

### type

type命令用来显示指定命令的类型，判断给出的指令是内部指令还是外部指令。

```shell
语法
type(选项)(参数)
选项
-t：输出“file”、“alias”或者“builtin”，分别表示给定的指令为“外部指令”、“命令别名”或者“内部指令”；
-p：如果给出的指令为外部指令，则显示其绝对路径；
-a：在环境变量“PATH”指定的路径中，显示给定指令的信息，包括命令别名。 参数 指令：要显示类型的指令。
参数
关键字：指定要搜索帮助的关键字
命令类型
alias：别名
keyword：关键字，Shell保留字
function：函数，Shell函数
builtin：内建命令，Shell内建命令
file：文件，磁盘文件，外部命令
unfound：没有找到
```

#### man,ls,touch,echo,cat 实验
```shell
[booboo@rhel7 ~]$ type man
man is /bin/man
[booboo@rhel7 ~]$ type ls
ls is aliased to `ls –color=auto'
[booboo@rhel7 ~]$ which ls
alias ls='ls --color=auto'
	/bin/ls
[booboo@rhel7 ~]$ type touch
touch is hashed (/bin/touch)
[booboo@rhel7 ~]$ type echo
echo is a shell builtin
[booboo@rhel7 ~]$ type cat
cat is hashed (/bin/cat)
```
## 关于时间的命令

### date

date命令是显示或设置系统时间与日期。 很多shell脚本里面需要打印不同格式的时间或日期，以及要根据时间和日期执行操作。延时通常用于脚本执行过程中提供一段等待的时间。日期可以以多种格式去打印，也可以使用命令设置固定的格式。在类UNIX系统中，日期被存储为一个整数，其大小为自世界标准时间（UTC）1970年1月1日0时0分0秒起流逝的秒数。

```config
语法
date(选项)(参数)
选项
-d<字符串>：显示字符串所指的日期与时间。字符串前后必须加上双引号；
-s<字符串>：根据字符串来设置日期与时间。字符串前后必须加上双引号；
 -u：显示GMT；
--help：在线帮助；
--version：显示版本信息。
参数
<+时间日期格式>：指定显示时使用的日期时间格式。
```

日期格式字符串列表
```shell
格式	说明
%H     小时，24小时制（00~23）                 
%I     小时，12小时制（01~12）                
%k     小时，24小时制（0~23）                  
%l     小时，12小时制（1~12）                  
%M     分钟（00~59）                      
%p     显示出AM或PM                        
%r     显示时间，12小时制（hh:mm:ss %p）         
%s     从1970年1月1日00:00:00到目前经历的秒数      
%S     显示秒（00~59）                      
%T     显示时间，24小时制（hh:mm:ss）            
%X     显示时间的格式（%H:%M:%S）               
%Z     显示时区，日期域（CST）                   
%a     星期的简称（Sun~Sat）                  
%A     星期的全称（Sunday~Saturday）          
%h,%b  月的简称（Jan~Dec）                   
%B     月的全称（January~December）          
%c     日期和时间（Tue Nov 20 14:12:58 2012） 
%d     一个月的第几天（01~31）                  
%x,%D  日期（mm/dd/yy）                    
%j     一年的第几天（001~366）                 
%m     月份（01~12）                       
%w     一个星期的第几天（0代表星期天）                
%W     一年的第几个星期（00~53，星期一为第一天）         
%y     年的最后两个数字（1999则是99）              
%Y     年1999                           
```

|格式  | 说明                              |
|:-------:| :------------------------------ |
%H    | 小时，24小时制（00~23）                 |
%I    | 小时，12小时制（01~12）                 |
%k    | 小时，24小时制（0~23）                  |
%l    | 小时，12小时制（1~12）                  |
%M    | 分钟（00~59）                       |
%p    | 显示出AM或PM                        |
%r    | 显示时间，12小时制（hh:mm:ss %p）         |
%s    | 从1970年1月1日00:00:00到目前经历的秒数      |
%S    | 显示秒（00~59）                      |
%T    | 显示时间，24小时制（hh:mm:ss）            |
%X    | 显示时间的格式（%H:%M:%S）               |
%Z    | 显示时区，日期域（CST）                   |
%a    | 星期的简称（Sun~Sat）                  |
%A    | 星期的全称（Sunday~Saturday）          |
%h,%b | 月的简称（Jan~Dec）                   |
%B    | 月的全称（January~December）          |
%c    | 日期和时间（Tue Nov 20 14:12:58 2012） |
%d    | 一个月的第几天（01~31）                  |
%x,%D | 日期（mm/dd/yy）                    |
%j    | 一年的第几天（001~366）                 |
%m    | 月份（01~12）                       |
%w    | 一个星期的第几天（0代表星期天）                |
%W    | 一年的第几个星期（00~53，星期一为第一天）         |
%y    | 年的最后两个数字（1999则是99）              |
%Y    | 年1999                           |


#### date 实验

```shell
格式化输出
[booboo@rhel7 ~]$ date +"%y/%m/%d"
16/06/16
[booboo@rhel7 ~]$ date +"%Y/%m/%d"
2016/06/16
输出昨天或后天的日期
[booboo@rhel7 ~]$ date -d "1 day ago" +"%Y-%m-%d"
2016-06-15
[booboo@rhel7 ~]$ date -d "-1 day" +%Y%m%d
20160615
[booboo@rhel7 ~]$ date -d "+1 day" +%Y%m%d
20160617
输出50秒后的时间
[booboo@rhel7 ~]$ date -d "50 second" +"%Y-%m-%d %H:%M:%S"
2016-06-16 02:52:41
传说中的1234567890秒
[booboo@rhel7 ~]$ date -d "1970-01-01 1234567890 seconds" +"%Y-%m-%d %H:%M:%S"
2009-02-13 23:31:30
2009年2月13日星期五，协调世界时（UTC）晚上11:31:30，UNIX时间将抵达1234567890秒。
UNIX时间是UNIX或类UNIX系统使用的时间表示方式：从协调世界时1970年1月1日0时0分0秒起至现在的总秒数，不包括闰秒。由于大部分UNIX的系统都是32位，因此到2038年时间计数就可能溢出，解决方法是更换为64位模式。Linux内核开发者Alan Cox表示，Linux现在都运行64位时间模式，它可以记录到2900亿年后，因此即使太阳燃料用尽也不会出问题。
普通格式转化
[booboo@rhel7 ~]$ date -d "2016-06-16" +"%Y/%m/%d %H:%M:%S"
2016/06/16 00:00:00
设定时间需要root用户权限，此处用booboo用户模拟，没有真的修改时间
[booboo@rhel7 ~]$ date
Thu Jun 16 03:01:19 EDT 2016
[booboo@rhel7 ~]$ date -s "02:03:08 2018-05-09"
date: cannot set date: Operation not permitted
Wed May  9 02:03:08 EDT 2018
[booboo@rhel7 ~]$ date -s "02:03:08 20180509"
date: cannot set date: Operation not permitted
Wed May  9 02:03:08 EDT 2018
[booboo@rhel7 ~]$ date -s "20180509 15:02:02"
date: cannot set date: Operation not permitted
Wed May  9 15:02:02 EDT 2018
[booboo@rhel7 ~]$ date -s "2018-05-09 15:02:02"
date: cannot set date: Operation not permitted
Wed May  9 15:02:02 EDT 2018
[booboo@rhel7 ~]$ date -s "2019/05/09 15:02:02"
date: cannot set date: Operation not permitted
Thu May  9 15:02:02 EDT 2019
```
#### date 拓展实验

1) 有时需要检查一组命令花费的时间 比如

```shell
ping执行的时间
[root@rhel7 ~]# vi a.sh
[root@rhel7 ~]# cat a.sh
#!/bin/bash
start=$(date +%s)
ping -c 10 172.25.0.11 &> /dev/null
end=$(date +%s)
difference=$(( $end - $start ))
echo $difference seconds.
[root@rhel7 ~]# bash a.sh
9 seconds.
sql脚本运行的是时间
#!/bin/bash
start=$(date +%s)
$mysql< mysql.all.sql &> /dev/null
end=$(date +%s)
difference=$(( $end - $start ))
echo $difference seconds.
```

2) 创建以当前时间为文件名的目录

```shell
[root@rhel7 ~]# mkdir `date +%Y%m%d`
[root@rhel7 ~]# ls
20160616  
```

3）备份以时间做为文件名的

```shell
[root@rhel7 ~]# tar -cvf `date +%Y%m%d`.tar ./`date +%Y%m%d`
./20160616/
[root@rhel7 ~]# ls
20160616         Documents                         Pictures
20160616.tar
```

4）编写shell脚本计算离自己生日还有多少天？
```shell
[root@rhel7 ~]# cat bb.sh
#!/bin/bash
read -p "Input your birthday(YYYYmmdd):" date1
m=`date -d "$date1" +%m`    #得到生日的月
d=`date -d "$date1" +%d`    #得到生日的日
date_now=`date +%s`             #得到当前时间的秒值
y=`date +%Y`                    #得到当前时间的年
birth=`date -d "$y$m$d" +%s`      #得到今年的生日日期的秒值
internal=$(($birth-$date_now))        #计算今日到生日日期的间隔时间
if [ "$internal" -lt "0" ]; then             #判断今天的生日是否已过
       	birth=`date --date="$(($y+1))$m$d" +%s`      #得到明年的生日日期秒值
       	internal=$(($birth-$date_now))               #计算今天到下一个生日的间隔时间
fi
        echo "There is :$(($internal/60/60/24)) days."       #输出结果，秒换算为天
Input your birthday(YYYYmmdd):19960506
There is :323 days.
[root@rhel7 ~]# bash bb.sh
Input your birthday(YYYYmmdd):19960902
There is :77 days.
```

### hwclock
hwclock命令是一个硬件时钟访问工具，它可以显示当前时间、设置硬件时钟的时间和设置硬件时钟为系统时间，也可设置系统时间为硬件时钟的时间。 在Linux中有硬件时钟与系统时钟等两种时钟。硬件时钟是指主机板上的时钟设备，也就是通常可在BIOS画面设定的时钟。系统时钟则是指kernel中的时钟。当Linux启动时，系统时钟会去读取硬件时钟的设定，之后系统时钟即独立运作。所有Linux相关指令与函数都是读取系统时钟的设定。

查看 BIOS 时间

修改 BIOS 时间

`hwclock --systohc` 将硬件时间与系统时间同步,以系统为基准

`hwclock --hctosys` 将系统时间与硬件时间同步,以硬件为基准

### timedatectl

比 date 多了时区的功能

rhel6修改时区
```shell
[booboo@rhel7 ~]$ tzselect
Please identify a location so that time zone rules can be set correctly.
Please select a continent or ocean.
 1) Africa
 2) Americas
 3) Antarctica
 4) Arctic Ocean
 5) Asia
 6) Atlantic Ocean
 7) Australia
 8) Europe
 9) Indian Ocean
10) Pacific Ocean
11) none - I want to specify the time zone using the Posix TZ format.
\#? 5
Please select a country.
 1) Afghanistan		  18) Israel		    35) Palestine
 2) Armenia		  19) Japan		    36) Philippines
 3) Azerbaijan		  20) Jordan		    37) Qatar
 4) Bahrain		  21) Kazakhstan	    38) Russia
 5) Bangladesh		  22) Korea (North)	    39) Saudi Arabia
 6) Bhutan		  23) Korea (South)	    40) Singapore
 7) Brunei		  24) Kuwait		    41) Sri Lanka
 8) Cambodia		  25) Kyrgyzstan	    42) Syria
 9) China		  26) Laos		    43) Taiwan
10) Cyprus		  27) Lebanon		    44) Tajikistan
11) East Timor		  28) Macau		    45) Thailand
12) Georgia		  29) Malaysia		    46) Turkmenistan
13) Hong Kong		  30) Mongolia		    47) United Arab Emirates
14) India		  31) Myanmar (Burma)	    48) Uzbekistan
15) Indonesia		  32) Nepal		    49) Vietnam
16) Iran		  33) Oman		    50) Yemen
17) Iraq		  34) Pakistan
\#? 9
Please select one of the following time zone regions.
1) east China - Beijing, Guangdong, Shanghai, etc.
2) Heilongjiang (except Mohe), Jilin
3) central China - Sichuan, Yunnan, Guangxi, Shaanxi, Guizhou, etc.
4) most of Tibet & Xinjiang
5) west Tibet & Xinjiang
\#? 1

The following information has been given:

	China
	east China - Beijing, Guangdong, Shanghai, etc.

Therefore TZ='Asia/Shanghai' will be used.
Local time is now:	Thu Jun 16 15:08:57 CST 2016.
Universal Time is now:	Thu Jun 16 07:08:57 UTC 2016.
Is the above information OK?
1) Yes
2) No
\#? 1

You can make this change permanent for yourself by appending the line
	TZ='Asia/Shanghai'; export TZ
to the file '.profile' in your home directory; then log out and log in again.

Here is that TZ value again, this time on standard output so that you
can use the /bin/tzselect command in shell scripts:
Asia/Shanghai
```

rhel7 版本
```shell
[kiosk@foundation0 Desktop]$ timedatectl
      Local time: Wed 2016-06-15 16:47:40 CST
  Universal time: Wed 2016-06-15 08:47:40 UTC
        RTC time: Wed 2016-06-15 16:47:40
       Time zone: Asia/Shanghai (CST, +0800)
     NTP enabled: yes
NTP synchronized: yes
 RTC in local TZ: yes
      DST active: n/a
```

关键词：
```shell
UTC	协调世界时 Coordinated Universal Time
	又称世界统一时间，世界标准时间，国际协调时间。1972 年1 月1日，UTC（协调世界时）成为新的世界标准时间。
CST	时区缩写
	CST可以为如下4个不同的时区的缩写：
　　	美国中部时间：Central Standard Time (USA) UT-6:00
	澳大利亚中部时间：Central Standard Time (Australia) UT+9:30
	中国标准时间：China Standard Time UT+8:00 例如，UTC是0点，那么CST中国为早晨8点
	古巴标准时间：Cuba Standard Time UT-4:00
RTC Time
	硬件时钟时间
	set-local-rtc 1 本地时区
	set-local-rtc 0	UTC
DST	Daylight Saving Time日光节约时间、夏令时
	是一种为节约能源而人为规定地方时间的制度，在这一制度实行期间所采用的统一时间称为“夏令时间”。
	一般在天亮早的夏季人为将时间提前一小时，可以使人早起早睡，减少照明量，以充分利用光照资源，从而节约照明用电。
	各个采纳夏时制的国家具体规定不同。目前全世界有近110个国家每年要实行夏令时。
	1986年至1991年，中国在全国范围实行了六年夏令时，1992年4月5日后不再实行。
```

### cal

cal命令用于显示当前日历，或者指定日期的日历。
```shell
cal [-smjy13] [[[day] month] year]
-1 显示当月日历并将今日标黑
-3 显示上个月、当月、下个月。
-s 周日作为第一列
-m 周一作为第一列
-j 列出今天是一年的第几天
-y 列出今年所有的月
[root@rhel7 ~]# cal
      June 2016     
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30

[root@rhel7 ~]# cal -3
      May 2016              June 2016             July 2016     
Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa  Su Mo Tu We Th Fr Sa
 1  2  3  4  5  6  7            1  2  3  4                  1  2
 8  9 10 11 12 13 14   5  6  7  8  9 10 11   3  4  5  6  7  8  9
15 16 17 18 19 20 21  12 13 14 15 16 17 18  10 11 12 13 14 15 16
22 23 24 25 26 27 28  19 20 21 22 23 24 25  17 18 19 20 21 22 23
29 30 31              26 27 28 29 30        24 25 26 27 28 29 30
                                            31                  
[root@rhel7 ~]# cal -j
         June 2016         
Sun Mon Tue Wed Thu Fri Sat
            153 154 155 156
157 158 159 160 161 162 163
164 165 166 167 168 169 170
171 172 173 174 175 176 177
178 179 180 181 182
```

## Linux压缩打包

### 压缩的原理

目前我们使用的计算机系统中都是使 bytes(字节)单位来计量的! 事实上 , 计算机最小的计量单位应该是 bits (比特)。

1 byte = 8 bits 。

如果让计算机记录 1 这个数字他会如何记录 ?

假设一个 byte 可以看成下面的样子 :

□□□□□□□□

Tips:

1 byte = 8 bits , 所以每个 byte 当中会有 8 个空格 , 而每个空格可以是 0, 或者 1 , 这里仅是做为一个粗略的介绍。由于我们记录数字是 1 , 表示成二进制就是 00000001 , 1 会在最右边占据 1 个 bit , 而其他 的 7 个bits 将会被填上 0 ! 有一种压缩技术示这么做的,他是将重复的数据进行统计记录的。

举个例子说 , 如果你的数据『 111.... 』共有 100 个 1 

那么压缩技术会记录为『 100 个 1 』而不是真的有 100 个 1 的位存在 ! 

简单的说 , 你可以将他想成 , 其实文件里面有相当多的『空间』存在 , 并不是完全填满的 

- 『压缩』 技术就是将这些『空间』填满 , 以让整个文件占用的容量下降 ! 
- 『压缩过的档案』并无法直接被我们的操作系统所使用 , 因此 , 若要使用这些被压缩过的文件数据 , 则必项将他『还原』回到 未压缩前的模样 ,那就是所谓的『解压缩』啰 ! 
- 至于压缩前与压缩后的档案所占用的磁盘空间大小 , 就可以被称为是『压缩比』。


### 压缩与解压缩的好处

最大的好处就是压缩过的文件容量变小了 , 所以你的 硬盘容量无形当中就可以容纳更多的资料。此外 , 在一些网络数据的传输中 , 也会由于数据量的降低 , 好让网络带宽可以用来作更多的工作 ! 而并是老是卡在一些大型的文件传输上面呢 ! 目前很多的 WWW 网站也是利用文件压缩的技术来进行数据的传送 , 好让网站带宽的可利用率上升。

### 压缩打包命令

命令概览

* compress 是一个相当古老的 unix 档案压缩指令。

* gzip 是 GNUzip 的缩写,它是一个 GNU( 全称是 GNU's Not Unix ) 自由软件的文件压缩程序 ; 由于 gzip 可以产生更理想的压缩比例,一般人多已改用 gzip 为档案压缩工具。

* bzip2 是一个基于 Burrows-Wheeler 变换的无损压缩软件,压缩效果比传统的 LZ77/LZ78 压缩算法来得好 ; 若说 gzip 是为了取代 compress 并提供更好的压缩比而成立的,那么 bzip2 则是为了取代 gzip 并提供更佳的压缩比而来的。 bzip2 这玩意的压缩比竟然比 gzip 还要好。

* tar 命令最初的设计目的是将文件备份到磁带上 (tape archive) ,因而得名 tar 。

![01](pic/01.png)

#### .zip

.zip 扩展名表示文件是使用许多 zip 归档程序和压缩程序之一(但不是 gzip )创建的。因为这是一种非常流行的压缩格式,算法的详细描述也有很多,所以可以找到用于所有操作系统的有用的移植形式。这包括创建和扩展带有 .zip 文件扩展名的档案的压缩和解压缩实用程序。在 Linux 上有两种这样的工具:

免费的 Info-ZIP 和以赢利为目的的 PKZIP for Linux 。

如果您只是偶尔需要创建或打开 zip 文件,使用 Info-ZIP 。如果希望使用在 MS-DOS 或其它系统上使用的相同工具,请选择PKZIP ( PKZIP 可用于许多操作系统)。用于微软 Windows 的 WinZIP 和用于 Mac OS 的Stufflt 这两种实用程序可以创建和打开相互之间兼容的档案。

Info-ZIP 在无法使用 gzip 或 tar 的情况下可以提供压缩和解压缩的一个不错的选择,这或许是在Linux 、微软 Windows 和 Mac OS 用户之间交换压缩文件的一种最好的形式。有许多不错的 zip 程序(有开放源码的,也有商业的)可用于这些操作系统,它们应该能确保文件的顺利交换(当然,只要是在特定于某个特定工具的特殊功能关闭的情况下)。

rhel7 默认带有 info-zip 软件

```shell
[root@mastera0 zip-3.0]# which zip
/usr/bin/zip
[root@mastera0 zip-3.0]# rpm -qf /usr/bin/zip
zip-3.0-10.el7.x86_64
[root@mastera0 zip-3.0]# head -n 18 /usr/share/doc/zip-3.0/README
Zip 3.0 is the first Zip update adding large file support. For now Zip 2.3x
remains available and supported, but users should switch to this new release.
Testing for Zip 3.0 has focused mainly on Unix, VMS, Max OS X, and Win32,
and some other ports may not be fully supported yet. If you find your
favorite port is broke, send us the details or, better, send bug fixes. It's
possible that support for some older ports may be dropped in the future.
Copyright (c) 1990-2008 Info-ZIP. All rights reserved.
See the accompanying file LICENSE (the contents of which are also included
in unzip.h, zip.h and wiz.h) for terms of use. If, for some reason, all
of these files are missing, the Info-ZIP license also may be found at:
ftp://ftp.info-zip.org/pub/infozip/license.html and
http://www.info-zip.org/pub/infozip/license.html.
[root@mastera0 ~]# rpm -qi zip
Name
: zip
Version : 3.0
Release : 10.el7
Architecture: x86_64
Install Date: Thu 23 Jun 2016 01:50:41 PM CST
Group
: Applications/Archiving
Size
: 815045License : BSD
Signature : RSA/SHA256, Thu 03 Apr 2014 06:52:17 AM CST, Key ID 199e2f91fd431d51
Source RPM : zip-3.0-10.el7.src.rpm
Build Date : Tue 28 Jan 2014 06:35:49 AM CST
Build Host : x86-019.build.eng.bos.redhat.com
Relocations : (not relocatable)
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Vendor
: Red Hat, Inc.
URL
: http://www.info-zip.org/Zip.html
Summary : A file compression and packaging utility compatible with PKZIP
Description :
The zip program is a compression and file packaging utility. Zip is
analogous to a combination of the UNIX tar and compress commands and
is compatible with PKZIP (a compression and file packaging utility for
MS-DOS systems).
Install the zip package if you need to compress files using the zip
program.
```

##### zip 命令用法

zip 命令可以用来解压缩文件,或者对文件进行打包操作。 zip 是个使用广泛的压缩程序,文件经它压缩后会另外产生具有 “ .zip” 扩展名的压缩文件。

```shell
语法 zip( 选项 )( 参数 )

选项

-A :调整可执行的自动解压缩文件;
-b< 工作目录 > :指定暂时存放文件的目录;
-c :替每个被压缩的文件加上注释;
-d :从压缩文件内删除指定的文件;
-D :压缩文件内不建立目录名称;
-f :此参数的效果和指定 “ -u” 参数类似,但不仅更新既有文件,如果某些文件原本不存在于压缩文
件内,使用本参数会一并将其加入压缩文件中;
-F :尝试修复已损坏的压缩文件;
-g :将文件压缩后附加在已有的压缩文件之后,而非另行建立新的压缩文件;
-h :在线帮助;
-i< 范本样式 > :只压缩符合条件的文件;
-j :只保存文件名称及其内容,而不存放任何目录名称;
-J :删除压缩文件前面不必要的数据;
-k :使用 MS-DOS 兼容格式的文件名称;
-l :压缩文件时,把 LF 字符置换成 LF+CR 字符;
-ll :压缩文件时,把 LF+cp 字符置换成 LF 字符;
-L :显示版权信息;
-m :将文件压缩并加入压缩文件后,删除原始文件,即把文件移到压缩文件中;
-n< 字尾字符串 > :不压缩具有特定字尾字符串的文件;
-o :以压缩文件内拥有最新更改时间的文件为准,将压缩文件的更改时间设成和该文件相同;
-q :不显示指令执行过程;
-r :递归处理,将指定目录下的所有文件和子目录一并处理;
-S :包含系统和隐藏文件;
-t< 日期时间 > :把压缩文件的日期设成指定的日期;
-T :检查备份文件内的每个文件是否正确无误;
-u :更换较新的文件到压缩文件内;
-v :显示指令执行过程或显示版本信息;
-V :保存 VMS 操作系统的文件属性;
-w :在文件名称里假如版本编号,本参数仅在 VMS 操作系统下有效;
-x< 范本样式 > :压缩时排除符合条件的文件;
-X :不保存额外的文件属性;
-y :直接保存符号连接,而非该链接所指向的文件,本参数仅在 UNIX 之类的系统下有效;
-z :替压缩文件加上注释;
-$ :保存第一个被压缩文件所在磁盘的卷册名称;
-< 压缩效率 > :压缩效率是一个介于 1~9 的数值。
参数
zip 压缩包:指定要创建的 zip 压缩包;
文件列表:指定要压缩的文件列表。
实例
zip -q -r html.zip /home/Blinux/html
zip -q -r html.zip *
```

##### unzip 的用法

unzip 命令用于解压缩由 zip 命令压缩的 “ .zip” 压缩包

```shell
语法 unzip( 选项 )( 参数 )

选项

-c :将解压缩的结果显示到屏幕上,并对字符做适当的转换;
-f :更新现有的文件;
-l :显示压缩文件内所包含的文件;
-p :与 -c 参数类似,会将解压缩的结果显示到屏幕上,但不会执行任何的转换;
-t :检查压缩文件是否正确;
-u :与 -f 参数类似,但是除了更新现有的文件外,也会将压缩文件中的其他文件解压缩到目录中;
-v :执行时显示详细的信息;
-z :仅显示压缩文件的备注文字;
-a :对文本文件进行必要的字符转换;
-b :不要对文本文件进行字符转换;
-C :压缩文件中的文件名称区分大小写;
-j :不处理压缩文件中原有的目录路径;
-L :将压缩文件中的全部文件名改为小写;
-M :将输出结果送到 more 程序处理;
-n :解压缩时不要覆盖原有的文件;
-o :不必先询问用户, unzip 执行后覆盖原有的文件;
-P< 密码 > :使用 zip 的密码选项;
-q :执行时不显示任何信息;
-s :将文件名中的空白字符转换为底线字符;
-V :保留 VMS 的文件版本信息;
-X :解压缩时同时回存文件原来的 UID/GID ;
-d< 目录 > :指定文件解压缩后所要存储的目录;
-x< 文件 > :指定不要处理 .zip 压缩文件中的哪些文件;
-Z : unzip-Z 等于执行 zipinfo 指令

参数 压缩包:指定要解压的 “ .zip” 压缩包。

实例

unzip test.zip
unzip -v test.zip
unzip -n test.zip -d /tmp
```

#### .gz

##### gzip 的用法

gzip 命令用来压缩文件。 gzip 是个使用广泛的压缩程序,文件经它压缩过后,其名称后面会多处 “ .gz”扩展名。 gzip 是在 Linux 系统中经常使用的一个对文件进行压缩和解压缩的命令,既方便又好用。

gzip 不仅可以用来压缩大的、较少使用的文件以节省磁盘空间,还可以和 tar 命令一起构成 Linux 操作系统中比较流行的压缩文件格式。据统计, gzip 命令对文本文件有 60% ~ 70% 的压缩率。减少文件大小有两个明显的好处,一是可以减少存储空间,二是通过网络传输文件时,可以减少传输的时间。

```shell
语法 gzip( 选项 )( 参数 )

选项

-a 或 —— ascii :使用 ASCII 文字模式;
-d 或 --decompress 或 ----uncompress :解开压缩文件;
-f 或 —— force :强行压缩文件。不理会文件名称或硬连接是否存在以及该文件是否为符号连接;
-h 或 —— help :在线帮助;
-l 或 —— list :列出压缩文件的相关信息;
-L 或 —— license :显示版本与版权信息;
-n 或 --no-name :压缩文件时,不保存原来的文件名称及时间戳记;
-N 或 —— name :压缩文件时,保存原来的文件名称及时间戳记;
-q 或 —— quiet :不显示警告信息;
-r 或 —— recursive :递归处理,将指定目录下的所有文件及子目录一并处理;
-S 或 < 压缩字尾字符串 > 或 ----suffix< 压缩字尾字符串 > :更改压缩字尾字符串;
-t 或 —— test :测试压缩文件是否正确无误;
-v 或 —— verbose :显示指令执行过程;
-V 或 —— version :显示版本信息;
-< 压缩效率 > :压缩效率是一个介于 1~9 的数值,预设值为 “ 6” ,指定愈大的数值,压缩效率就会
愈高;
--best :此参数的效果和指定 “ -9” 参数相同;
--fast :此参数的效果和指定 “ -1” 参数相同。

参数 文件列表:指定要压缩的文件或指定要解压的文件。。

实例

gzip * 将当前目录下的每个文件都压缩成 .gz 文件
gzip test 将 test 文件压缩成 test.gz 文件并删除源文件
gzip -rv /tmp 第归压缩目录中的所有文件,压缩成 .gz 结尾的文件,并显示指令执行过程
gizp -dr /tmp 第归解压 /tmp 目录下的 .gz 结尾的文件
```

##### gunzip 的用法

gunzip 命令用来解压缩文件。 gunzip 是个使用广泛的解压缩程序,它用于解开被 gzip 压缩过的文件,这些压缩文件预设最后的扩展名为 .gz 。其实压缩或解压缩,都可通过 gzip 指令单独完成。

```shell
语法 gunzip( 选项 )( 参数 )

选项

-a 或 —— ascii :使用 ASCII 文字模式;
-c 或 --stdout 或 --to-stdout :把解压后的文件输出到标准输出设备;
-f 或 -force :强行解开压缩文件,不理会文件名称或硬连接是否存在以及该文件是否为符号连接;
-h 或 —— help :在线帮助;
-l 或 —— list :列出压缩文件的相关信息;
-L 或 —— license :显示版本与版权信息;
-n 或 --no-name :解压缩时,若压缩文件内含有原来的文件名称及时间戳记,则将其忽略不予处理;
-N 或 —— name :解压缩时,若压缩文件内含有原来的文件名称及时间戳记,则将其回存到解开
的文件上;
-q 或 —— quiet :不显示警告信息;
-r 或 —— recursive :递归处理,将指定目录下的所有文件及子目录一并处理;
-S 或 < 压缩字尾字符串 > 或 ----suffix< 压缩字尾字符串 > :更改压缩字尾字符串;
-t 或 —— test :测试压缩文件是否正确无误;
-v 或 —— verbose :显示指令执行过程;
-V 或 —— version :显示版本信息;

参数 文件列表:指定要解压的压缩包。

实例
gzip -d test.gz
gunzip test.gz
效果一样
```

#### .bz2

##### bzip2 的用法

bzip2 命令用于创建和管理(包括解压缩) “ .bz2” 格式的压缩包。

```shell
语法 bzip2( 选项 )( 参数 )

选项

-c 或 —— stdout :将压缩与解压缩的结果送到标准输出;
-d 或 —— decompress :执行解压缩;
-f 或 -force : bzip2 在压缩或解压缩时,若输出文件与现有文件同名,预设不会覆盖现有文件。若
要覆盖。请使用此参数;
-h 或 —— help :在线帮助;
-k 或 —— keep : bzip2 在压缩或解压缩后,会删除原始文件。若要保留原始文件,请使用此参数;
-s 或 —— small :降低程序执行时内存的使用量;
-t 或 —— test :测试 .bz2 压缩文件的完整性;
-v 或 —— verbose :压缩或解压缩文件时,显示详细的信息;
-z 或 —— compress :强制执行压缩;
-V 或 —— version :显示版本信息;
--repetitive-best :若文件中有重复出现的资料时,可利用此参数提高压缩效果;
--repetitive-fast :若文件中有重复出现的资料时,可利用此参数加快执行效果。

参数 文件列表:指定要压缩的文件或指定要解压的文件。

实例

bzip2 test 压缩 test 文件,生成压缩文件 test.bz2 ,并删除源文件
bzip2 -k test 压缩 test 文件,生成压缩文件 test.bz2 ,并保留源文件
bzip2 -d test.bz2 解压文件
bunzip2 test.bz2 解压文件
```

##### bunzip2 的用法

bunzip2 命令解压缩由 bzip2 指令创建的 ” .bz2" 压缩包。对文件进行压缩与解压缩。此命令类似于“ gzip/gunzip” 命令,只能对文件进行压缩。对于目录只能压缩目录下的所有文件,压缩完成后,在目录下生成以 “ .bz2” 为后缀的压缩包。 bunzip2 其实是 bzip2 的符号链接,即软链接,因此压缩解压都可以通过 bzip2 实现。

```shell
[root@mastera0 ~]# which bzip2
/usr/bin/bzip2
[root@mastera0 ~]# which bunzip2
/usr/bin/bunzip2
[root@mastera0 ~]# ll -i /usr/bin/bzip2
33853111 -rwxr-xr-x. 1 root root 36752 Jul 31 2014 /usr/bin/bzip2
[root@mastera0 ~]# ll -i /usr/bin/bunzip2
34293684 lrwxrwxrwx. 1 root root 5 Jun 23 13:50 /usr/bin/bunzip2 -> bzip2

bunzip2 [ -fkvsVL ] [ filenames ... ]

-f 或 --force :解压缩时,若输出的文件与现有文件同名时,预设不会覆盖现有的文件;
-k 或 --keep :在解压缩后,预设会删除原来的压缩文件。若要保留压缩文件,请使用此参数;
-s 或 --small :降低程序执行时,内存的使用量;
-v 或 --verbose :解压缩文件时,显示详细的信息;
-l , --license , -V 或 —— version :显示版本信息。
```


#### .xz

XZ Utils 是为 POSIX 平台开发具有高压缩率的工具。它使用 LZMA2 压缩算法,生成的压缩文件比POSIX 平台传统使用的 gzip、bzip2 生成的压缩文件更小,而且解压缩速度也很快。最初 XZ Utils的是基于 LZMA-SDK 开发,但是 LZMA-SDK 包含了一些 WINDOWS 平台的特性,所以 XZ Utils 为以适应 POSIX 平台作了大幅的修改。XZ Utils 的出现也是为了取代 POSIX 系统中旧的 LZMA Utils。XZ Utils 主要包含了下列部分:

* 命令行程序 xz ,用来生成和解压缩 .xz 压缩文件。
* 一组实用的脚本工具 (xzcat, xdiff, xzgrep 等)提供浏览,查找以及比较 .xz 文件内
容等功能。
* liblzma 压缩库,提供算法的实现和近似于 ZLIB 的编程接口。
* 提供对 LZMA Utils 的一些兼容

xz 文件格式

XZ Utils 工具生成的压缩文件扩展名为 .xz (MIME 类型为"application/x-xz")。

.xz 文件格式具有下列特点:

* 基于数据流: 易于通过管道 (pipe) 生成压缩文件或解压缩文件。.xz 文件格式与 .gz/.bz2 文件一样,不具备对多个文件进行归档打包的能力。若要处理多个文件,可以和归档工具 tar 结合使用,生成扩展名为 .tar.xz 或 .txz 的压缩文件。
* 随机读取: 存储的数据被划分为独立的压缩块,并对每个压缩块进行索引,当每个压缩块比较小时,便能够进行有限的随机读取压缩数据。
* 完整性验证: 可以使用 CRC32、CRC64、SHA-256 来进行数据的完整性验证,也可以增加自定义验证方法。
* 可连接(concatenation): 类似于 .gz/.bz2 文件,可以把多个压缩数据流连接到一个文件中。解压缩时,就像解压一个正常单压缩流文件一样。
* 支持多 filter 和 filter 链: 提供自定义 filter 的能力,也能够将多个 filter 组成filter 链,对数据进行处理。这点与 Unix 命令间使用的管道 (pipe) 类似。
* 可填充(padding): 可以在 .xz 文件末尾填充二进制'0'以充满特定大小的空间,比如备份磁带上的一个块 (block)。

XZ Utils 具有高压缩率,解压速度快的特点。能够生成更小文件的同时,也能提供稳定快速的解压,在对数据大小比较敏感的场合,比如说大数据的网络传输,文件的备份,处理能力有限的嵌入系统等场合,有着十分广泛的用途。

##### xz 命令用法

```shell
语法 xz ( 选项 )( 参数 )

选项

-z, --compress
force compression 强制压缩
-d, --decompress, --uncompress
force decompression 解开压缩文件
-t, --test test compressed file integrity 测试压缩文件是否正确无误
-l, --list list information about .xz files 列出压缩文件的相关信息
-k, --keep keep (don't delete) input files 不删除源文件
-f, --force force overwrite of output file and (de)compress links 强制压缩,覆盖输出文件同名的文件
-c, --stdout, --to-stdout write to standard output and don't delete input files 写入标准输出,不要删除输入文件
-0 ... -9 compression preset; default is 6; take compressor *and* decompressor memory usage into account before using 7-9! 压缩效率是一个介于
1~9 的数值,预设值为 “ 6” ,指定愈大的数值,压缩效率就会愈高;解压由县考虑使用 7-9
-e, --extreme try to improve compression ratio by using more CPU time; does not affect decompressor memory requirements 通过使用更多的处理器时间
来提高压缩比;不影响解压时的内存需求
-T, --threads=NUM use at most NUM threads; the default is 1; set to 0 to use the number of processor cores 最多使用的线程数量,默认为 1 ,如果设置为
0 去使用处理器内核的数量
-q, --quiet suppress warnings; specify twice to suppress errors too 抑制警告;指定两次
以抑制错误
-v, --verbose be verbose; specify twice for even more verbose
-h, --help display this short help and exit
-H, --long-help display the long help (lists also the advanced options)
-V, --version display the version number and exit

参数 文件列表:指定要压缩的文件列表。

实例
xz test 压缩一个文件 test ,压缩成功后删除源文件
xz -d -k test.xz 解压 test.xz 文件, -k 参数保证源文件不被删除
xz -l test.xz 查看基本信息,包括压缩率等
xz -k7 test 使用参数 -0, -1, -2, ... -6, ... -9 或参数 --fast, --best 设定压缩率。 xz 命令的默认为-6 。
借助 xargs 命令并行压缩多文件。下面的命令行可以将 /var/log 目录下所有的扩展名为 .log 的文件压缩。通过 xargs 命令同时运行多个 xz 进行压缩。
find /var/log -type f -iname "*.log" -print0 | xargs -P4 -n16 xz -T1
注意:运行此命令须有 root 权限。
```


#### tar

tar 命令可以为 linux 的文件和目录创建档案。利用 tar ,可以为某一特定文件创建档案(备份文件),也可以在档案中改变文件,或者向档案中加入新的文件。 tar 最初被用来在磁带上创建档案,现在,用户可以在任何设备上创建档案。利用 tar 命令,可以把一大堆的文件和目录全部打包成一个文件,这对于备份文件或将几个文件组合成为一个文件以便于网络传输是非常有用的。

首先要弄清两个概念:打包和压缩。

* 打包是指将一大堆文件或目录变成一个总的文件;
* 压缩则是将一个大的文件通过一些压缩算法变成一个小文件。

为什么要区分这两个概念呢?

这源于 Linux 中很多压缩程序只能针对一个文件进行压缩,这样当你想要压缩一大堆文件时,你得先将这一大堆文件先打成一个包( tar 命令),然后再用压缩程序进行压缩( gzip bzip2 命令)。

```shell
语法 tar ( 选项 )( 参数 )

选项
-A 或 --catenate :新增文件到以存在的备份文件;
-B :设置区块大小;
-c 或 --create :建立新的备份文件;
-C < 目录 > :这个选项用在解压缩,若要在特定目录解压缩,可以使用这个选项。
-d :记录文件的差别;
-x 或 --extract 或 --get :从备份文件中还原文件;
-t 或 --list :列出备份文件的内容;
-z 或 --gzip 或 --ungzip :通过 gzip 指令处理备份文件;
-Z 或 --compress 或 --uncompress :通过 compress 指令处理备份文件;
-f< 备份文件 > 或 --file=< 备份文件 > :指定备份文件;
-v 或 --verbose :显示指令执行过程;
-r :添加文件到已经压缩的文件;
-u :添加改变了和现有的文件到已经存在的压缩文件;
-j :支持 bzip2 解压文件;
-J :支持 xz 解压文件;
-v :显示操作过程;
-l :文件系统边界设置;
-k :保留原有文件不覆盖;
-m :保留文件不被覆盖;
-w :确认压缩文件的正确性;
-p 或 --same-permissions :用原来的文件权限还原文件;
-P 或 --absolute-names :文件名使用绝对名称,不移除文件名称前的 “ /” 号;
-N < 日期格式 > 或 --newer=< 日期时间 > :只将较指定日期更新的文件保存到备份文件里;
--exclude=< 范本样式 > :排除符合范本样式的文件。

参数 文件列表:指定要打包的文件或目录列表。

实例
tar -cvf log.tar log2012.log 仅打包,不压缩! tar -xf 解压
tar -zcvf log.tar.gz log2012.log 打包后,以 gzip 压缩 tar -zxf 解压
tar -jcvf log.tar.bz2 log2012.log 打包后,以 bzip2 压缩 tar -jxf 解压
tar -Jcvf log.tar.xz log2012.log 打包后,以 xz 压缩 tar -Jxf 解压
tar -tf log.tar 查看打包文件
注意 -f 参数后面必须接文件名
```

## 独立搜索Q&A

**1. chrontable是什么**

2. [Shell字符串截取][6]
[6]:https://blog.csdn.net/weixin_39591031/article/details/114028113?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166012109316781790782853%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166012109316781790782853&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-1-114028113-null-null.142^v40^control,185^v2^control&utm_term=shell%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%88%AA%E5%8F%96&spm=1018.2226.3001.4187

**3. shell清空指令**

**4. $0、$?、$!、$$、$./* 、$#、$@ 意义**

```shell
$$  Shell本身的PID（ProcessID，即脚本运行的当前 进程ID号）
$!  Shell最后运行的后台Process的PID(后台运行的最后一个进程的 进程ID号)
$?  最后运行的命令的结束代码（返回值）即执行上一个指令的返回值 (显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误)
$-  显示shell使用的当前选项，与set命令功能相同
$*  所有参数列表。如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数，此选项参数可超过9个。
$@  所有参数列表。如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。
$@ 跟$*类似，但是可以当作数组用
$#  添加到Shell的参数个数
$0  Shell本身的文件名
$1～$n  添加到Shell的各参数值。$1是第1参数、$2是第2参数…。
```

## Here Document

### 什么是Here Document

### 使用方式&限制

```shell
使用格式

命令 << 分隔串（最为常见的为EOF）
字符串1
…
字符串n
分隔串
```
```shell
使用限制
分割串常见的为EOF，但不一定固定为EOF，可以使用开发者自行定义的，比如LIUMIAO
缺省方式下第二个分割串（EOF）必须顶格写，前后均不可有空格或者tab
缺省方式下第一个分割串（EOF）前后均可有空格或者tab，运行时会自动剔除，不会造成影响

使用场景示例：待补充!
```

[Here Document免交互与Expect][7]
[7]:https://blog.csdn.net/qq_47855463/article/details/117106635?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166123933016782425163492%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166123933016782425163492&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-117106635-null-null.142^v42^control,185^v2^control&utm_term=here%20document&spm=1018.2226.3001.4187

## 结合Oracle
### sqlder ctl控制文件 参数及模板
CTL 文件参数介绍
**前面部分**
LOAD DATA：通常以此为开头，其前可加如下参数：
* UNRECOVERABLE：表示数据不可恢复
* RECOVERABLE：表示数据可恢复
* CONTINUE_LOAD：表示继续添加

**主体部分**
* INFILE：表示数据文件位置，如果值为*，表示数据就在控制文件中，本例中没有单独的数据文件，对于大多数加载而言，都会将数据文件与控制文件分离
* INTO TABLE tbl_name：tbl_name 即数据要加载到的目标表，该表在你执行 SQLLDR 命令之前必须已经创建。
* INSERT：向表中插入数据，表必须为空，如果表非空的话，执行 SQLLDR 命令时会报错，默认就是 INSERT 参数。
* APPEND：向表中追加数据，不管表中是否有数据。
* REPLACE：替换表中数据，相当于先 DELETE 表中全部数据，然后再 INSERT。
* TRUNCATE：类似 REPLACE，只不过这里不使用 DELETE 方式删除表中数据，而是通过 TRUNCATE 的方式删除，然后再 INSERT。
* FIELDS TERMINATED BY “,”：设置数据部分字符串的分隔值，这里设置为逗号（,）分隔，当然也可以换成其他任意可见字符，只要确定那是数据行中的分隔符就行。
* (ENAME, JOB, SAL)：要插入的表的列名，这里需要注意的是列名要与表中列名完全相同，列的顺序可以与表中列顺序不同，但是必须与数据部分的列一一对应。
* position 关键字用来指定列的开始和结束位置
* position(m:n)：指从第 m 个字符开始截止到第 n 个字符作为列值
* position(+2:15)：直接指定数值的方式叫做绝对偏移量，如果使用号，则为相对偏移量，表示上一个字段哪里结束，这次就哪里开始，相对便宜量也可以再做运算。
* position(*) char(9)：这种相对偏移量+类型和长度的优势在于，你只需要为第一列指定开始位置，其他列只需要指定列长度就可以。
* FILLER：控制文件中指定 FILLER，表示该列值不导入表中。
* BEGINDATA：表示以下为待加载数据，仅当 INFILE 指定为 * 时有效

```shell
控制文件模板
OPTIONS (BINDSIZE=2097152,READSIZE=2097152,ERRORS=-1,ROWS=90000)
LOAD DATA
INFILE 'E:\DATA\OS_DATA\OS_DUE.dat'
truncate INTO TABLE OS_DUE
FIELDS TERMINATED BY '|' TRAILING NULLCOLS
(
"DATA_DT" DATE "yyyy-mm-dd hh24:mi:ss",–时间类型
"DUE_NO" CHAR(14),–字符类型
"DUE_AMT" DECIMAL EXTERNAL,浮点类型吧
"OVER_DAY" INTEGER EXTERNAL–整型
)
```


## Header 2

### Header 3

## Styling

**Bold**

*Italics*

***Bold and Italics***

## Lists

1. Item 1

2. Item 2

* Unordered Item

  * Sub Item 1

    1. **Bold** Sub Sub Ordered Item

## Links

[In-Line](https://www.google.com)

[I'm a reference-style link 1][1]

[I'm a reference-style link 1][2]

[1]:https://www.mozilla.org
[2]:http://www.reddit.com

## Images

Hold your pointer clicked over the image to expand the view.

![Description](http://projectpages.github.io/project-pages/img/Logo_Fairy_Tail_right.png)

## Code

Inline `code`.

{% highlight python %}
import numpy as np
def hello_world():
    print('Hello World!'')
{% endhighlight %}

## MathJax

Use MathJax for Math.
$$ A = \pi r^2 $$

## Tables

Here | is | a | row!
|---------|:----------|:----------:|---------:|
is   |Left|  Center  |Right|
a    | cut | it | A
column  | short | B | C

## Quotes

> War does not decide who is *right*, only who is **left**.

## Rule

---

## List
- [x] Finish my changes
- [ ] Push my commits to GitHub
- [ ] Open a pull request


## Data Projector

<embed src="/bonbon-is-not-available.github.io/2016/05/02/New-Projector/" height="500px" width="100%">


## Color and Alignment

<p align="center">This text is centered.</p>

<p style="color:red">This is a red text with <span style="color:blue">blue</span> and <span style="color:green">green</span> inline text.</p>

## 流程图
[Mermaid流程图制表: official web][3]
<embed src="https://mermaid-js.github.io/mermaid/#/./integrations" height="500px" width="100%">
[3]:https://mermaid-js.github.io/mermaid/#/./integrations

[Mermaid extension: github][4]

[4]:https://github.com/BackMarket/github-mermaid-extension/blob/master/README.md

```mermaid
    graph TB
	subgraph 实线
    A0[A] --- B0[B] 
    A1[A] --> B1[B]
    A2[A] -- 描述 --> B2[B] 
    end
    subgraph 虚线
    A3[A] -.- B3[B] 
   	A4[A] -.-> B4[B] 
   	A5[A] -. 描述 .-> B5[B] 
    end
    subgraph 加粗线
    A6[A] === B6[B]
    A7[A] ==> B7[B] 
    A8[A] == 描述 ==> B8[B] 
    end
```
