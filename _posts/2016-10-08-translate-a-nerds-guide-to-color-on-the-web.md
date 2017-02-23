---
layout: post
title: "[译] 网页色彩死抠指南"
tagline: "Translate: A Nerd's Guide to Color On the Web"
description: "分析显示器颜色原理"
tags: ["color", "css"]
---
网页色彩的使用方式有很多。而我认为，但凡用一件东西，懂得其原理肯定大有裨益。网页色彩也不例外。现在就来死抠一下网页色彩的究竟吧。

### 颜色混合

众多使用色彩的人，他们对色彩的理解还与孩童时候鼓弄颜料时一样。但电脑上的情形已然不同，因为颜色混合机制有变。你小时候用的是颜料。印刷机里的颜料和墨水含有一种叫做“色素”的微小颗粒，它们相互混合呈现出你眼中所见的色彩。**这是减色混合**。混合的颜色越多，最终看到的颜色越深，直到变成褐色。基础色就是你以前熟悉的：红、黄、蓝。你通过减色混合调配这些颜色最终会得到褐色。

![色素的减色混合](http://p3.qhimg.com/t01c5e3d761649d061c.jpg)

而在电脑（或任何显示器）上，我们是和**光**打交道。全部色光汇在一起则成白色。在[牛顿著名的棱镜实验](http://www.college-optometrists.org/en/college/museyeum/online_exhibitions/observatory/newton.cfm)之前，颜色一直被认为包含在实物对象中，而非被实物吸收并反射。艾萨克·牛顿用一块棱镜将太阳光或其他白色亮光分离成多种颜色，形成一道彩虹，证明了太阳光或白色亮光实际是多种色光。随后他又进一步尝试分离蓝光，而蓝光不再可分，证明颜色并不在棱镜内，而是棱镜将光线分离了。这说明，在**增色混合**（显示器上的颜色混合类型）中，红、绿、蓝一起能产生所有颜色。这种情况下，红和绿生成黄。

![增色混合与减色混合](http://p3.qhimg.com/t011e0583d34eb69f64.jpg)

显示器集合了许多小光点，它们组合起来产生无数的色彩。分辨率是指一个屏幕所容纳的独立色点（也叫像素）的总数。在显示器出现之前，艺术家一直在用此种类型的光频。瑟拉和点描派画家在画作中，如*La Grande Jatte*，用红和绿造出黄色。（瑟拉称作*chromo-luminarism*，而其他人称其为[divisionism](https://en.wikipedia.org/wiki/Divisionism)。）创作这类画作的基本观念是，光的混合会比传统的减色颜料混合在人眼产生更纯粹的谐振。

![瑟拉画作的细节](http://p2.qhimg.com/t01577d24e0efa749f2.jpg)

显示器是在一些不同的显示模式下做出来的，因而会改变我们从显示器上感知色彩的方式，**色深**就是用来描述这种情况的术语。单次能被显示的颜色数量取决于色深。如果色深为1，我们可以产生双色或单色。二级色深可以产生4色，以此类推可以得到32位色深。但通常投影网页的显示器只有24位色深、16777216种真彩色和Alpha通道。

称其为**真彩色**是因为我们人眼只能识别10000000（一千万）种不同的颜色，所以24位色深肯定绰绰有余。这24位中，8位用于表示红绿蓝，剩下的表示透明度或Alpha通道。

下面就用这些信息一 一拆解网页上可用的颜色属性。

### 颜色值

#### RGB 数值方式

上一部分解释了`rbga(x, x, x, y)`代表什么，接下来再拆解得细点，说明其它属性及其用法。以RGB通道的方式提及网页色彩的数值时，是特指0-255之间的数值。

```
x 是 0-255 之间的一个数
y 是 0.0-1.0 之间的一个数
rgb(x, x, x); or rgba(x, x, x, y);

例如: rbga(150, 150, 150, 0.5);
```

#### 十六进制数

十六进制的颜色数值只是表示形式略微不同而已，它可能是网页开发者指派网页颜色值最常用的方式。

如果你还记得**一字节就是八比特位**，那么每个十六进制颜色值或数字其实就代表一字节。确定一种颜色是根据它的红、绿、蓝三部分的强度，所以我们叫它“三元组”，每一组占两个位置。一个字节代表00到FF（十六进制表示法）之间的一个数，或者是0到255（十进制表示法）之间的一个数。第一个字节是红色，第二个是绿色，第三个是蓝色。称作**十六进制**是因为它使用了**基数16的计数系统**。十六进制里的数都在0-9和A-F之间，0最小，F最大；`#000000`表示黑色，`#FFFFFF`表示白色。

对于重复数值的三元组，可以用简写法省去重复的麻烦，例如，`#00FFFF`写成`#0FF`。这种方式电脑很容易解析，也很简短，方便书写，对快速复制粘贴和编程中赋值都很有用处。不过，如果你打算用更复杂的方式驾驭色彩，那 hsl 方式会让人更看得懂。

#### HSL 数值方式

Hsl 数值和 rgb 有类似的语义和取值范围，但它使用色相、饱和度、亮度值来表示颜色，而不像显示器解析颜色的那样。语法结构上，这挺像 rgb 数值；但取值范围不同。Hsl 是基于[孟塞尔颜色系统](https://en.wikipedia.org/wiki/Munsell_color_system)（孟塞尔最先利用贴近人类实际视觉的数学原理，将颜色分离成这三个分量，创造了一个描述颜色的三维系统）。

![](http://p0.qhimg.com/t01d6774405981615c2.png)

色调、饱和度、亮度可以用一个三个维度的模型表示。
色调在360度，一个完整的圆内变化；饱和度和亮度则是0到100的百分数。

```
x 是 0-360 的数值
y 是 0%-100% 的百分数
z 是 0.0-1.0 的数值
hsl(x, y, y); or hsla(x, y, y, z);

例如: hsla(150, 50%, 50%, 0.5);
```

对浏览器而言，rgb 和 hsl 数值间的转换不过是“举手之劳”（大约11行代码），但是对我们人来说，用 hsl 可容易理解得多。只需想象一个轮子，最浓稠最饱和的在轴心。[这个演示](http://www.workwithcolor.com/hsl-color-picker-01.htm)很好地解释了 hsl 的意思。

![](http://p0.qhimg.com/t01608b757477b30da0.gif)


几年前 Chris 也做了个酷炫的工具叫“hsla 探索器”，你可以[在这看看](https://css-tricks.com/examples/HSLaExplorer/)。

如果你觉得对色彩不太熟练，hsla() 为开发者提供了制作漂亮效果的简单规则——我们会在下面生成颜色的部分谈到更多。

#### 颜色俗名

开发者也可以使用颜色俗名，不过这些俗名因为不准确而留下不好用的坏名声。其中几个最突出和“名声斐然”的例子：黑灰色（dark grey）实际上比灰色（grey）更亮，柠檬色（lime）和石灰绿（limegreen）是截然不同的两种颜色。甚至有个[游戏](http://codepo8.github.io/css-colour-names/)让你猜猜网页色彩的俗名，是很久以前由 [Chris Heilmann](https://twitter.com/codepo8)编写的（现在我估计只能在 HMTL 上用了），曾是我的最爱。颜色的俗名在快速演示色彩用处时有用武之地，而开发者更规范的做法是，用 Sass 或其它预处理器存储颜色的十六进制数值，或 rgba 值，或 hsla 值，再和整个团队使用的颜色俗名映射起来。

#### 颜色变量
实践中一个好的做法是，绝不直接使用颜色值，而以变量存储它，再用更具语义的命名方案和其它变量映射起来。CSS 自带有原生的变量语法，如：

```
:root {
  --brandColor: red;
}

body {
  background: var(--brandColor);
}
```
但这些是相当新的语法，撰写本文的时候[还未被微软的浏览器所支持](http://caniuse.com/#feat=css-variables)

CSS 预处理器也支持变量，所以你可以创建个变量，如`$brandPrimary`，然后在你整个代码库中使用。或用一个[map](https://www.sitepoint.com/using-sass-maps/):

```
$colors: (
  mainBrand: #FA6ACC,
  secondaryBrand: #F02A52,
  highlight: #09A6E4
);

@function color($key) {
  @if map-has-key($colors, $key) {
    @return map-get($colors, $key);
  }

  @warn "Unknown `#{$key}` in $colors.";
  @return null;
}

// _component.scss
.element {
  background-color: color(highlight); // #09A6E4
}
```
切记，这里的命名很重要。抽象命名有时大有用处，你只需把一处代表蓝色的变量改为代表橙色，而不用来回穿梭在代码中去重命名颜色值。再作个记号——“`$blue` 现在表示橙色了.”——也不会更糟。此处响起*悲伤的长号声*。

#### currentColor
`currentColor` 是个非常有用的值。它识别层叠，可用在将一种颜色延展到另一个对象时，如盒模型阴影、轮廓线、边框，甚至背景。

比如说，你有一个div，div里还有另一个div。下面的写法会给里面的那个div加上橙色边框：

```
.div-external { color: orange; }
.div-internal { border: 1px solid currentColor; }
```
这对图标系统十分有用，不论是SVG图标还是图标字体。你可以为填充、描边或其他颜色设置默认值为`currentColor`，然后给吸管添加适合的有意义的CSS样式类名。

#### 预处理器

CSS预处理器简直是修改颜色的神器。下面的链接是不同预处理器文档中关于颜色功能的部分：
*   [Sass functions](http://sass-lang.com/documentation/Sass/Script/Functions.html)

*   [Less functions](http://lesscss.org/functions/#color-operations)

*   [Stylus functions](http://stylus-lang.com/docs/bifs.html)

*   [Example PostCSS plugin](https://github.com/postcss/postcss-color-function)

下面的是唯Sass专属的一些“黑科技”：
```
mix($color1, $color2, [$weight])
adjust-hue($color, $degrees)
lighten($color, $amount)
darken($color, $amount)
saturate($color, $amount)
```

确实有很多方法以编程的方式用预处理器组合、修改颜色，但我们不会全部都深入展开，这里有[很不错的互动资源](http://jackiebalzer.com/color)提供更详细的信息。

### 颜色的一些属性

作为CSS属性的“颜色”是指字体颜色。如果你打算设置一大片区域的颜色，就要用`background-color`，除非是在一个SVG元素中——那时得用`fill`来设置。“边框”是一个 HTML 元素周围的边界，而SVG中与之对应的是`stroke`。

#### 盒阴影与文本阴影

`box-shadow` 和 `text-shadow` 两个属性可设置成颜色值。文本阴影可设置为2-3个值：h-shadow（水平阴影）、v-shadow（垂直阴影）、一个可选的模糊半径（blur-radius）。盒阴影接受2-4个值：h-shadow, v-shadow, 可选的模糊距离（blur distance）,可选的分布距离（spread distance）。你也可以在一开始就设定为嵌入，以实现反转阴影。这个网站有[很棒的演示](http://www.cssmatic.com/box-shadow)，代码简单、可复制粘贴。

#### 渐变
通过指定一个方向可实现线性渐变。从，或到（根据浏览器）顶、底、左、右，多少度数或径向渐变。然后指定颜色节点和每个节点的颜色值。透明度也可加入其中。

下面是个例子:

参看[CodePen](http://codepen.io)上Sarah Drasner编写的一个Pen[0df6e25c52fedba5ed5fd221d082e539](http://codepen.io/sdras/pen/0df6e25c52fedba5ed5fd221d082e539/)。

大部分渐变语法并不是都那么难写，但我的确喜欢用这个[在线渐变效果生成器](http://www.colorzilla.com/gradient-editor/)来写，因为它也生成了支持 IE6-9 的复杂过滤器属性。这还有一个帅爆了的[UI 渐变生成器](http://uigradients.com/)。相当酷，而且开源，你不妨加入其中。

在SVG中实现渐变也差不多简单。我们定义一个指明id的块，也可以再自愿地定义一个专为渐变的表面区域（surface area）。

```
<linearGradient id="Gradient">
  <stop id="stop1" offset="0" stop-color="white" stop-opacity="0" />
  <stop id="stop2" offset="0.3" stop-color="black" stop-opacity="1" />
</linearGradient> 

```

这些渐变也支持透明度，创造一些很美的效果和层次，就像动态面罩一样。

参看[CodePen](http://codepen.io)上Sarah Drasner写的[动态透明面罩](http://codepen.io/sdras/pen/a8c85b6e331b2ebf85fb9254af471919/)

还可以渐变文字，不过只能在webkit内核中。[CSS-Tricks的这个代码片段](https://css-tricks.com/snippets/css/gradient-text/)是很好的示范。

### 生成颜色

有很多酷炫方法可以一下生成许多惊人的颜色。我发现在用代码创造合成艺术品或UI元素时，鼓捣这些颜色真的很有趣。

只要你一直留在上一部分讲到的颜色值范围内，就可以用Sass（或其他CSS预处理器）、JavaScriptS、或配合`Math.floor()`的`Math.Random()`，以一个`for`循环遍历所有颜色值。要用到`Math.floor()` 或 `Math.ceil()` 是因为，如果返回的不是整数就会出错，得不到一个颜色值。

一个首要规则是，你不应该同时都改变三个分量颜色值。我试过大幅度改变第一个值，第二个变化略小，第三个值不变，结果还不错。比如，**hsl 对取遍所有颜色很容易**，因为你知道让色相从0变到360度就能获得全范围的颜色。按度数旋转色相还有一个方便之处，你不一定非要取从0到360的数，甚至 -480 或 600 也是浏览器可以解析的值。

#### Sass

```
@mixin colors($max, $color-frequency) {
  $color: 300/$max;

  @for $i from 1 through $max {
    .s#{$i} {
      border: 1px solid hsl(($i - 10)*($color*1.25), ($i - 1)*($color / $color-frequency), 40%);
     }
  }
} 
.demo {
  @include colors(20,2);
}
```

我用上面的代码让水果循环变色：
参看[CodePen](http://codepen.io)上Sarah Drasner写的[根据动作反应和动态颜色实验](http://codepen.io/sdras/pen/pyedJE/)

还有这个，只是颜色范围不同 (**在列表中快速滚轮**)：
参看[CodePen](http://codepen.io)上Sarah Drasner写的[试验列表和滚轮](http://codepen.io/sdras/pen/yyGYeJ/)

下面的代码中，我在 rgb 数值里用 `Math.random()` 一下生成同一范围内的许多颜色。这个演示用 React 创造三维 VR 体验。我本来也可以用一个 for 循环取遍所有颜色，但我希望这些颜色随着运动随机产生。只有天空是它的极限。

[![](http://p4.qhimg.com/t01eea2af969e22ed1d.jpg)](https://sdras.github.io/react-aframe-demo1/)

点击图片查看完整演示。

#### JavaScript

```
class App extends React.Component {
  render () {
    const items = [],
          amt1 = 5,
          amt2 = 7;
    for (let i = 0; i < 30; i++) {
     let rando = Math.floor(Math.random() * (amt2 - 0 + 1)) + 0,
          addColor1 = parseInt(rando * i),
          addColor2 = 255 - parseInt(7 * i),
          updateColor = `rgb(200, ${addColor1}, ${addColor2})`;
      items.push(<Entity geometry="primitive: box; depth: 1.5; height: 1.5; width: 6" 
                material={{color: updateColor}} ...
                key={i}>
      ...
        </Entity>);
    }
    return (
      <Scene>
       ...
       {items}
      </Scene>
    );
  }
}
```

[GreenSock](http://greensock.com/)自带一个工具，让你动态变化相对的颜色值。这很有用，因为你可以一下选取许多元素，让它们相对于自己当前的协调色动态变化。这里有几只乌龟展示了这种方法：

参看[CodePen](http://codepen.io)上Sarah Drasner写的[Turtles that show Relative HSL tweening](http://codepen.io/sdras/pen/zvwGKw/)。

```
TweenMax.to(".turtle2 path, .turtle2 circle, .turtle2 ellipse", 1.5, {fill:"hsl(+=0, +=50%, +=0%)"});
```

### 其它很美的颜色效果

#### 交融混合模式与背景混合模式

如果你用过 Photoshop 里的图层效果，想必对交融混合模式不会陌生。几乎所有90年代的网站都用它们（我就是。*好尴尬*）。交融混合模式与背景混合模式把两张不同的图层组合在一起，有 16 种模式可用。每个都过一遍有点超出本文的主题，下面只列一些主要的点。

最顶层的图片或颜色称为`source`，而最底层的称为`destination`。两者之间正是施展混合魔法的地方，叫作`backdrop`。我们按照相当简单的数学公式将它们混在一起。

![](http://p2.qhimg.com/t011ccf48fa98c264a9.jpg)

如果你真想跟我打破砂锅问到底，我会告诉你那个用来混合颜色的数学公式取决于你想要什么效果。比如，乘法是`destination × source = backdrop`。其它效果就是用加减乘除对简单数学的变种。线性就是`A+B−1`，而颜色燃烧（color burn）是`1−(1−B)÷A`。不过，你真的不需要先知道它们再去用。

这是[更深入的文档](https://css-tricks.com/almanac/properties/m/mix-blend-mode/), 和一个用这些效果实现的展示颜色的演示：

参看[CodePen](http://codepen.io)上Sarah Drasner写的[Demo-ing Mix Blend Modes with SVG](http://codepen.io/sdras/pen/XJdGJe/)

这篇 Robin 写的文章演示了你能从[layering multiple blend modes](https://css-tricks.com/chaining-multiple-blend-modes/)实现的很复杂很震撼的效果。下文我们会提到用滤镜混合图层。在当今的浏览器，你能做的确实很多。

#### 滤镜

CSS 滤镜提供了很多花哨的颜色效果，也能将一张彩色图片处理成灰调。CSS-Tricks上有[很好的资源](https://css-tricks.com/almanac/properties/f/filter/)展示了滤镜的使用方法。现在的浏览器支持都非常好。如果你还意犹未尽，Bennett Feely 还有这个——[漂亮的滤镜图展](http://bennettfeely.com/filters-gallery/)。

滤镜可以和模糊模式一起用。Una Kravets 结合一些效果制作了常用的instagram滤镜，并造出了这个屌炸天的工具[CSS Gram](http://una.im/CSSgram/)，在底部她写有一些不错的文档。

#### feColorMatrix

[Una 有另一篇文章](http://alistapart.com/article/finessing-fecolormatrix)尝试用 `feColorMatrix` 来制作那些图片。`feColorMatrix`是SVG的原生滤镜，也可用在 HTML 元素上。它很强大，让你微调、完善颜色。顾名思义，`feColorMatrix` 的基本标记就是一组数值矩阵，我们通过它的关联id来应用。


```
<filter id="imInTheMatrix">
    <feColorMatrix in="SourceGraphic"
      type="matrix"
      values="0 0 0 0 0
              1 1 1 1 0
              0 0 0 0 0
              0 0 0 1 0" />
  </filter>

  <path filter="url(#imInTheMatrix)"  … /> 

```

我们也可以扩展这个矩阵，调整那些值的色调、饱和度等等：

```
<filter id="imInTheHueMatrix">
  <feColorMatrix in="SourceGraphic"
    type="hueRotate"
    values="150" />
</filter> 

```

Una 的文章深入探究了这里所提的所有特性，你还可以通过Amelia Belamy-Royd 的 O’Reilly 书籍[SVG Colors, Patterns & Gradients](http://shop.oreilly.com/product/0636920043065.do) 或 [Mike Mullany’s exploratory demo](http://codepen.io/mullany/full/qJCDk/) 获取更多信息，以及很多其它惊艳的SVG颜色和渐变工具。

### 颜色的可识别度和其它要留意的

一种颜色只是参照另一种颜色来说的。这是颜色中的难点。可能你更熟悉“可识别度”这个术语。放在黑色背景上的浅绿色可以被识别出来，但是你把浅绿色换到白色背景上就未必看得出来了。



![](http://p6.qhimg.com/t01a84f66e026431d01.jpg)


颜色的可识别程度可以用许多工具测量，下面是一些我最喜欢的：
*   [Colorable](http://jxnblk.com/colorable/demos/text/)

*   [Text on a background image a11y check](http://www.brandwood.com/a11y/)

*   [Contrast-A](http://dasplankton.de/ContrastA/)

*   [Accessible Colors](http://accessible-colors.com/)

一个很好的做法是，从开头就把你的调色板设置成方便识别。[Color Safe](http://colorsafe.co/) 是个帮你实现这个功能的绝佳工具。一旦你都设置好了，[WAVE (Web Accessibility Tool)](http://wave.webaim.org/) 会帮你评测网页。

#### 颜色和环境

颜色受环境影响。如果你要创作某种颇具纵深的视觉效果，知道这点就很重要。离你近的东西有更高的饱和度和更强的对比度，离你远的东西会看起来更模糊。




![](http://p9.qhimg.com/t011bc9bfe4377db056.jpg)


一张风景图，对比远近物

#### 阴影

阴影并非指灰色，而是色光的补色。如果照在你手背上的光呈黄色，那么它的阴影会是紫色。这点对你制作超长尾部阴影有用。




![阴影是色光的补色](http://p6.qhimg.com/t01b70ee62ca3c909c3.jpg)



#### 本地颜色输入

你可以用一个本地浏览器颜色选择器帮你的用户动态选色。想从颜色提示开始的话，可以敲下`<input type="color">`或`<input type="color" value="#ff0000">`。就是那么简单，浏览器干得很漂亮。有一点要记住，不同的浏览器出现提示的方式会略有不同，就像其它本地操作一样。[这里的代码](http://codepen.io/noahblon/pen/ZbjmbK/)演示了该方法与色调CSS颜色滤镜结合起来，动态选取图片的部分区域实现变色，而剩余部分都是灰调，不受影响。想出这个的人智商爆表。


### 有意思的开发工具和其它资源

*    [Sublime text 颜色高亮插件](https://packagecontrol.io/packages/Color%20Highlighter)，我用来快捷查看浏览器最后解析成什么颜色。我喜欢用`{"ha_style": "outlined"}`，但我在[这篇文章](http://wesbos.com/highlight-css-colours-in-sublime-text/)得知 Wes Bos 更爱用“filled”。


*   有很多不同的传统配色组合，在线网络资源也能帮你搞定。想更科学地配色，用 [Paletton](http://paletton.com/) 或 [Adobe Color](https://color.adobe.com/create/color-wheel/)。Benjamin Knight 的[recreated Adobe's color tool in d3 on CodePen](http://codepen.io/benknight/pen/nADpy)相当搞事，值得围观。如果你想自己的网页再高一个档次（谁不想呢？），[Coolors](https://coolors.co/)是再简单不过的方法了。

*   如果你解释颜色时有困难，并想要一个交换颜色属性类型的简捷工具，那么[Colorhexa](http://www.colorhexa.com/)几乎涉及了你能想到的颜色交换的所有类型。

*   如果你是最死抠的颜色痴迷分子，甚至可以让控制台输出颜色。这有[一份很棒的代码](http://codepen.io/jscottsmith/pen/VLzMLo/)展示如何做到。

### 总结

这篇文章涵盖极广，而网页上的颜色有很多可待深究，希望这篇短文为你的实践和理解提供了一个跳板。

（译文发布在[众成翻译](http://www.zcfy.cc/article/a-nerd-039-s-guide-to-color-on-the-web-1328.html)，英文原文来自 [A Nerd’s Guide to Color on the Web](https://css-tricks.com/nerds-guide-color-web/)。）


（完）