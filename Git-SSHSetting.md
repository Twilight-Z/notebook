# Github SSH setting通道设置

设置通道后可以无密码上传下载项目文件。


### 1.打开Git Bash


### 2.生成秘钥

在Git Bash输入命令（邮箱填自己的）：

```

$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

```

### 3.确认生成秘钥

一直回车确认

```

Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/Administrator/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/Administrator/.ssh/id_rsa.
Your public key has been saved in /c/Users/Administrator/.ssh/id_rsa.pub.
The key fingerprint is:

```

### 4.查看复制私钥

私钥：
```
$ cat .ssh/id_rsa.pub
```

公钥：
```
$ cat .ssh/id_rsa
```

### 5.启动秘钥

进入GitHub (https://github.com/) 登录用户setting（你的设置）

进入个人设置列表的SSH and GPG keys

点击New SSH key（新的秘钥）

在key里粘贴刚刚复制的秘钥即可

### 6.完成设置

设置完成了

现在你可以不用http，而用ssh来上传文件了
