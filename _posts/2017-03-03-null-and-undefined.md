---
layout: post
title: "null 和 undefined 傻傻分不清楚？"
tags: ["javascript","前端"]
---

当`null`和`undefined`出现在实际代码中，似乎并不用将它们分得很清，也出不了什么差错。因为基本都在`if`的条件判断中用到它们，而恰好它们转换成 Boolean 值都是`false`。但是，就这样不清不楚、不明不白地用着总有点不安，万一以后出错了呢。墨菲定律说：会出错的事总会出错。还是一探 null 和 undefined 的究竟为妙。

## 它们是两类基本数据类型
Null 和 Undefined 是 JavaScript 中的两种基本数据类型，而 null 和 undefined 是这两种类型的变量所拥有的值。好像说反了，应该说，如果一个变量的值等于 null 或 undefined，那么这个变量属于 Null 类型或 Undefined（请注意，首字母大写的 Null 和 Undefined 表示数据类型）。因为JavaScript 中的变量在声明时并不指定数据类型，所以一个变量被赋了什么值决定它是什么类型。比如，一个变量的值是`"abc"`或`"xdfa"`，那这个变量就属于 String 类型；如果一个变量的值是`true`或`false`，那这个变量就属于 Boolean 类型。

其它基本类型还有 String，Boolean, Number，外加一种复杂数据类型 Object。Null 和 Undefined 与其它数据类型的不同在于，Null 类型的变量只能等于一个 null 值，Undefined 类型的变量只能等于一个 undefined 值。

## 一个变量的值什么情况下会等于 null 或 undefined？
如果一个变量被声明之后没有初始化赋值，那么它自动被“悄悄”赋值为 `undefined`。而 `null` 值只能自己主动赋值给某个变量（通常为一个即将成为对象类型的变量赋值为 null，表示它现在还是一个为空的对象）。虽然也可以将某个变量显式赋值为 undefined，但一般不建议这么做，因为没有意义、多此一举。你可能会说：“怎么没有意义、多此一举呢？我把一个被赋过其它值的变量重置为 undefined，让它回到初始状态不是可以吗？”如果让一个变量回到初始状态是为了接下来重新用它，那么直接在那个时候用它就行了，不必多中间这个动作；如果将一个变量重置为 undefined，是为了让它在条件判断中等于`false`，那么更好的做法是，原来这个变量是什么类型，就重置为那个类型对应的`false`；比如，原来是 Number 类型的变量就重置为 `0`，进行布尔运算后也是`false`，好处是不会改变这个变量的数据类型。

## 对 null 和 undefined 进行 typeof 运算的结果
typeof 运算符的作用是求得某个变量的数据类型。如：
```
var n = 123;
var s = "abc"
console.log(typeof n) // 输出“number”
console.log(typeof s) // 输出“string”
```

所以，`typeof undefined` 应该等于`undefined`，表示值为 undefined 的这个变量属于 Undefined 类型。同理，理论上`typeof null`应该等于`null`，表示值为 null 的这个变量属于 Null 类型。但这时实际情况有点怪异，需要特别留意——`typeof null`的运算结果是 object。

另外，对一个未声明的变量进行 typeof 运算也是得到 undefined 结果。但是除了 typeof 运算，其它任何情况使用一个未声明的变量都会导致报错（error），而使用值为 undefined 的变量是合理的，不会报错。

（完）