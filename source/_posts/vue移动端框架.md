---
title: vue移动端框架到底哪家强
date: 2017-03-06 16:30:11
categories: "vue"
tags:
     - vue

---

> ***


## Weex


2016年4月21日，阿里巴巴在Qcon大会上宣布跨平台移动开发工具Weex开放内测邀请。

Weex

是一套简单易用的跨平台开发方案，能以 web 的开发体验构建高性能、可扩展的 native 应用，为了做到这些，Weex 与 Vue

合作，使用 Vue 作为上层框架，并遵循 W3C 标准实现了统一的 JSEngine 和 DOM API，这样一来，你甚至可以使用其他框架驱动

Weex，打造三端一致的 native 应用。

Weex能够完美兼顾性能与动态性，支持iOS、安卓、YunOS及Web等多端部署。

 ***


  <!-- more -->


其工作原理

Weex

表面上是一个客户端技术，但实际上它串联起了从本地开发环境到云端部署和分发的整个链路。开发者首先可以在本地像撰写 web 页面一样撰写一个

app 的页面，然后编译成一段 JavaScript 代码，形成 Weex 的一个 JS bundle；在云端，开发者可以把生成的 JS

bundle 部署上去，然后通过网络请求或预下发的方式传递到用户的移动应用客户端；在移动应用客户端里，WeexSDK 会准备好一个

JavaScript 引擎，并且在用户打开一个 Weex 页面时执行相应的 JS bundle，并在执行过程中产生各种命令发送到 native

端进行的界面渲染或数据存储、网络通信、调用设备功能、用户交互响应等移动应用的场景实践；同时，如果用户没有安装移动应用，他仍然可以在浏览器里打开一个相同的

web 页面，这个页面是使用相同的页面源代码，通过浏览器里的 JavaScript 引擎运行起来的。


## Mint UI


基于 Vue.js 的移动端组件库

Mint UI 包含丰富的 CSS 和 JS 组件，能够满足日常的移动端开发需要。通过它，可以快速构建出风格统一的页面，提升开发效率。

真正意义上的按需加载组件。可以只加载声明过的组件及其样式文件，无需再纠结文件体积过大。

考虑到移动端的性能门槛，Mint UI 采用 CSS3 处理各种动效，避免浏览器进行不必要的重绘和重排，从而使用户获得流畅顺滑的体验。

依托 Vue.js 高效的组件化方案，Mint UI 做到了轻量化。即使全部引入，压缩后的文件体积也仅有 ~30kb (JS + CSS) gzip。


## vue-carbon


基于 vuejs 1.0 开发 material design 风格的移动端 WEB UI 库

使用文档地址 https://myronliu347.github.io/vue-carbon/book/v0.5.0/index.html


## Muse-UI


基于 Vue 2.0 和 Material Desigin 的 UI 组件库

特性

1.组件丰富

Muse UI 基本实现了 Material Design 设计规范类的所有组件，另外还开发许多的功能性的组件

2.可定制

Muse UI 使用less文件，所有的颜色都有一个变量维护，通过编写 less 文件完成自定义主题，另外组件内部也提供一些修改效果的参数

3.基于 Vue 2.0

Muse UI 基于 Vue2.0 开发，Vue2.0是当下最快的前端框架之一，小巧，api友好，可用于开发的复杂单页应用


## VUWE


vuwe是一款基于微信WeUI所开发的，专用于Vue2的组件库。

它与WeUI完全解耦。用户通过自定义WeUI的样式文件，可以方便地对VUWE实现定制化。


## vue-mobile


vue-mobile is an UI Framework build with Vue.js for SPA:

Full Page Structure - header, content, footer

Page transition support by vue-router

Bunch of Powerful Components, easy to use and extend

high performance CSS3 Animation

1px border for all components - as well as round border

Write with Vue - the most important


## vonic


一个基于 vue.js 和 ionic 样式的 UI 框架，用于快速构建移动端单页应用。

和 ionic 的关系：没有关系，只是在样式方面以 ionic 的 css 文件为基础（做了一些调整）


## vux


Vux（读音 [v'ju:z]，同views）是基于WeUI和Vue(2.x)开发的移动端UI组件库，主要服务于微信页面。

基于webpack+vue-loader+vux可以快速开发移动端页面，配合vux-loader方便你在WeUI的基础上定制需要的样式。

vux-loader保证了组件按需使用，因此不用担心最终打包了整个vux的组件库代码。

vux并不完全依赖于WeUI，但是尽量保持整体UI样式接近WeUI的设计规范。最初目标是创建一个易用，实用，美观的移动端UI组件库，现在离理想状态还有不少距离，因此需要大家及时反馈问题及贡献代码。

即使你不使用vux的代码, 但能从源码得到一些参考那么也是件让人高兴的事情。

