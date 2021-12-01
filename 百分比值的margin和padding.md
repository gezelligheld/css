在默认的水平文档流方向下，CSS margin和padding属性的百分比值都是相对于父元素宽度计算的，纵向的margin和padding也是如此

如下，子元素位于父元素的左下角，紧贴着父元素的底部

```html
<div style="width: '300px'; height: '200px'; background: 'grey'; overflow: 'hidden'">
    <div style="width: '50px'; height: '50px'; marginTop: '50%'; background: '#0ff'"></div>
</div>
```

writing-mode属性可以修改文档流方向为垂直，易得知此时CSS margin和padding属性的百分比值都是相对于父元素高度计算的，此时子元素位于右边靠中间的位置

```html
<div style="width: '300px'; height: '200px'; background: 'grey'; overflow: 'hidden'; writingMode: 'vertical-rl'">
    <div style="width: '50px'; height: '50px'; marginTop: '50%'; background: '#0ff'"></div>
</div>
```

CSS权威指南中的解释：若是相对于父元素的高度计算会形成死循环。正常流中的大多数元素都会足够高以包含其后代元素，如果一个元素的上下外边距是父元素的height的百分数，父元素的height会增加，以适应后代元素上下外边距的增加，而相应的，上下外边距因为父元素height的增加也会增加，形成无限循环

#### 应用

可以用于高度占位，避免闪烁

举例这样的一个情况，设置一个图片的宽度为100%，高度不限制，有加载后的图片撑开，这样会出现图片占据的高度有一个从0到计算高度的图片变化，视觉上会有明显的闪烁，解决方式如下

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