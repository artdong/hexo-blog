---
title: css常用的清除浮动方法有哪些？
date: 2019-07-03 17:30:11
categories: "css"
tags:
     - css
---

> ***

- 父级元素添加伪元素
```css
.clear-float:after {
    content: '';
    display: block;
    clear: both;
}
```

 ***


 <!-- more -->

- 在与浮动元素平级的最后面添加新元素 div.clear
```css
.clear {
    clear: both;
}
```
- 在父级元素添加样式 overflow: auto; 或者 overflow: hidden; 会存在兼容性问题。

