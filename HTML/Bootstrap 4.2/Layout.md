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
