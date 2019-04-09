# cmder 基本配置和使用
cmder是windows下的一款终端工具，支持很多linux命令，用起来还是很爽的。

更新：现在用git bash了~cmder很多功能也用不到，提供类似bash的环境感觉git bash已经够了
WIN10-NOTE：win10的console默认把颜色支持关闭了，需要程序自己开启，所以你使用的cosole程序如果输出颜色失败，更新一下往往就能解决。

php存在问题，7.2.0已经解决，不过部分console软件为了兼容开始的win10关闭了颜色，可以使用--ansi之类的开启

### 安装
直接在官网下载即可，免安装，解压即可用。

### 配置
cmder配置

使用win+alt+p打开配置面板
main

字体、外观。。。
StartUp

配置打开终端执行的一些任务和环境变量设置
+ specified name task这儿可以选择默认启动的终端类型，如cmder、bash、cmd、powershell、git bash等
+ 解决中文乱码，很重要的设置：set LC_ALL=zh-CN.UTF8 ，不要使用set LANGUAGE=zh-CN.UTF8，因为这个设置了之后对{cmd:cmder}有效但是对{bash:bash}无效
+ current directory设置
+ cmder其实使用的是ComEmu终端，当我们新建一个相同终端的时候，想要从当前的目录开启一个新的终端而不是从startup目录开启。首先需要修改一下task的配置。
![](https://images2015.cnblogs.com/blog/971915/201707/971915-20170710205028634-952196635.png '1')
