---
layout: post
title: "如何实现简单的响应式两栏居中布局"
tags: ["css", "bootstrap", "flexbox"]
---

## 需求

1. 为博客设计两栏布局，左栏用于阅读正文，右栏陈列分类目录；
2. 两栏居中；
3. 在手机小屏上自动变为上下排列；
4. 始终不出现横向滚动条。

HTML结构如下：

```
// html

<section class="blog">
    <article class="post">
        // post content
    </article>
    <nav class="categories-list">
        // categories navigation
    </nav>
</section>
```

## 尝试方法

### 方法一：Bootstrap grid

最简单的就是引入`bootstrap.css`，用它的**栅格（Grid）布局**：

```html
// html

<head>
<link rel="stylesheet" href="bootstrap.css">
</head>

<section class="blog container">
    <div class="row">
        <article class="post col-md-8 col-sm-12">
            // post content
        </article>
        <nav class="categories-list col-md-4 col-sm-12">
            // categories navigation
        </nav>
    </div>
</section>
```

Bootstrap grid 作用下，`container`会根据设备类型不同而设置不同宽度，且大小固定、居中，其下`row`的宽度等分成**12**列。包含`col-md-8`，`col-sm-12`类的`<ariticle>`元素会在宽屏设备中占8列宽度，而在小屏中占全部宽度。`<nav>`同理。从而实现了需求。

### 方法二：Flexbox

为了实现这么简单的布局就引入bootstrap有点小题大作，也不合理。试想，每当要实现一个小功能都先考虑引入一个大而全的框架，而非从现有的基础上实现，恐怕最后会“框架与bug齐飞”。

所以找了第二种方法——用CSS3提供的一个新属性`flexbox`：

```css
// css

.blog {
    display: -webkit-flex; /* Safari */
    display: flex; /* 这是flex box */
    justify-content: center; /* 让两栏居中 */
    flex-wrap: wrap; /* 屏幕太小不足以放下两栏时自动换行 */
}

.post {
    max-width: 670px;
}

.categories-list {
    max-width: 288px;
}
```

如果不设置`flex-wrap: wrap`，那么默认为`nowrap`，即两栏始终挤在同一行，不管屏幕多小。

### 方法三：Auto margin

用flexbox实现有一点隐患：这个属性比较新，在较低版本的浏览器可能不被支持。所以就尝试第三种方法——不用第三方框架，也不用较新的CSS3属性。

首先，实现居中比较容易，auto margin 即可。难处在于，屏幕变小的时候如何自动变为上下两栏。设想用 `float` 来实现

```css
// css

.blog {
    max-width: 960px;
    margin: 0 auto;
}

.post {
    float: left;
    max-width: 670px;
}

.categories-list {
    float: left;
    max-width: 288px;
}
```

为什么用 `max-width` 呢？因为不能设置具体的宽度，那样在屏幕宽度变小时可能导致横向滚动条；也不能用百分比设置，那样两栏会永远在同一行。我用 `max-width` 是期待这样的效果：当屏幕很大时，`div.post` 和 `div.categories-list` 保持在各自的 `max-width`；而当屏幕满足不了 `div.post` 的 `max-width` 加上 `div.categories-list` 的 `max-width` 之和时，前者会把后者挤到第二行，便实现了简陋的响应式布局。

可惜实际情况差得太远，出现了三个偏差，都是之前的知识盲点：
1. 两个设置 `max-width` 的 div 无法同处一行（相互是有多大仇），无论屏幕多大。一个 div 的 `max-width` 满足后，该行剩下的空间不会再分配给其它元素（除非是正常流以外的元素，如 `position: absolute;`?），也不是当作自身的 margin 或 border。设置 `max-width`的意思大概就是：这一行我全占了，你们一般人都不能用，我也不是给自己用，就让它荒着。
2. `max-width` 在 `float` 的 div 上失效，其实际宽度只恰好包裹 div 里的内容。
3. `div.post` 和 `div.categories-list` 因为 `float` 撑不开其容器 `div.blog`，导致它没有高度，不过居中效果还在。

那么，如果在不用第三方框架，也不用较新CSS3属性的前提下，要实现响应式布局估计得用 media query 这个似乎很古老现在没多少人用的东西。暂时不再扩展了，以后想了解的话，会搜索关键字：Bootstrap 出现之前如何实现响应式布局。

所以第三种方法尝试失败。

## 总结

现在基础知识太弱，问我能不能实现一个需求，就好像问一个瞎猫到底会不会碰上死耗子。所以，抓紧地补充基础知识，有系统地补充。扪心自问，至今完整看过一本讲解CSS的书籍没有？——不写了，我看书去。

（完）