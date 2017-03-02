---
layout: post
title:  "基于react的通用table内容过滤算法"
date:   2016-3-22
author: ihtml5
categories: [components]
description: ' 通用表格需面对不同类型的数据格式，比如url，email，datetime等，而这些类型的数据在数据库存储时只是作为字符串存储，因此，前端界面在正确显示这些数据时面临着挑战，为了使界面能够正确显示，后端向前端传输时需要增加这些字段的描述信息。'
---

 &nbsp;&nbsp;&nbsp;&nbsp;通用表格需面对不同类型的数据格式，比如url，email，datetime等，而这些类型的数据在数据库存储时只是作为字符串存储，因此，前端界面在正确显示这些数据时面临着挑战，为了使界面能够正确显示，后端向前端传输时需要增加这些字段的描述信息。

2.json结构描述及解读

```json
{
    "data": {
        "form": "/framejson/role.json",
        "headers": [
            "ID",
            "名称"
        ],
        "headersEN": [
            "id",
            "name"
        ],
        "rows": [
            {
                "id": 3,
                "name": "超级管理员",
            }
        ]
    },
    "id": "",
    "message": "",
    "status": 1,
    "total": 3
}
```
需要将原来的form字段值由请求地址改为请求数据。具体格式如下:

```json
{
  "form": {
    "name": {
      "type": "text",
      "label":"角色名称",
      "initValue": [],
      "readOnly": false,
      "maxLength": 6,
      "placeholder": "请输入不超过5个字符",
      "validator": [
        "noneEmptyFunc"
      ],
      "message":"不能为空"
    },
    "rolekey": {
      "type": "text",
      "label":"roleKey",
      "initValue": [],
      "readOnly": false,
      "validator": [
        "noneEmptyFunc"
      ],
      "message":"不能为空"
    },
    "state": {
      "type": "select",
      "label":"状态",
      "keyValue": [
        "在线",
        "离线"
      ],
      "initValue": [
        "0",
        "1"
      ],
      "readOnly": false,
      "validator": [
        "noneEmptyFunc"
      ],
      "message":"不能为空"
    },
    "description": {
      "type": "text",
      "label":"描述",
      "initValue": [],
      "readOnly": false,
      "validator": [
        "noneEmptyFunc"
      ],
      "message":"不能为空"
    }
  }
}
```
3.如何过滤数据，让其显示

```javascript
let metaInfo = this.state.form[this.state.headers[idx]];
newFilter(data,metaInfo);
export function newFilter(data,metaInfo) {
  switch(metaInfo.type) {
    case 'url':
      return <a href={data} target="_blank">{data}</a>
      break;
    case  'email':
       return <a href="mailto:"+ {data} target="_blank">{data}</a>
       break;
    case  'datetime':
      return  new Date(data.time).toLocaleString();
      break;
    case 'select':
      return metaInfo.keyValue[metaInfo.initValue.indexOf(data)];
      break;
    case  other:
      return data;
      break;
  }
}
```
 
