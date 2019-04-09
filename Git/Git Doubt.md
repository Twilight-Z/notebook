# Git 疑难杂症

### 1、fatal: remote origin already exists. 
git 添加远程github仓库的时候提示错误：fatal: remote origin already exists. 
(Git错误：远程仓库已经存在。 )
解决步骤：

###### 1.先删除远程 Git 仓库
`$ git remote rm origin`

###### 2.再添加远程 Git 仓库
`$ git remote add origin git@github.com:FBing/java-code-generator`

如果执行 git remote rm origin 报错的话，我们可以手动修改gitconfig文件的内容
```
$ vi .git/config
```
把 `[remote “origin”] `那一行删掉就好了。
<br><br><br>

### 2、Git 删除缓存区
使用 `git rm` 命令即可，有两种选择,

###### 1.一种是 `git rm –cached` “文件路径”，不删除物理文件，仅将该文件从缓存中删除；

###### 2.一种是 `git rm –f` “文件路径”，不仅将该文件从缓存中删除，还会将物理文件删除（不会回收到垃圾桶）。

git –如何撤销已放入缓存区（Index区）的修改 
修改或新增的文件通过 `git add –all` 命令全部加入缓存区（index区）之后，使用 `git status` 查看状态

（`git status -s` 简单模式查看状态，第一列本地库和缓存区的差异，第二列缓存区和工作目录的差异），

提示使用 `git reset HEAD` 来取消缓存区的修改。

不添加参数，撤销所有缓存区的修改。

另外可以使用 `git rm –cached` 文件名 ，可以从缓存区移除文件，使该文件变为未跟踪的状态，
<br><br><br>
