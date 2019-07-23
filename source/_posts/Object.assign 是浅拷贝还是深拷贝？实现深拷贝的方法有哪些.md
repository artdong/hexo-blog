---
title: Object.assign 是浅拷贝还是深拷贝？实现深拷贝的方法有哪些？
date: 2019-07-04 17:30:11
categories: "js"
tags:
     - js
---

> ***

>  Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

- 如果目标对象中的属性具有相同的键，则属性将被源对象中的属性覆盖。后面的源对象的属性将类似地覆盖前面的源对象的属性。

- Object.assign 方法只会拷贝源对象自身的并且可枚举的属性到目标对象。该方法使用源对象的[[Get]]和目标对象的[[Set]]，所以它会调用相关 getter 和 setter。因此，它分配属性，而不仅仅是复制或定义新的属性。如果合并源包含getter，这可能使其不适合将新属性合并到原型中。为了将属性定义（包括其可枚举性）复制到原型，应使用Object.getOwnPropertyDescriptor()和Object.defineProperty() 。

- String类型和 Symbol 类型的属性都会被拷贝。

- 在出现错误的情况下，例如，如果属性不可写，会引发TypeError，如果在引发错误之前添加了任何属性，则可以更改target对象。

- Object.assign 不会在那些source对象值为 `null `或 `undefined` 的时候抛出错误。

- 针对**深拷贝**，需要使用其他办法，因为 Object.assign()拷贝的是属性值。假如源对象的属性值是一个对象的引用，那么它也只指向那个引用。也就是说，如果对象的属性值为简单类型（如string， number），通过Object.assign({},srcObj);得到的新对象为`深拷贝`；如果属性值为对象或其它引用类型，那对于这个对象而言其实是`浅拷贝`的。

 ***


 <!-- more -->

## 深拷贝的几种实现方法

### JSON.stringify 和 JSON.parse

>用 JSON.stringify 把对象转换成字符串，再用 JSON.parse 把字符串转换成新的对象。

可以转成 JSON 格式的对象才能使用这种方法，如果对象中包含 function 或 RegExp 这些就不能用这种方法了。

```
//通过js的内置对象JSON来进行数组对象的深拷贝
function deepClone(obj) {
  let _obj = JSON.stringify(obj);
  let objClone = JSON.parse(_obj);
  return objClone;
}
```

### Object.assign()拷贝

当对象中只有一级属性，没有二级属性的时候，此方法为深拷贝，但是对象中有对象的时候，此方法，在二级属性以后就是浅拷贝。

### 通过jQuery的extend方法实现深拷贝

```
let $ = require('jquery');
let obj1 = {
   a: 1,
   b: {
     f: {
       g: 1
     }
   },
   c: [1, 2, 3]
};
let obj2 = $.extend(true, {}, obj1);
```

### lodash.cloneDeep()实现深拷贝

```
let _ = require('lodash');
let obj1 = {
    a: 1,
    b: { f: { g: 1 } },
    c: [1, 2, 3]
};
let obj2 = _.cloneDeep(obj1);
```

### 使用递归的方式实现深拷贝

```
function _deepClone(source) {
  let target;
  if (typeof source === 'object') {
    target = Array.isArray(source) ? [] : {}
    for (let key in source) {
      if (source.hasOwnProperty(key)) {
        if (typeof source[key] !== 'object') {
          target[key] = source[key]
        } else {
          target[key] = _deepClone(source[key])
        }
      }
    }
  } else {
    target = source
  }
  return target
}
```