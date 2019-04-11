# 布局


### 概念
用于布置Bootstrap项目的组件和选项，包括包装容器，强大的网格系统，灵活的媒体对象和响应式实用程序类。

##### 集装箱
容器是Bootstrap中最基本的布局元素，在使用我们的默认网格系统时是必需的。从响应的固定宽度容器中选择（意味着它max-width在每个断点处的更改）或流体宽度（意味着它100%始终是宽的）。

虽然容器可以嵌套，但大多数布局不需要嵌套容器。
```
<div class="container">
  <!-- Content here -->
</div>
```
使用.container-fluid了全宽的容器，跨越视口的整个宽度。
```
<div class="container-fluid">
  ...
</div>
```
##### 响应断点
由于Bootstrap是首先开发的，我们使用少量媒体查询为我们的布局和界面创建合理的断点。这些断点主要基于最小视口宽度，并允许我们在视口更改时放大元素。

Bootstrap主要在我们的布局，网格系统和组件的源Sass文件中使用以下媒体查询范围或断点。
```
// Extra small devices (portrait phones, less than 576px)
// No media query since this is the default in Bootstrap

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) { ... }

// Medium devices (tablets, 768px and up)
@media (min-width: 768px) { ... }

// Large devices (desktops, 992px and up)
@media (min-width: 992px) { ... }

// Extra large devices (large desktops, 1200px and up)
@media (min-width: 1200px) { ... }
```
由于我们在Sass中编写源CSS，因此我们所有的媒体查询都可以通过Sass mixins获得：
```
@include media-breakpoint-up(xs) { ... }
@include media-breakpoint-up(sm) { ... }
@include media-breakpoint-up(md) { ... }
@include media-breakpoint-up(lg) { ... }
@include media-breakpoint-up(xl) { ... }

// Example usage:
@include media-breakpoint-up(sm) {
  .some-class {
    display: block;
  }
}
```
我们偶尔会使用向另一个方向（给定屏幕尺寸或更小）的媒体查询：
```
// Extra small devices (portrait phones, less than 576px)
@media (max-width: 575.98px) { ... }

// Small devices (landscape phones, less than 768px)
@media (max-width: 767.98px) { ... }

// Medium devices (tablets, less than 992px)
@media (max-width: 991.98px) { ... }

// Large devices (desktops, less than 1200px)
@media (max-width: 1199.98px) { ... }

// Extra large devices (large desktops)
// No media query since the extra-large breakpoint has no upper bound on its width
```
> 请注意，由于浏览器目前不支持范围方面的查询，我们解决的局限性min-和max-前缀和视口带小数的宽度（可下的高DPI设备一定的条件下发生，例如）通过使用值与这些比较高的精度。
再一次，这些媒体查询也可以通过Sass mixins获得：
```
@include media-breakpoint-down(xs) { ... }
@include media-breakpoint-down(sm) { ... }
@include media-breakpoint-down(md) { ... }
@include media-breakpoint-down(lg) { ... }
```
还有媒体查询和mixins，用于使用最小和最大断点宽度来定位单个屏幕尺寸段。
```
// Extra small devices (portrait phones, less than 576px)
@media (max-width: 575.98px) { ... }

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) and (max-width: 767.98px) { ... }

// Medium devices (tablets, 768px and up)
@media (min-width: 768px) and (max-width: 991.98px) { ... }

// Large devices (desktops, 992px and up)
@media (min-width: 992px) and (max-width: 1199.98px) { ... }

// Extra large devices (large desktops, 1200px and up)
@media (min-width: 1200px) { ... }
```
这些媒体查询也可以通过Sass mixins获得：
```
@include media-breakpoint-only(xs) { ... }
@include media-breakpoint-only(sm) { ... }
@include media-breakpoint-only(md) { ... }
@include media-breakpoint-only(lg) { ... }
@include media-breakpoint-only(xl) { ... }
```
同样，媒体查询可能跨越多个断点宽度：
```
// Example
// Apply styles starting from medium devices and up to extra large devices
@media (min-width: 768px) and (max-width: 1199.98px) { ... }
```
针对相同屏幕尺寸范围的Sass mixin将是：
```
@include media-breakpoint-between(md, xl) { ... }
```
Z-指数
几个Bootstrap组件利用z-indexCSS属性，通过提供第三个轴来排列内容来帮助控制布局。我们在Bootstrap中使用默认的z-index标度，该标度旨在正确地分层导航，工具提示和弹出窗口，模态等。

