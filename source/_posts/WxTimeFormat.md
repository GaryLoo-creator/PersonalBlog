---
title: 微信小程序里苹果手机时间会显示NAN的问题
updated_option: "date"
description: 解决微信小程序里苹果手机时间会显示NAN的问题
categories:
  - 微信小程序
tags:
  - BUG
top_img: https://lh5.googleusercontent.com/-BE6X7Evxlcc/UK8-SoLjYDI/AAAAAAAANjI/UzGFS87LMss/s1600/Zalevskij75%252520-%25252058.jpg
cover: https://lh5.googleusercontent.com/-BE6X7Evxlcc/UK8-SoLjYDI/AAAAAAAANjI/UzGFS87LMss/s1600/Zalevskij75%252520-%25252058.jpg
---

用后端传过来的时间转换后微信小程序 ios 真机显示的时间变成了 NAN，安卓没这个问题。而且最坑的是开发工具模拟器没有这个问题，真机调试也不会出现这个问题

他只有在线上版本和体验版 ios 真机才会出现这个问题

### 原因：

- 一种说法：安卓会把这个带 T 字母的时间看做 UTC 时间格式，（包括 ios 打包后也会相差 8 个小时）与北京时间相差 8 个小时。**（这种情况没遇到过，我是直接显示 NAN 的）**
- 另一种说法：Android 和 iOS 在日期格式上的处理方式有所不同，这个不同也影响到小程序的相关日期时间函数。因为 iOS 只支持**2020/01/01**这种日期格式，不支持**2020-01-01**这样的格式，而现在很多后端处理日期的格式是 2020-01-01，发送过来的或者自己小程序前端生成的也是这种格式，new Date()就会出现兼容性问题。

如果让后端直接给时间戳就不会有这个问题了-。-

### 解决方案

- 第一种显示的时间与实际相差 8 个小时的情况，你要将 UTC 时间转化为北京时间然后进行格式化。GMT+0800 已经是加了 8 个小时的了

```js
// 字符串转换成时间  ios中要把毫秒去掉
function toTime(strTime) {
  if (!strTime) {
    return "";
  }
  var myDate = new Date(strTime + "+0800");
  if (myDate == "Invalid Date") {
    strTime = strTime.replace(/T/g, " "); //去掉T
    strTime = strTime.replace(/-/g, "/");
    strTime = strTime.replace(/\.\d+/, " "); //去掉毫秒
    myDate = new Date(strTime + "+0800");
  }
  return myDate;
}
```

- 第二种直接显示成了 NAN 的情况，把后端给的时间转换成**2020/01/01**这种日期格式，如果是直接给时间戳的话就不用处理了直接转成日期就行。

```js
let t = "2021-10-28 10:30:48";
let date = new Date(t.replace(/-/g, "/"));
```
