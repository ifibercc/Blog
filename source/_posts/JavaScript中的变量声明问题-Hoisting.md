title: JavaScript中的变量声明提升问题 - Hoisting
date: 2016-08-09 17:23:11
tags:
- tech
- JavaScript
---
## 1. 变量声明提升
> hoisting  英['hɔɪstɪŋ]  美['hɔɪstɪŋ]  
> n.	起重，提升  
> v.	把…吊起，升起( hoist的现在分词 )

先来看一个栗子
``` javascript
var cc = 'hello';
function foo(){
    console.log(cc);
    var cc = 'world';
    console.log(cc);
}
foo();
console.log(cc);
```
这里将会输出 undefined、'world'、'hello'  
此处主要有两个知识点：
- 作用域
- 变量声明提升

JavaScript是一门解释性语言，当代码在解释器（如Chrome的V8引擎）环境中执行时，会有一个预解析的过程，此时会将变量声明和函数声明提升至当前作用域的最前方，这个行为被称为声明提升（Hoisting）

再来看上面的例子，此代码有两层作用域，全局作用域和函数foo作用域，而foo中的变量声明在预解析的过程中会被提升至函数作用域的前方，于是代码就会变成这样：
``` javascript
var cc = 'hello';
function foo(){
    var cc;
    console.log(cc);
    cc = 'world';
    console.log(cc);
}
foo();
console.log(cc);
```
当执行到第一个log时，变量cc只是进行了声明，并未赋值，所以打印出的是`undefined`

## 2. 函数声明提升

函数的声明有两种方式：函数声明和函数表达式
``` javascript
// 函数声明
function foo(a, b) {
    return a + b;
}

// 函数表达式
var foo = function(a, b) {
    return a + b;
}
```
> 解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问）；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。

当然，也可以函数声明和函数表达式同时使用,如`var a = function b(){}`,其结果是只具有函数表达式的作用，b会被自动忽略，所以只会发生变量提升效果。
