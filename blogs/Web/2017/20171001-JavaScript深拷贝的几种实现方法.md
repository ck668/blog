---
title: JavaScript深拷贝的几种实现方法
date: 2017-10-01
tags:
 - JavaScript
categories:
 -  JavaScript
---

# 深拷贝的几种实现方法

## 使用JSON.stringify 和 JSON.parses

 - 用 JSON.stringify 把对象转换成字符串，再用 JSON.parse 把字符串转换成新的对象。如果对象中包含 function 或 RegExp 这些就不能用这种方法了。

 ```js
  const source = { x: [1, 2, 3], y: {a: 1, b: 2, c: 3}};
  function deepClone(obj) {
    let _obj = JSON.stringify(obj);
    let objClone = JSON.parse(_obj);
    return objClone;
  }
  const objClone = _deepClone(source);
 ```

## 使用Object.assign()

  - 当对象中只有一级属性,没有二级属性的时候,此方法为深拷贝，但是当属性值为对象或其它引用类型时,此方法在二级属性以后就是浅拷贝。

  ```js
    const source = { x: 4, y: 5, z: z => z};
    const objClone = Object.assign({}, source);
  ```

## 使用jQuery的extend

  ```js
    const $ = require('jquery');
    const source = { x: [1, 2, 3], y: {a: 1, b: 2, c: 3}, z: z => z};
    const objClone = $.extend(true, {}, source);
  ```

## 使用lodash.cloneDeep()

  ```js
    const _ = require('lodash');
    const source = { x: [1, 2, 3], y: {a: 1, b: 2, c: 3}, z: z => z};
    const objClone = _.cloneDeep(obj);
  ```

## 使用递归的方式

  ```js
    const source = { x: [1, 2, 3], y: {a: [1, 2, 3], b : [4, 5, 6], c: 7}, z: z => z};
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
    const objClone = _deepClone(source);
  ```