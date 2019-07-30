# Git 服务器搭建

### 1、安装Git
```
$ yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel perl-devel
$ yum install git
```
接下来我们 创建一个git用户组和用户，用来运行git服务：
```
$ groupadd git
$ useradd git -g git
```
<br><br><br>


### 2、创建证书登录
收集所有需要登录的用户的公钥，公钥位于id_rsa.pub文件中，把我们的公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

如果没有该文件创建它：
```
$ cd /home/git/
$ mkdir .ssh
$ chmod 700 .ssh
$ touch .ssh/authorized_keys
$ chmod 600 .ssh/authorized_keys
```
<br><br><br>


### 3、生成SSH：
查看是否有文件 没有则需要生成 ： `ls -al ~/.ssh`

其实生成ssh也是特别简单 看网上教程总是扯一堆有的无得，这里采用简单方法

执行生成命令 ： `ssh-keygen`

期间会提示你输入邮箱、密码（邮箱密码）直接输入就ok(或者直接空 回车) ，

成功之后会在一个文件夹下生成一个私钥 id_rsa和一个公钥 id_rsa.pub(放在服务器上)

查看一下是否生成 ：`cd ~/.ssh `

查看公钥 ：`cat ~/.ssh/id_rsa.pub`

展示你cv大法的时候到了，直接cv到git服务器authorized_keys文件里就ok了
<br><br><br>


### 4、初始化Git仓库
首先我们选定一个目录作为Git仓库，假定是/home/gitrepo/runoob.git，在/home/gitrepo目录下输入命令：
```
$ cd /home
$ mkdir gitrepo
$ chown git:git gitrepo/
$ cd gitrepo

$ git init --bare test.git
Initialized empty Git repository in /home/gitrepo/test.git/
```
以上命令Git创建一个空仓库，服务器上的Git仓库通常都以.git结尾。然后，把仓库所属用户改为git：
```
$ chown -R git:git test.git
```
<br><br><br>


### 5、克隆仓库
```
$ git clone git@192.xxx.xx.x:/home/gitrepo/test.git
Cloning into 'test'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```
192.xxx.xx.x 为 Git 所在服务器 ip ，你需要将其修改为你自己的 Git 服务 ip。

这样我们的 Git 服务器安装就完成。
<br><br><br>

