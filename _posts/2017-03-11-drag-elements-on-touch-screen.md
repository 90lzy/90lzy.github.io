---
layout: post
title: "在触摸屏上拖拽元素"
tags: ["javascript","前端", "动态效果"]
---

应聘时遇到一道题：做个页面，页面上有五个离散的太极图碎片，通过手指拖拽，将它们拼回原位。所以就涉及了触摸屏特有的触摸、移动等事件，还有如何判断被拖拽的元素到达了它的目的地。[先看看我完成后的效果](/taiji)(手机查看，或打开浏览器调试器模拟手机设备。)

## 基本思路
手指拖拽很容易联想到鼠标拖拽。在张鑫旭[JavaScript实现最简单的拖拽效果](http://www.zhangxinxu.com/wordpress/2010/03/javascript%E5%AE%9E%E7%8E%B0%E6%9C%80%E7%AE%80%E5%8D%95%E7%9A%84%E6%8B%96%E6%8B%BD%E6%95%88%E6%9E%9C/)中描述了他的鼠标拖拽原理：
1. 鼠标在触发触发拖拽的区域按下，就准备拖拽指定元素；
2. 准备拖拽的情况下，鼠标移动，则根据移动距离修改指定拖拽元素的位置属性；
3. 鼠标松开，停止拖拽。

要实现太极拼图的拖拽，原理也类似，多加了一个判断是否到达目的地的操作：
1. 手指触摸太极碎片，准备拖拽；
2. 准备拖拽的情况下，手指移动，则根据移动距离即时修改碎片的位置属性；
3. 手指离开，停止拖拽。此时如果太极碎片到达它的原定目的地，则放置下去；否则回到拖拽开始时的位置。

## 了解触摸屏的触摸、移动事件

在《JavaScript 高级程序设计》讲“事件”那章，有介绍移动设备的触摸事件，主要有`touchstart`、`touchmove`、`touchend`。

只要你的手指接触屏幕就会触发`touchstart`事件，不论此前是否已经有手指接触屏幕，也不论是多个手指同时接触。

与之对应的是`touchend`，在你的手指离开屏幕时触发。

在接触和离开之间有可能手指会移动，于是就触发`touchmove`事件。这个事件有点不同，它是持续触发，一旦触发几乎不可能仅触发一次，不像`touchstart`、`touchend`。比如，你给`touchmove`事件绑定了一个处理程序输出“手指移动中”，那么只要你的手指稍稍在屏幕上移动一下，就会有十几句“手指移动中”被输出。

以上三个事件触发时屏幕上都可能存在多个触摸点，比如多个手指在触摸屏幕、多个手指同时移动、多个手指同时离开，所以它们的`event`对象里就得记录下那时所有触摸点的信息。一个触摸点的信息保存在一个`Touch`对象里，所有触摸点的信息保存在`event`对象的`touches`数组（对`touchstart`而言）或`changedTouches`数组（对`touchend`、`touchend`而言）。因为`touchend`发生时其实已经没有触摸点了，所有你要找刚刚离开的那个触摸点信息，就要去找最近变化的`Touch`对象，于是就有了`changedTouches`这样一个数组；`touchmove`同理。

`Touch`对象保存了触摸点的什么信息呢？类似通常的鼠标事件，`Touch`也保存了触摸点的位置信息、目标元素等。

## 判断拖拽元素是否到达目的地
为了进行判断，我用一个`div`标签标记出目的地，所以就转化为判断两块矩形区域是否重叠。重叠包括相交和包含，网上找到一个简便方法：
```
function isOverlap(objOne, objTwo) {
    var offsetOne = objOne.offset();
    var offsetTwo = objTwo.offset();
    var x1 = offsetOne.left;
    var y1 = offsetOne.top;
    var x2 = x1 + objOne.width();
    var y2 = y1 + objOne.height();

    var x3 = offsetTwo.left;
    var y3 = offsetTwo.top;
    var x4 = x3 + objTwo.width();
    var y4 = y3 + objTwo.height();

    var zx = Math.abs(x1 + x2 - x3 - x4);
    var x = Math.abs(x1 - x2) + Math.abs(x3 - x4);
    var zy = Math.abs(y1 + y2 - y3 - y4);
    var y = Math.abs(y1 - y2) + Math.abs(y3 - y4);
    return (zx <= x && zy <= y);
}
```

## 完整代码
参看[代码库](https://github.com/90lzy/taiji)
