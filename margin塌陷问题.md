- 同级元素塌陷

在垂直方向如果有两个元素的外边距有相遇，在浏览器中加载的真正的外边距不是两个间距的加和，而是两个边距中值比较大的，边距小的塌陷到了边距值大的值内部

如下，两个div实际的间距为20px

```css
.box1 {
    width: 50px;
    height: 50px;
    margin-bottom: 20px;
}
.box2 {
    width: 50px;
    height: 50px;
    margin-top: 10px;
}
```

- 父子元素塌陷

父元素和子元素都设置了同方向的margin-top值，两个属性之间没有其他内容进行隔离，导致两个属性相遇，发生margin塌陷

如下，div距顶部20px，且父子元素无间距

```html
<body>
    <div style="width: 100px;height: 100px;background-color: blue;margin-top: 20px;">
        <div style="width: 50px;height: 50px;background-color: red;margin-top: 10px;"></div>
    </div>
</body>
```

父元素与上一个元素的距离是0，子元素如果设置了垂直方向的上边距，会带着父级元素一起掉下来

如下，删掉父元素的margin-top后，div距顶部10px，且父子元素无间距

```html
<body>
    <div style="width: 100px;height: 100px;background-color: blue;">
        <div style="width: 50px;height: 50px;background-color: red;margin-top: 10px;"></div>
    </div>
</body>
```