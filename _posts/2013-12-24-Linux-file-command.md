---
title:  Linux文件相关命令.
date: 2013-12-24 23:31:06
categories:
- Linux
tags:
- Linux
---

### ls:显示文件名
**作用：**   ls用于显示目录内容，类似dos下的dir命令，它的使用权限是所有用户。
**格式：**用法： ls [选项] 文件名
**选项参数：**
* **ls -l：**列出文件的详细信息，一行只输出一个文件

* **ls -a:**列出目录下的所有文件，包括以"."开头的隐藏文件


>隐藏文件多数是配置文件，它们给程序、窗口管理器、shell等设置首选项，它们被隐藏的目的是防止用户对其无意义的篡改。

| 蓝色 |    绿色    |   红色   |  浅蓝色  | 加粗黑色 |     灰色     |
| :--: | :--------: | :------: | :------: | :------: | :----------: |
| 目录 | 可执行文件 | 压缩文件 | 链接文件 | 符号链接 | 其他格式文件 |

ls最常见的命令是ls -l
提示：man ls | col -b | lpr



### cat :显示文本文件内容

**作用：**将[文件]或标准输入组合输出到标准输出

**格式：**用法： cat \[选项]  [文件]...

* **-A:** --show-all
* **-b :**对非空输出hang编号
* **-E: **--show-ends:在每行结束出显示$
* **-n:** 对所有行输出行编号



### rm:删除文件

**作用:**  删除指定的文件

**格式：** rm [选项]...文件...

**选项：**

- **-d:** --directory 删除<文件>，即便该文件可能是空目录
- **-f:** --force:  略过不存在的文件，绝不提醒
- **-i:** --interactive:  进行任何删除操作线必须先确认
- **-r,-R：**  --recursive:  递归删除目录及其内容
- **-v:**  --verbose:  详细显示进行的步骤



### less:分屏显示文件

**作用：**less命令的功能几乎和more命令一样，也用来按页显示文件，不同之处在于less命令在现实文件时，允许用户既可以向前又可以向后翻阅文件。

**格式：**用法： less	\[选项]  [文件]...

**选项**

- **-c:**   从上到下刷新屏幕，并显示文件内容，而不是通过底部滚从完成刷新。
- **-f :**   强制打开文件，二进制文件显示时，不会提示警告
- **-i:**    搜索时忽略大小写，除非搜索串中包含大写字母
- **-I:**    搜索时忽略大小写，除非搜索串中包含小写字母
- **-m:**   显示读取文件的百分比
- **-M：**   显示读取文件的百分比、行号及总行数
- **-N:**   在每行前输出行号



### cp: 复制文件

**作用：** 文件或目录的复制



### mv:更改文件名

**作用：**mv可以移动一个文件（目录）到另一个文件（目录），如果文件不存在，则创建它。因此也可以理解为改名过程，所以说mv命令可以修改文件名和目录名。


**格式：**用法： mv	[选项]... 源  目的

**选项**

- **-b:**   若覆盖文件，则覆盖前先行备份。
- **-f:**    若目录文件或者目录与现有的文件或者目录重复，则直接覆盖现有的文件或目录。
- **-i:**    覆盖前先行询问用户  

**应用实例**
(1)改名(当前目录下不存在b.md)
>  mv a.md b.md

(2)mv修改目录
> mv  kernel/  kernelBak1



### grep：查找字符串

**作用：**查找文件里符合条件的字符串

**格式：**    grep [选项] \<pattern>\<files>

**选项：**

* **-E:**    每个模式作为一个扩展的正则表达式对待
* **-F:**    每个模式作为一组固定字符串对待，而不作为正则表达式
* **-b:**    在输出的每一行前显示包括匹配字符串的行在文件中的字节偏移量
* **-c:**   只显示匹配行的数量
* **-I:**    比较时不区分大小写



**应用实例：**

(1) 查找文件"file.php"中是否包含字符串"html"

> grep 'html' file.php

(2) 检查/etc/passwd文件中是否有可以用户

