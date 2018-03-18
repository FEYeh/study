# CSS的浮动
为什么要清除css的浮动？
css布局中，DIV一般都是嵌套的，如下面这段代码
```html
<head>
<style type="text/css">
  .layout { background:#DDD; }
  .left { width:50%; height:200px; background:#EEE; line-height:200px; }
  .right { width:50%; height:100px; background:#EEE; line-height:100px; }
</style>
</head>
<body>
  <div class="layout">
    <div class="left">left</div>
    <div class="right">right</div>
  </div>
</body>
```
显示的效果就是外面背景为#DDD的层包含了里面背景为#EEE的两个层。
如果想让left在左边，right在右边呢，那就用到了float，给left和right分别加上float:left和float:right

但是这样之后就会出现一个问题，外面layout的背景消失了，是因为这时它的高度为0了，那么这时就要清除浮动，清除浮动一般有三种方法，

### 第一种
使用空标签，比如<p>标签，然后再为<p>标签写相应的css代码：clear:both.
```html
<head>
<style type="text/css">
  .layout { background:#DDD; }
  .left { width:50%; height:200px; background:#EEE; line-height:200px; }
  .right { width:50%; height:100px; background:#EEE; line-height:100px; }
  .clear { clear:both; }
</style>
</head>
<body>
  <div class="layout">
  <div class="left">left</div>
  <div class="right">right</div>
  <p class="clear"></p>
  </div>
</body>
```
### 第二种
使用overflow属性，这种方法是在需要清除浮动的最外层div的css中定义属性overflow:auto; zoom:1，如在#laytout中加上这两个属性即可实现效果，
```css
.layout { background:#CCC; overflow:auto; zoom:1 }
```
### 第三种
使用after伪对象，after伪对象仅有非IE浏览器支持(IE8以上)，所以对于IE来说还要加上zoom:1这个属性，如
```html
<head>
<style type="text/css">
  .layout { background:#DDD; zoom:1; }
  .layout:after { display:block; clear:both; content:""; visibility:hidden; height:0; }
  .left { float；left; width:20%; height:200px; background:#EEE; line-height:200px;}
  .right { float:right; width:30%; height:80px; background:#EEE; line-height:80px; }
</style>
</head>
<body>
  <div class="layout">
    <div class="left">left</div>
    <div class="right">right</div>
  </div>
</body>
```