---
title: hello es6
layout: default
---

## hello es6

- ECMAScript简称就是ES,你可以把它看成是一套标准,JavaScript就是实施了这套标准的一门语言 现在主流浏览器使用的是ECMAScript5。

ECMAScript 6.0（以下简称ES6）是JavaScript语言的下一代标准，已经在2015年6月正式发布了。它的目标，是使得JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言。在项目中80%的时间用到的ES6语法只占其20%，所以我们暂时先集中精力把这20%学好，那就差不多够用了，剩下的可以看书或是查文档，现学现用。

### 1. Let + Const 块级作用域和常量

let和const的出现让 JS 有了块级作用域，还可以像强类型语言一样定义常量。由于之前没有块级作用域以及 var 关键字所带来的变量提升，经常给我们的开发带来一些莫名其妙的问题。

下面看两个简单的demo理解。

```

// demo 1
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}

// demo 2
const PI = 3.1415;
console.log(PI); // 3.1415

PI = 3;
console.log(PI); // TypeError: "PI" is read-only

if (true) {
  var a = "a"; // 期望a是某一个值
}
console.log(a);
if(true){
  let name = 'zfpx';
}
console.log(name);// ReferenceError: name is not defined

// 嵌套循环不会相互影响
for (let i = 0; i < 3; i++) {
  console.log("out", i);
  for (let i = 0; i < 2; i++) {
    console.log("in", i);
  }
}
//结果 out 0 in 0 in 1 out 1 in 0 in 1 out 2 in 0 in 1

重复定义会报错
if(true){
  let a = 1;
  let a = 2; //Identifier 'a' has already been declared
}

不存在变量的提升
console.log(i)
let i=10;
结果 i is not defined

// 闭包新写法
// 以前
;(function () {

})();

现在
{
}
```
