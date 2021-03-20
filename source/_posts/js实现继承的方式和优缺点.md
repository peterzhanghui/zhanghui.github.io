---
title: js实现继承的方式和优缺点
categories: 前端开发
tags: js
date: 2021-03-20 21:33:25
---

## 一、 原型继承

实现的核心代码：

```
Child.prototype = new Parent();

var child1 = new Child();
```

缺点：1、引用类型的属性被所有实例共享 2、创建实例时不能想 parent 传参

## 二、构造函数继承

```
function Parent () {
    this.names = ['kevin', 'daisy'];
}

function Child () {
    Parent.call(this);
}

var child1 = new Child();

```

优点：

1.避免了引用类型的属性被所有实例共享

2.可以在 Child 中向 Parent 传参

缺点：

方法都在构造函数中定义，每次创建实例都会创建一遍方法。

## 三、组合继承

结合原型继承和构造函数继承

```
function Parent (name) {
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}

Parent.prototype.getName = function () {
    console.log(this.name)
}

function Child (name, age) {

    Parent.call(this, name);

    this.age = age;

}

Child.prototype = new Parent();
Child.prototype.constructor = Child;

var child1 = new Child('kevin', '18');
```

缺点：会调用两次父构造函数

## 四、寄生式继承

```
function createObj (o) {
    var clone = Object.create(o);
    clone.sayName = function () {
        console.log('hi');
    }
    return clone;
}

```

缺点：跟借用构造函数模式一样，每次创建对象都会创建一遍方法。

## 五、寄生组合式继承

```
function Parent (name) {
    this.name = name;
    this.colors = ['red', 'blue', 'green'];
}

Parent.prototype.getName = function () {
    console.log(this.name)
}

function Child (name, age) {
    Parent.call(this, name);
    this.age = age;
}

// 关键的三步
var F = function () {};

F.prototype = Parent.prototype;

Child.prototype = new F();


var child1 = new Child('kevin', '18');

```

最佳的继承实现 能够正常使用 instanceof 和 isPrototypeOf

## 总结：

ES6 中的 extends 继承就是类似寄生组合式继承的实现方式
