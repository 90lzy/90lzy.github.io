---
layout: post
title: "用阿里矢量图库自定义单选框的样式"
tags: ["css", "radio", "iconfont"]
---

弃用单选框的默认样式，是因为：
1. 不够美观；
2. 不同浏览器默认样式不同。

所以有时需要自定义一种单选框样式。

我的方法是阿里矢量图库（iconfont）搭配 CSS3。分三步实现：
1. 隐藏`input`元素；
2. HTML 中添加未选中状态时的图标；
3. CSS 中通过伪类`:checked`和伪元素`::before`设置单选框被选中时的图标。

## 隐藏`input`的不同方法
1. display: none
2. visibility: hidden
3. opacity: 0
4. width: 0

## 单选框的 HTML 结构
用 `div`包裹：
```
<div class="my-radio">
    <input type="radio" name="myRadio" id="myRadio">
    <label for="myRadio"><i class="iconfont icon-custom-radio">我的单选框</label>
</div>
```

或者直接`label`包裹：
```
<label class="my-radio" for="myRadio">
    <input type="radio" name="myRadio" id="myRadio">
    <i class="iconfont icon-custom-radio"></i>我的单选框
</label>
```

## CSS 设置选中状态的样式
首先必须引入阿里矢量库的 CSS 文件`iconfont.css`，然后在自己的样式表中写（假定 HTML 写法是上面第二种）：
```
.my-radio > input:not(old) {
    width: 0;
}
.my-radio > input:not(old):checked + i::before {
    content: "\e605";/* iconfont 的 unicode 编码去掉头尾 */
}
```
