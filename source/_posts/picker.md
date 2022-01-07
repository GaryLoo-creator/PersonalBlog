---
title: picker
updated_option: "date"
categories:
  - 组件
tags:
  - 组件
description: el-date-picker组件当设置了默认的具体时间点后无法选中今天的解决方案
top_img: "linear-gradient(20deg, #0062be, #925696, #cc426e, #fb0347)"
---

## elementUI el-date-picker

el-date-picker 组件当设置了默认的具体时间点后无法选中今天的解决方案

### html 部分举例

```html
<el-date-picker
  style="width:388px;height:36px;"
  size="medium"
  prefix-icon="el-icon-date"
  v-model="searchIptinfo.date"
  value-format="yyyy-MM-dd HH:mm:ss"
  @change="daterangechange"
  :clearable="false"
  type="datetimerange"
  range-separator="至"
  start-placeholder="开始时间"
  end-placeholder="结束时间"
  :picker-options="pickerOptions"
  :time-arrow-control="true"
  :default-time="['00:00:00', '23:59:59']" //设置了选中日期后的默认具体时刻
>
</el-date-picker>
```

### js 部分

```js
// 日期选择器配置
pickerOptions: {
  disabledDate(time) {
    //設置了default-time:[00:00:00,23:59:59] 后无法选中今天的解决方案
    let ct = new Date();
    let ctYear = ct.getFullYear();
    let ctMonth = ct.getMonth();
    let ctDate = ct.getDate()
    return (
      time >
      new Date(ctYear +"-" +(ctMonth + 1)+"-" +(ctDate) +" " +"23:59:59")
    );
  }
}
```
