# CSS打印采坑

### 指定打印时的样式

例如使用**@media print**来隐藏菜单和设置标题大小

```css
@media print {
  .menu {
    display: none;
  }
  h1 {
    font-size: 16px;
  }
}
```

### 防止内容被隔成两页

```css
@media print {
  ...
  /* 在所有p标签后面设置换页符，使后面的内容移到下一页 */
  p {
    page-break-after: always;
  }
  /* 禁止tr内部换页 */
  tr {
    page-break-inside: avoid;
  }
  /* 禁止table跨页 */
  .table {
    page-break-before: left;
  }
  /* 如果内容有滑动，需要设置overflow-y为visible */
  .content {
    overflow-y: visible;
  }
}

```