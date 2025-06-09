# CSS 基础知识笔记 - 第5天

## 结构伪类选择器

结构伪类选择器根据元素在文档树中的结构位置来选择元素。

### 常用的结构伪类选择器

```css
/* 选择第一个子元素 */
:first-child {
    color: red;
}

/* 选择最后一个子元素 */
:last-child {
    color: blue;
}

/* 选择第n个子元素 */
:nth-child(n) {
    background-color: yellow;
}

/* 选择奇数位置的子元素 */
:nth-child(odd) {
    background-color: #f0f0f0;
}

/* 选择偶数位置的子元素 */
:nth-child(even) {
    background-color: #e0e0e0;
}

/* 选择第一个特定类型的子元素 */
p:first-of-type {
    font-weight: bold;
}

/* 选择最后一个特定类型的子元素 */
p:last-of-type {
    font-style: italic;
}
```

### 实际应用示例

```html
<ul>
    <li>第一个列表项</li>  <!-- 会被 :first-child 选中 -->
    <li>第二个列表项</li>  <!-- 会被 :nth-child(even) 选中 -->
    <li>第三个列表项</li>  <!-- 会被 :nth-child(odd) 选中 -->
    <li>第四个列表项</li>  <!-- 会被 :last-child 选中 -->
</ul>
```

## 伪元素选择器

伪元素选择器用于设置元素指定部分的样式，或在元素内容前后插入内容。

### 常用的伪元素选择器

```css
/* 在元素内容之前插入内容 */
.quote::before {
    content: """;
    font-size: 1.5em;
    color: #666;
}

/* 在元素内容之后插入内容 */
.quote::after {
    content: """;
    font-size: 1.5em;
    color: #666;
}

/* 选择元素的第一行 */
p::first-line {
    font-weight: bold;
    color: #333;
}

/* 选择元素的第一个字母 */
p::first-letter {
    font-size: 2em;
    float: left;
    margin-right: 5px;
}

/* 选择用户选中的文本 */
::selection {
    background-color: #ffeb3b;
    color: #000;
}
```

### 实际应用示例

```html
<p class="quote">这是一段引用文字</p>
<p>这是一个段落，第一个字母会被特殊样式化。</p>
```


## 盒子模型

每个 HTML 元素都可被视为一个盒子，包含以下属性：

### 内容区域（content）
```css
.box {
    width: 200px;
    height: 200px;
}
```

### 内边距（padding）
```css
.box {
    padding: 10px;           /* 四个方向相同 */
    padding: 10px 20px;      /* 上下 10px，左右 20px */
    padding: 10px 20px 30px; /* 上 10px，左右 20px，下 30px */
    padding: 10px 20px 30px 40px; /* 上右下左（顺时针） */
    
    /* 单独设置 */
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 30px;
    padding-left: 40px;
}
```

### 边框（border）
```css
.box {
    border: 1px solid #000;  /* 宽度、样式、颜色 */
    
    /* 单独设置边框样式 */
    border-width: 1px;
    border-style: solid;     /* solid, dashed, dotted, double 等 */
    border-color: #000;
    
    /* 单独设置某一边 */
    border-top: 1px solid #000;
    border-right: 2px dashed red;
    border-bottom: 3px dotted blue;
    border-left: 4px double green;
    
    /* 圆角边框 */
    border-radius: 10px;     /* 四个角相同 */
    border-radius: 10px 20px 30px 40px; /* 左上、右上、右下、左下 */
}
```

### 外边距（margin）
```css
.box {
    margin: 10px;            /* 四个方向相同 */
    margin: 10px 20px;       /* 上下 10px，左右 20px */
    margin: 10px 20px 30px;  /* 上 10px，左右 20px，下 30px */
    margin: 10px 20px 30px 40px; /* 上右下左（顺时针） */
    
    /* 单独设置 */
    margin-top: 10px;
    margin-right: 20px;
    margin-bottom: 30px;
    margin-left: 40px;
    
    /* 水平居中 */
    margin: 0 auto;
}
```

### 盒子模型计算
默认情况下，盒子的总宽度 = width + padding-left + padding-right + border-left + border-right + margin-left + margin-right

可以使用 `box-sizing` 属性改变计算方式：
```css
.box {
    box-sizing: content-box; /* 默认值，width/height 仅包含内容区域 */
    box-sizing: border-box;  /* width/height 包含内容、内边距和边框 */
}
```

### 版心居中
版心是网页中主要内容显示的区域，通常为了美观和可读性，我们会将版心在浏览器中水平居中。

**实现方法：**
1.  确保元素是块级元素。
2.  给元素设置一个明确的宽度 (`width`)。
3.  设置左右外边距为 `auto`。