这些较高的值从任意数字开始，高且具体到足以理想地避免冲突。我们需要在我们的分层组件中提供一组标准 - 工具提示，弹出窗口，导航栏，下拉菜单，模态 - 因此我们可以在行为中合理地保持一致。我们没有理由不能使用100+或500+。

我们不鼓励定制这些个人价值观; 如果你换一个，你可能需要改变它们。
```
$zindex-dropdown:          1000 !default;
$zindex-sticky:            1020 !default;
$zindex-fixed:             1030 !default;
$zindex-modal-backdrop:    1040 !default;
$zindex-modal:             1050 !default;
$zindex-popover:           1060 !default;
$zindex-tooltip:           1070 !default;
```
为了处理重叠的组件（例如，按钮和输入组的输入）内的边界中，我们使用低单数位z-index的值1，2和3用于默认，悬停状态和活动状态。在悬停/焦点/活动时，我们将一个特定元素带到最前面，使用更高的z-index值来显示它们在兄弟元素上的边界。
<br><br><br>


### 网格系统
借助十二列系统，五个默认响应层，Sass变量和mixins以及数十个预定义类，使用我们强大的移动优先灵活盒网格来构建各种形状和大小的布局。

##### 这个怎么运作
Bootstrap的网格系统使用一系列容器，行和列来布局和对齐内容。它采用flexbox构建，完全响应。下面是一个示例，并深入了解网格如何组合在一起。

对flexbox不熟悉或不熟悉？ 阅读此CSS Tricks flexbox指南，了解背景，术语，指南和代码段。
```
<div class="container">
  <div class="row">
    <div class="col-sm">
      One of three columns
    </div>
    <div class="col-sm">
      One of three columns
    </div>
    <div class="col-sm">
      One of three columns
    </div>
  </div>
</div>
```
上面的示例使用我们预定义的网格类在小型，中型，大型和超大型设备上创建三个等宽列。这些列在父页面的中心位置.container。

打破它，这是它的工作原理：
+ 容器提供了一种中心和水平填充站点内容的方法。使用.container了应答像素宽度或.container-fluid用于width: 100%在所有视窗和器件尺寸。
+ 行是列的包装器。每列都有水平padding（称为装订线），用于控制它们之间的空间。这padding随后抵消上切缘阴性的行。这样，列中的所有内容都在左侧可视化对齐。
+ 在网格布局中，内容必须放在列中，只有列可以是行的直接子项。
+ 由于flexbox，没有指定的网格列width将自动布局为等宽列。例如，四个实例.col-sm将从小断点向上自动增加25％。有关更多示例，请参阅自动布局列部分。
+ 列类指示您希望在每行可能使用的12列中使用的列数。因此，如果您想要三个相等宽度的列，则可以使用.col-4。
+ 列widths以百分比形式设置，因此它们总是相对于其父元素是流动的和大小的。
+ 列具有水平padding创建单独的列之间的排水沟，然而，你可以删除margin从行，padding从列与.no-gutters上.row。
+ 为了使网格响应，有五个网格断点，每个响应断点一个：所有断点（超小），小，中，大和超大。
+ 网格断点基于最小宽度的媒体查询，这意味着它们适用于那个断点以及它上面的所有断点（例如，.col-sm-4适用于小型，中型，大型和超大型设备，但不适用于第一个xs断点）。
+ 您可以使用预定义的网格类（如.col-4）或Sass mixins进行更多语义标记。
请注意flexbox的限制和错误，例如无法将某些HTML元素用作Flex容器。

##### 网格选项
虽然Bootstrap使用ems或rems来定义大多数大小，但pxs用于网格断点和容器宽度。这是因为视口宽度以像素为单位，并且不随字体大小而变化。

