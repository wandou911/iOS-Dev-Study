### 环境（Vultr服务器）

* 服务器操作系统：CentOS 7.4 ；
* 博客部署服务器：Apache HTTP；
* 数据库：MySql；
* 框架：WordPress；

### 步骤

#### 一、安装 Apache HTTP

安装 Apache HTTP 很简单，只需要在终端输入以下命令就可以了：

`sudo yum install httpd`

如果当前登录用户不是 root 的话，执行，sudo 命令是需要输入 root 用户的密码； 
安装完毕后，启动服务：

`systemctl start httpd.service`

当启动服务器完成之后，先别着急往下弄，可以直接在浏览器中输入服务器的 ip 地址，应该就可以看到 Apache 的欢迎页面了； 
如果你的 ip 地址已经和域名绑定了，那么在浏览器中输入你的域名也可以访问了； 
如果输入 ip 没有访问到 Apache 的欢迎页面，原因是linux防火墙的原因，apache是80端口，linux系统默认只开放22端口，所以此时我们需要将80端口进行开放！执行如下命令： 

`iptables -I INPUT 5 -i eth0 -p tcp --dport 80 -j ACCEPT`

上面这行命令的意思是：修改系统防火墙配置文件，在第五行配置中增加允许80端口监听外来ip

这时我们来看看我们修改配置文件是否成功，执行下面的代码你可以看到配置文件的内容，一般情况下你可以看到我们刚刚加进去的内容

`iptables --line -vnL`

以上命令重启后会失效 永久开放80端口

`firewall-cmd --zone=public --add-port=80/tcp --permanent`

### 二、安装 MySql

Centos 7安装Mysql服务

在CentOS7中，mariadb代替了Mysql，其实mariadb只是一个M有sql的一个分支，由于Mysql旧部员工不满Oracle收购Mysql导致更新速度变慢，又重新开发了和Mysql类似的开源数据库。来应对Oracle的Mysql。
安装

```
yum install mariadb*  //默认安装

```
启动MariaDB

`systemctl start mariadb //启动mariadb`

设置密码

```
安装成功后，root用户默认密码为空且仅限本机登陆
mysql_secure_installation

Set root password? [Y/n] <– 是否设置root用户密码，输入y并回车或直接回车
New password: <– 设置root用户的密码
Re-enter new password: <– 再输入一次你设置的密码
```
其他配置
```
Remove anonymous users? [Y/n] <– 是否删除匿名用户，回车

Disallow root login remotely? [Y/n] <–是否禁止root远程登录,回车,

Remove test database and access to it? [Y/n] <– 是否删除test数据库，回车

Reload privilege tables now? [Y/n] <– 是否重新加载权限表，回车
```

初始化MariaDB完成，接下来测试登录

`mysql -uroot -p [回车，之后输入密码]`

