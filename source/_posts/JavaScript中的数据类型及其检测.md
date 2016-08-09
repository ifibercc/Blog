title: JavaScript中的数据类型及其检测
date: 2016-08-09 17:12:26
tags:
- tech
- JavaScript
---
## 1. 数据类型
### 1.1 基本类型
- Number
- String
- Boolean
- Null
- Undefined
- Symbol

### 1.2 引用类型
- Object
- Array
- Function
- RegExp
- Date

## 2. 类型检测
### 2.1 typeof
``` javascript
var s = 'Nicholas';
var b = true;
var i = 22;
var u;
var n = null;
var o = new Object();
var f = new Function();

console.info(typeof s);     // string
console.info(typeof b);     // boolean
console.info(typeof i);     // number
console.info(typeof u);     // undefined
console.info(typeof n);     // object
console.info(typeof o);     // object
console.info(typeof f);     // function
```
**`typeof`只能检测基本数据类型，对于`null`还有一个Bug**
### 2.2 instanceof
`result = variable instanceof constructor`  
`instanceof`用于检测某个对象的原型链是否包含某个构造函数的`prototype`属性  
``` javascript
function C() {}
function D() {}
var o = new C();
o instanceof C     // true, Object.getPrototypeOf(o) === C.prototype
o instanceof D     // false

function Animal() {}
function Cat() {}
Cat.prototype = new Animal();
var b = new Cat();
b instanceof Animal     // true

[1, 2, 3] instanceof Array      // true
/abc/ instanceof RegExp     // true
({}) instanceof Object      // true
(function() {}) instanceof Function     // true
```
**`instanceof`适用于检测对象，它是基于原型链运作的**

### 2.3 constructor
`constructor`属性返回一个指向创建了该对象原型的函数引用，该属性的值是哪个函数本身。  
``` javascript
function Animal() {}
function Cat() {}
function BadCat() {}
Cat.prototype = new Animal();
BadCat.prototype = new Cat();
var a = new Animal();
a.constructor === Animal    // true
var b = new BadCat();
b.constructor === Animal    // true
```
**`constructor`指向的是最初创建者，而且易于伪造，不适合做类型判断**

### 2.4 toString
``` javascript
Object.prototype.toString.call();
({}).toString.call();
window.toString.call();
toString.call();
```

``` javascript
Object.prototype.toString.call([]);     // [object Array]
Object.prototype.toString.call({});     // [object Object]
Object.prototype.toString.call('');     // [object String]
Object.prototype.toString.call(new Date());     // [object Date]
Object.prototype.toString.call(1);      // [object Number]
Object.prototype.toString.call(function () {});     // [object Function]
Object.prototype.toString.call(/test/i);    // [object RegExp]
Object.prototype.toString.call(true);       // [object Boolean]
Object.prototype.toString.call(null);       // [object Null]
Object.prototype.toString.call();       // [object Undefined]
```
- [ ] 原理

**几乎十全十美，只是不能检测用户自定义类型**
### 2.5 小结
- `typeof`只能检测基本数据类型，对于`null`还有Bug
- `instanceof`适用于检测对象，它是基于原型链运作的
- `constructor`指向的是最初创建者，而且容易伪造，不适合做类型判断
- `toString`适用于ECMA内置JavaScript类型（包括基本数据类型和内置对象）的类型判断
- 基于引用判等的类型检查都有跨窗口问题，比如`instanceof`和`constructor`

**如果你要判断的是基本数据类型或JavaScript内置对象，使用`toString`；如果要判断的是自定义类型，请使用`instanceof`**

## 3. 参考
- [w3cPlus - JavaScrit的变量：如何检测变量类型](http://mp.weixin.qq.com/s?__biz=MjM5NzE0MjQ2Mw==&mid=2652491694&idx=1&sn=9d3257c6bac07f911a0a71e2b8167845&scene=4#wechat_redirect)
- [JavaScript高级程序设计（第3版）](https://book.douban.com/subject/10546125/)
