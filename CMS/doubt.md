# CMS疑难杂症

### 1、PHP7 环境的兼容性问题
在 PHP7 上安装 ECShop V2.7.3时，报错！ 

`Deprecated: Methods with the same name as their class will not be constructors in a future version of PHP;`

 这个报错的原因是 PHP7 不再支持与类名相同的构造方法，构造方法统一使用 __construct(), 比如下面的写法 PHP7 就会报这个错误。

果然有与类名相同的构造方法，我们将构造方法 ECS 修改为 __construct，


`Deprecated: Non-static method cls_image::gd_version() should not be called statically in ... `
这个报错的原因是静态调用非静态方法，比如下面的代码就会报这个错误：
```
<?php  
class foo {  
    function bar() {
        echo 'I am not static!';
    }
}
foo::bar();  
?>
```
##### 第一种修改方式
将该方法修改为静态方法，在方法前加关键字 public static

##### 第二种修改方式
采用非静态方式的调用，修改lib_installer.php 的 31行代码
