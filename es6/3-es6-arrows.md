---
title : Arrows 箭头函数
layout : default
---

## Arrows 箭头函数

- 箭头函数简化了函数的的定义方式，一般以 "=>" 操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。
- 箭头函数根本没有自己的this，导致内部的this就是外层代码块的this。正是因为它没有this，所以也就不能用作构造函数，从而避免了this指向的问题。

请看下面的例子。

```
//以前
let [a,b]=[1,2];
function add(a,b) {
  console.log(a+b);
}
add(a,b);
//现在
let add = (a,b) => console.log(a+b);
//forEach
var numbers = [1, 2, 3, 4];
numbers.forEach(function(item, index, array) {
  console.log(item + "\t" + index + "\t" + array);
});
var array = [1, 2, 3];
//传统写法
array.forEach(function(v, i, a) {
    console.log(v);
});
//ES6
array.forEach(v = > console.log(v));
输入参数如果多于一个要用()包起来，函数体如果有多条语句需要用{}包起来
```
