---
layout: post
title: "用 github 快速搭建免费博客"
tags: ["github","博客"]
---
这个博客建起来已有一段时间，当时忘了记录折腾过程。近来一个朋友问我怎么用 github 建博客，借此机会回忆整理下。

我是从阮一峰博客[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)知道 github 建博客这个妙用。照着试过，其它都正常，除了一点——现在好像不需要创建 orphan 分支 `gh-pages`。

按照阮一峰的教程，最后通过浏览器访问成功，博客就算搭建好了。只是有点简陋，所以我又着手设计样式。

鼓捣了一阵，最终放弃自己设计样式——实在太丑。我也建议后来者，如果不是娴熟的设计人员，就不要自己去设计，复制一套别人的模板，或者引用现成的主题。我现在的模板选自[别人展示出来的博客示例](https://github.com/jekyll/jekyll/wiki/sites)。

他人的模板复制过来，还需要修改几个地方才能当做自己的使用：

1. `_config.yml` 文件里的博主个人信息。
2. `_post` 文件夹里的文章都删掉，以后存放你自己写的。博客文章可以用 Markdown 语法（看一篇入门指南就可以用了），纯文本也行。
3. 如果有 `CNAME`文件，删除。它是用来配置你自己购买的域名，代替 github 提供的免费域名。

阮一峰的那篇介绍主要用来了解 github pages 的基本要素。而复制过来的他人模板，往往文件结构更复杂，因为使用了更丰富的功能，如自定义的工具、评论框、页面效果等。一开始不懂这些，不敢乱改。

博客建好，成功访问，样子还不赖——虽然是别人的——就可以开始写博客文章了。

听说世界上有两种前端工程师，写博客的和写博客的。以此为诫！

（完）