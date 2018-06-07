---
title: webpack loader全家桶
date: 2017-03-06 16:30:11
categories: "webpack"
tags:
     - webpack

---

> ***


webpack的loaders是一大特色，也是很重要的一部分。下面介绍一些常用的loader。

 ***


  <!-- more -->


## loaders之 js处理


babel-loader

jsx-loader


npm install --save-dev babel-core babel-preset-es2015 babel-loader jsx-loader


## loaders之预处理


css-loader 处理css中路径引用等问题

style-loader 动态把样式写入css

sass-loader scss编译器

less-loader less编译器

postcss-loader scss再处理


npm install --save -dev css-loader style-loader sass-loader less-loader postcss-loader


## loaders之 json处理


json-loader


npm install --save-dev json-loader


## loaders之 图片处理


url-loader


npm install --save-dev url-loader


## loaders之 文件处理


file-loader


npm install --save-dev file-loader


## loaders之 html处理


raw-loader


npm install --save-dev raw-loader

