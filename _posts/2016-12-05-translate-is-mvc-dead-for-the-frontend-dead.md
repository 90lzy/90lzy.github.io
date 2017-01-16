---
layout: post
title: "译：前端 MVC 已死吗？"
tags: ["前端架构","mvc","单向架构"]
---
（译文发布于[众成翻译](http://www.zcfy.cc/article/is-model-view-controller-dead-on-the-front-end-1603.html)，这是[英文原文](https://medium.freecodecamp.com/is-mvc-dead-for-the-frontend-35b4d1fe39ec#.q25l7qkpu)）

![](http://p0.qhimg.com/t010ee52a04b27a942e.png)

越来越多的前端开发者采用[单向架构](http://staltz.com/unidirectional-user-interface-architectures.html)。那么经典的“模型-视图-控制（MVC）”前景如何呢？

为了理解我们是怎么到了现在的境地，不妨回首一下前端架构的演化之路。

过去四年，我倾力于大量的网页项目，花了很多时间做前端架构、将不同的框架整合进来。

2010 年之前，**JavaScript**——就是那个写出 jQuery 的编程语言——主要用来给传统网站加上 DOM 的操作。开发者似乎并不关心“架构”这个东西。像“[暴露模块模式](https://toddmotto.com/mastering-the-module-pattern/#revealing-module-pattern)”对组织我们的代码库就够用了。

如当下关于前端架构与后端架构那样的讨论最早是在 2010 年末段出现，因为那时开发者才开始严肃探讨“单页应用程序”的概念。也是在那时，像 [Backbone](http://backbonejs.org/)、[Knockout](http://knockoutjs.com/) 那样的框架开始盛行。

构建这些框架所用的原理在当时颇为新潮，所以设计者不得不从别处取经。服务器端架构已经成熟的做法被他们借鉴了过来。而当时服务器端所有流行的框架无不用到了 [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) 模型（[因为有多种衍变](https://www.quora.com/What-are-the-main-differences-between-MVC-MVP-and-MVVM-design-patterns-for-the-JavaScript-developer)，也叫做 MV*）。

[React.js](https://facebook.github.io/react/) 以“渲染库”身份首次亮相时，遭受了众多开发者的讥讽，他们认为 React 用 JavaScript 处理 HTML 的方式“一反直觉”。然而他们忽略了 React 的一个重要贡献——将**基于组件的架构**带到前端世界。

React 并不是“组件”的发明者，但它的确在这领域深凿了一步。

Facebook 把 React 当作“MVC 中的 V”来宣传，恐怕也是忽略了它在架构上作出的重大突破。

说句题外话，至今我还对评阅一个[Angular 1.x 和 React 并存](https://github.com/ngReact/ngReact)的代码库心有余悸。

2015 年，我们的思维方式有个大跳变——从熟悉的 MVC 模式转向**单向架构和数据流**，它发源于 Flux 和 “函数响应式编程”（Functional Reactive Programming），支持的工具有 [Redux](https://github.com/reactjs/redux) 和 [RxJS](https://github.com/Reactive-Extensions/RxJS)。


### 那么 MVC 到底哪里出了毛病？

也许 MVC 依旧是服务器端的最佳实践。如 [Rails](http://rubyonrails.org/)、[Django](https://www.djangoproject.com/) 这样的框架用起来不失为一种乐趣。

问题的根源，是 MVC 在服务端引介进来的原理和分离做法到了客户端并不完全一样。

#### 控制层-视图层的耦合
下面的图解释了在服务器端视图层是如何与控制层交互的。它们之间只有两处接触，都在客户端与服务器端彼此的边界上。

服务器端的 MVC：
![服务器端的 MVC](http://p0.qhimg.com/t01985f64c9a12474b6.png)



但你来看客户端的 MVC ，就会发现问题。控制器很像我们所说的“背后的代码”，极度依赖前面的视图层。而在绝大多数框架中，控制器甚至是在视图层创建的（比如 Angular 的 ng-controller 就是这样的）。

客户端的 MVC：
![客户端的 MVC](http://p0.qhimg.com/t01770bbdf78b8b0892.png)


此外，你再想想[单一职责原则](http://www.oodesign.com/single-responsibility-principle.html)，客户端的 MVC 明显打破了这条原则。客户端的控制器代码在某种程度上既负责了**事件处理**又在掺和**业务逻辑**。

#### “臃肿的模型层”
细想一下在客户端你放入模型层的数据是什么样的？

其一，你有一些如 `users`、`products` 那样的数据，代表你的**应用程序状态**。再者，你还需要保存 **UI 状态**——像 `showTab`、`selectedValue` 那样的东西。

跟控制器类似，模型层也打破了单一职责原则，因为你没有方法将 **UI 状态**和**应用程序状态**的管理分离开来。

### 那么“组件”又有什么独到之处呢？

组件就是**视图** + **事件处理** + ** UI 状态**。

下面的示意图展示的是如何分离原始的 MVC 模型以实现组件。红线以上的部分正是 **Flux**所致力解决的：管理**应用程序状态**和**业务逻辑**。

![](http://p0.qhimg.com/t01722abc48558d58b2.png)

随着 React 和**基于组件的架构**的流行，我们见到越来越多人使用**单向架构**来管理应用程序状态。

它们两者如此契合，其中一个原因是它们完全涵盖了经典的 MVC 方法，并且在构建前端架构时提供了更好的方法来分离项目要点。

然而这不再是 React 的独家特色。看看 [Angular 2](https://angular.io/)，你就会发现它也应用了完全一样的模型，尽管你可能对管理应用程序状态有不同看法，如 [ngrx/store](https://github.com/ngrx/store)。

MVC 过去在客户端所能做的已经做到最好了。但从一开始它便注定落败，我们仅仅需要一些时日才能看透。经过这五年的发展，前端架构演变成现如今的模样。你回首一下，花五年时间等来一个最佳实践的横空出世也不算太长吧。

MVC 在最初是很有必要的，因为我们的前端应用程序越来越庞大、越来越繁杂，我们不知道该如何组织它们。我觉得 MVC 做了它该做的，是时候功成身退了；同时也留下了前车之鉴，关于把一种环境（服务器）的好做法移植到另一种环境（客户端）的前车之鉴。

### 未来偏向哪种架构？
我认为短时间内我们不会再回到经典的 MVC 架构来开发前端应用程序。

当越来越多的开发者见识了组件和单向架构的长处，大家的焦点就会沿着这条路向前聚集到如何开发更好的工具和库上面。

这类架构会是接下来五年内最好的解决方案吗？——很有可能，不过话又说回来，没有什么是绝对肯定的。

五年前，没人能够预测我们如今会如何写应用程序。所以我觉得现在就对未来下定论不太保险。
