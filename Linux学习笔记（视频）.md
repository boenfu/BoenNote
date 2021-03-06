##### Linux是自由软件，是源代码开放的UNIX

分时系统

#### 文件处理命令

##### ls 

选项可以多个合并在一起使用

​	-a 所有 包括隐藏

​	-d 目录属性

​	-l 详细信息显示 如读写权限

​	-i i节点数字标识 （每个文件都有i节点）

​	例:

​	-rwxr-xr-x   1 root root  5988 Apr  5 05:37 appex.sh

​		结果的第一个属性是文件类型 主要有 d 目录     - 二进制     l 软连接文件

​	解析:

1.   \-  二进制文件  rwx所有者(u)的权限   r-x所属组(g)     r-x 其他人(o)
2.  1 表示硬链接数
3.   root root 分别是所有者和所属组
4.   文件大小 日期 和 名称



##### cd  

​	cd / 根目录 

​	cd .. 回上一级

##### pwd

​	当前目录

##### mkdir

​	创建目录

##### touch

​	创建一个空文件

##### cp

​	复制文件 一个或多个 加 路径名

​	复制目录要加 -R

​	-p 可以保持拷贝时间跟原文件一样

##### mv

​	移动文件或改名

​	第一个参数是文件名 第二个是新文件名或者路径

##### rm

​	删除文件或目录 

​	删除目录要加 -r

​	加 -f 可以不询问是否删除

​	还可以用转义符 \ 例:  \rm 就是用 rm 本身删除 就不会询问，因为实际上用 rm 时 是调的 rm -i  (4.8日加)

##### cat

​	显示文件内容

##### more

​	分页显示文件内容

​	执行后可以输入命令控制

​		空格或f 下一页

​		enter 下一行

​		q或Q 退出

##### head & tail

​	查看文件前n行 / 后n行

​	head xxx -20 查看前二十行

​	tail 还有个 -f 可以动态查看最新的n行（如监视日志文件）

##### ln

​	产生链接文件

​	参数 源文件  和  想生成的文件

​	不加 -s 是硬链接 加是软链接

软链接的权限都是 lrwxrwxrwx 会指向源文件 时间值是创建软链接的时间

相当于 windows 下的快捷方式

硬链接有点像拷贝 但是会跟原文件同步更新 

（是因为硬链接  两个文件 i 节点一样，而拷贝 的文件会新产生 i 节点）

原文件删了硬链接还能用 （备份的感觉）

软链接可以话文件系统（c盘d盘，分区的意思），硬链接不行



#### 权限管理命令

##### chmod

​	改变文件或目录权限

​	参数例:

​	u + r   所有者加上读的权限

​	g - w  所属组加上写的权限

​	o = rwx 其他人的权限等于 可读可写可执行

另外一种方式  直接写数字

r-4 w-2 x-1

如 权限 rwxr-xr--  = 754   r-xr-xr-x = 555

例子：

```
chmod 754 a //a文件被赋 所有者所有权限 所属组读和执行 其他人读
chmod o-r a //a文件被赋 其他人 读
```

注： 权限详解

| 字符 | 权限 | 对文件含义 |       对目录的含义       |
| :--: | :--: | :--------: | :----------------------: |
|  r   |  读  |  查看文件  |     可以列出目录内容     |
|  w   |  写  |  修改文件  | 可以创建删除目录中的文件 |
|  x   | 执行 |  执行文件  |       可以进入目录       |

##### chown & chgrp

​	改变所有者 / 所属组

​	用户/组名  + 文件名

##### umask

​	出现的第一个数是特殊权限位

​	后面的是相应权限掩码 需要用 777 - 后三位

​	-S 显示文件创建时的默认权限，会直观点

注： 想改变系统默认缺省权限 用umask + 掩码

如 umask 027 表示把默认权限改成 777-027 = 750 rwxr-x---

再注： 缺省创建的文件！不能授予可执行x权限

#### 账户操作

​	useradd + 用户名 添加用户

​	passwd + 用户名 设置密码





2018.4.8

#### 文件搜索

##### 	which 

​		命令查找 which ls

​		whereis 和 which 用法一样 都能找到命令的绝对路径

​		区别 which可以找到别名 whereis 可以找到帮助文件

##### 	find

​		可以找任何文件或目录

​		find 搜索路径 搜索关键字

​		如 find / -name init 这样只会找到 init 包含的不会找到

​		 find / -name init * 以 init 开头的

​		 find / -name init??? 以init 开头 后面有三个字符

​		-size 以大小查找 很多 Linux 单位是数据块 一个数据库

​		512字节 = 0.5KB 可以用 大于小于等于

​		-user 所有者

​		时间查找

​			天为单位 ctime,atime,mtime

​			分钟 cmin amin mmin

​			c表示改变 ，文件属性被修改 如所有者所属组权限

​			a表示访问 

​			m表示修改，内容被修改 

​			如 find -atime 30 一个月之内被访问过的

​			-a and与    -o or或 操作

​			-type f 二进制文件 l软链接文件 d目录

​				如 find -type f -o -size 204800 查找二进制文件或大小超过100m

​			

​		连接符 find .... -exec 命令 {} \; 固定格式  {}find查询结果

​			如： find / -name test -exec ls -l {}\; 表示先找到test再查看他详细内容

​				find / -name test -exec rm -rf  {} \; 找到test 然后删除

​			exec 可以换成 ok ok会询问

3-3 40分钟

​			

















