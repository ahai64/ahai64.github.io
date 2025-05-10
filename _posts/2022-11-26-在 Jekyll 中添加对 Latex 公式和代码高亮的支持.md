---
layout: post
tags: 技术 Jekyll
title: 在 Jekyll 中添加对 Latex 公式和代码高亮的支持
---

Jekyll 对 Latex 和 highlight 的支持都需要一些额外的设置，随着各个库的更新，StackOverflow 等网站上的解决方案都有些过时了，只能自己翻各种文档，现将解决方案记录如下。

## Latex

Jekyll 的 kramdown 解析器默认支持 MathJax，但是功能只做到把 `$` 和 `$$` 转换成 MathJax 可辨识的 `\(...\)` 和 `\[...\]`，需要你自己在模板里引入 MathJax 再进行处理。

MathJax 官方文档所给的方式如下：

```html
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3.0.1/es5/tex-mml-chtml.js"></script>
```

polyfill 是为了兼容一些老旧浏览器用的，可以不要。

`async` 参数会让脚本和网页加载异步，无法保证运行时机，可能会导致一部分公式不被渲染。要确保此脚本在正文加载完成后运行，我认为应该不用 `async` 而用 `defer` 参数。或者不用这些参数，而是把此元素放到 html 文件最后。

本站是把如下元素放到网页模板的最后：

```html
<script src="https://cdn.jsdelivr.net/npm/mathjax@3.2.2/es5/tex-chtml.js"></script>
```

显示效果：

$$E=mc^2$$

注意 kramdown 解析器的行内公式与区块公式都是用 `$$` 来包裹，区别在于区块公式前后各有一个空行。

## 代码高亮

Jekyll 默认使用 rouge 这个扩展，功能不是很完善。如果不在意这点，直接引入一个 rouge 可用的 css 文件就行了，Github 上可以搜到很多。

highlight.js 这个库提供了更强大的代码高亮功能，但是与 Jekyll 的 rouge 冲突。

所以先要在 `_config.yml` 中取消 rouge 的使用：

```yml
highlighter: none
```

如果是在 Github Pages 中使用则需加入：

```yml
markdown: kramdown
kramdown:
  syntax_highlighter_opts:
    disable : true
```

接着，在模板中引入 highlight (一个 css 文件，一个 js 库文件)，并加入运行脚本：

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@highlightjs/cdn-assets@11.7.0/styles/atom-one-dark.min.css">
<script src="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@11.7.0/build/highlight.min.js"></script>
<script>hljs.highlightAll();</script>
```

效果如下：

```python
# Sattolo
def shuffle(li):
    for i in range(len(li)-2, 1, -1):
        j = random.randint(0, i-1)
        li[i], li[j] = li[j], li[i]
```

更多主题和更新的版本可在 [jsdelivr](https://www.jsdelivr.com/package/npm/@highlightjs/cdn-assets) 上选择。但请注意 js 脚本要使用 `tex-mml-chtml.js` 这个文件，而不是最前面的 `index.min.js`.

## 参考资料

1. [MathJax - kramdown](https://kramdown.gettalong.org/math_engine/mathjax.html)
2. [MathJax Getting Started](https://www.mathjax.org/#gettingstarted)
3. [MathJax CDN by Jsdelivr](https://www.jsdelivr.com/package/npm/mathjax)
4. [Disable Jekyll's default syntax highlighter Rouge](https://vilcins.medium.com/disable-jekylls-default-syntax-highlighter-rouge-12130ccac779)
5. [How to use highlight.js](https://highlightjs.org/usage/)
6. [highlightjs/cdn-assets CDN Files](https://www.jsdelivr.com/package/npm/@highlightjs/cdn-assets)