# Git 疑难杂症

### 1、fatal: remote origin already exists. 
git 添加远程github仓库的时候提示错误：fatal: remote origin already exists. 

###### 1.先删除远程 Git 仓库
`$ git remote rm origin`

###### 2.再添加远程 Git 仓库
`$ git remote add origin git@github.com:FBing/java-code-generator`

如果执行 git remote rm origin 报错的话，我们可以手动修改gitconfig文件的内容
```$ vi .git/config```
把 [remote “origin”] 那一行删掉就好了。
<br><br><br>
