BFC（block formatting context）是块级格式化上下文，是一个独立的渲染区域，区域内外的元素不会相互影响

#### 触发BFC的条件

- 设置了float属性，并且不为none

- position属性为absolute或fixed

- display为inline-block、table-cell、table-caption、flex、inline-flex

- overflow属性不为visible

- 根元素html

#### BFC特性

- 区域的子元素会在垂直方向上一个接一个的放置

- 属于同一个BFC的两个相邻元素的margin会发生折叠，不同BFC不会发生折叠

- 每个元素的左外边距与包含块的左边界相接触（从左向右），即使浮动元素也是如此

- BFC的区域不会与float的元素区域重叠

- 计算BFC的高度时，浮动子元素也参与计算

#### 用途

1. 清除元素内部浮动

2. margin塌陷

将两个元素放到不同的bfc中即可防止