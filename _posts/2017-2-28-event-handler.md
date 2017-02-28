---
layout: post
title: "JavaScript 中绑定事件处理程序（Event Handler）的三种方法"
tags: ["javascript","前端"]
---

编写 JavaScript 频繁要做的一件事，是为某个网页事件指定相应的处理函数。用惯了 jQuery 的`.bind()`或`.on()`，会觉不出这个操作有什么困难、对不同浏览器有什么差异。假如不依赖第三方库，自己用原生 JavaScript 编写又该怎么样呢？《JavaScript 高级程序设计》（第三版）有一节详细讲解了。

事件处理程序（Event Handler）是一个函数，用于响应某个事件，如鼠标点击（click）等。代码中常见到 click 和 onclick，其中 click 是事件名，前缀加“on”就表示事件处理程序。记住这个有助于区分什么时候写 click，什么时候写 onclick。

## 方法一：在 HTML 中给事件处理程序这个属性赋值
一个元素支持哪些事件，你就可以直接在它的属性中为这个事件的处理程序赋值。比如，一个`button`支持 click 事件，那么这个 `button`元素肯定有一个`onclick`属性，给这个属性赋值就是指定事件处理程序。但所赋的值必须是正确的 JavaScript 代码。
```
<button onclick="alert('clicked')" id="myBtn"></button>
```

给事件处理程序赋的值里可以调用全局作用域内的函数。

所有版本的浏览器几乎都支持这个方法，但现在很少有人用，主要因为在 HTML 代码中又嵌入了 JavaScript 代码，耦合度太高，不利维护。

## 方法二：用 JavaScript 给事件处理程序赋值（DOM 0 级方法）
不在 HTML 中直接给事件处理程序属性赋值，而是在它的 JavaScript 文件中给这个属性赋值。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(){
    // do something
}
```

用这种方法给某个事件绑定处理程序，只能绑一个，后面绑定的会覆盖之前的。所以要清除一个事件的处理程序，只需赋值为`null`。

## 方法三：addEventListener 或 attachEvent（DOM 2 级方法）
非 IE 浏览器提供了一个更方便的方法，`addEventListener()`，有三个参数：
1. `event`，事件名，如 click；
2. `eventHandler`，事件处理程序，即一个函数，匿名或非匿名。如果匿名，则后面无法用`removeEventListener`移除；
3. `captureOrBubble`，一个 Boolean 值，`true`表示在捕捉阶段调用处理函数；`false`表示不在捕捉阶段，而在冒泡阶段调用处理函数。

这个方法可以给一个事件绑定多个处理函数，按绑定顺序依次调用。

IE 浏览器与之对应的方法是`attachEvent()`，但有两点不同：
1. 只有两个参数，因为 IE 只支持在冒泡阶段调用事件处理程序，所以没有`addEventListener()`的第三个参数
2. 第一个参数不是事件名（event），而是事件处理程序的属性名，也就是要加前缀“on”。

和绑定对应的是移除，分别是`removeEventListener()`和`detachEvent()`

## 封装一个跨浏览器的方法
结合以上三种方法，根据浏览器能力检测（capability detection），优先使用方法三中的非 IE 方法，然后是 IE 方法，最后才用方法二（方法一绝对不用）：
```js
var addHandler = function(element, type, handler){
    if (element.addEventListener){
        element.addEventListener(type, handler, false);
    } else if (element.attachEvent){
        element.attachEvent(“on” + type, handler);
    } else {
        element[“on” + type] = handler;
    }
 };

var removeHandler = function(element, type, handler){
    if (element.removeEventListener){
        element.removeEventListener(type, handler, false);
    } else if (element.detachEvent){
        element.detachEvent(“on” + type, handler);
    } else {
        element[“on” + type] = null;
    }
 }
```

和事件处理程序绑定息息相关的是 `Event`事件对象，它在不同浏览器中也有差异，留待以后讨论。