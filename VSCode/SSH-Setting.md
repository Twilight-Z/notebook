# VSCode终端 SSH通道设置

### 1、创建秘钥
打开vscode终端
`ctrl+shift+~`

创建秘钥，输入
```
ssh-keygen -t rsa
```
<br><br>

### 2、绑定秘钥
打开腾讯服务器->创建SSH秘钥->使用已有秘钥。

打开秘钥文件：
`C:\Users\Administrator\.ssh\id_rsa.pub`
复制内容，粘贴到公钥输入框。（名字随意）
确认，绑定到你的服务器实例里。
然后你的服务器密码无法使用了，按重置密码重新输入。
<br><br>

### 3、ssh连接服务器
打开vscode终端，输入`ssh root@<服务器ip>`
成功！
<br><br>
