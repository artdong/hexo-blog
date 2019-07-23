---
title: promise和setTimeout执行顺序是怎样的？
date: 2019-07-05 17:30:11
categories: "js"
tags:
     - js
---

> ***

写出下列程序运行结果并做出解释：

```javascript
setTimeout(function(){
    console.log(1);
},0); 

new Promise(function(resolve) { 
    console.log(2) 
    for(let i=0; i<10000 ; i++ ) { 
        i==9999 && resolve(); 
    } 
    console.log(3) 
}).then(function(){ 
    console.log(4) 
}); 
console.log(5); 
```

 ***


 <!-- more -->

这个就涉及到**事件循环（Event Loop）**
> JS运行时，对代码执行顺序的一个算法（任务调度算法）

JS 分类：同步任务和异步任务
JS 的执行机制：
- 首先判断JS代码是同步还是异步，同步就进入主线程，异步就进入 event table
- 异步任务在 event table 中注册函数，当满足触发条件后，被推入event queue
- 同步任务进入主线程后一直执行，直到主线程空闲时，才回去 event queue 中查看是否有可执行的异步任务，如果有就推入主线程

event loop 里有维护两个不同的异步任务队列
- macro Tasks（宏任务）：script（整体代码）, setTimeout, setInterval, setImmediate, I/O, UI rendering
- micro Tasks（微任务）：process.nextTick, Promise（浏览器实现的原生Promise）, Object.observe,  MutationObserver, MessageChannel

每次执行一段代码（一个script标签）都是一个 macroTask
执行流程：
- event loop 开始
- 从macro Tasks 队列抽取一个任务，执行
- micro Tasks 清空队列执行，若有任务不可执行，推入下一轮 micro Tasks
- 结束 event loop

浏览器执行代码的过程如下整个流程
![image](https://user-images.githubusercontent.com/18480722/60965123-9f2c5900-a347-11e9-81d5-e93ec6c60840.png)

那么回到题目上去，就是
```js
setTimeout(function(){
    console.log(1);    // 1-放入宏任务队列，7-执行下一轮事件循环，宏任务输出1
},0); 

new Promise(function(resolve) { 
    console.log(2);    // 2-同步输出 2
    for(let i=0; i<10000 ; i++ ) { 
        i==9999 && resolve(); 
    } 
    console.log(3);    // 4-同步输出 3
}).then(function(){ 
    console.log(4);    // 3-放入微任务队列，6-回到微任务队列，执行剩余的微任务，输出4
}); 
console.log(5);    // 5-同步输出 5
```