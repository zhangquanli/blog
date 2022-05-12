项目中经常需要我们对溢出文本进行 "..." 显示的操作。如果文本所在元素不是块级元素，使用 display 属性为块级元素。以下代码分别对块级元素和行内元素进行设置，注意代码只针对单行文本的情况。

```html
<div class="div-ellipsis">
  2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。
</div>
<div>
  <span class="span-ellipsis">
    2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。
  </span>
</div>
<style>
  .div-ellipsis {
    width: 200px;

    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }

  .span-ellipsis {
    display: inline-block;
    width: 400px;

    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
</style>
```

