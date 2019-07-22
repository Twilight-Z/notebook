# Polylang多语言函数参考

### pll_the_languages，显示语言切换器
```
pll_the_languages($args);
```

$args是一个可选参数，选项如下：

· ‘dropdown’ => 显示为列表设置为 0, 下拉设置为1 (default: 0)

· ‘show_names’ => 显示语言名称设置为 1 (default: 1)

· ‘display_names_as’ => 可以是 ‘name’ 或 ‘slug’ (default: ‘name’)

· ‘show_flags’ => 显示国旗设置为1 (default: 0)

· ‘hide_if_empty’ => 设置为1，在没有翻译时，隐藏语言切换器 (或页面) (default: 1)

· ‘force_home’ => 如果设置为1，强制链接到首页 (default: 0)
‘echo’ => 显示设置为 1, 返回设置为 0 (default: 1)

· ‘hide_if_no_translation’ => 如果设置为1，在没有翻译时隐藏该语言 (default: 0)

· ‘hide_current’=> 如果设置为1，隐藏当前语言 (default: 0)

· ‘post_id’ => 如果设置了，显示指向翻译文章（或页面）的链接 (default: null)

· ‘raw’ => 用来创建自定义语言切换器 (default:0)

重要：如果以下拉方式使用语言切换器，你必须自行提供附加到语言切换器的 Action，如果你想要小工具提供的同一个内容，你可以在 polylang/include/widget.php 中找到正确的代码，如果不使用下拉选项，你必须自定输入ul标签。
```
<?php // 输出语言名称列表 ?> <ul><?php pll_the_languages(); ?></ul>
<?php // 输出国旗列表 (没有语言名称) ?> <ul>
<?php pll_the_languages(array('show_flags'=>1,'show_names'=>0)); ?></ul>
<?php // 以下拉方式输出语言列表 ?> <?php pll_the_languages(array('dropdown'=>1)); ?>
```
如果以上选项不够用，你还可以是用 ‘raw’ 参数自定义语言切换器。
```
$translations = pll_the_languages(array('raw'=>1));
```
此函数将赴会一个多元数组，每个语言都有以下内容。

· [id] => 语言 id

· [slug] => urls中使用的语言代码

· [name] => 语言名称

· [url] => 翻译的url

· [flag] => 语言国旗的 url

· [current_lang] => 如果显示的是当前语言为 true，其他情况下为 false

· [no_translation] => 如果没有可用翻译为 true，其他情况下为 false


<br><br><br>
### pll_current_language，返回当前语言
使用方法：
```
pll_current_language($value);
```
· ‘$value’ => (optional) 可以是 ‘name’ 或 ‘locale’ 或 ‘slug’, 默认为 ‘slug’

返回当前语言的全名，或 WordPress locale，（类似于WordPress核心函数‘get_locale’），或当前语言的slug（2个字母的语言代码）


<br><br><br>
### pll_default_language，返回默认语言
使用方法：
```
pll_default_language($value);
```
· ‘$value’ => (optional) 可以是 ‘name’ 或 ‘locale’ 或 ‘slug’, 默认为 ‘slug’

返回当前语言的全名，或 WordPress locale，（类似于WordPress核心函数‘get_locale’），或当前语言的 slug（2个字母的语言代码）


<br><br><br>
### pll_get_post，返回文章（或页面）的翻译
这个函数获取的是指定文章对应的当前语言的文章 ID (注意：不是文章对象)，理解起来可能有点绕，比如说关于我们中文语言的页面 ID 是 “100”，而关于我们英文语言版本的页面 ID 是 “101”，这个函数就是获取这两个页面的 ID 的。下面函数中的$post_id 参数就是 “100”，在中文语言下，返回的还是 “100”，在英文语言下，返回的 “101”，同理，我们把$post_id 设置为 “101” 也是一样的效果。

使用方法：
```
pll_get_post($post_id, $slug);
```
· ‘$post_id’ => (required) 需要翻译的文章id

· ‘$slug’ => (optional) 22个字母的语言代码，默认为当前语言
根据获取某个文章各种语言版本的对象

有时候，我们需要根据固定的文章 ID 获取某篇文章的内容，如果直接使用 WordPress 的 get_post 函数获取，获取的只是固定的一篇文章，切换语言时页面内容不会根据语言的不同而变化。Polylang 当然考虑到这个问题了，使用以下的方法即可获取某篇文章当前语言或者对应的翻译内容。
```
<?php $post = get_post( pll_get_post( 97, pll_current_language() ) ); ?>
```


<br><br><br>
### pll_get_term，返回文章（或页面）的翻译
使用方法：
```
pll_get_post($post_id, $slug);
```
· ‘$post_id’ => (required) 需要翻译的分类id

· ‘$slug’ => (optional) 22个字母的语言代码，默认为当前语言

以整数方法返回翻译后的分类id


<br><br><br>
### pll_home_url，返回首页 URL
使用方法：
```
pll_home_url($slug);
```
· ‘$slug’ => (optional) 22个字母的语言代码，此参数为可选项，如果在前段调用，默认为当前语言。

以字符串方式返回当前请求语言的 URL。