[Mariadb安装之后的各种设置](https://blog.csdn.net/zhezhebie/article/details/73549741)

### 三、开机默认启动 Apache 和 Mysql 服务

```
systemctl enable httpd.service
systemctl enable mysqld.service
```

最好把这些服务都再重启一下：

```
systemctl restart httpd.service
systemctl restart mysqld.service
```

### 四、在 Mysql 中新建数据库

`mysql> mysql -u root -p`

通过上面的命令进入数据库，然后输入密码，但其实默认是没有密码的，直接回车就能进入了； 
进入后，创建一个叫 wordpress 的数据库：

`mysql> create database wordpress;`

创建用户

```
mysql> use mysql;
mysql> create user wordpress@localhost identified by '123456';
```

数据库访问授权

`mysql> grant all on wordpress.* to wordpress@localhost indentified by '123456';`

### 五、安装 PHP 以及相关 PHP 组件

```
yum install php
yum install php-mysql
yum install php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc
```

我先安装了这几个组件，为以后使用，你要想了解所有的 PHP 组件的话，可以使用如下命令搜索：

`yum search php-`

### 六、测试 PHP 是否安装成功

建立一个 info.php 文件：

`vim /var/www/html/info.php`

然后输入 i 进入编辑模式，在文件中写入下面的 PHP 命令：
```
<?php
phpinfo();
?>
```
Esc，退出编辑模式，:wq 保存修改并退出；

在浏览器中输入 ip 地址 /info.php，例如：123.56.183.34/info.php 回车，就可以看到 PHP 的信息了；

### 七、下载 WordPress

可以到 https://wordpress.org/ 官网上去翻，或通过下面的命令下载：

`wget https://wordpress.org/latest.tar.gz`

使用 tar 来解压文件：

 `tar zxvf latest.tar.gz`



### 八、把文件复制到 /var/www/html 目录下

`cp -rf wordpress/* /var/www/html/`

（注：建议去看看 WordPress 的 wp-conten-sample.php 文件） 
在浏览器中输入你的 ip 地址，就可以看到 WordPress 的配置页； 
如何根据其提示，完成最后的配置；

### 九、安装 FTP

[CentOS 7上搭建FTP服务](https://blog.csdn.net/u012804762/article/details/52108086)

当你进行（首次）进行下载或更新时 WordPress 会让你填入以下信息（没有图片…）： 

主机名：（填 ip 地址） 
FTP 用户名：xxx 
FTP 密码：xxx 

#### 安装FTP软件包
通过 `yum -y install vsftpd`  进行安装。 安装完后，有/etc/vsftpd/vsftpd.conf文件，该文件是vsftp的配置文件

#### 专门新建一个FTP服务器的用户
```
useradd ftpuser //新增一个用户ftpuser

passwd  ftpuser  //为ftpuser设定密码，期间会有两次提示输入密码确认
```
#### 设置 FTP 服务为开机自启，并重启其服务：
```
systemctl enable vsftpd.service
systemctl restart vsftpd.service
```

#### 为FTP服务设置防火墙

ftp默认端口是21，而centos默认是没有开启的，所以要修改iptables文件


### 十、[域名解析](https://www.cnblogs.com/mnstar/p/8134994.html)

解析成功后，输入域名就可以访问博客，不用每次输入IP了

然后就 OK 啦！？ 

当然事情没那么简单： 
在这里我总结了两个我所遇到的错误及解决方案： 
如果你们遇到了可以借鉴参考下：
问题总结：

1. “无法定位 WordPress 内容目录” 
解决方案： 
打开 WordPress 根目录的 wp-config.php 文件，把下面这段代码加到文件末尾；

```
/** Override default file permissions */
if(is_admin()) {
add_filter('filesystem_method', create_function('$a', 'return "direct";' ));
define( 'FS_CHMOD_DIR', 0751 );
}
```

2. “主题安装失败，无法创建目录” 
解决方案： 
在到 WordPress 的安装路径下找到 wp-content 文件（注：这个文件夹是用于存放语言包，插件及主题的文件夹），键入以下命令：

`chmod -R 777 wp-content/`

再进行安装或更新，应该就能解决！

3.发布博客后 打开出现 “有点尴尬诶！该页无法显示”

解决方案：
博客链接中带有中文，导致无法解析
打开wordpress后台：设置—->固定链接，看到现在的设置，尝试选其他类型都不行，都会在链接中带中文，最后选第一项的“朴素”类型，OK搞定！
![修改固定链接](https://img-blog.csdn.net/20170318220228955?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3MyMDA4ZG4yMDA4/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)


4 [ CentOS cannot change locale UTF-8解决方法及设置中文支持](https://www.jianshu.com/p/2de3c13cde89)

如果要设置中文版的字体编码。在每个文件中增加以下内容。
中文版
```
# vim /etc/profile.d/locale.sh
export LC_CTYPE=zh_CN.UTF-8
export LC_ALL=zh_CN.UTF-8

# vim /etc/locale.conf
LANG=zh_CN.UTF-8

# vim /etc/sysconfig/i18n
LANG=zh_CN.UTF-8

# vim /etc/environment
LANG=zh_CN.UTF-8
LC_ALL=zh_CN.UTF-8
```


参考链接1：[在CentOS 7上搭建WordPress](https://blog.csdn.net/qq_35723367/article/details/79544001)
参考链接2：[linux打开80端口及80端口占用解决办法](https://blog.csdn.net/csdn265/article/details/69942482)
参考链接3：[CentOS 7 yum方式配置LAMP环境](https://www.cnblogs.com/zutbaz/p/4420791.html)
