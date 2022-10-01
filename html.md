html（超文本标记语言），定义了网页内容的结构和含义

#### DOCTYPE

Doctype 是 HTML5 的文档声明，通过它可以告诉浏览器，使用哪一个 HTML 版本标准解析文档

```html
<!DOCTYPE html>
</html>
```

HTML4 因为基于 SGML（一种通用语言协议）所以需要引入 DTD，DTD 规定了标记语言的规则，这样浏览器才能正确的呈现内容；而 HTML5 不基于 SGML，所以不需要引用 DTD

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

#### html 语义化

HTML5 新增了许多语义化标签，如 article、footer、header、nav 等，使用语义化标签的好处是

- 增强 html 代码可读性

- 在没有 CSS 样式情况下也能够让页面呈现出清晰的结构

- 有利于 SEO 和搜索引擎建立良好的沟通

> (语义化标签)[https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element#%E5%86%85%E8%81%94%E6%96%87%E6%9C%AC%E8%AF%AD%E4%B9%89]

#### 行内元素和块级元素

块级元素：

- 每个块级元素独占一行，默认从上到下排列
- 默认宽度为容器的 100%
- 高度、行高、外边距、内边距都是可以设置的
- 可以容纳其它行级元素和块级元素

行内元素：

- 和其它元素都会在一行显示
- 宽度就是内容的宽度
- 无法设置宽高，可以设置行高；设置 margin、padding 只有左右有效，上下无效
- 只能容纳文本或者其它行内元素

行内块元素：

- 和其它元素都会在一行显示
- 宽度就是内容的宽度
- 高度、行高、外边距、内边距都是可以设置的
- 可以容纳其它行级元素和块级元素

#### html 解析顺序

1. 自上而下解析 html 结构，当遇到 script、link 标签时会同时并行下载外部脚本和样式文件

2. 下载完成后解析执行，如果是 js 代码则由 js 引擎线程来解析，解析完成后将控制权交给 GUI 渲染线程，它会阻塞页面的加载

   - 一般会将 script 标签放到 body 标签的末尾，此时网页基本已加载完成，不会造成阻塞，但是如果是含有 dom 操作的脚本会造成重绘，酌情考虑

   - 设置了 async 和 defer 属性的 script 标签，其引入的脚本会异步执行，区别在于执行时机：async 会在 DOMContentLoaded 事件之后、load 事件之前执行，执行顺序取决于脚本加载完成的顺序；而 defer 会在整个文档解析完成后、DOMContentLoaded 事件之前执行，执行顺序取决于它们在文档中的顺序

3. 当初始 HTML 文档完全加载和解析时，触发 DOMContentLoaded 事件，无需等待样式表、图像和子框架完成加载

4. 整个页面的样式加载完成后，会重新渲染整个页面的 html 元素

5. 当页面中所有的内容都加载完毕时，触发 load 事件
