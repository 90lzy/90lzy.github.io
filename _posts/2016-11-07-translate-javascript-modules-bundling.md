---
layout: post
title: "译：继 JavaScript 模块入门，再详解“模块打包"
tagline: ""
description: ""
tags: ["javascript","模块"]
---

（译文发布于[众成翻译](http://www.zcfy.cc/article/javascript-modules-part-2-module-bundling-1386.html)，这是[英文原文](https://medium.freecodecamp.com/javascript-modules-part-2-module-bundling-5020383cf306#.fjulakt54)）


![](http://p0.qhimg.com/t01dd3e11baa5334f0b.jpg)


在这篇文章的[第一部分](http://www.zcfy.cc/article/javascript-modules-a-beginner-s-guide-1378.html)，我谈到了什么是模块，开发者为什么使用它们，以及，在你的程序中实现模块的不同方式。

在这第二部分，将会回答打包模块到底意味着什么：为什么要打包，打包的不同方法，以及在网页开发中模块的未来发展。

## 什么是模块打包

抽象的概括，模块打包就是这样一个简单的处理：把一组模块以及它们的依赖，按照正确的次序，拼接在一个文件或一组文件里。

但正如网页开发的其它方方面面，棘手的总是潜藏在具体细节里。

## 为什么一定要打包模块?

当你将程序划分成模块时，一般把它们组织成不同的文件或文件夹。很可能你还有一组所用库的模块，比如 Underscore、React。

结果，这些文件每一个都得用 `<script>` 标签引入你的主 HTML 文件，当用户访问你的主页时再由浏览器加载进来。每个文件都用单独的  `<script>` 标签引入，意味着浏览器不得不分别挨个加载它们。

对网页加载时间来说这简直是噩梦。

于是，为了解决这个问题，我们把所有文件打包，或“拼接”到一个文件（有时也是一组文件）中，正是为了减少请求数。当你听到开发人员谈论“构建步骤”或“构建过程”时，他们谈的就是这个。

另一个加速构建操作的常用方法是，“缩减”打包后的代码。缩减，是把源代码中不需要的字符（如空格、评论、换行符等等）移除，从而减小了代码的总体积，却不改变其功能。

数据更少，浏览器处理的时间就更短，便减少了下载文件花费的时间。如果你见过带 “min” 扩展名的文件，比如 “[underscore-min.js](https://github.com/jashkenas/underscore/blob/master/underscore-min.js)”，可能就已经留意到，相比[完整版](https://github.com/jashkenas/underscore/blob/master/underscore.js)，缩减版小了好多（不过很难阅读）。

任务执行工具，如 Gulp、Grunt，让开发者操作拼接和缩减更简单便捷。一边是展示给开发者看的人类可读代码，另一边是提供给浏览器的捆绑后的计算机可读代码。

## 打包模块有哪些不同的方法？

如果你用的是一种标准模块模式（在[第一部分](https://medium.freecodecamp.com/javascript-modules-a-beginner-s-guide-783f7d7a5fcc#.y8hs0nsne)讨论过）来定义模块，那么拼接和缩减文件不会出任何岔子，你其实就是把几堆纯 JavaScript 代码捆成一束。


但如果你用的是非原生模块系统，浏览器不能像 CommonJS、AMD、甚至原生 ES6 模块格式那样解析，你就需要用专门工具先转化成排列正确、浏览器可识别的代码。这正是 Browserify、RequireJS、Webpack 和其他模块打包工具，或模块加载工具粉墨登场的时候。

除了打包或加载你的模块，模块打包工具还有许多额外的功能，比如，当你修改或为了调试生成源码映射时，它会自动重编译你的代码。

下面就来过一遍常用的模块打包方法：

## 打包 CommonJS
从[第一部分](http://www.zcfy.cc/article/javascript-modules-a-beginner-s-guide-1378.html)已经知道，CommonJS 是同步加载模块，虽然没什么毛病，但对浏览器来说不太现实。我曾提过有方法可以解决——其中之一就是模块打包工具 Browserify ，它是为浏览器编译 CommonJS 模块的工具。

举个例子，假如你有一个个文件，它引入一个模块以计算一组数值的平均值：

```
var myDependency = require(‘myDependency’);
var myGrades = [93, 95, 88, 0, 91];
var myAverageGrade = myDependency.average(myGrades);
```

在这个场景中，我们只有一个依赖。用下面的这个命令，Browserify 会以这个文件为入口把所有依赖的模块递归地打包进一个文件：

```
browserify main.js  -o bundle.js
```

Browserify 实际做的是，跳入文件为每一个依赖分析它的抽象语法树，从而遍历出工程的整个依赖关系。一旦它搞懂了你的依赖结构，就把它们按照正确的顺序捆绑进一个文件。那时，你只需用一个 `<script>` 标签，引入 `bundle.js` 到你的 HTML，从而只要一个 http 请求，就把你的所有源代码下载下来了。哇，还不去捆绑！

与之类似，如果你有多个文件，每个文件又有多个依赖，你要做的也很简单：告诉他你的入口文件，然后就可以瘫坐在椅子上看好戏。

最后打包后的文件，可以直接导向到一些工具做压缩处理。

## 打包 AMD
如果你用的是 AMD， 就需要像 RequireJS、Curl 那样的 AMD 模块加载工具。模块加载工具（与模块打包工具不同）会动态加载你的程序所需的模块。

再提醒一下，AMD 跟 CommonJS 最大不同在于，AMD 会异步加载模块。所以，如果你用 AMD，就无需打包模块到一个文件里，技术上讲也就不需要执行打包模块动作的构建过程。因为异步加载模块意味着在运行过程中逐步下载那些程序所必需的文件，而不是用户刚进入页面就一下把所有文件都下载下来。

然后实际中，每个用户动作会额外产生大数据量的请求，这对产品而言很不合理。所以大多数网页开发者仍然为了更优的性能，使用构建工具打包、缩减他们的 AMD 模块，比如像 RequireJS 优化器 [r.js](http://requirejs.org/docs/optimization.html) 一样的工具。

概括地说，在打包方面 AMD 和 CommonJS 的区别在于：开发时, 用 AMD 的程序可以省去构建过程。直到实际运行时，再让 r.js 那些优化工具介入处理。

要想围观 CommonJS 和 AMD 更有意思的“互撕”，看看这篇[Tom Dale 的博文](http://tomdale.net/2012/01/amd-is-not-the-answer/)。

## Webpack
打包工具算有些年头了，Webpack 则是初来乍到的新人。它的设计基于不知道你所用的模块系统是什么，从而让开发者各依所需选用 CommonJS、AMD 或 ES6。

你是不是纳闷，已经有像 Browserify、RequireJS 那样的打包工具各司其职、表现优异，为什么还需要 Webpack？好吧，至少因为一点，Webpack 额外提供了一些有用的特性，如“代码分割”——把你的代码库分割成按需加载的“块”。

比如，你有一个网页应用程序，其中相当一块代码只在特定条件下才用到，那么把整个代码库都打包进一个大文件就不是很高效。这时，你可以用代码分割功能，将那部分代码抽离、捆绑到另外一块，在执行时按需加载，从而避免在最开始就遇到大量负载的麻烦。其实大部分用户只会用到你应用程序的核心代码。

代码分割仅仅是 Webpack 提供的众多亮眼功能之一。关于 Webpack 与 Browserify 哪个更好，网络上充斥着各种观点，下面的是一些客观冷静的讨论，助我稍微理清了头绪：

*   [https://gist.github.com/substack/68f8d502be42d5cd4942](https://gist.github.com/substack/68f8d502be42d5cd4942)
*   [http://mattdesl.svbtle.com/browserify-vs-webpack](http://mattdesl.svbtle.com/browserify-vs-webpack)
*   [http://blog.namangoel.com/browserify-vs-webpack-js-drama](http://blog.namangoel.com/browserify-vs-webpack-js-drama)

## ES6 模块
看完了吗？好，接下来我想谈谈 ES6 模块，它在未来会减少打包工具的使用。（你很快就会明白我的意思。）先来弄懂 ES6 模块是怎么被加载的。

ES6 模块同现有的 JS 模块格式最关键的区别是，它在设计之初就考虑到了静态分析。什么意思呢？当你导入模块时，导入的模块会在编译阶段，即代码开始运行之前，被解析。于是，我们能够在运行程序之前，把导出模块中不被其他模块使用的部分移除。这节省了很大的空间，减少了浏览器的压力。

那么问题来了。你在用一些工具，像 Uglify.js，缩减代码时，有一个死代码去除的处理，它和 ES6 移除没用的模块又有什么不同呢？只能说“得看情况”。

（注：死代码去除是可选步骤，即去除未使用的代码和变量。就把它想成，扔掉打包后代码中不需要运行的冗余部分，一定在打包之后。）

有时，死代码去除在 Uglify.js 和 ES6 模块中表现完全一样，而有时也不同。如果你想验证一下，[Rollup’s wiki](https://github.com/rollup/rollup) 里有个很好的示例。

ES6 的不同在于，它去除死代码的方法不同，叫做“tree shaking”，本质上它是死代码去除的反过程。它只保留你运行所需的代码，而非排除你运行所不需要的。来看个例子：

我们有一个 `util.js` 文件，里面写了一些函数，再用 ES6 语法将它们一一导出（exports）：

```javascript
export function each(collection, iterator) {
  if (Array.isArray(collection)) {
    for (var i = 0; i < collection.length; i++) {
      iterator(collection[i], i, collection);
    }
  } else {
    for (var key in collection) {
      iterator(collection[key], key, collection);
    }
  }
}
export function filter(collection, test) {
  var filtered = [];
  each(collection, function (item) {
    if (test(item)) {
      filtered.push(item);
    }
  });
  return filtered;
}
export function map(collection, iterator) {
  var mapped = [];
  each(collection, function (value, key, collection) {
    mapped.push(iterator(value));
  });
  return mapped;
}
export function reduce(collection, iterator, accumulator) {
  var startingValueMissing = accumulator === undefined;
  each(collection, function (item) {
    if (startingValueMissing) {
      accumulator = item;
      startingValueMissing = false;
    } else {
      accumulator = iterator(accumulator, item);
    }
  });
  return accumulator;
}
```

然后，假设我们不知道自己的程序将要用到哪个功能函数，所以把这些模块全都导入（import）到 main.js：

```javascript
import  *  as  Utils  from ‘./utils.js’;
```

但到最后我们只用了 `each` 函数：

```javascript
import * as Utils from ‘./utils.js’;

Utils.each([1, 2, 3], function (x) { console.log(x) });
```

经过“tree shaking”之后，把相应的模块加载进来，新的 `main.js` 会是这个样子：

```javascript
function each(collection, iterator) {
  if (Array.isArray(collection)) {
    for (var i = 0; i < collection.length; i++) {
      iterator(collection[i], i, collection);
    }
  } else {
    for (var key in collection) {
      iterator(collection[key], key, collection);
    }
  }
};

each([1, 2, 3], function (x) { console.log(x) });
```

注意到了吗，导出模块中只有我们用到的 `each` 被引入进来了。

另外，如果我们突然决定用 `filter` 函数而非 `each`，结果就会是这样：

```
import * as Utils from ‘./utils.js’;

Utils.filter([1, 2, 3], function (x) { return x === 2 });
```

“tree shaking” 之后的样子：

```javascript
function each(collection, iterator) {
  if (Array.isArray(collection)) {
    for (var i = 0; i < collection.length; i++) {
      iterator(collection[i], i, collection);
    }
  } else {
    for (var key in collection) {
      iterator(collection[key], key, collection);
    }
  }
};

function filter(collection, test) {
  var filtered = [];
  each(collection, function (item) {
    if (test(item)) {
      filtered.push(item);
    }
  });
  return filtered;
};

filter([1, 2, 3], function (x) { return x === 2 });
```

注意了（敲黑板），这次 `each` 和 `filter` 都包括了进来。这是因为 `filter` 定义中用到了 `each`，所以要把两者都导入才能让模块正常运行。

很炫吧？

想来点有难度的吗，可以去 Rollup.js 的 [live demo and editor](http://rollupjs.org/) 鼓捣鼓捣 “tree shaking”。

## 构建 ES6 模块

现在我们已经知道 ES6 模块的加载方式与其它模块格式不同，但仍未谈到使用 ES6 模块时它的构建过程是怎样的？

而不尽完美的是，ES6 模块还需要一些额外的处理，因为有关浏览器如何加载 ES6 模块还没有原生的实现方法。

![](http://p0.qhimg.com/t01ceeaf059db7df76a.png)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

下面列出一些可选方案来构建或转换 ES6 模块，以便在浏览器中运行。其中**第一条**是当下最常用的方法：

1. 使用转译工具（如 Babel、Traceur）将你的 ES6 代码转译成 ES5 中 CommonJS、AMD或 UMD 中任一格式。再以管道的方式导向一个模块打包工具，如 Browserify、Webpack，打包成一个或多个文件。

2. 用 [Rollup.js](http://rollupjs.org/)。它和第一条很类似，但捎带上了 ES6 模块的特性——在构建之前静态分析 ES6 代码和它的依赖关系。它利用“tree shaking”让你的代码包最小。大体来说，使用 `Rollup.js` 处理你的 ES6 模块比使用 Browserify 或 Webpack 最主要的好处就是，“tree shaking”能让你的代码包更小。有一点要谨慎，Rollup 能让你把代码打包成多种格式，包括 ES6、CommonJS、AMD、UMD 和 IIFE。IIFE 和 UMD 代码包在浏览器中照常运行，但如果你打包成 AMD、CommonJS 或 ES6，就得用另外的方法再将其转化成浏览器能解析的格式（比如用 Browserify、Webpack、RequireJS 等等）。


## 过关斩将

一个网页开发者不得不过五关斩六将。把我们养眼的 ES6 模块转化成浏览器可解析的东西往往不是那么轻而易举。

有人会问，什么时候 ES6 模块可以直接运行在浏览器中，不用再做额外的修修补补？

庆幸的是，“迟早会的”。

ECMAScript 目前有一个解决方案叫[ECMAScript 6 module loader API](https://github.com/ModuleLoader/es6-module-loader)。概括地说，它是基于 Promise 的程序 API，将会动态加载模块，并缓存起来，以免后面再引入时不再重新加载新版本。

像这样：

**myModule.js**

```javascript
export class myModule {
  constructor() {
    console.log('Hello, I am a module');
  }

  hello() {
    console.log('hello!');
  }

  goodbye() {
    console.log('goodbye!');
  }
}
```

**main.js**

```javascript
System.import(‘myModule’).then(function (myModule) {
  new myModule.hello();
});

// ‘Hello!, I am a module!’
```

还有另一种方式，你可以在 `script` 标签直接指定 “type=module” 来定义模块：

```
<script type="module">
  // loads the 'myModule' export from 'mymodule.js'
  import { hello } from 'mymodule';
  new Hello(); // 'Hello, I am a module!'
</script>
```

如果你还没看过模块加载器 API 的代码库，我强烈建议去[瞟一眼](https://github.com/ModuleLoader/es6-module-loader)。

另外，如果你想以测试驱动方式推动这个方案，去看下 [SystemJS](https://github.com/systemjs/systemjs)，它正是基于 [ES6 Module Loader polyfill](https://github.com/ModuleLoader/es6-module-loader)。SystemJS 在浏览器和 Node 中动态加载任何格式的模块（ES6 模块、AMD、CommonJS、全局代码）。它在一个“注册表”里记录所有加载过的模块，以免重复加载已有的模块。而且，它可以自动转译 ES6 模块（你只需简单设置一个选项），还能够从其它任何类型的模块中加载成任何类型的模块。相当利索！

## 有了原生 ES6 模块，我们仍然需要捆绑工具吗？
ES6 模块的日益盛行引起了一些有趣的现象：

### HTTP/2 会让模块打包工具被废弃吗？

HTTP/1 只允许一次 TCP 连接发送一个请求，所以在加载多个资源时得要多个请求。用HTTP/2 的话，一切都不一样了。它是完全的多路复用，多个请求和响应可以并行发生。于是，我们可以用一个连接同时处理多个请求。

因为每个 HTTP 请求的代价大大低于 HTTP/1，长远来看，加载一批模块不再导致严重的性能问题。有人便说，这表示没必要再打包模块了。这肯定是大有可能，但实际上要看情况而定。

因为一点，模块打包还有 HTTP/2 所没有的好处，比如移除冗余的导出模块以节省空间。如果你是建一个网站，性能至关重要、分秒必争，那么长久下来，打包模块或许能给你额外的优势。不过，如果说你对性能要求没有如此苛刻，那么跳过构建步骤是可以省下一些为了减小代码包而花去的时间。

总的来说，绝大多数网站都用上 HTTP/2 的那个时候离我们现在还很远。我预测构建过程将会保留，**至少**在近期内。

附注：HTTP/2 还有其它不同，如果你感兴趣，[这是很好的资源](https://http2.github.io/faq/#what-are-the-key-differences-to-http1x)。

### CommonJS、AMD、UMD 会被废弃吗?
一旦 ES6 真成了绝对的标准，我们还需要其它非原生的模块格式吗？

我觉得还有。

遵循单一标准在 JavaScript 中导入、导出模块，而不需要中间步骤——网页开发长期受益于此。得要多久才能来到 ES6 成为模块标准的那一天？

有可能要相当一段时间。

况且很多人都喜欢有多种“口味”可选，“仅此一款”可能永远不会成真。

## 总结
我希望这篇分上下两部分的文章有助于理清开发者谈论模块打包时所用的一些术语概念。如果你还不甚了了，倒回去再看看[第一部分](http://www.zcfy.cc/article/javascript-modules-a-beginner-s-guide-1378.html)

一如既往，请在评论中自由交流、提问。

祝你“捆绑”（bundle）愉快！
