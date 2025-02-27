---
title: 查询设备状态
last_updated: 2019-10-31
sidebar: mydoc_sidebar
permalink: deviceStatusHttp.html
folder: mydoc
---

查询设备的状态，比如：定时器、分享、开关状态等。

---

接口地址： https://{区域}-api.coolkit.cc:8080/api/user/device/status

请求方法： get

**请求参数：**

Headers：

|名称|参数值|是否必须|示例|
:-: | :-: | :-: | :-: | :-:
|Authorization|Bearer+空格+at|是|Bearer 174e8af6f5f10183647a6a4f5b51fdc6788f6172|
|Content-Type|application/json|是|application/json|

Params：

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|deviceid |是  |String |设备id  |
|apikey |是  |String |设备apikey|
|params |否  |String | 参数列表，指定要查询的参数，用\|符号分隔（需要做URI encode）。如果为空，表示查询所有参数    |
|appid|是|string|APPID|
|nonce|是|string|8位字母数字随机数|
|ts|是|int|时间戳精确到秒|
|version|是|int|接口版本：8|

举例说明：

需要查询switch和timers，请求url为:

```Json
https://cn-api.coolkit.cc:8080/api/user/device/status?deviceid=1234abcd&params=switch|timers&appid=McFJj4Noke1mGDZCR1QarGW7P9Ycp0Vr&ts=1558004249&version=8&nonce=asbsedwq
```

响应参数

|参数名|必选|类型|说明|
|:----    |:---|:----- |-----   |
|error |是  |Int |状态码  |
|errmsg |否  |String | 错误说明，error非0时返回 |
|params |否  |Params | 参数  |

状态码：

    0：操作成功
    400：参数错误
    401：认证失败
    403：无权限
    500：服务器内部错误


Params说明：

返回对应参数的json值，如果没有查询到任何参数值，则返回空对象，例如：

```Json
{ "error": 0,"params": { "switch": "on" } }
```
没有查询到任何参数：

```Json
{ "error": 0,"params": {} }
```