---
title: hexo的Next主题支持Latex
categories: [Memo]
tags: [hexo]
mathjax: true
---

我本来没打算用NexT主题，但是因为Latex支持，我屈服了TWT，然后就开始了无穷无尽的踩坑。记一下以免下次忘掉。按着顺序怼我是成功了的，但据说方法一和方法二可以独立使用，我因为没有成功就两个都做了一遍...(如果有单个方法能成功的大佬麻烦救救孩子orz)

<!--more-->

### 0x1 使用hexo-math插件

#### 安装hexo-math插件
https://github.com/hexojs/hexo-math

```
npm install hexo-math --save
```
#### 修改配置配置文件
在站点的_config.yml中添加：

```Markdown
math:
  engine: 'mathjax' # or 'katex'
  mathjax:
    src: https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS-MML_HTMLorMML
    config: {
      tex2jax: {
        inlineMath: [ ['$','$'], ["\\(","\\)"] ],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code'],
        processEscapes: true
      },
      TeX: {
        equationNumbers: {
          autoNumber: "AMS"
        }
      }
    }
```

注意config=TeX-AMS-MML_HTMLorMML很关键，没有的话会渲染失败。

#### 解决语义冲突
修改`/node_modules/kramed/lib/rules/inline.js`文件
```javascript
// escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,改为
escape: /^\\([`*\[\]()#$+\-.!_>])/,
//em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/, 改为
em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,

```

#### 在md文件头部添加：mathjax: true
如：
```
---
title: hexo配置latex数学公式支持
date: 2019-10-25 22:31:45
categories: 环境搭建
tags:
mathjax: true
---
```
重新启动hexo（先clean再generate）

### 0x2 使用next主题

- 使用mathjax 卸载hexo-renderer-marked并更换为一下二选一。查了一下发现mathjax支持的比较全。

```
npm un hexo-renderer-marked --save 
npm i hexo-renderer-kramed --save ＃ or hexo-renderer-pandoc
```
在我自己的尝试里，pandoc报错了，所以我又卸载了。

在主题的配置文件中修改

```
mathjax：    
enable：true
```

- 使用katex 卸载hexo-renderer-marked并更换为一下二选一
```
npm un hexo-renderer-marked --save 
npm i hexo-renderer-markdown-it-plus --save ＃ or hexo-renderer-markdown-it
```

在主题的配置文件中修改

```
katex:
enable：true
```

### 0x3 测试

```
\begin{equation}
\left\{
\begin{array}{lr}
x=\dfrac{3\pi}{2}(1+2t)\cos(\dfrac{3\pi}{2}(1+2t)), & \\
y=s, & 0 \leq s \leq L,|t| \leq1. \\
z=\dfrac{3\pi}{2}(1+2t)\sin(\dfrac{3\pi}{2}(1+2t)), &  
\end{array}
\right.
\end{equation}
```

\begin{equation}
\left\{
\begin{array}{lr}
x=\dfrac{3\pi}{2}(1+2t)\cos(\dfrac{3\pi}{2}(1+2t)), & \\
y=s, & 0 \leq s \leq L,|t| \leq1. \\
z=\dfrac{3\pi}{2}(1+2t)\sin(\dfrac{3\pi}{2}(1+2t)), &  
\end{array}
\right.
\end{equation}

### 0x4 参考链接
- [在Hexo的Next主题中支持Latex](https://aipikachu.me/posts/2631/)
- [hexo配置latex数学公式支持](http://blog.wangcaimeng.top/2019/10/25/hexo%E9%85%8D%E7%BD%AElatex%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F%E6%94%AF%E6%8C%81/)
