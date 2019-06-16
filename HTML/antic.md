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


### 2、点击图片 上传
html代码如下：
```
<div class="img_show">
     <img style="max-width: 100%; min-height: 100%" src="<?php echo $user['u_photo']==''?'images/user_01.gif':          _UPLOAD_.$user['u_photo'] ?>" alt="">
     <input style="display: none" type="file" name="upload" class="upfile" accept="*/*">
</div>
```

js代码如下：
```
<script>
	let DI = $('.main .img_show .upfile');
     let oBtn = $('.img_show>img');
	oBtn.click(function(){
		DI.trigger('click');
	});
	DI.upfile = function () {
		$('.img_show').each(function () {
			var $this = $(this),
                    btn = $this.find('.upfile'),
                    img = $this.find('img');
			DI.on('change', function () {
				var file = $(this)[0].files[0],
					imgSrc = $(this)[0].value,
					url = URL.createObjectURL(file);
				if (!/\.(jpg|jpeg|png|JPG|PNG|JPEG)$/.test(imgSrc)) {
					alert("请上传jpg或png格式的图片！");
					return false;
				} else {
					img.attr('src', url);
					img.css({
						'opacity': '1'
					});
				}

			});
		});
	}();
</script>
```
<br><br><br>


### 3、页面加载动画
```
<script src="js/jquery-2.2.3.min.js"></script>
<!--页面加载start-->
{load href="css/loader.css" /}
<script type="text/javascript">
 // 等待所有加载
 // $(window).load(function(){
 //    $('body').addClass('loaded');
 //    $('#loader-wrapper .load_title').remove();
 // });
 // 0-1秒加载动画
 setTimeout(function(){
    $('body').addClass('loaded');
    $('#loader-wrapper .load_title').remove();
 },Math.random());
</script>
<div id="loader-wrapper">
 <div id="loader"></div>
 <div class="loader-section section-left"></div>
 <div class="loader-section section-right"></div>
 <div class="load_title"><br>正在加载XX网站<br><span>V1.0</span></div>
</div>
<!--页面加载end-->
```
<br><br><br>
