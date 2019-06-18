# meta标签 常用方法

### 规范用法
```
<meta charset="utf-8"> <!-- 设置文档字符编码 -->
<meta http-equiv="x-ua-compatible" content="ie=edge"><!-- 告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面。 -->
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no"><!-- 指定页面初始缩放比例。-->
 
<!-- 上述3个meta标签须放在head标签最前面;其它head内容放在其后面，如link标签-->
 
<!-- 允许控制加载资源 -->
<meta http-equiv="Content-Security-Policy" content="default-src 'self'">
<!-- 尽可能早的放在文档 -->
<!-- 只适用于下面这个标签的内容 -->
 
<!-- 使用web应用程序的名称(当网站作为一个应用程序的时候)-->
<meta name="application-name" content="Application Name">
 
<!-- 页面的简短描述(限150个字符)-->
<!-- 在某些情况下这个描述作为搜索结果中所示的代码片段的一部分。-->
<meta name="description" content="A description of the page">
 
<!-- 控制搜索引擎爬行和索引的行为 -->
<meta name="robots" content="index,follow,noodp"><!-- 所有搜索引擎 -->
<meta name="googlebot" content="index,follow"><!-- 谷歌 -->
 
<!-- 告诉谷歌搜索框不显示链接 -->
<meta name="google" content="nositelinkssearchbox">
 
<!-- 告诉谷歌不要翻译这个页面 -->
<meta name="google" content="notranslate">
 
<!-- Google网站管理员工具的特定元标记，核实对谷歌搜索控制台所有权 -->
<meta name="google-site-verification" content="verification_token">
 
<!-- 说明用什么软件构建生成的网站，(例如,WordPress,Dreamweaver) -->
<meta name="generator" content="program">
 
<!-- 简短描述你的网站的主题 -->
<meta name="subject" content="your website's subject">
 
<!-- 很短(10个词以内)描述。主要学术论文 -->
<meta name="abstract" content="">
 
<!-- 完整的域名或网址 -->
<meta name="url" content="https://example.com/">
 
<meta name="directory" content="submission">
 
<!-- 对当前页面一个等级衡量，告诉蜘蛛当前页面在整个网站中的权重到底是多少。General是一般页面，Mature是比较成熟的页面，Restricted代表受限制的。 -->
<meta name="rating" content="General">
 
<!-- 隐藏发送请求时请求头表示来源的referrer字段。 -->
<meta name="referrer" content="no-referrer">
 
<!-- 禁用自动检测和格式的电话号码 -->
<meta name="format-detection" content="telephone=no">
 
<!-- 通过设置“off”,完全退出DNS队列 -->
<meta http-equiv="x-dns-prefetch-control" content="off">
 
<!-- 在客户端存储 cookie，web 浏览器的客户端识别-->
<meta http-equiv="set-cookie" content="name=value; expires=date; path=url">
 
<!-- 指定要显示在一个特定框架中的页面 -->
<meta http-equiv="Window-Target" content="_value">
 
<!-- 地理标签 -->
<meta name="ICBM" content="latitude, longitude">
<meta name="geo.position" content="latitude;longitude">
<meta name="geo.region" content="country[-state]"><!-- 国家代码 (ISO 3166-1): 强制性, 州代码 (ISO 3166-2): 可选; 如 content="US" / content="US-NY" -->
<meta name="geo.placename" content="city/town"><!-- 如 content="New York City" -->
```

