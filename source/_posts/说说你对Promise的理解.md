---
title: 说说你对Promise的理解？
date: 2019-07-06 17:30:11
categories: "js"
tags:
     - js
---

> ***

## Promise 核心

- Promise 概括来说是对异步的执行结果的描述对象。（这句话的理解很重要）
- Promise 规范中规定了，promise 的状态只有3种：
    - pending
    - fulfilled
    - rejected                          
    Promise 的状态一旦改变则不会再改变。
- Promise 规范中还规定了 Promise 中必须有 then 方法，这个方法也是实现异步的链式操作的基本。

 ***


 <!-- more -->

## ES6 Promise细节

- Promise 构造器中必须传入函数，否则会抛出错误。(没有执行器还怎么做异步操作。。。)
- Promise.prototype上的 catch(onrejected) 方法是 then(null,onrejected) 的别名,并且会处理链之前的任何的reject。
- Promise.prototype 上的 then和 catch 方法总会返回一个全新的 Promise 对象。
- 如果传入构造器的函数中抛出了错误,该 promise 对象的[[PromiseStatus]]会赋值为 rejected，并且[[PromiseValue]]赋值为 Error 对象。
- then 中的回调如果抛出错误，返回的 promise 对象的[[PromiseStatus]]会赋值为 rejected，并且[[PromiseValue]]赋值为 Error 对象。
- then 中的回调返回值会影响 then 返回的 promise 对象。

## Promise优点

- Promise最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了。

{% img /img/promise.png %}

- 解决回调地狱（Callback Hell）问题 

Promise还可以做更多的事情，比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。

要串行执行这样的异步任务，不用Promise需要写一层一层的嵌套代码。有了Promise，我们只需要简单地写：

```
job1.then(job2).then(job3).catch(handleError);
```

> 其中，job1、job2和job3都是Promise对象。

- Promise.all()并行执行异步任务

- Promise.race()获得先返回的结果即可

>eg.同时向两个URL读取用户的个人信息，只需要获得先返回的结果即可。

## Promise如何解决这两个问题

- 解决可读性的问题

这一点不用多说，用过Promise的人很容易明白。Promise的应用相当于给了你一张可以把解题思路清晰记录下来的草稿纸，你不在需要用脑子去记忆执行顺序。

- 解决信任问题

Promise并没有取消控制反转，而是把反转出去的控制再反转一次，也就是反转了控制反转。

这种机制有点像事件的触发。它与普通的回调的方式的区别在于，普通的方式，回调成功之后的操作直接写在了回调函数里面，而这些操作的调用由第三方控制。在Promise的方式中，回调只负责成功之后的通知，而回调成功之后的操作放在了then的回调里面，由Promise精确控制。

Promise有这些特征：只能决议一次，决议值只能有一个，决议之后无法改变。任何then中的回调也只会被调用一次。Promise的特征保证了Promise可以解决信任问题。

对于回调过早的问题，由于Promise只能是异步的，所以不会出现异步的同步调用。即便是在决议之前的错误，也是异步的，并不是会产生同步（调用过早）的困扰。
```
let a = new Promise((resolve, reject) => {
  let b = 1 + c;  // ReferenceError: c is not defined，错误会在下面的a打印出来之后报出。
  resolve(true);
})
console.log(1, a);
a.then(res => {
  console.log(2, res);
})
.catch(err => {
  console.log(err);
})
```
对于回调过晚或没有调用的问题，Promise本身不会回调过晚，只要决议了，它就会按照规定运行。至于服务器或者网络的问题，并不是Promise能解决的，一般这种情况会使用Promise的竞态APIPromise.race加一个超时的时间：
```
function timeoutPromise(delay) {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      reject("Timeout!");
    }, delay);
  });
}

Promise.race([doSomething(), timeoutPromise(3000)])
.then(...)
.catch(...);
```
对于回调次数太少或太多的问题，由于Promise只能被决议一次，且决议之后无法改变，所以，即便是多次回调，也不会影响结果，决议之后的调用都会被忽略。