了解Bootstrap网格系统的各个方面如何在具有便捷表的多个设备上工作。

##### 自动布局列
利用特定于断点的列类，可以轻松进行列大小调整，而无需使用明确的编号类.col-sm-6。

##### 等宽
例如，下面是适用于所有的设备和视口，从两个网格布局xs来xl。为您需要的每个断点添加任意数量的无单位类，每列的宽度相同。
```
<div class="container">
  <div class="row">
    <div class="col">
      1 of 2
    </div>
    <div class="col">
      2 of 2
    </div>
  </div>
  <div class="row">
    <div class="col">
      1 of 3
    </div>
    <div class="col">
      2 of 3
    </div>
    <div class="col">
      3 of 3
    </div>
  </div>
</div>
```
等宽列可以分成多行，但有一个Safari flexbox错误阻止它在没有显式flex-basis或border。有较旧的浏览器版本的解决方法，但如果您是最新的，则不需要它们。
```
<div class="container">
  <div class="row">
    <div class="col">Column</div>
    <div class="col">Column</div>
    <div class="w-100"></div>
    <div class="col">Column</div>
    <div class="col">Column</div>
  </div>
</div>
```

##### 设置一个列宽
flexbox网格列的自动布局还意味着您可以设置一列的宽度，并让兄弟列自动调整其大小。您可以使用预定义的网格类（如下所示），网格混合或内联宽度。请注意，无论中心列的宽度如何，其他列都将调整大小。
```
<div class="container">
  <div class="row">
    <div class="col">
      1 of 3
    </div>
    <div class="col-6">
      2 of 3 (wider)
    </div>
    <div class="col">
      3 of 3
    </div>
  </div>
  <div class="row">
    <div class="col">
      1 of 3
    </div>
    <div class="col-5">
      2 of 3 (wider)
    </div>
    <div class="col">
      3 of 3
    </div>
  </div>
</div>
```

##### 可变宽度内容
使用col-{breakpoint}-auto类根据内容的自然宽度调整列的大小。
```
<div class="container">
  <div class="row justify-content-md-center">
    <div class="col col-lg-2">
      1 of 3
    </div>
    <div class="col-md-auto">
      Variable width content
    </div>
    <div class="col col-lg-2">
      3 of 3
    </div>
  </div>
  <div class="row">
    <div class="col">
      1 of 3
    </div>
    <div class="col-md-auto">
      Variable width content
    </div>
    <div class="col col-lg-2">
      3 of 3
    </div>
  </div>
</div>
```

##### 等宽多排
通过插入.w-100要将列拆分到新行的位置，创建跨越多行的等宽列。通过混合.w-100使用一些响应式显示实用程序来使休息响应。
```
<div class="row">
  <div class="col">col</div>
  <div class="col">col</div>
  <div class="w-100"></div>
  <div class="col">col</div>
  <div class="col">col</div>
</div>
```

##### 反应级
Bootstrap的网格包括五层预定义类，用于构建复杂的响应式布局。根据您认为合适的额外小型，小型，中型，大型或超大型设备自定义列的大小。

##### 所有断点
对于从最小设备到最大设备相同的网格，请使用.col和.col-*类。当需要特别大小的列时，请指定编号的类; 否则，请随时坚持下去.col。
```
<div class="row">
  <div class="col">col</div>
  <div class="col">col</div>
  <div class="col">col</div>
  <div class="col">col</div>
</div>
<div class="row">
  <div class="col-8">col-8</div>
  <div class="col-4">col-4</div>
</div>
```

