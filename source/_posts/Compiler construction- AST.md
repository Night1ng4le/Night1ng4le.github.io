---
title: Compiler construction - Abstract Syntax Trees
categories: [Compiler]
tags: [Theroy & Practice,BaseCS]
---

### From concrete to abstract
`抽象语法树（AST）本质是是精简的解析树。`解析树的核心是一个句子语法结构的图示。编译器设计中*“AST”*和**语法树**是可以等价的”

> 语法解析树是一个句子的图解结构，任何一种语言都可以来实现这个句子，这意味着他可以遵循任何语法规则。

<!--more-->

*如何构建语法树？*
我们尝试切割句子中最小单位的有区别的部分。
例如句子：`"Vaidehi ate the pie"`
![alt](https://miro.medium.com/max/2496/1*zQ_bUppUhjPj3JjJ-uQv0w.jpeg)
首先把句子切割为**noun**和**verb phrase**，因为一个名词不能继续往下划分，所以这个分支叶子结点直接为`“Vaidehi”`。对于动词短语`“ate the pie”`，可以分为**verb**和**noun phrase**，因为动词也无法继续划分，所以该分支叶子结点为`“ate”`。最后对于名词短语`"the pie"`，可以分为**determiner**和**noun**，其叶子结点分别为`“the”`，`“pie”`。

> In the case of the English language, the smallest “part” of every sentence is a word; words can be combined into phrases, like noun phrases or verb phrases, which can, in turn, be joined with other phrases to create a sentence epression.

*通常来说，一个语言的语法和句法包含了这个语言句子结构化的方式，成为语言定义的规则。规定我们如何写，如何理解。*

有趣的是，我们知道如何用图表表示简单句“Vaidehi ate the pie”，因为我们已经熟悉了英语的语法。想象一下，如果我们的句子中少了一个名词或一个动词?将会发生什么?嗯，我们可能第一次读到这个句子时，很快就会意识到它根本不是一个句子!甚至，当我们读到它，几乎立刻意识到到我们处理的是一个句子片段，或者说是一个不完整的句子片段。

我们能够识别之歌句子的原因就是我们知道英语的语法，即大多数句子都需要一个名词和一个动词才被认为有效。`语言的语法是我们检查一个句子在一种语言中是否有效的方法;这种“检查”有效性的过程被称为分析一个句子。`

当我们第一次阅读一个句子时，解析它以理解它的过程和与绘制一个句子图有着相同的思维步骤，而绘制一个句子图与构建一个解析树有相同的步骤。当我们第一次读一个句子的时候，我们是在做一种思维上的解构和解析。

事实证明，计算机对我们编写的代码所做的事情是完全相同的!

### Parsing expressions like it’s our job
我们可以把一个解析树看作是我们代码表达式的一个图示。如果我们把代码、程序、甚至是最简单的脚本想象成句子的形式，我们可能很快就会意识到我们写的所有代码都可以简化成表达式集。

一棵解析树可以对应一个句子，解析树是唯一的，但是生成的结果并不一定惟一（由于树本身的遍历方式可以不同）。当我们的机器对这些树进行解释时，需要对如何解析这些树制定`严格`的规则，以便我们最终得到正确的表达式，所有术语的顺序和位置都正确。







