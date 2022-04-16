---
title: CSS 背景透明文字不透明
updated_option: "date"
description: 用 CSS 实现背景透明并且文字不透明
categories:
  - CSS
tags:
  - 样式
highlight_shrink: true
top_img: http://static.simpledesktops.com/uploads/desktops/2017/03/05/owl.png
cover: http://static.simpledesktops.com/uploads/desktops/2017/03/05/owl.png
---

**在平时开发中需要调整元素的透明度时，其实是在样式中设置元素的不透明度**

在 css3 中常用的方法比如：

- opacity:0.5 //表示不透明度为 50%
- rgba(255,255,255,0.5) //表示不透明度为 50%
- filter:Alpha(opacity=50) //表示不透明度为 50%

但是使用 **opacity** 设置元素的不透明度会**使其所有后代元素都会随着一起具有透明度**一般都用于调整图片或者模块的整体不透明度

#### opacity 举例

```html
<style>
  * {
    padding: 0;
    margin: 0;
  }
  body {
    padding: 50px;
    background-color: #eef;
  }
  .demo {
    padding: 25px;
    background-color: #000000;
    opacity: 0.2;
  }
  .demo p {
    color: #ffffff;
  }
</style>
<div class="demo">
  <p>背景透明，文字也透明</p>
</div>
```

使用后整个元素包括文字都会变透明，具体效果可自行体验

**rgba** 设置颜色的不透明度，一般都用于调整 background-color、color、box-shadow 等的不透明度

#### rgba 举例

```html
<style>
  * {
    padding: 0;
    margin: 0;
  }
  body {
    padding: 50px;
    background-color: #eef;
  }
  .demo {
    padding: 25px;
    background-color: #000000;
    background-color: rgba(0, 0, 0, 0.2);
  }
  .demo p {
    color: #ffffff;
  }
</style>
<div class="demo">
  <p>背景透明，文字不透明</p>
</div>
```

在 background-color 中使用了 rgba，在标准浏览器中**背景会透明，而文字不透明**具体效果可自行体验

IE 专属滤镜**filter:Alpha(opacity=x)**

- 仅支持 IE6、7、8，在 IE10 版本中被废除。
- 在 IE6、7 中，需要激活 IE 的 haslayout 属性（如：*zoom：1 或者*overflow：hidden），让它能够读懂 filter:Alpha。
- 在 IE6、7、8 中，设置了 filter:Alpha 的元素，父元素设置 position:static，其子元素设置为相对定位，可让子元素不继承 Alpha 值，保证字体颜色不透明。

#### filter 举例

```html
<style>
  * {
    padding: 0;
    margin: 0;
  }
  body {
    padding: 50px;
    background-color: #eef;
  }
  .demo {
    padding: 25px;
    background: #000000;
    filter: Alpha(opacity=50); /* 只支持IE6、7、8、9 */
    position: static; /* IE6、7、8只能设置position:static(默认属性) ，否则会导致子元素继承Alpha值 */
    *zoom: 1; /* 激活IE6、7的haslayout属性，让它读懂Alpha */
  }
  .demo p {
    color: #ffffff;
    position: relative; /* 设置子元素为相对定位，可让子元素不继承Alpha值，保证字体颜色不透明 */
  }
</style>
<div class="demo">
  <p>背景透明，文字不透明</p>
</div>
```

**综上所述**
想要设置透明背景，文字不透明，可以采用**rgba**和 IE 的专属滤镜**filter:Alpha**这样就可以在所以浏览器都实现这个效果。