```css
.container {
    width: 960px; /* 或者其他你需要的宽度，如 80%, 1200px 等 */
    margin-left: auto;
    margin-right: auto;
    /* 简写 */
    /* margin: 0 auto; */ 
    background-color: #f0f0f0; /* 仅为示例，方便观察效果 */
    padding: 20px; /* 仅为示例 */
}
```
```html
<div class="container">
  这里是版心内容...
</div>
```

### 清除默认样式 (CSS Reset)
不同的浏览器对 HTML 元素的默认样式（如 `margin`, `padding`, `font-size` 等）可能存在差异，这会导致页面在不同浏览器下的显示效果不一致。为了解决这个问题，开发者通常会使用 CSS Reset 或 Normalize.css 来统一或清除这些默认样式。

**简单的清除默认样式示例：**
```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box; /* 推荐，改变盒子模型的计算方式 */
}

body {
    font-family: Arial, sans-serif; /* 设置一个通用的字体 */
    line-height: 1.6; /* 设置一个合适的行高 */
}

a {
    text-decoration: none; /* 清除链接下划线 */
    color: inherit; /* 继承父元素颜色 */
}

ul, ol {
    list-style: none; /* 清除列表的项目符号 */
}
```
**注意：** `*` 通配符选择器会选中所有元素，可能会有性能影响，对于大型项目，更推荐使用 Normalize.css 或更精细化的 Reset。

### 内容溢出 (`overflow`)
当一个块级元素的内容超出了其指定的尺寸时，`overflow` 属性用于控制如何处理溢出的内容。

**常用属性值：**
-   `visible` (默认值): 内容会溢出到盒子外部，并且可见。
-   `hidden`: 溢出的内容会被裁剪，并且不可见。
-   `scroll`: 无论内容是否溢出，都会显示滚动条（水平和垂直）。
-   `auto`: 如果内容溢出，则显示滚动条；否则不显示。这是最常用的值。
-   `overflow-x`: 单独控制水平方向的溢出。
-   `overflow-y`: 单独控制垂直方向的溢出。

```css
.box {
    width: 200px;
    height: 100px;
    border: 1px solid #ccc;
    overflow: auto; /* 或者 hidden, scroll, visible */
}

.box-x {
    width: 200px;
    height: 100px;
    border: 1px solid #ccc;
    overflow-x: scroll;
    overflow-y: hidden;
    white-space: nowrap; /* 配合 overflow-x: scroll/auto 使用，防止文本换行 */
}
```
```html
<div class="box">
  这是一段很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长很长的文字内容。
</div>

<div class="box-x">
  这段文字会水平滚动，因为设置了white-space: nowrap; 这段文字会水平滚动，因为设置了white-space: nowrap; 这段文字会水平滚动，因为设置了white-space: nowrap;
</div>
```
## 外边距问题-合并与塌陷

外边距合并（Margin Collapsing）是指当两个或多个垂直方向的块级元素的相邻外边距相遇时，它们会合并成一个外边距。

### 两个盒子之间的举例

相邻兄弟元素的外边距会发生合并，合并后的外边距等于两个外边距中较大的那个。

```css
.box1 {
    width: 200px;
    height: 100px;
    background-color: #ff6b6b;
    margin-bottom: 30px; /* 下外边距 30px */
}

.box2 {
    width: 200px;
    height: 100px;
    background-color: #4ecdc4;
    margin-top: 20px; /* 上外边距 20px */
}
/* 实际两个盒子之间的距离是 30px（较大的那个），而不是 50px */
```

```html
<div class="box1">盒子1</div>
<div class="box2">盒子2</div>
```

### 父子之间设置外边距导致塌陷

当父元素和第一个/最后一个子元素的外边距相邻时，会发生外边距塌陷。

```css
.parent {
    width: 300px;
    background-color: #f0f0f0;
    margin-top: 50px;
    /* 没有 padding-top 或 border-top */
}

.child {
    width: 200px;
    height: 100px;
    background-color: #ff9f43;
    margin-top: 30px; /* 这个会和父元素的 margin-top 合并 */
}
```

```html
<div class="parent">
    <div class="child">子元素</div>
</div>
```

**解决外边距塌陷的方法：**

```css
/* 方法1：为父元素添加边框 */
.parent-with-border {
    border-top: 1px solid transparent;
}

/* 方法2：为父元素添加内边距 */
.parent-with-padding {
    padding-top: 1px;
}

/* 方法3：触发BFC */
.parent-with-bfc {
    overflow: hidden;
    /* 或者 display: flow-root; */
}

/* 方法4：使用 Flexbox */
.parent-flex {
    display: flex;
    flex-direction: column;
}
```

## 行内元素设置垂直高度

行内元素（如 `<span>`, `<a>`, `<em>` 等）有特殊的高度设置规则。

