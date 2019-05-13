# VSCode 连接服务器

### 1、安装SFTP拓展
在侧边栏拓展里搜索SFTP
安装后重启
<br><br>

### 2、SFTP配置
按`Ctrl+Shift+p`
输入`>SFTP: Config`
回车打开SFTP配置文件
<br><br>

### 3、保存配置
![blockchain](https://img-blog.csdn.net/20180717170403866?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhY2tlcl95bA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 "配置")
如图所示，把配置项填好。
+ host填域名
+ username是服务器用户名（root）
+ password填密码（默认没有， 自己加上一行）
+ remotePath是需要打到的远程的文件夹地址(填：/wwww/wwwroot)
  不填也可以，不过加载太多文件容易卡
+ uploadOnSave自动保存
<br><br>

### 4、成功
+ 保存配置，重启vscode。
+ 侧边栏拓展下面出现SFTP，没有报错就会出现服务器的文件列表。
+ 找个文件，按右键点击`Edit in Local`编辑模式。
+ 同时，vscode 工作区文件夹出现服务器文件列表。
+ 右键列表`Download Folder`下载服务器文件列表。（前一个是上传）
+ 现在在VS Code中编辑的代码只需保存（command+s或ctrl+s）即可上传到服务器中。

![blockchain](https://img-blog.csdn.net/20180717170636363?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhY2tlcl95bA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70 "成功")
<br><br>
