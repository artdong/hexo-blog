---
title: 认识Ionic 2
date: 2017-03-06 16:30:11
categories: "ionic2"
tags:
     - ionic
     - ionic2
---

> ***

## Ionic 2 介绍


Ionic 2专注于以标准的HTML、CSS和JavaScript来构建移动站点，并可以通过Cordova打包成移动 App，只需编写一次代码，就可以分别部署到iOS、Android等多种移动平台上。这项技术已经帮助很多开发者创建了很多漂亮的 App。现在Ionic 2已经发布了第二代版本，使移动开发更容易、更有效率。

Ionic 2与一代相比有较大的变化，基于最新的Angular 2，使用TypeScript进行开发，如果您没有接触过 AngularJS或Ionic1.x，完全不用担心，直接从Ionic 2` 开始学习即可。

在使用Ionic 2之前，您应该具备HTML、CSS、JavaScript基础。
 ***

 <!-- more -->


## 2. Ionic2 的优势与不足


Ionic 2借助Angular 2的革命性改进，与 1.x 版本相比具有以下优势：


### 更快的性能


Angular 1的检测机制在某些场景下会导致性能降低，由于最初的架构限制已经很难进行提升了。Angular 2有效避免了这种情况。数据显示Angular 2比Angular 1快5到10倍。

官方提供了一个动画来展示Ionic 2的性能提升：

因图片较大，请点击查看:

http://blog.ionic.io/wp-content/uploads/2016/09/beta11-vs-beta12.gif


### 更清晰的项目结构


Angualr 2应用是模块化的，因此Ionic 2的项目结构比Ionic 1更为清晰，如：

-home.page

--home.page.ts

--home.page.html

--home.page.scss

-about.page

--about.page.ts

--about.page.html

--about.page.scss

每个页面的代码、模板、样式都放在一块，意义非常清晰。


### 更强大的CLI


Ionic CLI提供了更强大的功能，如添加一个页面，可以使用以下命令：

ionic g page NewPage

Ionic CLI会生成以下的文件，并且文件中已经生成了基本的代码：

-new-page

--new-page.ts

--new-page.html

--new-page.scss

Ionic CLI可以生成pages,providers,tabs,pipes,components，directives等。


### 更友好的页面导航


Ionic 2 的导航方式相比一代有了巨大的改进，完全进行了重写。在 Ionic 1.x 中，需要配置路由：

.config(function($stateProvider, $urlRouterProvider){     $stateProvider         .state('home', {             url:'/',             templateUrl:'templates/home.html',             controller:'HomeCtrl'})         .state('main', {             url:'/main',             templateUrl:'templates/main.html',             controller:'MainCtrl'});     $urlRouterProvider.otherwise("/"); });

Ionic 2抛弃了这种繁琐的方式，更类似原生的开发体验，一行代码即可搞定：

this.nav.push(SecondPage);

使用全新的NavController组件，导航栈的操作方式更加方便，实现前进、后退等功能就像操作数组那么简单。


### 更强大的模板语法


Angular 2的模板语法刚接触时可能会觉得有点难以上手，但熟悉之后就能够更加灵活的控制单向绑定、双向绑定、事件绑定等各种功能。

更高效的开发体验

基于TypeScript，使用Ionic 2拥有更好的开发体验，支持类、模块、接口、lambda表达式等新的特性，大大改善了JavaScript的开发体验。当然你需要一个好的编辑器，如VS Code。

强大的智能感知，自定义的类都可以哦，真的有点开发强类型语言的感觉啊 8-)

当然，因为最终还是要依靠Cordova进行打包，因此不可避免的会遇到所有Cordova类跨平台应用面临的问题，在某些性能较差的移动设备上渲染速度较慢。Ionic 2已经明确提出不支持低版本Android设备，并且在Angular 2正式版发布以后，支持AoT编译也会在一定程度上优化 App 性能。


## 3. Ionic 2 开发基础


在开始学习ionic2之前最好能熟悉HTML、CSS及JavaScript，初步了解TypeScript、Angular 2的基础知识，如果了解不深入也没关系，Ionic 2已经为我们隐藏了很多底层的细节，封装的方法意义都很清晰，我们会在实践中，逐步掌握那些奇怪的标签。

Ionic 2基于Angular 2进行构建，这是对于原始版本完全的重写。一些语法和架构都有了变化，开发者需要注意。在Ionic 1中使用的views和controllers等，在Ionic 2中都被合并到了一块。

TypeScript是由微软开发的开源语言，是JavaScript的超集，兼容JavaScript。提供了静态类型、Lambda表达式、接口等先进的概念，可以说是面向对象的JavaScript。2012年10月第一次发行公开版本，目前已经发布了2.0正式版。开发者是大名鼎鼎的Delphi和.NET之父：安德斯·海尔斯(Anders Hejlsberg)。上次大神来华时有幸见过一次，非常和蔼可亲。

AngularJS是由谷歌推出的一款优秀的前端框架，被用于谷歌公司的多款产品中。AngularJS提供了MVVM、模块化、双向绑定、语义化标签、依赖注入等先进思想。AngularJS 诞生于2009年，但是1.x版本在性能上存在诸多问题，谷歌继续发布了颠覆性的Angular 2，目前已经发布了2.0正式版。Angular 2的设计思路与1.x版本是有较大区别的，采用了TypeScript进行开发，因此如果之前没有接触过Angular 1.x的话，可以完全从Angular 2开始。