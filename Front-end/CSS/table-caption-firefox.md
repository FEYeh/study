# table的caption标签在火狐下的坑

```css
caption {
  height:20px;
  padding-top:10px;
}
```

chrome浏览器采用的是标准盒模型的计算方式，height仅代表内容的高度
firefox在计算高度时除了包括内容之外还包括了padding和border

可以使用CSS3的**box-sizing**属性来解决：

```css
caption {
  height:30px;
  padding-top:10px;
  box-sizing:border-box;
}
```