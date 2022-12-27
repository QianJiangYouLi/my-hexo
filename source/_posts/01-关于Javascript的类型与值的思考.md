---
title: 01-关于JavaScript的类型与值的思考
date: 2022-12-24 01:02:58
categories:
  - JavaScript
tags:
  - JavaScript
---

## 类型

很多开发者认为 JavaScript 是动态语言，没有类型。

ECMAScript 对此的界定是：ECMAScript 语言中所有的值都有一个对应的语言类型，包括
Undefined、Null、Boolean、String、Number、Object 和 Symbol。

也有很多开发者认为 JavaScript 中的类型应该称为标签或者子类型。

但抛开学术界对类型的定义，对 JavaScript，类型就是值的内部特征，定义了值的行为，让语言引擎和开发者方便区别于其他的值。这
样说或许不够准确，但足以让人理解。

准确认识 JS 的类型很重要吗？我的回答是很重要。

只有准确理解数据类型，才能正确合理的进行数据类型转换，几乎所有的 JS 程序都会涉及某种形式的强制数据类型转换。

强制数据类型转换是 JS 中很令人头痛的问题之一，甚至很多开发者认为这是语言设计上的一个缺陷。

个人认为强制数据类型转换的缺点被过分夸大了，不然都快 2023 年了，JS 为什么都没有对此做出弥补。

## 内置类型

JS 有七种内置类型：

- 空值（null）
- 未定义（undefined）
- 布尔值（boolean）
- 数值（number）
- 字符串（string）、
- 对象（object）
- 符号（symbol）

> 除了对象，其他统称为基本数据类型

通过`tyoeof`运算符可以检测值的类型，返回的是类型字符串值。

![image-20221227182638772](https://imgs-bed-1309190146.cos.ap-shanghai.myqcloud.com/%E5%89%8D%E7%AB%AF/202212271826269.png)

这里有个要注意的地方`typeof null `返回的不是 null 而是 object。

这个 bug 由来已久，也存在了二十来年，也许以后也不会修复，毕竟这牵扯到了太多的 Web 系统，修复这个 bug 会带来更多的 bug，
甚至导致系统不能正常工作。

为准确检测 null 值的类型，需要使用符合条件。

![image-20221227192034288](https://imgs-bed-1309190146.cos.ap-shanghai.myqcloud.com/%E5%89%8D%E7%AB%AF/202212271920338.png)

除了这七种明面的数据类型，在 JS 中，函数通过 typeof 检测返回的是 function，这样看，function 也是 JS 的一个内置类型，但查
阅规范就知道，函数实际上是 object 的子类型。

数组是对象，确切的说也是 object 的子类型。

## 值和类型

JS 中的变量没有类型，只有存储在变量的值才有类型。变量可以随时保存任意类型的值。

换句话说，JS 不做类型强制，语言引擎不要求变量总是持有与其初始值同类型的值。

![image-20221227195016988](https://imgs-bed-1309190146.cos.ap-shanghai.myqcloud.com/%E5%89%8D%E7%AB%AF/202212271950006.png)

### undefined 和 undeclared

作用域中，当变量申明了但没有赋值，此时 typeof 返回的就是`undefined`。当作用域中，没有声明过的变量就是`undeclared`。

有一些人将两者等同，但实际上完全是两码事。

![image-20221227195749409](https://imgs-bed-1309190146.cos.ap-shanghai.myqcloud.com/%E5%89%8D%E7%AB%AF/202212271957434.png)

typeof 在处理没有声明的变量时会返回 undefined，这就很容易造成误解。这是 typeof 的安全防范机制造成的。

![image-20221227200126322](https://imgs-bed-1309190146.cos.ap-shanghai.myqcloud.com/%E5%89%8D%E7%AB%AF/202212272001347.png)

通过 typeof 安全防范机制可以很好的避免全局变量出现 ReferenceError 错误。

如：

```js
if (typeof DEBUG !== 'undefined') console.log('Debugging is starting')
```