Linux中/etc/passwd文件是存储系统用户密码等重要信息的文件，黑客入侵往往会使用在passwd文件中增加特权用户的方法为自己留后门，特权用户UID为0

> grep '0:0'  /etc/passwd

(3) 通过管道过滤ls -l输出的内容，只显示以a开头的行

> ls -l | grep '^a'

(4) 显示所有以d开头的文件中包含test的行

> grep 'test' d*

(5) 显示aa , bb , cc文件中匹配test的行

> grep 'test'  aa  bb  cc



### head:显示文件头部

**作用：**head是显示一个文件的内容的前多少行

**格式：**head \[选项]  \[文件]

**选项:**

* **-c:**    处理文件前面指定字节数，加**b**(512字节块)，**k**(KB数)、**m**(MB数)
* **-n:**    显示文件头n行内容
* **-p:**    处理多个文件时不显示文件头信息
* **-v: **   处理多个文件时显示文件头信息

**应用实例：**

(1) 显示 /etc/profile 的前10行内容

> head -n 10  /etc/profile

(2) 将 etc/named.conf 中前3行的内容发送至标准输出

> head -n 3  /etc/named.conf
>
> /etc/named.conf <==
>
> // generated by named-bootconf.pl
>
> options{



### tail:显示文件尾部

**作用：tail**是显示一个文件的内容的最后多少行

**格式：tail** \[选项]  \[文件]

**选项:**

* **-b:**     列出辨识结构时，不显示文件名称

- **-c:**    处理文件前面指定字节数，加**b**(512字节块)，**k**(KB数)、**m**(MB数)
- **-n:**    显示文件头n行内容
- **-p:**    处理多个文件时不显示文件头信息
- **-f:**    如果文件大小在增长的话，tail将岁文件增长而一直显示
- **-v: **   输出“==>文件名<==” 形式
- 

### sort: 按顺序显示文件内容

**作用：**head是显示一个文件的内容的前多少行

**格式：**head \[选项]  \[文件]

**选项:**

- **-c:**    处理文件前面指定字节数，加**b**(512字节块)，**k**(KB数)、**m**(MB数)
- **-n:**    显示文件头n行内容
- **-p:**    处理多个文件时不显示文件头信息
- **-v: **   处理多个文件时显示文件头信息

**应用实例：**

(1) 显示 /etc/profile 的前10行内容

> head -n 10  /etc/profile

(2) 将 etc/named.conf 中前3行的内容发送至标准输出

> head -n 3  /etc/named.conf
>
> /etc/named.conf <==
>
> // generated by named-bootconf.pl
>
> options{



### echo:显示文本

**格式：**echo   \[-ne]  [字符串]

**选项:**

- **-n:**    不要再最后自动换行

- **-e:**    字符中出现以下字符，则特别处理，不会将它当做一般参数

|   \a   |       \b       |         \c         |   \t    |  \\\  |    \nnn    |
| :----: | :------------: | :----------------: | :-----: | :---: | :--------: |
| 警告声 | 删除前一个字符 | 最后不要加换行符号 | 插入tab | 插入\ | 插入八进制 |



### locate：搜索文件

**作用：** locate用于查找符合条件的文件，它会去保存文件与目录名称的数据库内查找符合范本样式条件的文件或目录。

**格式：** locate \[选项\]  相关字

**选项：**

* **-u,-U: \<dir>**  建立数据库，



### touch：更新文件或目录时间

**作用：** 修改文件时间信息

**格式：** touch \[选项] ... [目录] ...

**选项：**

* **-a:**  改变文件的读取时间记录
* **-c:**   不建立任何文件
* **-d:**  设定时间与日期，可以使用各种不同的格式
* **-t:**  使用\[[CC]YY]MMDDhhmm[.ss]格式的时间而非目前的时间。

**实例：**

(1) 将文件的时间记录修改为现在的时间，若文件不存在，则创建一个新的文件。

> touch myfile

(2) 将文件 myfile 的时间记录修改为1月6日18点3分。

> touch -c -t  01061803  myfile

(3) 按给定的日期格式修改

> touch -d "6:03pm 01/06/2005" myfile











