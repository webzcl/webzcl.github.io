---
title : Class, extends, super 类的支持
layout : default
---

## Class, extends, super 类的支持

回想之前，如果我们需要模拟一个js的类，一般会采用构造函数加原型的方式。

```

function Point(x,y){
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
}
var point = new Point(6,3);
console.log(point.toString());//(6,3)
```
ES6中添加了对类的支持，引入了class关键字（其实class在JavaScript中一直是保留字，目的就是考虑到可能在以后的新版本中会用到，现在终于派上用场了）。

JS本身就是面向对象的，ES6中提供的类实际上只是JS原型模式的包装。现在提供原生的class支持后，对象的创建，继承更加直观了，并且父类方法的调用，实例化，静态方法和构造函数等概念都更加形象化。

下面代码展示了类在ES6中的使用。

```

//类的定义
class Animal {
    //ES6中新型构造器
    constructor(name) {
        this.name = name;
    }
    //实例方法
    sayName() {
        console.log('My name is '+this.name);
    }
}
//类的继承
class Programmer extends Animal {
  constructor(name) {
      //直接调用父类构造器进行初始化
    super(name);
  }
  program() {
    console.log("I'm coding...");
  }
}

//测试我们的类
var animal=new Animal('dummy'),
zf=new Programmer('zf');

animal.sayName();//输出 ‘My name is dummy’
zf.sayName();//输出 ‘My name is zf’
zf.program();//输出 ‘I'm coding...’
//定义“类”的方法的时候，前面不需要加上function这个关键字，直接把函数定义放进去了就可以了。另外，方法之间不需要逗号分隔，加了会报错。
```
