#### 百分比的 marge 和 padding

在默认的水平文档流方向下，CSS margin 和 padding 属性的百分比值都是相对于父元素宽度计算的，纵向的 margin 和 padding 也是如此

如下，子元素位于父元素的左下角，紧贴着父元素的底部

```html
<div
  style="width: '300px'; height: '200px'; background: 'grey'; overflow: 'hidden'"
>
  <div
    style="width: '50px'; height: '50px'; marginTop: '50%'; background: '#0ff'"
  ></div>
</div>
```

writing-mode 属性可以修改文档流方向为垂直，易得知此时 CSS margin 和 padding 属性的百分比值都是相对于父元素高度计算的，此时子元素位于右边靠中间的位置

```html
<div
  style="width: '300px'; height: '200px'; background: 'grey'; overflow: 'hidden'; writingMode: 'vertical-rl'"
>
  <div
    style="width: '50px'; height: '50px'; marginTop: '50%'; background: '#0ff'"
  ></div>
</div>
```

CSS 权威指南中的解释：若是相对于父元素的高度计算会形成死循环。正常流中的大多数元素都会足够高以包含其后代元素，如果一个元素的上下外边距是父元素的 height 的百分数，父元素的 height 会增加，以适应后代元素上下外边距的增加，而相应的，上下外边距因为父元素 height 的增加也会增加，形成无限循环

#### 应用

可以用于高度占位，避免闪烁

举例这样的一个情况，设置一个图片的宽度为 100%，高度不限制，有加载后的图片撑开，这样会出现图片占据的高度有一个从 0 到计算高度的图片变化，视觉上会有明显的闪烁，解决方式如下

```html
<div style="width:100px; border: 1px solid gray;overflow:hidden;">
  <div id="container">
    <img src="xxx.jpg" />
  </div>
</div>
```

```css
#container {
  position: relative;
  background-color: pink;
  overflow: hidden;
}
#container:after {
  content: ' ';
  display: block;
  margin-top: 100%;
}
img {
  position: absolute;
  top: 0;
  width: 100%;
}
```

#### 负值的 margin

注意 padding 不能为负值，当 margin 为负值时有以下几种情况

- margin-left、margin-right 为负值时

  - 元素本身没有宽度，会增加元素宽度

  - 元素本身有宽度，会产生位移

- margin-top 为负值时

不管是否设置高度，都会产生向上的位移

- margin-bottom 为负值时

该元素的高度和位置不受影响，但其后的元素会向上补足
