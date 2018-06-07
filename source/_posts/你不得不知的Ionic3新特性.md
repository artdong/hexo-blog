---
title: 你不得不知的Ionic3新特性
date: 2017-03-06 16:30:11
categories: "ionic3"
tags:
     - ionic
     - ionic3
---

> ***

Ionic3新特性：


## Angular 4.0


新的版本下，改进 AOT 编译器，分离 animations 包，缩小生成后的代码量，运行更快，改进ngIf 和ngFor 等具体内容可以访问http://angularjs.blogspot.sg/2017/03/angular-400-now-available.html来查看。


## typescript 2.1, 2.2的支持


这一次的更新将提升typescript应用构建和类型检查的速度并且引入了对mix-in的支持等具体可以访问https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-2.html来查看。


 ***


 <!-- more -->


## @IonicPage装饰器


ionic2中导航器不是基于url的，如果想使用url访问就要通过DeepLinker来实现，这是非常麻烦的，而在新版本我们可以通过@IonicPage装饰器来实现。并且可以更轻松的在项目中设置延迟加载，设置延迟加载页面的优先级，并为每个页面自定义配置。


## 懒加载


Ionic3.0版本开始，支持了延迟加载，我们可以将某些模块设置为延时加载，只有用户打开相关的页面的时候，这个模块所在的js才会被下载，这样能减少用户初次下载的文件的大小。

总的来说，升级Ionic3将使我们的项目变得更小，更快，而更吸引我们的则是懒加载，不仅仅是加快了app首次的启动时间，更多的是配合上@IonicPage可以非常方便部署web版本，让每次进入不用去请求庞大的js文件，做到首屏的快速加载，write once run anywhere，这些就是我们需要升级Ionic3的原因。


那么，问题来了，怎样升级到Ionic3呢？

首先访问https://github.com/ionic-team/ionic2-app-base/复制package.json的dependencies和devDependencies到自己的项目中后删除掉原本的node_modules文件夹，运行npm install重新下载依赖。

将BrowserModule加入你的app/app.module.ts
import { BrowserModule } from '@angular/platform-browser';
在app.module.ts中将BrowserModule添加进imports中。


``` javascript
imports: [   BrowserModule,   IonicModule.forRoot(MyApp) ],
```


由于ionic3将ionic-native拆开成个各种小的包@ionic-native/*,splash-screen，status-bar等之前ionic-native中的模块都需要重新引入具体可以参照http://ionicframework.com/docs/native/来对号入座。

最后打开cmd控制台运行ionic serve

开始享受ionic3带来的改变吧！