# html

- Doctype：HTML5 的文档声明，通过它可以告诉浏览器，使用哪一个 HTML 版本标准解析文档

- 语义化标签

- html 解析顺序

  - 自上而下解析 html
  - 遇到 script 时停止解析 html，请求资源并执行 js，然后继续解析 html
  - 遇到 async script 时，并行请求资源，获取后如果 html 还没有解析完成就停止解析并执行 js，执行时机不固定
  - 遇到 defer script 时，并行请求资源，等待 html 解析完成后再执行 js
  - 等到 HTML 文档完全加载和解析且 defer script 执行完毕后，触发 DOMContentLoaded 事件
  - 等到页面所有内容都加载完毕后，触发 load 事件

# css

##### 水平垂直居中的方式

- 块级元素

  - 绝对定位 + 负 magin 值（子元素需要固定宽度）
  - 绝对定位 + transform
  - 绝对定位 + left/right/bottom/top + margin
  - flex
  - flex + margin: auto
  - grid
  - grid + margin: auto
  - table-cell

- 内联元素

  - table-cell
  - ::after 或::before 添加行内元素
  - 单行行内元素且父元素定高时，设置 line-height 与父元素高度一致+text-align：center

##### 盒模型（IE 盒模型、标准盒模型、块级盒子、内联盒子）

- 块级盒子：和父元素一样宽，独占一行，width 和 height 属性起作用，padding、margin、border 会把其他元素从当前盒子周围“推开”

- 内联盒子：不独占一行，width 和 height 属性不起作用，垂直方向的 padding、margin、border 不会把其他元素从当前盒子周围“推开”

- 标准盒模型：width、height 只包含内容 content，不包含 border 和 padding

- IE 盒模型：width、height 包含 content、border 和 padding

##### 选择器及优先级计算方式

优先级：!important > 行内样式 > ID 选择器 > 类、伪类、属性 > 标签、伪元素 > 继承 > 通配符

计算方式：{A, B, C, D}，其中如果存在内联样式，那么 A = 1, 否则 A = 0；B 的值等于 ID 选择器 出现的次数；C 的值等于 类选择器、属性选择器、伪类 出现的总次数；D 的值等于 标签选择器、伪元素 出现的总次数，之后从左到右依次比较，较大的优先级更高

##### 常见页面布局方式

- 两列：一列宽度固定，另一列宽度自适应

  - float + margin
  - float + overflow，右边元素设置为 bfc 防止与浮动元素重叠
  - flex

- 三行：顶部底部固定，中间部分高度自适应

  - 定位
  - flex

- 三列：连续两列宽度固定，剩余一列宽度自适应，且三列高度固定且相等

  - float + overflow，右边元素设置为 bfc 防止与浮动元素重叠
  - flex

- 圣杯布局：左右两列宽度固定，中间一列宽度自适应，且三列高度固定且相等

  - margin + float：左右两列浮动，中间一列设置 margin

- 均分布局：每列宽度相等，每列高度固定且相等

  - float
  - flex
  - grid

##### margin 和 padding

- 百分比的 margin 和 padding：默认的水平文档流方向下，margin 和 padding 属性的百分比值都是相对于父元素宽度计算的

- 负值的 margin

  - margin-bottom 为负时不影响元素的高度和位置，其后的元素会向上补足
  - margin-top 为负值时产生向上的位移
  - margin-left、margin-right 为负值时，如果元素有宽度会产生位移，否则会增加元素宽度

- margin 塌陷问题

  - 同级元素塌陷，将两个元素设置为 BFC 可以避免
  - 父子元素塌陷，将父元素设置为 BFC 可以避免

##### css 动画

- 渐变 transition
- 转变 transform
- 自定义动画 animation

##### 设备像素比

设备像素比 = 物理像素 / 设备独立像素，其中物理像素是指像素点的多少，是一个设备的固有属性；设备独立像素是一个虚拟的单位，是用于逻辑上衡量长度的单位，其值等于 css 像素

设备像素比为了让页面上的元素以相同的比例显示到不同页面上。假设同样屏幕长度的两个设备，分辨率分别为 320x480 和 640x960，如果按真实的物理像素布局，在 320 的屏幕上铺满，到了 640 的屏幕上只有一半，为了避免这种问题，统一两个设备为 320 个虚拟像素保证页面布局一致，这样 320 的设备上 1 物理像素=1 逻辑像素，640 的设备上 2 物理像素=1 虚拟像素

##### 定位（绝对、相对、粘性）

- static：正常布局，默认
- relative：相对定位，相对于自身原有的位置进行定位
- absolute：绝对定位，元素会被移出正常文档流，并不为元素预留空间，相对于最近的 position 为非 static 的祖先元素定位
- fixed：固定定位，元素会被移出正常文档流，并不为元素预留空间，相对于屏幕视口定位，元素的位置不会随屏幕滚动而改变
- sticky：元素根据正常文档流进行定位，相对于最近的滚动祖先元素（当该祖先的 overflow 是 hidden, scroll, auto, 或 overlay 时）定位，不脱离文档流

##### 浮动

- 特点

  - 指定一个元素应沿其容器的左侧或右侧平移，直到遇到容器的边界或另一个浮动元素，会脱离正常文档流
  - 设置为浮动的元素 display 默认为 block
  - 设置了浮动的元素会被文本和内联元素环绕

- 清除浮动

  - 下一个元素不想受浮动元素影响时，设置 clear 清除浮动
  - 子元素设置浮动后，若父元素没有其他子元素撑起高度，将会发生高度塌陷，可以设置父元素为 BFC 清除元素内部浮动

##### 格式化上下文

- 块级格式化上下文 BFC

  - 触发方式：float 不为 none；position 为 absolute 或 fixed；display 为 inline-block、table-cell、table-caption、flow-root；overflow 不为 visible；根元素 html；弹性盒容器 和 网格容器的 第一级子元素，且它们本身不为 flex、grid、table 容器
  - 特点：BFC 不与浮动元素重叠；BFC 计算高度时浮动子元素也会被考虑在内；两个 BFC 垂直方向的 marge 不会重叠

- 行内格式化上下文 IFC

  - 触发方式：display 的值是 inline，inline-block，inline-table 的元素；行内元素
  - 特点：margin/padding 在竖直方向无效等

##### 弹性盒布局

- 容器属性

  - flex-direction：主轴方向
  - flex-wrap：一条轴线排不下时换行方式，与 flex-direction 可简写为 flex-flow
  - justify-content：项目在主轴上的对齐方式
  - align-items：项目在交叉轴上的对齐方式
  - align-content：多个轴线的对齐方式

- 项目属性

  - order：项目排列顺序
  - flex-grow：项目放大比例，默认为 0，即如果存在剩余空间，也不放大
  - flex-shrink：项目的缩小比例，默认为 1，即如果空间不足，将会缩小
  - flex-basis：在分配多余空间之前，项目占据的主轴空间，默认为 auto，即项目自身大小，与 flex-grow、flex-shrink 可简写为 flex
  - align-self：允许单个项目有与其他项目不一样的交叉轴对齐方式
  - justify-self：弹性盒中无效，主轴上将项目作为一个组处理，无法单独设置某一个

##### 网格布局（网格轨道、网格单元、网格线）

##### 媒体查询

根据各种设备特征和参数的值或者是否存在进行响应式布局

##### 项目中的 css

- 预处理语言 less 和 sass
- 原子化 css
- css modules
- css in js
