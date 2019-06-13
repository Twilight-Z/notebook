# 常用代码

### 1、防止页面引用
使用iframe框架引用网页，是某些不法分子的“钓鱼”手段。

如果你发现自己的站点网页被另外非授权网站框架引用，该如何应对？

PHP代码如下：
```
// Break Out of Frames for WordPress
function break_out_of_frames() {
     if (!is_preview()) {
          echo "\n<script type=\"text/javascript\">";
          echo "\n<!--";
          echo "\nif (parent.frames.length > 0) { parent.location.href = location.href; }";
          echo "\n-->";
          echo "\n</script>\n\n";
     }
}
add_action('wp_head', 'break_out_of_frames');
```
<br><br><br>


### 2、网站简繁体切换
##### 首先，下载tw_cn.js 繁体包，并上传到你的网站的目录。

##### 第二，把以下代码添加到你的WordPress主题的footer中。
```
<script type="text/javascript"
src="http://www.ikxs.org/tw_cn.js"></script>
<script type="text/javascript">
var defaultEncoding = 0; //默认是否繁体，0-简体，1-繁体
var translateDelay = 0; //延迟时间,若不在前, 要设定延迟翻译时间, 如100表示100ms,默认为0
var cookieDomain = "http://www.ikxs.org"; //Cookie地址, 一定要设定, 通常为你的网址
var msgToTraditionalChinese = "繁體"; //默认切换为繁体时显示的中文字符
var msgToSimplifiedChinese = "简体"; //默认切换为简体时显示的中文字符
var translateButtonId = "translateLink"; //默认互换id
translateInitilization();
</script>
```

##### 第三，修改tw_cn.js第三行变量cookieDomain的值为你自己的域名。

##### 第四，在你需要添加繁简互译的地方加入以下代码
```
<aid="translateLink">繁體</a>
```
<br><br><br>


### 3、
```
```
<br><br><br>


### 1、
```
```
<br><br><br>
