# cmder 基本配置和使用

### 简介
cmder是windows下的一款终端工具，支持很多linux命令，用起来还是很爽的。

更新：现在用git bash了~cmder很多功能也用不到，提供类似bash的环境感觉git bash已经够了
WIN10-NOTE：win10的console默认把颜色支持关闭了，需要程序自己开启，所以你使用的cosole程序如果输出颜色失败，更新一下往往就能解决。

php存在问题，7.2.0已经解决，不过部分console软件为了兼容开始的win10关闭了颜色，可以使用--ansi之类的开启
<br><br><br>

### 安装
直接在官网下载即可，免安装，解压即可用。
<br><br><br>


### cmder配置

使用win+alt+p打开配置面板
main

字体、外观。。。
StartUp

配置打开终端执行的一些任务和环境变量设置
+ `specified name task`这儿可以选择默认启动的终端类型，如cmder、bash、cmd、powershell、git bash等
+ 解决中文乱码，很重要的设置：`set LC_ALL=zh-CN.UTF8` ，不要使用 `set LANGUAGE=zh-CN.UTF8`，因为这个设置了之后对{cmd:cmder}有效但是对{bash:bash}无效
+ current directory设置
+ cmder其实使用的是ComEmu终端，当我们新建一个相同终端的时候，想要从当前的目录开启一个新的终端而不是从startup目录开启。首先需要修改一下task的配置。
![](https://images2015.cnblogs.com/blog/971915/201707/971915-20170710205028634-952196635.png '1')
Keys & Macro

快捷键等

+ `ctrl+\`会和vscode的快捷键冲突，可以在这儿改一下

Integretion

设置右键菜单等

+ Command那一行的设置：cmd -new_console:d: !ConEmuWorkDir! /C "d:\cmder\vendor\git-for-windows\bin\bash --login -i"
++ new_console:d:指定目录，!ConEmuWorkDir!代表右键菜单点击时候的目录名，注意前后一定要是空格，否则不会被识别为预定义变量
++ cmd /C 是执行某个命令，填写bash的位置即可
+ Icon file设置icon的目录
  这个bash也是可以设置`~/.bash`和`~/.bash_profile`的

右键菜单快捷命令

这个的开始目录是固定的
注册了之后好像去不掉了。。。。
```
cmder /register user/all
cmder /unregister user/all
```
<br><br><br>


### 和vscode好基友合作

用户配置中制定终端和git的可执行路径
```
 "terminal.integrated.shell.windows": "D:\\cmder\\vendor\\git-for-windows\\bin\\bash.exe"，
 "git.path":"D:\\cmder\\vendor\\git-for-windows\\mingw32\\bin\\git.exe"
```

NOTE:这个时候windows cmd里边的环境变量此时不会载入，也许要特殊设置task？？有知道的大佬可以留言指导一下，蟹蟹罗~

PS：这个bash的工作目录不是通过命令行参数传递的，写一个bat脚本获取vscode传给调用shell程序的参数就知道了，bat脚本里通过%1获取第一个参数
可能的bug

如果是windows 10版本是1703，在vscode中使用终端的时候非英文环境可能存在输出异常，只要下载 KB4020102补丁即可。
<br><br><br>