##### 堆叠到水平
使用一组.col-sm-*类，您可以创建一个基本的网格系统，该系统在小断点（sm）变为水平之前开始堆叠。
``` 
<div class="row">
  <div class="col-sm-8">col-sm-8</div>
  <div class="col-sm-4">col-sm-4</div>
</div>
<div class="row">
  <div class="col-sm">col-sm</div>
  <div class="col-sm">col-sm</div>
  <div class="col-sm">col-sm</div>
</div>
```
##### 连连看
不希望您的列只是在一些网格层中堆叠？根据需要为每个层使用不同类的组合。请参阅下面的示例，以便更好地了解它是如何工作的。
```
<!-- Stack the columns on mobile by making one full-width and the other half-width -->
<div class="row">
  <div class="col-12 col-md-8">.col-12 .col-md-8</div>
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
</div>

<!-- Columns start at 50% wide on mobile and bump up to 33.3% wide on desktop -->
<div class="row">
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
</div>

<!-- Columns are always 50% wide, on mobile and desktop -->
<div class="row">
  <div class="col-6">.col-6</div>
  <div class="col-6">.col-6</div>
</div>
```

##### 对准
使用flexbox对齐实用程序垂直和水平对齐列。

##### 垂直对齐
```
<div class="container">
  <div class="row align-items-start">
    <div class="col">
      One of three columns
    </div>
    <div class="col">
      One of three columns
    </div>
    <div class="col">
      One of three columns
    </div>
  </div>
  <div class="row align-items-center">
    <div class="col">
      One of three columns
    </div>
    <div class="col">
      One of three columns
    </div>
    <div class="col">
      One of three columns
    </div>
  </div>
  <div class="row align-items-end">
    <div class="col">
      One of three columns
    </div>
    <div class="col">
      One of three columns
    </div>
    <div class="col">
      One of three columns
    </div>
  </div>
</div>
```
```
<div class="container">
  <div class="row">
    <div class="col align-self-start">
      One of three columns
    </div>
    <div class="col align-self-center">
      One of three columns
    </div>
    <div class="col align-self-end">
      One of three columns
    </div>
  </div>
</div>
```

##### 水平对齐
```
<div class="container">
  <div class="row justify-content-start">
    <div class="col-4">
      One of two columns
    </div>
    <div class="col-4">
      One of two columns
    </div>
  </div>
  <div class="row justify-content-center">
    <div class="col-4">
      One of two columns
    </div>
    <div class="col-4">
      One of two columns
    </div>
  </div>
  <div class="row justify-content-end">
    <div class="col-4">
      One of two columns
    </div>
    <div class="col-4">
      One of two columns
    </div>
  </div>
  <div class="row justify-content-around">
    <div class="col-4">
      One of two columns
    </div>
    <div class="col-4">
      One of two columns
    </div>
  </div>
  <div class="row justify-content-between">
    <div class="col-4">
      One of two columns
    </div>
    <div class="col-4">
      One of two columns
    </div>
  </div>
</div>
```

##### 没有排水沟
我们预定义的网格类中的列之间的排水沟可以删除.no-gutters。这消除了负margin从s .row和水平padding从所有直接子列。

这是创建这些样式的源代码。请注意，列覆盖仅限于第一个子列，并通过属性选择器进行定位。虽然这会生成更具体的选择器，但仍可以使用间距实用程序进一步自定义列填充。

需要边缘到边缘的设计？放弃父母.container或.container-fluid。
```
.no-gutters {
  margin-right: 0;
  margin-left: 0;

  > .col,
  > [class*="col-"] {
    padding-right: 0;
    padding-left: 0;
  }
}
```
在实践中，这是它的外观。请注意，您可以继续将其与所有其他预定义网格类（包括列宽，响应层，重新排序等）一起使用。
```
<div class="row no-gutters">
  <div class="col-12 col-sm-6 col-md-8">.col-12 .col-sm-6 .col-md-8</div>
  <div class="col-6 col-md-4">.col-6 .col-md-4</div>
</div>
```

##### 列包装
如果在一行中放置超过12列，则每组额外列将作为一个单元包裹到新行上。
```
<div class="row">
  <div class="col-9">.col-9</div>
  <div class="col-4">.col-4<br>Since 9 + 4 = 13 &gt; 12, this 4-column-wide div gets wrapped onto a new line as one contiguous unit.</div>
  <div class="col-6">.col-6<br>Subsequent columns continue along the new line.</div>
</div>
```

