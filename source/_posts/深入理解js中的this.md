---
title: 深入理解普通函数中的this及ES6箭头函数的this
date: 2018-06-06 11:11:11
categories: "js"
tags:
     - js
     - this
---

> ***

## 普通函数中的this:

1. this总是代表它的直接调用者(js的this是执行上下文), 例如 obj.func ,那么func中的this就是obj

2. 在默认情况(非严格模式下,未使用 'use strict'),没找到直接调用者,则this指的是 window (约定俗成)

3. 在严格模式下,没有直接调用者的函数中的this是 undefined

4. 使用call,apply,bind(ES5新增)绑定的,this指的是绑定的对象

## 箭头函数中的this

箭头函数没有自己的this, 它的this是继承而来; 默认指向在定义它时所处的对象(宿主对象),而不是执行时的对象, 定义它的时候,可能环境是window; 箭头函数可以方便地让我们在 setTimeout ,setInterval中方便的使用this
 
下面通过一些例子来研究一下 this的一些使用场景

 ***

 <!-- more -->

## 首先了解一下作用域链:

当在函数中使用一个变量的时候,首先在本函数内部查找该变量,如果找不到则找其父级函数,

最后直到window,全局变量默认挂载在window对象下

1. 全局变量默认挂载在window对象下

2. 在普通函数中,this指向它的直接调用者;如果找不到直接调用者,则是window

```javascript
<script>
  function test() {
    console.log(this);
  }
  test();
</script>
```
结果是: window 

原因: test()是一个全局函数,也就是说是挂在window对象下的,所以test()等价于 window.test() ,所以此时的this是window

```javascript
<script>
   var obj = {
       say: function () {
         setTimeout(function () {
           console.log(this)
         });
       }
   }
   obj.say();
</script>
```
结果是: window

匿名函数,定时器中的函数,由于没有默认的宿主对象,所以默认this指向window

3.在严格模式下的this

```javascript
<script>
  function test() {
    'use strict';
    console.log(this);
  }
test();
</script>
```
结果是: undefined

4.箭头函数中的 this

```javascript
<script>
var obj = {
  say: function () {
    setTimeout(() => {
      console.log(this)
    });
  }
}
obj.say(); // obj
</script>
```
此时的 this继承自obj, 指的是定义它的对象obj, 而不是 window!

示例(多层嵌套的箭头函数):

```javascript
<script>
var obj = {
  say: function () {
    var f1 = () => {
      console.log(this); // obj
      setTimeout(() => {
        console.log(this); // obj
      })
    }
    f1();
  }
}
obj.say()
</script>
```
因为f1定义时所处的函数 中的 this是指的 obj, setTimeout中的箭头函数this继承自f1, 所以不管有多层嵌套,都是 obj

示例(复杂情况: 普通函数和箭头函数混杂嵌套)

```javascript
<script>
var obj = {
  say: function () {
    var f1 = function () {
      console.log(this); // window, f1调用时,没有宿主对象,默认是window
      setTimeout(() => {
        console.log(this); // window
      })
    };
    f1();
  }
}
obj.say()
</script>
```
结果: 都是 window,因为 箭头函数在定义的时候它所处的环境相当于是window, 所以在箭头函数内部的this函数window

示例(严格模式下的混杂嵌套)

```javascript
<script>
var obj = {
  say: function () {
    'use strict';
    var f1 = function () {
      console.log(this); // undefined
      setTimeout(() => {
        console.log(this); // undefined
      })
    };
    f1();
  }
}
obj.say()
</script>
```
结果都是undefined

说明: 严格模式下,没有宿主调用的函数中的this是undefined!!!所以箭头函数中的也是undefined!


* 总结:

使用箭头函数,可以让我们解决一些在匿名函数中this指向不正确的问题; 但是要注意在和普通函数混合的时候,this的指向可能是window !