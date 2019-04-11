#　用于布局的实用程序
为了实现更快的移动友好和响应式开发，Bootstrap包含许多实用程序类，用于显示，隐藏，对齐和分隔内容。

### 更改 display
使用我们的显示实用程序来响应切换display属性的常见值。将其与我们的网格系统，内容或组件混合，以在特定视口中显示或隐藏它们。

### Flexbox选项
Bootstrap 4是使用flexbox构建的，但并不是每个元素display都被更改为，display: flex因为这会添加许多不必要的覆盖并意外地更改关键浏览器行为。我们的大多数组件都是在启用Flexbox的情况下构建的

如果您需要添加display: flex元素，请使用.d-flex其中一个响应变体（例如，.d-sm-flex）。您需要使用此类或display值来允许使用我们额外的flexbox实用程序来调整大小，对齐，间距等。

### 保证金和填充
使用margin和padding spacing实用程序来控制元素和组件的间距和大小。Bootstrap 4包含基于1rem值默认$spacer变量的间隔实用程序的五级刻度。选择所有视口（例如，值.mr-3了margin-right: 1rem），或挑响应变种，以针对特定的视口（例如，.mr-md-3对于margin-right: 1rem处于起步md断点）。

### 切换 visibility
当display不需要切换时，您可以visibility使用我们的可见性实用程序切换元素。不可见元素仍将影响页面的布局，但在视觉上对访问者隐藏。