### 行内元素的特点

```css
span.inline-element {
    width: 100px;        /* 无效 */
    height: 50px;        /* 无效 */
    margin-top: 20px;    /* 无效 */
    margin-bottom: 20px; /* 无效 */
    padding-top: 10px;   /* 有视觉效果，但不影响行高 */
    padding-bottom: 10px;/* 有视觉效果，但不影响行高 */
}
```

### 有效的垂直控制方法

```css
/* 方法1：使用 line-height */
.line-height-control {
    line-height: 2; /* 行高是字体大小的2倍 */
}

/* 方法2：转换为 inline-block */
span.inline-block {
    display: inline-block;
    width: 100px;     /* 现在有效 */
    height: 50px;     /* 现在有效 */
    margin: 10px;     /* 现在有效 */
    padding: 10px;    /* 现在有效且影响布局 */
}

/* 方法3：使用 vertical-align */
span.vertical-align {
    vertical-align: middle; /* top, bottom, text-top, text-bottom 等 */
}
```

```html
<p>这是一段包含 <span class="inline-element">行内元素</span> 的文本。</p>
<p>这是一段包含 <span class="inline-block">行内块元素</span> 的文本。</p>
```
## 圆角与盒子阴影

### 圆角 (border-radius)

`border-radius` 属性用于创建圆角效果，可以应用于任何元素。

```css
/* 基本圆角 */
.basic-radius {
    border-radius: 10px; /* 四个角都是 10px 圆角 */
}

/* 不同的圆角值 */
.different-radius {
    border-radius: 10px 20px 30px 40px; /* 左上 右上 右下 左下 */
}

/* 椭圆形圆角 */
.ellipse-radius {
    border-radius: 50px / 25px; /* 水平半径 / 垂直半径 */
}
```

### 正方形中的圆形（头像）

创建完美的圆形，通常用于头像显示。

```css
.avatar {
    width: 100px;
    height: 100px;
    background-color: #e74c3c;
    border-radius: 50%; /* 关键：50% 创建完美圆形 */
    overflow: hidden;   /* 确保内容不会溢出 */
    position: relative;
}

.avatar img {
    width: 100%;
    height: 100%;
    object-fit: cover; /* 保持图片比例并填满容器 */
}

/* 带边框的头像 */
.avatar-with-border {
    width: 100px;
    height: 100px;
    border: 3px solid #fff;
    border-radius: 50%;
    box-shadow: 0 2px 10px rgba(0,0,0,0.2);
}
```

```html
<div class="avatar">
    <img src="avatar.jpg" alt="用户头像">
</div>

<div class="avatar-with-border">
    <img src="avatar.jpg" alt="用户头像">
</div>
```

### 胶囊形状（按钮）

创建现代化的胶囊形按钮。

```css
.capsule-button {
    display: inline-block;
    padding: 12px 24px;
    background-color: #3498db;
    color: white;
    text-decoration: none;
    border: none;
    border-radius: 25px; /* 高度的一半，创建胶囊效果 */
    font-size: 16px;
    cursor: pointer;
    transition: all 0.3s ease;
}

.capsule-button:hover {
    background-color: #2980b9;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}

/* 大号胶囊按钮 */
.capsule-large {
    padding: 15px 30px;
    border-radius: 30px;
    font-size: 18px;
}

/* 小号胶囊按钮 */
.capsule-small {
    padding: 8px 16px;
    border-radius: 20px;
    font-size: 14px;
}
```

```html
<button class="capsule-button">普通胶囊按钮</button>
<button class="capsule-button capsule-large">大号按钮</button>
<button class="capsule-button capsule-small">小号按钮</button>
```

### 盒子阴影 (box-shadow)

`box-shadow` 属性为元素添加阴影效果。

**语法：** `box-shadow: h-offset v-offset blur spread color inset;`

```css
/* 基本阴影 */
.basic-shadow {
    box-shadow: 5px 5px 10px rgba(0,0,0,0.3);
    /* 水平偏移 垂直偏移 模糊半径 颜色 */
}

/* 多重阴影 */
.multiple-shadow {
    box-shadow: 
        0 2px 4px rgba(0,0,0,0.1),
        0 8px 16px rgba(0,0,0,0.1);
}

/* 内阴影 */
.inset-shadow {
    box-shadow: inset 0 2px 4px rgba(0,0,0,0.2);
}

/* 悬浮效果阴影 */
.hover-shadow {
    transition: box-shadow 0.3s ease;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.hover-shadow:hover {
    box-shadow: 0 8px 24px rgba(0,0,0,0.2);
}

/* 彩色阴影 */
.colored-shadow {
    box-shadow: 0 4px 12px rgba(52, 152, 219, 0.4);
}
```