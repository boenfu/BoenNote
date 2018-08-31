系统为：center os 7

## 安装 FTP

查看有没有  **rpm -qa |grep vsftpd**

安装 **yum install -y vsftpd**

进入 **/etc/vsftpd/** 去配置

编辑 **nano vsftpd.conf**  把 匿名登录关了 anonymous_enable



> 自己使用的服务器 主要使用 root 账号

编辑 **ftpuser** 和 **user_list** 把 root 用 # 注释



> syetemclt就是service和chkconfig这两个命令的整合，在CentOS 7就开始被使用了

启动 **systemctl start vsftpd**

开机自启  **systemctl enable vsftpd.service**



## 安装 Node

> 我是在根目录下 创建了 software 文件夹

创建文件夹 **mkdir node**  并进入**cd node**

获取安装包

`wget https://nodejs.org/dist/v8.11.4/node-v8.11.4-linux-x64.tar.xz -b`

解压 **xz -d .tar.xz**  再 **tar -xvf  .tar**

修改名字 **mv node-v8.11.4-linux-x64  ./node-v8.11.4**

现在的 目录结构就是

/software/node/node-v8.11.4

在 /software/node/node-v8.11.4/bin 目录下输入 **./node -v** 看是否可用

添加软链接 ( 全局使用 )

**ln -s /software/node/node-v8.11.4/bin/node /usr/local/bin/node**  
**ln -s /software/node/node-v8.11.4/bin/npm /usr/local/bin/npm**



## 安装 PM2 node进程管理工具

安装 **npm install -g pm2**

添加软链接 ( 全局使用 )

**ln -s /software/node/node-v8.11.4/bin/pm2 /usr/local/bin/pm2 **



> 开机启动

**pm2 start 项目**

**pm2 save**

**pm2 startup**





## 安装 Mysql 数据库

获取安装包

`wget https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.23-linux-glibc2.12-x86_64.tar.gz -b`

解压 **tar -zxvf**   **解压后的mysql文件夹**

复制   **cp -r  解压后的mysql文件夹** **/usr/local/mysql**

添加系统mysql组 **groupadd mysql**

添加mysql用户 **useradd -r -g mysql mysql**

切到mysql目录 **cd /usr/local/mysql**

修改当前目录拥有者为 mysql 用户 **chown -R mysql:mysql ./**

安装数据库 **bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data**



> 如果报这个错
>
> error while loading shared libraries: libnuma.so.1: cannot open shared object file: No such file or directory
>
> 可以先尝试卸载 yum remove libnuma.so.1
>
> 再安装 yum -y install numactl.x86_64



数据库安装成功 显示的信息的末尾有初始密码

如 root@localhost: V4BC!7<;yD:p



执行以下命令创建RSA private key 

  **bin/mysql_ssl_rsa_setup --datadir=/usr/local/mysql/data**

修改当前目录拥有者为 mysql 用户 **chown -R mysql:mysql ./**

修改当前data目录拥有者为mysql用户 **chown -R mysql:mysql data**

配置my.cnf  **nano  /etc/my.cnf **   （直接把下面内容复制上就行）



```
[mysqld]
character_set_server=utf8
init_connect='SET NAMES utf8'
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
socket=/tmp/mysql.sock
#不区分大小写 (sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 这个简单来说就是sql语句是否严格)
lower_case_table_names = 1
log-error=/var/log/mysqld.log
pid-file=/usr/local/mysql/data/mysqld.pid
```



**添加开机启动     cp /usr/local/mysql/support-files/mysql.server  /etc/init.d/mysqld**

修改   **nano  /etc/init.d/mysqld**   

```
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
```

启动mysql   **service mysqld start** 

加入开机起动    **chkconfig --add mysqld**  



登录修改密码 **mysql -uroot -p** 

输入 初始密码

修改初始密码

**SET PASSWORD = PASSWORD('your new password');**

**ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;**

刷新权限 之后退出重新登录

**flush privileges;**

授权新用户

**GRANT ALL PRIVILEGES ON *.* TO 'boen '@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;** 

就可以用 boen 登录了



## 安装 JDK

https://www.oracle.com/technetwork/java/javase/downloads/index.html

获取下载链接 后用 wget 下载

创建java文件目录  **mkdir -p /usr/local/java** 

解压到java文件目录 **tar -vzxf jdkxxx.tar.gz -C /usr/local/java/** 

添加环境变量，编辑配置文件 **nano  /etc/profile** 

```
export JAVA_HOME=/usr/local/java/jdk1.8.0_161 
export CLASSPATH=$:CLASSPATH:$JAVA_HOME/lib/ 
export PATH=$PATH:$JAVA_HOME/bin 
```



重新加载配置文件 **source  /etc/profile** 

测试 **java -version**



## 安装 Mongodb

https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.0.2.tgz

解压 **tar -zxvf mongodb-linux-x86_64-rhel70-4.0.2.tgz** 

移动目录 **mv  mongodb-linux-x86_64-rhel70-4.0.2  /usr/local/mongodb**

添加环境变量 在 **/etc/profile** 里

**export PATH= /usr/local/mongodb/bin:$PATH**

手动创建数据库文件夹 和 日志文件

**mkdir /usr/local/mongodb/data**

mkdir /usr/local/mongodb/log/mongodb.log

创建配置文件

**nano /usr/local/mongodb/mongodb.conf**

```
port=27017 #端口  
nohttpinterface=false
dbpath= /usr/local/mongodb/data #数据库存文件存放目录  
logpath= /usr/local/mongodb/log/mongodb.log #日志文件存放路径  
logappend=true #使用追加的方式写日志  
fork=true #不以守护程序的方式启用，即不在后台运行  
maxConns=100 #最大同时连接数  
noauth=true #不启用验证  
journal=true #每次写入会记录一条操作日志（通过journal可以重新构造出写入的数据）。
#即使宕机，启动时wiredtiger会先将数据恢复到最近一次的checkpoint点，然后重放后续的journal日志来恢复。
storageEngine=wiredTiger  #存储引擎有mmapv1、wiretiger、mongorocks
bind_ip = 0.0.0.0  #这样就可外部访问了，例如从win10中去连虚拟机中的MongoDB
```

启动命令 **mongod --config /usr/local/mongodb/mongodb.conf**



**开机自启**

在 **/lib/systemd/system/** 目录下新建 **mongodb.service** 文件

```
[Unit]

Description=mongodb
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
ExecStart=/usr/local/mongodb/bin/mongod --config /usr/local/mongodb/mongodb.conf
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/usr/local/mongodb/bin/mongod --shutdown --config /usr/local/mongodb/mongodb.conf                     
PrivateTmp=true

[Install]
WantedBy=multi-user.target

```

设置权限

**chmod 754 mongodb.service**

启动关闭服务，设置开机启动

```

#启动服务
systemctl start mongodb.service  
#关闭服务  
systemctl stop mongodb.service  
#开机启动  
systemctl enable mongodb.service
```



**新增管理员用户**

> 新增后 可以在 conf 里把 noauth=true #不启用验证  改为 false ，之后登陆需要用户名密码

```
$ mongo

> use admin

> db.createUser(
     {
       user:"boen",
       pwd:"boen",
       roles:[{role:"root",db:"admin"}]
     }
  )

> exit
```

