# Git Configure(配置)

### 1.打开Git bush软件

### 2.输入用户信息
当安装完 Git 应该做的第一件事就是设置你的用户名称与邮件地址。
这样做很重要，因为每一个 Git 的提交都会使用这些信息，并且它会写入到你的每一次提交中，不可更改：
（里面用户和邮箱填自己的！）
```

$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com

```
如果使用了 --global 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事情， Git 都会使用那些信息。 
当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 --global 选项的命令来配置。

### 文本编辑器

既然用户信息已经设置完毕，你可以配置默认文本编辑器了，当 Git 需要你输入信息时会调用它。
如果未配置，Git 会使用操作系统默认的文本编辑器，通常是 Vim。 
如果你想使用不同的文本编辑器，例如 Emacs，可以这样做：
```
$ git config --global core.editor emacs
```

### 检查配置信息
如果想要检查你的配置，可以使用 git config --list 命令来列出所有 Git 当时能找到的配置。
```
$ git config --list
user.name=John Doe
user.email=johndoe@example.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```
你可能会看到重复的变量名，因为 Git 会从不同的文件中读取同一个配置（例如：/etc/gitconfig 与 ~/.gitconfig）。
这种情况下，Git 会使用它找到的每一个变量的最后一个配置。

你可以通过输入 git config <key>： 来检查 Git 的某一项配置
```
$ git config user.name
John Doe
```
