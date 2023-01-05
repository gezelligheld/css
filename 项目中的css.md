#### CSS 预处理器

CSS 仅仅是一个标记语言，不可以自定义变量，不可以引用，CSS 预处理器在 CSS 原本的语法格式基础上，增加了编程语言的特性，如变量的使用、逻辑语句的支持、函数等；使用预处理器可以提高样式代码可读性和可复用性。常见的预处理器有 Sass/Scss、Less 和 Stylus

##### less

是一门向后兼容的 CSS 扩展语言，Less 仅对 CSS 语言增加了少许方便的扩展。变量机制以全局的最后一次赋值为准，这也是为什么大部分 UI 组件库都选择 Less

##### sass

兼容所有版本的 css，比较成熟。Dart Sass 是 Sass 的主要实现，Dart 的语法类似于 C 语言，可以编译为纯 JavaScript。变量机制类似 JS 的块级作用域一样，可以在作用域内重新赋值而不影响外部

> 常用的部分其实没有太多差别，sass 功能更为强大

#### CSS 后处理器

PostCSS 用来解析和处理 CSS 代码，包括 px 转换为 rem、根据目标浏览器情况自动加上类似于--moz--、-o-的属性前缀等

#### 原子化 css

一种新的 CSS 编写和构建方式，可以大幅减少业务样式代码体积，常见的原子化框架有 Tailwind CSS、Windi CSS，通过类名来指定样式

例如，Tailwind 可以通过配置的方式抽象出一组类名 -> 原子功能的集合

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

#### css modules

react 并没有像 vue 的 style scoped，使用 CSS Modules 进行 css 模块化。CSS Modules 是所有的类名和动画名称默认都有各自的作用域的 CSS 文件,在构建时对对 CSS 类名和选择器限定作用域的一种方式

构建过程中,构建工具会将把以一定规则命名的样式文件(如 index.module.css)的类名编译成一个独一无二的哈希值,可以实现组件间的样式隔离,不会影响其他模块的样式

webpack 配置 css modules 如下

```js
// webpack.config.js
module.exports = {
  // ...
  module: {
    rules: [
      {
        test: /\.module\.css$/,
        loader: 'style-loader!css-loader?modules',
      },
    ],
  },
};
```

使用如下

```js
// index.css
.content {
    width: 100px;
    height: 100px;
}

// index.js
import style from './index.css';
export default () => (
    <div className={style.content}></div>
);
```

默认均为局部作用域,需要特殊的语法声明为全局作用域

```css
:global(.title) {
  color: green;
}
```

修改类名哈希值命名规则

```js
module.exports = {
  // ...
  module: {
    rules: [
      {
        test: /\.module\.css$/,
        loader:
          'style-loader!css-loader?modules&localIdentName=[path][name]---[local]---[hash:base64:5]',
      },
    ],
  },
};
```

#### css in js

CSS-in-JS 就是将应用的 CSS 样式写在 JavaScript 文件里面，而不是独立为一些.css，.scss 或者 less 之类的文件

##### 为什么使用 CSS-in-JS

- 局部样式：提供自动局部 CSS 作用域的功能，仅作用于当前组件，避免冲突

- 避免无用的 CSS 样式堆积

由于 HTML 代码和 CSS 样式之间没有显式的一一对应关系，很难辨认出项目中哪些 CSS 样式代码是有用的哪些是无用的，导致不敢轻易删除样式，随着时间推移 CSS 只会不断增加，而 CSS-in-JS 会把样式和组件绑定在一起

- Critical CSS

Critical CSS 是指将一些重要的 CSS 代码直接放到 style 标签中，link 引入的样式会阻塞渲染，而 style 标签中的样式解析完 html 就可以渲染到页面中了。CSS-in-JS 中由于 CSS 是和组件绑定在一起的，只有当组件挂载到页面上的时候，它们的 CSS 样式才会被插入到页面的 style 标签内

- 方便根据组件的状态动态地生成样式

##### CSS-in-JS 的缺点

- 运行时消耗：大多数的 CSS-in-JS 的库都是在动态生成 CSS 的，发送到客户端的代码会包括使用到的 CSS-in-JS 运行时（runtime）代码，有一定的性能代价
- 代码可读性差
- 上手有学习成本

##### CSS-in-JS 库

- Styled-components

使用 ES6 的标签模板字符串语法为需要 styled 的 Component 定义一系列 CSS 属性，当该组件的 JS 代码被解析执行的时候，styled-components 会动态生成一个 CSS 选择器，并把对应的 CSS 样式通过 style 标签的形式插入到 head 标签里面，动态生成的 CSS 选择器会有一小段哈希值来保证全局唯一避免冲突

```jsx
import styled from 'styled-components';

const Container = styled.div`
  width: 100px;
`;

const Page = () => {
  return <Container>123</Container>;
};
```

- Radium

和 styled-components 的最大区别是它生成的是标签内联样式