#####　列断裂
将列拆分为flexbox中的新行需要一个小的hack：添加一个元素，width: 100%无论您想将列包装到新行。通常这是通过多个.rows 来完成的，但并非每种实现方法都可以解释这一点。
｀｀｀
<div class="row">
  <div class="col-6 col-sm-3">.col-6 .col-sm-3</div>
  <div class="col-6 col-sm-3">.col-6 .col-sm-3</div>

  <!-- Force next columns to break to new line -->
  <div class="w-100"></div>

  <div class="col-6 col-sm-3">.col-6 .col-sm-3</div>
  <div class="col-6 col-sm-3">.col-6 .col-sm-3</div>
</div>
｀｀｀
您也可以使用我们的响应式显示实用程序在特定断点处应用此中断。
｀｀｀
<div class="row">
  <div class="col-6 col-sm-4">.col-6 .col-sm-4</div>
  <div class="col-6 col-sm-4">.col-6 .col-sm-4</div>

  <!-- Force next columns to break to new line at md breakpoint and up -->
  <div class="w-100 d-none d-md-block"></div>

  <div class="col-6 col-sm-4">.col-6 .col-sm-4</div>
  <div class="col-6 col-sm-4">.col-6 .col-sm-4</div>
</div>
｀｀｀

#### 重新排序
##### 订单类
使用.order-类来控制内容的可视顺序。这些类是响应式的，因此您可以设置orderby断点（例如，.order-1.order-md-2）。包括支持1通过12所有五格层。
```
<div class="container">
  <div class="row">
    <div class="col">
      First, but unordered
    </div>
    <div class="col order-12">
      Second, but last
    </div>
    <div class="col order-1">
      Third, but first
    </div>
  </div>
</div>
```
还有响应.order-first和.order-last类order通过分别应用order: -1和order: 13（order: $columns + 1）来改变元素。这些类也可以.order-*根据需要与编号的类混合。
```
<div class="container">
  <div class="row">
    <div class="col order-last">
      First, but last
    </div>
    <div class="col">
      Second, but unordered
    </div>
    <div class="col order-first">
      Third, but first
    </div>
  </div>
</div>
```

##### 偏移列
您可以通过两种方式偏移网格列：响应.offset-网格类和边际效用。网格类的大小可以匹配列，而边距对于偏移宽度可变的快速布局更有用。

##### 抵消课程
使用.offset-md-*类将列向右移动。这些类按*列增加列的左边距。例如，.offset-md-4移动.col-md-4四列。
```
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4 offset-md-4">.col-md-4 .offset-md-4</div>
</div>
<div class="row">
  <div class="col-md-3 offset-md-3">.col-md-3 .offset-md-3</div>
  <div class="col-md-3 offset-md-3">.col-md-3 .offset-md-3</div>
</div>
<div class="row">
  <div class="col-md-6 offset-md-3">.col-md-6 .offset-md-3</div>
</div>
```
除了响应断点处的列清除之外，您可能还需要重置偏移量。在网格示例中查看此操作。
```
<div class="row">
  <div class="col-sm-5 col-md-6">.col-sm-5 .col-md-6</div>
  <div class="col-sm-5 offset-sm-2 col-md-6 offset-md-0">.col-sm-5 .offset-sm-2 .col-md-6 .offset-md-0</div>
</div>

<div class="row">
  <div class="col-sm-6 col-md-5 col-lg-6">.col-sm-6 .col-md-5 .col-lg-6</div>
  <div class="col-sm-6 col-md-5 offset-md-2 col-lg-6 offset-lg-0">.col-sm-6 .col-md-5 .offset-md-2 .col-lg-6 .offset-lg-0</div>
</div>
```

##### 保证金公用事业
随着在v4中转向flexbox，您可以使用保证金实用程序，例如.mr-auto强制兄弟列彼此远离。
```
<div class="row">
  <div class="col-md-4">.col-md-4</div>
  <div class="col-md-4 ml-auto">.col-md-4 .ml-auto</div>
</div>
<div class="row">
  <div class="col-md-3 ml-md-auto">.col-md-3 .ml-md-auto</div>
  <div class="col-md-3 ml-md-auto">.col-md-3 .ml-md-auto</div>
</div>
<div class="row">
  <div class="col-auto mr-auto">.col-auto .mr-auto</div>
  <div class="col-auto">.col-auto</div>
</div>
```

