---
title: 两种方法轻松搞定NodeJS实时编译，动态调试
date: 2017-03-06 16:30:11
categories: "nodejs"
tags:
     - node

---

> ***


## Node.js开发中遇到这样的问题


总是重新读取并解析脚本(如果没有专门的优化配置)。Node.js的这种设计虽然有利于提高性能，却不利于开发调试，因为我们在开发过程中总是希望修改后立即看到效果，而不是每次都要终止进程并重启。

这时若你修改了js文件，或是调试功能，或是增加功能。这时需要重新发布该服务，每次修改都需要执行以下两步：


``` bash
control+c
node server.js
```


很不爽有木有！因此有人开发了一个自动发布（热发布）的工具，你只需要在修改文件后保存，它就能自动替你发布，这就是所谓的热部署。就像tomcat或websphere等一些主流的web应用服务器那样保存即热部署。下面将介绍两个NodeJS中的开源热部署工具。


 ***


  <!-- more -->


## (1)supervisor


supervisor 可以帮助你实现这个功能，它会监视你对代码的改动，并自动重启 Node.js。使用方法很简单，首先使用 npm 安装 supervisor：

``` bash
$ npm install -g supervisor
```

如果你使用的是 Linux 或 Mac，直接键入上面的命令很可能会有权限错误。原因是 npm需要把 supervisor 安装到系统目录，需要管理员授权，可以使用 sudo npm install -g supervisor 命令来安装。

接下来，使用 supervisor 命令启动 app.js：

``` bash
$ supervisor app.js
```

命令行窗口会显示启动成功信息，即开启了代码监听。

当代码被改动时，运行的脚本会被终止，然后重新启动。

supervisor 这个小工具可以解决开发中的调试问题。


github地址：https://github.com/isaacs/node-supervisor


## (2)hotnode


首先需要安装，打开NodeJS命令行工具，输入sudo npm -g install hotcode进行全局安装

安装成功后，可以随时查看它的版本号，在命令行输入：hotcode -v

使用很简单，执行命令:hotcode server.js。

每次修改都会有一条日志打印出来。


github地址：https://github.com/saschagehlich/hotnode


## nodejs + express入门示例


nodejs + express入门示例： https://github.com/artdong/node-server

