---
title: js 计算图片的比例
updated_option: "date"
categories:
  - js
tags:
  - 实用
description: el-date-picker组件当设置了默认的具体时间点后无法选中今天的解决方案
top_img: http://static.simpledesktops.com/uploads/desktops/2017/04/30/jerli_bg02.jpg
cover: http://static.simpledesktops.com/uploads/desktops/2017/04/30/jerli_bg02.jpg
---

# 根据图片的宽高计算出比例

**很多时候项目需要计算比例，限制上传，其实计算比例 就是约分，懂约分就很好写了**

- 例如一个图片的分辨率是 1280X720，那么这个图片的比例就是 1280:720 进行约分，也就是 16:9。
- 例如一个图片的分辨率是 800X600，那么这个图片的比例就是 800:600 进行约分，也就是 4:3。

```js
//m,n为正整数的分子和分母
function reductionTo(m, n) {
  var arr = [];
  if (!isInteger(m) || !isInteger(n)) {
    console.log("m和n必须为整数");
    return;
  } else if (m <= 0 || n <= 0) {
    console.log("m和n必须大于0");
    return;
  }
  var a = m;
  var b = n;
  a >= b ? ((a = m), (b = n)) : ((a = n), (b = m));
  if (m != 1 && n != 1) {
    for (var i = b; i >= 2; i--) {
      if (m % i == 0 && n % i == 0) {
        m = m / i;
        n = n / i;
      }
    }
  }
  arr[0] = m;
  arr[1] = n;
  return arr;
}

//判断一个数是否为整数
function isInteger(obj) {
  return obj % 1 === 0;
}
```