##### 嵌套
要使用默认网格嵌套内容，请在现有列中添加一组新列.row和一组列。嵌套行应包含一组最多可添加12个或更少的列（不要求您使用所有12个可用列）。.col-sm-*.col-sm-*
```
<div class="row">
  <div class="col-sm-9">
    Level 1: .col-sm-9
    <div class="row">
      <div class="col-8 col-sm-6">
        Level 2: .col-8 .col-sm-6
      </div>
      <div class="col-4 col-sm-6">
        Level 2: .col-4 .col-sm-6
      </div>
    </div>
  </div>
</div>
```

##### Sass mixins
使用Bootstrap的源Sass文件时，您可以选择使用Sass变量和mixins来创建自定义，语义和响应式页面布局。我们的预定义网格类使用这些相同的变量和mixins来提供一整套即用型类，以实现快速响应式布局。

##### 变量
变量和映射确定列的数量，装订线宽度以及开始浮动列的媒体查询点。我们使用它们来生成上面记录的预定义网格类，以及下面列出的自定义混合类。
```
$grid-columns:      12;
$grid-gutter-width: 30px;

$grid-breakpoints: (
  // Extra small screen / phone
  xs: 0,
  // Small screen / phone
  sm: 576px,
  // Medium screen / tablet
  md: 768px,
  // Large screen / desktop
  lg: 992px,
  // Extra large screen / wide desktop
  xl: 1200px
);

$container-max-widths: (
  sm: 540px,
  md: 720px,
  lg: 960px,
  xl: 1140px
);
```

##### 混入
Mixins与网格变量结合使用，为各个网格列生成语义CSS。
```
// Creates a wrapper for a series of columns
@include make-row();

// Make the element grid-ready (applying everything but the width)
@include make-col-ready();
@include make-col($size, $columns: $grid-columns);

// Get fancy by offsetting, or changing the sort order
@include make-col-offset($size, $columns: $grid-columns);
```

##### 用法示例
您可以将变量修改为您自己的自定义值，或者只使用带有默认值的mixins。下面是使用默认设置创建两列布局的示例。
```
.example-container {
  width: 800px;
  @include make-container();
}

.example-row {
  @include make-row();
}

.example-content-main {
  @include make-col-ready();

  @include media-breakpoint-up(sm) {
    @include make-col(6);
  }
  @include media-breakpoint-up(lg) {
    @include make-col(8);
  }
}

.example-content-secondary {
  @include make-col-ready();

  @include media-breakpoint-up(sm) {
    @include make-col(6);
  }
  @include media-breakpoint-up(lg) {
    @include make-col(4);
  }
}
```
```
<div class="example-container">
  <div class="example-row">
    <div class="example-content-main">Main content</div>
    <div class="example-content-secondary">Secondary content</div>
  </div>
</div>
```

##### 自定义网格
使用我们内置的网格Sass变量和映射，可以完全自定义预定义的网格类。更改层数，媒体查询维度和容器宽度 - 然后重新编译。

##### 列和排水沟
可以通过Sass变量修改网格列的数量。$grid-columns用于产生每个单独的列的宽度（以百分数表示），同时$grid-gutter-width允许断点特定宽度在跨越均匀划分padding-left并padding-right为列水槽。
```
$grid-columns: 12 !default;
$grid-gutter-width: 30px !default;
```

##### 网格层
超出列本身，您还可以自定义网格层的数量。如果你想只有四格层，你会更新$grid-breakpoints，并$container-max-widths以这样的：
```
$grid-breakpoints: (
  xs: 0,
  sm: 480px,
  md: 768px,
  lg: 1024px
);

$container-max-widths: (
  sm: 420px,
  md: 720px,
  lg: 960px
);
```
对Sass变量或映射进行任何更改时，您需要保存更改并重新编译。这样做将为列宽，偏移和排序输出一组全新的预定义网格类。响应式可见性实用程序也将更新为使用自定义断点。确保在设置网格值px（不是rem，em或%）。

