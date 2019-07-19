# WordPress 常用代码

### 一、去版本号
```
// 同时删除head和feed中的WP版本号
function ludou_remove_wp_version() {
  return '';
}
add_filter('the_generator', 'ludou_remove_wp_version');

// 隐藏js/css附加的WP版本号
function ludou_remove_wp_version_strings( $src ) {
  global $wp_version;
  parse_str(parse_url($src, PHP_URL_QUERY), $query);
  if ( !empty($query['ver']) && $query['ver'] === $wp_version ) {
    // 用WP版本号 + 12.8来替代js/css附加的版本号
    // 既隐藏了WordPress版本号，也不会影响缓存
    // 建议把下面的 12.8 替换成其他数字，以免被别人猜出
    $src = str_replace($wp_version, $wp_version + 12.8, $src);
  }
  return $src;
}
add_filter( 'script_loader_src', 'ludou_remove_wp_version_strings' );
add_filter( 'style_loader_src', 'ludou_remove_wp_version_strings' );
```
WordPress安装目录下的readme.html也会泄漏版本，每次更新后记得删除。
<br><br><br>

### 二、网站简繁体切换
##### 首先，下载[tw_cn.js](https://www.chendexin.com/zb_users/upload/2016/05/zh-cn-tw.zip) 繁体包，并上传到你的网站的目录。

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

### 三、去双击评论内容可以编辑评论
```
<?php
/*
 * Plugin Name: Remove Double-Click to Edit for Comments
 * Description: Disables the double-click to edit action for comments
 * Author: Pippin Williamson
 * Version: 1.0
 */

class Remove_Double_Click_To_Edit {
      
   public function __construct() {
      add_action( 'admin_footer', array( $this, 'javascript' ) );
   }

   public function javascript() {

      global $pagenow;

      if( 'edit-comments.php' != $pagenow ) {
         return;
      }
?>
      <script>
      (function($){
         $('tr.comment').each(function() {
            $(this).find('a.vim-q').each(function() {
               $(this).removeClass('vim-q');
            });
         });
      }(jQuery));
      </script>
<?php
   }

}
new Remove_Double_Click_To_Edit;
```
<br><br><br>


### 四、只允许用户评论一次
这个功能实现起来也比较简单，只需每次用户发表的评论进数据库之前，从当前文章的所有评论中查找是否有相同的用户名或邮箱已经发表过评论，如果有就跳到错误页面即可。

实现代码，放到当前主题的functions.php中即可（这里还增加了对IP的判断，更保险）：
```
// 获取评论用户的ip，参考wp-includes/comment.php
function ludou_getIP() {
  $ip = $_SERVER['REMOTE_ADDR'];
  $ip = preg_replace( '/[^0-9a-fA-F:., ]/', '', $ip );
    
  return $ip;
}

function ludou_only_one_comment( $commentdata ) {
  global $wpdb;
  $currentUser = wp_get_current_user();
  
  // 不限制管理员发表评论
  if(empty($currentUser->roles) || !in_array('administrator', $currentUser->roles)) {
    $bool = $wpdb->get_var("SELECT comment_ID FROM $wpdb->comments WHERE comment_post_ID = ".$commentdata['comment_post_ID']."  AND (comment_author = '".$commentdata['comment_author']."' OR comment_author_email = '".$commentdata['comment_author_email']."' OR comment_author_IP = '".ludou_getIP()."') LIMIT 0, 1;");
  
    if($bool)
      wp_die('本站每篇文章只允许评论一次。<a href="'.get_permalink($commentdata['comment_post_ID']).'">点此返回</a>');
  }
  
  return $commentdata;
}
add_action( 'preprocess_comment' , 'ludou_only_one_comment', 20);
```
<br><br><br>


### 五、去除带replytocom参数链接，防止收录重复内容
##### 1.禁止蜘蛛抓取replytocom

  在网站根目录下的robots.txt中，加入以下规则，禁止搜索引擎抓取含有 ?replytocom= 的链接：
```
User-agent: *
Disallow: /*?replytocom=
```

##### 2.给链接添加nofollow
  此方法效果跟上面的差不多。我们可以在当前主题的functions.php中添加以下PHP代码，
  这样就给回复按钮链接添加rel="nofollow"属性，同样可以告诉搜索引擎不要抓取此链接：
```
add_filter('comment_reply_link', 'add_nofollow', 420, 4);

function add_nofollow($link, $args, $comment, $post){
  return preg_replace( '/href=\'(.*(\?|&)replytocom=(\d+)#respond)/', 'href=\'#comment-$3', $link );
}
```

##### 3.直接删除replytocom链接
   有些搜索引擎并不遵守robots.txt规则或nofollow属性，会照样抓取replytocom链接。
     
   我们可以在当前主题的functions.php中添加以下PHP代码，这样链接A就会直接被替换成了#comment-评论id，
   
   搜索引擎会自动忽略带 # 号的链接，并且你的网站再也不存在replytocom链接了：
