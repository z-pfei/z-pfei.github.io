---
title: JS-delete
date: 2016-08-02 17:48:25
tags: js
comments: true
categories: js
---
#### 学习js中的delete操作符

<!-- more -->

#### 1	基础语法
###### 1.1表达式
```javascript
delete object.property;
```
###### 1.2返回值

如果一个属性被删除了，或者对象中的这个属性不存在，返回true；如果不能删除该属性则返回false。
___
#### 2 可删除&不可删除
###### 2.1可删除
* 隐式声明的属性
* 对象的属性
* 在eval代码中声明的变量和函数

###### 2.2不可删除
* 全局或在函数中显示声明的变量和函数
* 函数参数
* 原型中定义的属性和对象自带的属性
* eval特例，在eval代码中的函数内部声明的变量和函数
___
#### 3 原因
```javascript
// 尝试删除一个变量
var x = 1;
delete x;
x;	// 1

// 尝试删除一个对象的属性
var y = {};
y.o = 3;
delete y.o;
y.o;	// undefined
```
用两个例子验证第二部分中的结论，确实有的可以删除有的不可以删除，为什么。经过学习知道，原来每个属性还拥有内部属性，而有一个属性`DontDelete`控制着这个属性可不可以被删除。

内部属性是在属性生成时确定的，以后的赋值不会改变已有内部属性。

因此很好理解为什么声明的变量不能删除，未声明赋值的变量可删除。声明的变量带有`DontDelete`内部属性，而未声明赋值的变量在生成时没有生成内部属性，可以被删除。

举一个栗子 ![lizi](http://ob7xfgq70.bkt.clouddn.com/lizi.jpg)
```javascript
// 删除声明的变量
var a = 1;
delete a; // false
a; // 1

//删除未声明的变量
x = 10;
delete x; //true
x; // undefined
```
还有一个栗子解释一下原型中定义的属性和对象自带的属性不可删除
```javascript
// 删除原型中定义的属性
function Foo () { this.x = 1; }
Foo.prototype.x = 2;
var a = new Foo();
a.x; // 1
delete a.x; // true
a.x; // 2
delete a.x; // true 即使再删也不能删除原型中定义的x
a.x // 2

//删除对象自带的属性
var x = [1,2,3];
delete x.length; // false
x.length; // 3
```
___
扩展阅读：[本文学习链接](http://bubkoo.com/2014/01/23/deep-in-delete)