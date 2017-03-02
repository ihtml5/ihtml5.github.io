---
layout: post
title:  "基于react的通用form表单设计"
date:   2016-3-17
author: ihtml5
categories: [components]
---

### 一.设计思路

 <p>将form表单映射成json结构，实现form表单数据和显示的分离,进而实现form表单的通用性。</p>

### 二.设计原则

1. 将form表单的验证规则，置于form表单中，而非form表单控件中
2. 基于react的状态更新机制，所有form表单里的控件为受控组件**[中文](http://www.reactjs.cn/react/docs/forms.html)** **[英文](http://facebook.github.io/react/tips/controlled-input-null-value.html)**

### 三. json描述及解读

| 属性        | 类型           | 说明 | 是否可以为空|   规则    |
| ------------- |:-------------:| -----:| -------:|-------:|
| type          | string        | 组件名| 否      | 小写   |
| label      | string     |   字段中文名 |  否     | 字段中文名|
| initValue | array      |    控件初始值|       否  | 必须是数组|
| placeholder | string     |    控件默认提示|       是  | 必须为字符串|
| message | string     |    控件错误信息提示|       是  | 必须为字符串|
| matchfield | string     |    确认密码是否相同的字段|     是 | 必须为字符串|
| readonly | boolean     |   控件是否只读|       否  | 必须为true/false|
| validator | array     |  控件验证规则|       是  | 必须是数组|
| dataUrl | string     |   控件初始化请求地址|       是  | 必须为字符串|
| validateUrl | string     |  与服务器端验证接口|       是  | 必须为字符串|
{% highlight ruby %}
  {
    "form": {
      "accountname": {
          "type": "text",
          "label": "账户名",
          "initValue": [
              ""
          ],
          "readOnly": false,
          "placeholder": "请输入不超过5个字符",
          "validator": [
              "noneEmptyFunc",
              "isExistFunc",
              "checkMaxLength"
          ],
          "message": "不能为空",
          "isModify": false,
          "validateUrl": "/user/isExist.shtml"
      },
      "locked": {
          "type": "select",
          "label": "锁",
          "initValue": [
              {
              "0": "否",
              "1": "是"
              }
          ],
          "readOnly": false,
          "placeholder": "是否被锁定",
          "validator": [
              "noneEmptyFunc"
          ],
          "message": "不能为空"
      },
      "roleId": {
          "type": "transfer",
          "label": "角色分配",
          "dataUrl": "/user/getRoles.shtml",
          "initValue": [],
          "placeholder": "请选择",
          "readOnly": false,
          "validator": [
              "noneEmptyFunc",
              "isExistFunc"
          ],
          "message": "不能为空"
      }
    }
  }
 {% endhighlight %}
**以上几个字段为必填字段，并按照规则配好初始化值** 其他字段可根据控件类型可选添加