```
add_filter('comment_reply_link', 'add_nofollow', 420, 4);

function add_nofollow($link, $args, $comment, $post){
  return preg_replace( '/href=\'(.*(\?|&)replytocom=(\d+)#respond)/', 'href=\'#comment-$3', $link );
}
```
如果你不喜欢 #comment-评论id 这样的链接，可以将第4行代码中的 #comment-$3 改成你自己喜欢的链接。
<br><br><br>

### 六、默认角色用户无法进入后台
有些时候我们会用到WordPress的用户注册功能，但是限于WordPress的用户系统功能比较单调，

除了登录和注册，我们可能不会让用户直接使用WordPress的后台，而是在前台编写个用户系统，

或者使用WP User Frontend等插件自动在前台生成一个用户系统。

如果你不想让默认角色的用户进入WordPress后台乱逛，你可以在当前主题的functions.php中加入以下代码，

然后使用默认角色的用户帐号登录，看是什么情况，是不是直接跳转到首页了呢？
```
if ( is_admin() && ( !defined( 'DOING_AJAX' ) || !DOING_AJAX ) ) {
  $current_user = wp_get_current_user();
  if($current_user->roles[0] == get_option('default_role')) {
    wp_safe_redirect( home_url() );
    exit();
  }
```
<br><br><br>


### 七、注册成功后跳转到指定页面
有些时候我们并不想让他跳转到这个页面，而是跳转到我们指定的一个页面，那么怎么办呢？

我们可以在当前主题的functions.php的第一个<?php 下面添加以下php代码：
```
// 注册成功后跳转到指定页面
function __my_registration_redirect() {
  // 这里设置的是跳转到首页，要换成其他页面
  // 可以将home_url()改成你指定的URL
  // 如 return 'http://www.baidu.com';
  return home_url();
}
add_filter( 'registration_redirect', '__my_registration_redirect' );
```
<br><br><br>


### 八、退出后跳转到指定页面
将下面的php代码放到当前主题的functions.php中即可：
```
add_filter('logout_url', 'ludou_logout_redirect', 10, 2);

function ludou_logout_redirect($logouturl, $redir) {
  $redir = 'https://www.ludou.org/'; // 这里改成你要跳转的网址
  return $logouturl . '&redirect_to=' . urlencode($redir);
}
```
这样你在后台页面右上角点击退出后，就可以跳转到指定页面了。

如果你是想在前台添加一个退出链接，点击后退出登录并跳转到指定站内页面，可以使用以下代码(代码中网址改成你的)：
```
<?php if ( $user_ID )  { ?>
<a href="<?php echo wp_logout_url( 'https://www.ludou.org/' ); ?>" title="Logout">Logout</a>
<?php } ?>
```
如果是要跳转到首页，可以使用下面的代码：
```
<?php if ( $user_ID )  { ?>
<a href="<?php echo wp_logout_url( home_url() ); ?>" title="Logout">Logout</a>
<?php } ?>
```
如果是要跳转到退出前所在的页面，可以使用以下代码：
```
<?php if ( $user_ID )  { ?>
<a href="<?php echo wp_logout_url( home_url(add_query_arg(array(),$wp->request)) ); ?>" title="Logout">Logout</a>
<?php } ?>
```
<br><br><br>


### 九、自动去除img的width和height属性
当访客使用手机访问时，自动删除文章内容中图片的width和height属性，以达到自适应的效果。

为了达到此目的，在当前主题的functions.php中加入以下PHP代码即可：
```
// 自适应图片删除width和height，by Ludou
function ludou_remove_width_height_attribute($content){
  preg_match_all('/<[img|IMG].*?src=[\'|"](.*?(?:[\.gif|\.jpg|\.png\.bmp]))[\'|"].*?[\/]?>/', $content, $images);
  if(!empty($images)) {
    foreach($images[0] as $index => $value){
      $new_img = preg_replace('/(width|height)="\d*"\s/', "", $images[0][$index]);
      $content = str_replace($images[0][$index], $new_img, $content);
    }
  }
  return $content;
}

// 判断是否是移动设备浏览
if(wp_is_mobile()) {
   // 删除文章内容中img的width和height属性
   add_filter('the_content', 'ludou_remove_width_height_attribute', 99);
}
```
<br><br><br>

### 十、url跳转
##### 一、页面跳转
```
<script language="javascript">
    document.location= "http://www.xiaoz.me/";
</script>
```
需要注意的是页面的固定链接建议自己设置一下，不要使用中文，否则会被转义增加长度，对SEO不利。 

##### 二、页面跳转
1、打开Editplus新建一个PHP文件，复制粘贴如下代码,然后另存为go.php再上传到网站根目录。

然后跳转的格式为：`{本站地址}/go.php?url={外链地址}`，例如：

`http://www.xiaoz.me/go.php?url=http://weibo.com/337003006`

2、打开Editplus新建一个PHP文件，复制粘贴如下代码,然后另存为go.php再上传到网站根目录。

这样出来的形式就是`{本站地址}/go.php?{外链地址}`，相对于第一种来说去掉了`url=`，然后稍微简短了一些。 

    最后不要忘记在robots.txt文件中添加：Disallow: /go.php?，防止搜索引擎抓取go.php，不然起不到任何作用。

<br><br><br>
