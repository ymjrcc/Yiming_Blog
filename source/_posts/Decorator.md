---
title: ES7 Decorator 小结
date: 2017-11-30 14:12:28
tags:
  - javascript
---
这几天因为要学习 mobx，把 ES7 Decorator 的语法翻出来复习了一下，在这里做个归纳总结。

```js
@decorator
class A {}

// 等同于
class A {}
A = decorator(A) || A;
```

<!-- more -->

修饰器是一个对类进行处理的函数。修饰器函数的第一个参数，就是所要修饰的目标类。

修饰器可以给类添加静态属性，也可以添加实例属性。如果想添加实例属性，可以通过目标类的 `prototype` 对象操作。

```js
function testable(target) {
  target.prototype.isTestable = true;
}

@testable
class MyTestableClass {}

let obj = new MyTestableClass();
obj.isTestable // true
```

修饰器不仅可以修饰类，还可以修饰类的属性。

```js
class Person {
  @readonly
  name() { return `${this.first} ${this.last}` }
}
```

此时，修饰器函数一共可以接受三个参数：

* 第一个参数是所要修饰的目标对象，即类的实例（这不同于类的修饰，那种情况时 `target` 参数指的是类本身）；  
* 第二个参数是所要修饰的属性名；  
* 第三个参数是该属性的描述对象。  

```js
function readonly(target, name, descriptor){
  // descriptor对象原来的值如下
  // {
  //   value: specifiedFunction,
  //   enumerable: false,
  //   configurable: true,
  //   writable: true
  // };
  descriptor.writable = false;
  return descriptor;
}

readonly(Person.prototype, 'name', descriptor);
// 类似于
Object.defineProperty(Person.prototype, 'name', descriptor);
```

[core-decorators.js](https://github.com/jayphelps/core-decorators)是一个第三方模块，提供了几个常见的修饰器。如 `@autobind`、`@readonly`、`@override` 等。