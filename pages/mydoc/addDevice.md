---
title: 添加设备
last_updated: 2019-10-21
sidebar: mydoc_sidebar
permalink: addDevice.html
folder: mydoc
---

添加设备到用户帐号下，返回添加成功的设备数据。

---

接口地址： https://{区域}-api.coolkit.cc:8080/api/user/device/add

请求方法： post

**请求参数：**

Headers：

|名称|参数值|是否必须|示例|
:-: | :-: | :-: | :-: | :-:
|Authorization|Bearer+空格+at|是|Bearer 174e8af6f5f10183647a6a4f5b51fdc6788f6172|
|Content-Type|application/json|是|application/json|

Body：

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|deviceid     |是  |string | 设备id |
|apikey     |是  |string | 设备apikey |
|name |是  |string | 设备名称 |
|subDeviceId |否  |string | 如果isSub:1， subDeviceId必填 |
|isSub |是  |string | 是否为子设备0：不是   1：是 |
|chipid |否  |string | 设备的芯片id |
|appid|是|string|APPID|
|nonce|是|string|8位字母数字随机数|
|ts|是|int|时间戳精确到秒|
|version|是|int|接口版本：8|


举例：

```Json
{
    "deviceid":"100000001",
    "apikey":"xxxx-xxxx-xxx",
    "name":"我的设备0001",
    "chipid": "zaqozs",
    "appid":"McFJj4Noke1mGDZCR1QarGW7P9Ycp0Vr",
    "ts":15452192511,
    "version":8,
    "nonce":"asbsedwq"

}
```

**响应参数：**

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|code |否  |Int | code码  |
|error |否  |string | 返回的异常信息  |
|device |是  |object | 设备信息，成功才返回  |

设备信息：

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|name |是  |string | 设备名称  |
|type |是  |string | 类型  |
|deviceid |是  |string | 设备id  |
|apikey |是  |string | 用户apikey  |
|extra |是  |object | 关联表引用信息  |
|onlineTime |是  |string | 设备最后上线时间  |
|ip |是  |string | 设备上线的ip地址  |
|location |是  |string | 设备上线的地方  |
|settings |是  |object | 设备配置信息  |
|groups |是  | [string] | 设备所属的分组ID，设备可以属于多个分组。如果不属于任何分组，则返回空数组[]  |
|params |是  |object | 设备参数  |
|online |是  |Boolean | 设备是否在线  |
|createdAt |是  |Date | 设备添加时间  |
|sharedBy |否  |object | 分享列表,分享方返回  |
|sharedTo |否  |object | 分享列表，被分享方返回  |
|devicekey |是  |string | 设备apikey  |
|deviceUrl |否  |string | 设备详情界面url  |
|brandName |是  |string | 品牌  |
|productModel |是  |string | 产品型号  |
|showBrand |是  |Boolean | 是否展示品牌和产品型号  |
|uiid |是  | Int | 设备ui的id  |


返回示例：

```
{
   "name": "我的设备00001",
   "deviceid"" "100000001"
   ...
}
```
