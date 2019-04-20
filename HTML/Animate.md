# animate.css的使用

## 效果演示
animate.css的使用非常简单，因为它是把不同的动画绑定到了不同的类里，所以想要使用哪种动画，只需要把通用类animated和相应的类添加到元素上就行了

下面来详细介绍animate.css里面的类，主要包括Attention(晃动效果)、bounce(弹性缓冲效果)、fade(透明度变化效果)、flip(翻转效果)、rotate(旋转效果)、slide(滑动效果)、zoom(变焦效果)、special(特殊效果)这8类

### 【Attention(晃动效果)】
```
bounce
flash
pulse
rubberBand
shake
headShake
swing
tada
wobble
jello

<div class="animated bounce"></div>

```

### 【bounce(弹性缓冲效果)】
```
bounceIn
bounceInDown
bounceInLeft
bounceInRight
bounceInUp
bounceOut
bounceOutDown
bounceOutLeft
bounceOutRight
bounceOutUp
```

### 【fade(透明度变化效果)】
```
fadeIn
fadeInDown
fadeInDownBig
fadeInLeft
fadeInLeftBig
fadeInRight
fadeInRightBig
fadeInUp
fadeInUpBig
fadeOut
fadeOutDown
fadeOutDownBig
fadeOutLeft
fadeOutLeftBig
fadeOutRight
fadeOutRightBig
fadeOutUp
fadeOutUpBig
```

### 【flip(翻转效果)】
```
flip
flipInX
flipInY
flipOutX
flipOutY
```

### 【rotate(旋转效果)】 
```
rotateIn
rotateInDownLeft
rotateInDownRight
rotateInUpLeft
rotateInUpRight
rotateOut
rotateOutDownLeft
rotateOutDownRight
rotateOutUpLeft
rotateOutUpRight
```

### 【slide(滑动效果)】 
```
slideInDown
slideInLeft
slideInRight
slideInUp
slideOutDown
slideOutLeft
slideOutRight
slideOutUp
```

### 【zoom(变焦效果)】
```
zoomIn
zoomInDown
zoomInLeft
zoomInRight
zoomInUp
zoomOut
zoomOutDown
zoomOutLeft
zoomOutRight
zoomOutUp
```

### 【special(特殊效果)】 
```
hinge
rollIn
rollOut
lightSpeedIn
lightSpeedOut
```

## 实际应用
在一般的使用中，直接在元素上添加animated和对应的类名即可
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Document</title>
<link rel="stylesheet" href="https://unpkg.com/animate.css@3.5.2/animate.min.css">
<style>
.box{height: 100px;width: 100px;background-color: lightblue}
</style>
</head>
<body>
<div class="box animated flash"></div>
</body>
</html>
```
通过给JS添加或删除class，可以实现动态效果
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Document</title>
<link rel="stylesheet" href="https://unpkg.com/animate.css@3.5.2/animate.min.css">
<style>
.box{height: 100px;width: 100px;background-color: lightblue}
</style>
</head>
<body>
<button id="btn1">添加</button>
<button id="btn2">移除</button>
<div id="box" class="box"></div>
<script>
var oBtn1 = document.getElementById('btn1');
var oBtn2 = document.getElementById('btn2');
var oBox = document.getElementById('box');
oBtn1.onclick = function(){
  oBox.classList.add('animated');
  oBox.classList.add('flash');
}
oBtn2.onclick = function(){
  oBox.classList.remove('flash');
}
</script>
</body>
</html>
```
至于动画的配置参数，比如动画持续时间，动画的执行次数等等，可以在元素上自行定义，覆盖掉animate.css里面所定义的就行了 
```
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Document</title>
<link rel="stylesheet" href="https://unpkg.com/animate.css@3.5.2/animate.min.css">
<style>
.box{height: 100px;width: 100px;background-color: lightblue}
.infinite{animation-iteration-count:infinite;}
</style>
</head>
<body>
<button id="btn1">添加循环的动画效果</button>
<button id="btn2">移除</button>
<div id="box" class="box"></div>
<script>
var oBtn1 = document.getElementById('btn1');
var oBtn2 = document.getElementById('btn2');
var oBox = document.getElementById('box');
oBtn1.onclick = function(){
  oBox.classList.add('animated');
  oBox.classList.add('flash');
  oBox.classList.add('infinite');
}
oBtn2.onclick = function(){
  oBox.classList.remove('flash');
}
</script>
</body>
</html>
```
