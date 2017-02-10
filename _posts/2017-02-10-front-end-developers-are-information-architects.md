---
layout: post
title: "前端开发者亦是「信息建筑师」"
tags: ["前端"]
---
（查看原文 [Front-End Developers Are Information Architects Too](https://24ways.org/2016/front-end-developers-are-information-architects-too/?utm_source=Frontend+Weekly&utm_campaign=48c2e5385c-EMAIL_CAMPAIGN_2017_01_11&utm_medium=email&utm_term=0_9af01549dd-48c2e5385c-710613017)，或在众成翻译网站查看 [该译文](http://www.zcfy.cc/article/front-end-developers-are-information-architects-too-9670-24-ways-2488.html)）

（译者写在前面：「信息建筑师」原文是 information architect，而 architect 在计算机领域常译为架构师，但此处没有这样译。因为文中把网页开发者编写 HTML 代码比拟为传统建筑师排布一砖一瓦，然后才说前端开发者也是一种建筑师，信息建筑师。）

2016 年 [世界信息建筑日](http://www.2016.worldiaday.org/)（World IA Day）的主题是「无处不在的信息，无处不在的建筑师」。这篇文章不是讲你可能以为的那种「信息架构师」——从事用户体验领域，可能学过图书馆学，时常谈论分类法——而是关于我多年前的一个领悟，在我刚开始主持和残障人士一起的、不断增多的可用性测试会议时的领悟：前端代码产生的结构、标记、元素间的联系，这些正是「信息建筑学」。人们在网页上畅行无阻的能力严格地与所写代码的质量相关。

## 由信息筑成的地方

在信息建筑学中我们讨论由信息筑成的地方。那些地方虽是由许多 0 和 1 搭成，但也被视为物理建筑。我们会说，**上到**一个社交媒体平台、**张贴**一篇文章到博客里、被一处环境**挡在门外**、**搭建**应用程序。2002年 [Andrew Hinton](http://www.inkblurt.com/) 写道：

> 人们生活工作在这些「建筑物」中，就像生活工作在家里、办公室内、工厂中、步行街上。这些「建筑物」虽非实质，却和我们的思想一样真实。
> 
> [25 Theses](http://archive.iainstitute.org/en/learn/research/25_theses.php)

我们建造的这类建筑物，人们生活中举足轻重的部分将依赖于它。因此，负责任地去完成也变得举足轻重。我们**必须**正确使用建筑材料。幸好，我们最重要的材料——HTML——有详备的说明文档，指导我们如何搭建稳健、无障碍使用的处所。而我又坚信一件相当重要的事——理解好 HTML 的语义。

## 语义
「语义」的英文单词 semantic 可溯源到希腊语，有「意味深长」「表达」「符号」的意思。在现实世界中，一个结构可拥有语义，传达它自身的信息。比如，叹为观止的威斯敏斯特修道院（Westminster Abbey，也叫西敏寺）会引人敬畏，并传达出一些这栋建筑的目的和意图。这座建筑的尺寸、石艺的品质、精致的大块彩色玻璃，都是有意义的符号，道出它是一座承载建造者深意的建筑。或者另外想想某个写字楼区一楼那些宽大整洁、位置极佳又明亮的大门，它们无需贴上「入口」标志来说明自己的作用，也不担心被那些想从消防通道进入大楼的人误用。那些门的设计就表达了它的功用。有时平实一点，[用略微没那么震撼人心的方式表达建筑的意图](http://hyperallergic.com/312337/from-a-pineapple-to-a-six-pack-23-buildings-that-resemble-the-things-they-sell/) 也可以，但效果是类似的：建筑物在表达自身意图。

HTML 有超过 115 种元素，许多都具备语义，让人、让浏览器、让 [残障人士辅助设备](https://en.wikipedia.org/wiki/Assistive_technology) 知道它的结构、该如何使用。[HTML 5.1 说明文档](https://www.w3.org/TR/html/) 里提过语义，说：

> HTML 中的元素、属性、属性值如此定义是为了赋予其意义（语义）。比如，`ol` 元素代表无序列表，`lang` 元素代表其内容所用的语言。
>
> [HTML 5.1 Semantics, structure, and APIs of HTML documents](https://www.w3.org/TR/html/dom.html#elements-semantics)

HTML 与生俱来的语义，意味着开发者可以通过代码来表现结构、产生元素间的关系、为内容打上标记，看的人才能理解正在和什么东西互动。组织并标记信息，让人获取、使用、理解，正是信息建筑师的职责所在。也是前端开发者的职责所在，不论做没做到。


## 信息建筑学简介
我们要从什么是信息建筑师开始。对此有许多定义，我打算引用 Richard Saul Wurman，被普遍承认为是信息建筑学之父的话。1976 年他说，信息建筑师是这样一类人：

> 他们把数据固有的模式组织起来，化繁为简；他们创造出信息的结构或地图，让来者各自寻得通往知识的道路。21 世纪新兴的、解决时代需求的职业都专注在清晰简化、人类理解和信息组织学上。
> 
> [Of Patterns And Structures](http://andrearesmini.com/blog/of-patterns-and-structures)

在我看来，它也清楚地定义了写代码的开发者。他们所写代码由浏览器或其他用户代理（如屏幕阅读器）生成有结构的、人可通行的「地方」。

正如信息建筑师的定义颇多，信息建筑学本身的定义也有不少。我将使用 《Information Architecture For The World Wide Web》（第四版）中的定义。信息建筑学：
> 是共享信息环境的结构设计；
是在数字的、物理的、跨通道的生态系统内对组织、标记、搜索、导航的综合；
是构造一类可用、可查找、可理解的信息产品和体验的艺术与科学。
> 
> Information Architecture For The World Wide Web, 4th Edition

对我而言，它正描述了前端开发。前端开发除了把事情做对，也需要一点艺术来创造健壮的、于残障人士无碍的、可用可查找的空间，这样的空间愉悦所有用户。比如，在 2015 年的 State Of The Browser 会议上， [Edd Sowden 谈了 table 元素在无障碍设计中的使用](https://vimeo.com/139062429)。他发现，稍未按语义正确地使用 `<th>` 元素来修饰 `<table>` 的标题，某些情况下浏览器就会错判，认为这个 `<table>` 是用于布局，从而根本不让辅助性技术设备识别到。另一个例子说明了代码中的某些做法如何影响内容能否被使用、被查找，由 Léonie Watson 在视频 [ARIA 如何帮助屏幕阅读器用户](https://www.youtube.com/watch?v=IhWMou12_Vk) 中演示。借助 [ARIA landmark roles](http://alistapart.com/column/wai-finding-with-aria-landmark-roles)，用屏幕阅读器的人能够很快定位并跳到网页上的常用部分。

我们对信息建筑师和信息建筑学的定义提到了模式、规则、组织、标记、结构以及关系。有颇多不同的模型阐述这些元素如何归结到一些基本原理上来。Andrew Hinton 在他的书 [Understanding Context book](http://www.contextbook.com/) 里称这些元素为标记（Labels）、关系（Relations）、规则（Rules）；Jorge Arango 的则是 [链接（Links）、节点（Nodes）和次序（Orders）](https://jarango.com/2013/04/07/links-nodes-order/)；而 Dan Klyn 用了 [本体论、分类学、与编舞术](https://vimeo.com/8866160) ——这正是我们要用的。Dan 的定义如下：
- 本体论（Ontology）：定义并阐述规则和模式，这些规则和模式决定了我们所要交流的内涵。

- 分类学（Taxonomy）：对各部分的规划。开发出一套系统和结构，确定每个部分的名称、如何归类、标记跟类别的对应关系。

- 编舞术（Choreography）：各部分之间的交互规则。由此建立的结构促成特定类型的动态交互；预先绸缪用户和信息希望的下一步走向，并长期改进元素的「示能」（affordance，译者注：能提示自身作用的一种性质）。

至此我们便有了信息建筑师和信息建筑学的定义，还有一套信息建筑学基本元素的模型。然而，编写 HTML 是真产生信息，还是仅仅把所有数据搅在一起？何时数据会脱胎成信息？[Peter Drucker](https://en.wikipedia.org/wiki/Peter_Drucker) 在他的书《Managing For The Future》中写到：
> 数据并非信息。信息是被赋予了目的和关系的数据。
> 
> 《Managing For The Future》

如果我们使用正确语义的元素去修饰相应内容，便是在赋予目的和搭建关系。比如，若我们遵从 HTML 5.1 说明文档中的建议，[使用等级（h1-h6）来修饰标题而非额外的大纲算法](https://www.w3.org/TR/html/sections.html#creating-an-outline)，就生成了一个结构，在这个结构中某个标题的层级和它之前一个相关联。组织得当，一个 `<h2>` 元素定和它的父级——必为 `<h1>` ——相关联。遵循 HTML 说明文档我们可以创作出结构合理、搜索方便、标记恰当的网页，供用户各取所需通向成功。如果你从未用过屏幕阅读器，就会纳闷怎么页面上的标题是可以搜索的。屏幕阅读器有多种方式让用户操作标题：
- 通过生成标题列表，让用户快速浏览页面信息
- 通过键盘指令逐个循环所有标题

假定有一份圣诞节电视节目的文件，我们或许会 [这样编写](https://media.24ways.org/2016/storr/christmas-day.html)：
```
<h1>Christmas Day TV schedule</h1>
  <h2>BBC1</h2>
    <h3>Morning</h3>
      <h3>Evening</h3>
  <h2>BBC2</h2>
    <h3>Morning</h3>
    <h3>Evening</h3>
  <h2>ITV</h2>
    <h3>Morning</h3>
    <h3>Evening</h3>
  <h2>Channel 4</h2>
    <h3>Morning</h3>
    <h3>Evening</h3>

```

如果我用 VoiceOver 生成标题列表，就得到这个：

![VoiceOver's Web Rotor showing a list of headings.](http://p0.qhimg.com/t0173711b6844251ad5.png)

一旦有了列表我就能借助键盘，基于标题等级来筛选。比如我按 2 就能只听所有 `<h2>` 标题：

![VoiceOver's Web Rotor showing a filtered list of level-two headings.](http://p0.qhimg.com/t01c4955a5b3302ea39.png)

但是如果我们没有用这些标题，或错误地嵌套使用它们，那么用户就会受挫。

## 用一个例子把所有串起来
下面用一个例子把所有串起来：[有个按钮，按下后改变一组链接的显示或隐藏](https://media.24ways.org/2016/storr/disclosure-button.html)。有五花八门的方法在网页上造出一个按钮，最好的是 [仅用一个 button 元素](https://www.paciellogroup.com/blog/2011/04/html5-accessibility-chops-just-use-a-button/)。所有的浏览器都识别 `<button>` 是什么、怎么作用、有哪些键盘快捷键。[HTML 说明文档中对 button 元素如此说明](https://www.w3.org/TR/html/sec-forms.html#elementdef-button)：
> `<button>` 元素代表按钮，其标记是所包含的内容。

一个 `button` 的内容可以有属性中的 `type`、相关的 [ARIA](https://www.w3.org/TR/wai-aria/) 属性、用户看见的按钮文字。这些信息比按钮的样子更重要——如果背后的代码语义不通、胡乱标记，用它的人会很煎熬，样子设计得再炫酷再蹩脚便无关痛痒了。下面是三个按钮，[一模一样的 HTML 代码](https://media.24ways.org/2016/storr/buttons.html)，只是样式设计不同：

![Three buttons styled differently. One has a coloured background and shadow to make it it stand out and look like something which can be pressed, one has the same background colour as the page but has a border to make it stand out, and the last is styled to look like a link.](http://p0.qhimg.com/t01b69447473e0aeb4b.png)

抛开它们的样子不说，正因为我们选用了有语义的 HTML 元素而非一堆不知所云的 `<div>` 或 `<span>`，使用辅助技术的那些人才得以受益。遇到非常规情形时，即便不对 `<button>` 作额外编程处理，它也能通过键盘实现无障碍使用，也无需编写事件处理程序监听键盘 `Enter` 或空格的敲击事件；但如果我们用语义不当的元素来假造一个按钮，那些麻烦事就不得不做。`<button>` 还可以快速被查找，好比用屏幕阅读器可以生成一个标题列表，以同样方式也能生成一个表单元素的列表，然后快速跳到我想的那个。

有了 `<button>`，我们还要加上那组被显示或隐藏的链接。代码如下：
```
<button aria-controls="panel" aria-expanded="false" class="settings" id="settings" type="button">Settings</button>

<div class="panel hidden" id="panel">
    <ul aria-labelledby="settings">
        <li><a href="…">Account</a></li>
        <li><a href="…">Privacy</a></li>
        <li><a href="…">Security</a></li>
    </ul>
</div>

```

刚才一下子可有不少动作，我们用了：
- `aria-controls` 属性使 `<button>` 和它所控制的那组链接有了联系。当某些辅助技术设备，像 JAWS 屏幕阅读器，遇到带 `aria-controls` 属性的元素时，会发声告诉用户存在另一个被控制的元素，并允许用户转移过去。

- `aria-expanded` 属性注明了那组链接是否可见。若可见，我们则通过 JavaScript 改为 `true`；不可见，则为 `false`。这个重要的属性告知使用屏幕阅读器的人它们所操作的元素状态如何。比如，VoiceOver 在那组链接可见时念出 「Settings expanded button」，在被隐藏时念出 「Settings collapsed button」。

- `aria-labelledby` 属性将那组链接命名为「Settings」，会对辅助技术的用户有帮助。比如，屏幕阅读器可以循环遍历页面上的所有列表，所以叫得出其中一个的名字就很利于查找。我敢说，能听到「设置列表有三项」一定比「某列表有三项」更有用。我们做这些就实现了可用可查找。

- `<ul>` 元素用来盛放那组链接。

来看看为什么选择 `<ul>` 盛放那几个设置项。首先，那几个设置项彼此有关系，所以得放入一个能表达这种意思的分组结构中。这正是列表能做而其它元素或模式不能的。比如，下面的模式就不能表达「有关系」的意思，也不具备结构：

```
<div><a href="…">Account</a></div>
<div><a href="…">Privacy</a></div>
<div><a href="…">Security</a></div>

```
我们只见有三个元素在屏幕上、在 DOM 里傻愣愣地相互挨着，这样的代码毫不健壮，也不表达任何意义。

接着，为什么我们用了 [无序列表](https://www.w3.org/TR/html/grouping-content.html#the-ul-element) 而不是 [有序列表](https://www.w3.org/TR/html/grouping-content.html#the-ol-element) 或 [定义列表](https://www.w3.org/TR/html/grouping-content.html#the-dl-element)？瞥一眼 HTML 说明文档就明白：
> `<ul>` 元素代表一列事物，这列事物的次序无关紧要，也就是说，改变其次序不怎么影响文档的含义。
> 
> The HTML 5.1 specification’s description of the  element

如果变换那组链接的次序，文档的含义会迥然变化吗？显然不会。因此，我得说我们用了对的元素来组织内容。

### 这些编程考量就是信息建筑学
我认为刚才所做的就是百分百信息建筑学。回去对照 Dan Klyn 的模型，我们其实刚实践了本体论，通过审视自己意图表达的含义：
- 我们想表达页面上有个可交互的元素，它控制某元素显示或隐藏。于是就用了一个有那样含义的 `button`。
- 我们自写了 `type='button'` 的属性来表达这个 button 不是别的什么 `menu`、`reset`、`submit`。
- 样子上我们把 `button` 设计成看起来可以互动，重要地是，[我们没有移走「光标圈」](http://www.outlinenone.com/)（译者注：光标圈，focus ring，指用键盘 Tab 导航时，按钮、链接等元素出现轮廓线，指示光标所在。）
- 我们用文字 「Settings」标记了 `<button>`，有望用户明白这个按钮是做什么的。
- 我们用了 `ul` 来组织和表达一列相关项。

我们还实践了分类学，通过构造系统和结构使元素产生关系：
- 用 `aria-controls` 属性将 `<button>` 和那组链接联系起来，我们便以自定义属性的方式为两个元素创造了关系。
- 用相同的名称标记 `<ul>` 和控制它显示与否的 `button`，我们便构造了一个元素间的结构。

并且最终我们也实践过编舞术，通过创造可以促成动作和交互的元素。我们已经预判了用户和信息的流向：
- 我们选用了 `button`，即便常规情形之外也能操作、能无障碍使用。
- 我们设置的 `aria-controls` 属性有助于使用屏幕阅读器的人简便地从 `button` 跳到它所控制的元素。
- 通过改变 `aria-expanded` 属性值，我们构造了一个系统，告知辅助性技术设备我们元素间关系的状态：那块区域可见还是隐藏。
- 我们确信信息变得更好用、更容易查找，无论用户想不想或需不需要与之交互。不管一些人如何“看”待我们所做的，他们都能够在想用的时候用上它，因为我们筑好多条路通向其中的信息。

## 信息建筑学、健壮的代码、无障碍使用
[联合国统计，世界上约 10% 的人口有某种形式的残疾。](http://www.un.org/disabilities/convention/facts.shtml) 在本文撰写的时候（2016 年 12 月 17 日），10% 就等于 7.4 亿人，如此庞大的一群人依赖于结构良好、语义正确的代码被自已用的辅助性技术设备解读出来。

如果大家都参与创造由信息组成的处所，并实践信息建筑学，那么轻而易举便能满足 [WCAG 2.0 四原则](https://www.w3.org/TR/UNDERSTANDING-WCAG20/intro.html#introduction-fourprincs-head)。我们代码建筑中的一砖一瓦直接影响数以百万人的生活，我们有这个责任让他们用上这个时代的技术。[Abby Covert](http://abbytheia.com/) 在她的书 [《How To Make Sense Of Any Mess》](http://www.howtomakesenseofanymess.com) 中写道：
> 如果我们想在这个新世界获得成功，得把信息视为可加工的材料，并学会用某种方式组织起来，以助于通往我们的目标。
> 
> [How To Make Sense Of Any Mess](http://www.howtomakesenseofanymess.com/chapter/1/page/9/people-architect-information/)

如果人人都把前端开发者看作信息建筑师，世界将会是更美好的人间。
                