CSS 仅仅是一个标记语言，不可以自定义变量，不可以引用，CSS 预处理器在 CSS 原本的语法格式基础上，增加了编程语言的特性，如变量的使用、逻辑语句的支持、函数等；使用预处理器可以提高样式代码可读性和可复用性

#### less

是一门向后兼容的 CSS 扩展语言，Less 仅对 CSS 语言增加了少许方便的扩展

变量机制以全局的最后一次赋值为准，这也是为什么大部分 UI 组件库都选择 Less

#### sass

兼容所有版本的 css，比较成熟

Dart Sass 是 Sass 的主要实现，Dart 的语法类似于 C 语言，可以编译为纯 JavaScript

变量机制类似 JS 的块级作用域一样，可以在作用域内重新赋值而不影响外部

> 常用的部分其实没有太多差别，sass 功能更为强大

#### 原子化 css

一种新的 CSS 编写和构建方式，可以大幅减少业务样式代码体积

Tailwind 可以通过配置的方式抽象出一组类名 -> 原子功能的集合

```js
// tailwind.config.js
module.exports = {
  theme: {
    screens: {
      sm: '640px',
      // => @media (min-width: 640px) { ... }

      md: '768px',
      // => @media (min-width: 768px) { ... }

      lg: '1024px',
      // => @media (min-width: 1024px) { ... }

      xl: '1280px',
      // => @media (min-width: 1280px) { ... }
    },
  },
};
```

这样的解决方案问题在于，需要规范命名约定，不然会越来越臃肿和混乱；一个类名可能需要组合很多个原子 css，造成了 html 代码的冗杂
