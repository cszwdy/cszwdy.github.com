---
layout: post
title: "排版设计的基础知识（一）"
date: 2013-11-11 10:23:58 +0800
comments: false
categories: iOS
---
![Cover](http://imageblogemiaostein.qiniudn.com/Emiaostein_Blog_paibanshejiyi_Cover.png)


关于文字的知识繁杂庞大，本篇介绍了文字系统API中经常出现且重要的概念，对深入理解和使用文字系统，例如coreText、textKit，有所帮助。希望各位同学喜爱。: ]

__目录__

* list element with functor item
{:toc}

<!--more-->

## 字符、字形、字型与字体

字符（character）是一个抽象概念。

字形（glyph）是具体字符的特殊图形表现（某个字的形体（写法））。

字体（typeface）是一个抽象概念，表示了一套完整的设计。

字型（font）是具体的字型表现机制（确定了大小，字型，字型风格）。

关于字型和字体的区别， Mark Simonson在[这个讨论](http://www.typophile.com/node/14701#comment-84393)中作出了经典解释：

> The physical embodiment of a collection of letters, numbers, symbols, etc. (whether it’s a case of metal pieces or a computer file) is a font. When referring to the design of the collection (the way it looks) you call it a typeface.

由此可见，字体表示的是一个抽象概念，而字型是使这种设计得以体现的载体。用一句话来概括，就是："字体（ font ）是你所使用的，字型 （ typeface ） 是你所看到的。"

![image](http://imageblogemiaostein.qiniudn.com/blog_TextFont_character-glyph-typeface-font-9.png)

## 文本的布局

在日常工作或生活中，都会涉及大量文本，这些文本使用某些字型（font）合理（或不合理）的排列在一起，这个排列的过程，就是`文本的布局(text layout)`。当然，我们讨论的，是“合理”的排列。既然需要“合理”，那么就有必要精确知道字形在布局中所占的空间，由此我们引入了一组测量参数，用来精确衡量字形占用的空间，这些用来衡量字型空间的参数统称为`度量值（metrics）`,如下图用蓝色标示：

![image](http://imageblogemiaostein.qiniudn.com/blog_TextFont_glyph_metrics_4.png)
![image](http://imageblogemiaostein.qiniudn.com/blog_TextFont_Letter_3.png)

度量值：

* __边界框（Bounding rectangle）__ ：一个矩形区域，该区域恰好包含字型的可视部分。例如，图中‘j’ 与 ‘E’的边界框大小不相同，但都恰好包含了字母的可视部分。

* __左右留白宽度（Left/Right-side bearing）__：字型的左右各有留白值，当文字排列在一起，就会留出适当的间距。为了让字型每个字距保持稳定，整套字型的左右留白宽度，应做整体的规划，对特殊字（如 f 的右留白宽度）单独调整。

* __步进宽度（Advance width）__：边界框的宽度加上左右留白的宽度，称为步进宽度。

* __上升部（Ascent）__：从基线到上缘线的高度。

* __下降部（Descent）__：从基线到下缘线的高度。

除度量值外，还有一些其他概念，图中黑色字体标示：

* __原点（Origin）__：文字系统根据原点，在基线上校准字形的排列。

* __基线（Baseline）__：英文字体设计中最重要的一条线，所有字型都依据基线排列。其余几条线根据基线来分布，这几条线的分布位置会大幅影响整个字体给人的印象。

* __上缘线（Ascender line）__：中间线到上缘线的部分，也就是b、d这些字母上面突出的这段，称为 ascender.

* __下缘线（Descender line）__：基准线到下缘线的部分，也就是g、p、y这些字母，超过基准线的本分，称为descender。

* __大写线（Cap line）__：大写高度的顶端。基准线到大写线之间的高度称为大写高度（Cap height）。

* __中间线（Mean line）__：a，c，m，n，x 这类小写字母的顶端线。从基准线到中间线的高度，称为x高（x-height）。

* __x高（X-height）__：从基准线到中间线的高度。

* __大写高度（Cap height）__：基准线到大写线之间的高度。

* __行距（Leading）__：字体排版过程中，两行文字之间的距离。

* __行高（Line height）__：上升部 ＋ 下降部 ＋ 行距（Leading）的高度。

## 字形视觉间距调整和合字

字形视觉间距调整（kerning）

![image](https://developer.apple.com/library/mac/documentation/TextFonts/Conceptual/CocoaTextArchitecture/Art/kerning_2x.png)

合字（Ligatures）：

![image](http://blog.justfont.com/wp-content/uploads/2012/11/latin_ligatures.png)

## 文本的对齐方式

左对齐（Left aligned）

居中对齐(Centered)

右对齐（Right aligned）

![image](https://developer.apple.com/library/mac/documentation/TextFonts/Conceptual/CocoaTextArchitecture/Art/alignmentkinds_2x.png)

两端对齐（justified）

![image](https://developer.apple.com/library/mac/documentation/TextFonts/Conceptual/CocoaTextArchitecture/Art/justified_2x.png)

## 总结

本篇对文字系统中的常见概念做了介绍，对经常使用诸如CoreText,TextKit,但对字体概念相关的API不太理解的同学，有所帮助。

## 附录：术语速查

以下是文中涉及的术语，供你参考：

文字：

字符（character）

字形（glyph）

字型（font）

字体（typeface）

合字（ligatures）

字体样式（typestyle）

字体家族（typeface family）

字型家族（font family）


排版：

文本布局（text layout）

文本布局方向（text direction）

页边距（margins）

行距（leading）

换行（line breaking）

字号（font size）

磅值大小（point size）

对齐方式（alignment）

原点（origin）

基准线（baseline）

下源线（descenders）

度量值（metrics）

x高（x-height）

中间线（mean line）

大写字母线（cap line）

上缘线（asence line）

左右留白宽度（left-side bearing, right-side bearing）

步进宽度（advance width）

边界框（bounding box）

字母之间平均字距（letter-spacing）

字母之间视觉字距调整（kerning）


文字特点：

衬线体（serif）

无衬线体（sans-serif）
