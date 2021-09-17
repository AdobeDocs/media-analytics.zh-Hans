---
title: 流媒体收集API — 会话请求端点
description: “媒体收集API会话请求端点参数和响应是什么？”
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
exl-id: f55f5838-610f-4f82-b3c5-72165ea2c86b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ef881900766be773256e2732953f7b63c5d488fa
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 46%

---

# 会话请求{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI 参数

无

## 请求正文

请求正文必须是 JSON，且还必须具有与此示例请求正文相同的结构：

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "sessionStart", 
    "params": { 
        "media.playerName": "sample-html5-api-player", 
        "analytics.trackingServer": "<your-aa-tracking-server>", 
        "analytics.reportSuite": "<your-aa-rsid>", 
        "analytics.visitorId": "<your-userId>", 
        "media.contentType": "VOD", 
        "media.length": 60.39333333333333, 
        "media.id": "MA API Sample Player", 
        "visitor.marketingCloudOrgId": "<your-org-id>", 
        "media.name": "ClickMe", 
        "media.channel": "sample-channel", 
        "media.sdkVersion": "va-api-0.0.0", 
        "analytics.enableSSL": false 
    }, 
    "customMetadata": { 
        "myCustomData": "<your metadata>", 
        "myCustomData2": "<your metadata>", 
        ... 
    }, 
    "qoeData": { 
        "param1": "<your param-value>", 
        "param2": "<your param-value>", 
        ... 
    } 
}
```

* `playerTime`（必需）
   * `playhead`  — 如果内容是实时的，则播放头必须是一天中的当前秒，0  &lt;>如果记录了内容，则播放头必须是内容的当前秒数，0 &lt;=播放头&lt;内容长度。 该值可以是浮点数。
   * `ts`  — 时间戳；必须以毫秒为单位；协调世界时(UTC)。
* `eventType`（必需）

   **有效值：**`sessionStart`
* `params`（必需）
* `customMetadata`（可选）
* `qoeData`（可选）

## 响应

```
HTTP/1.1 201 Created 
Server: nginx/1.13.5 
Date: Wed, 06 Dec 2017 19:14:51 GMT 
Content-Type: application/octet-stream 
Content-Length: 0 
Location: /api/v1/sessions/bfcca2ca597a3c71bc03b4ce357833ad02b3570d262ecd0c595fcf8f2ae4df58 
Access-Control-Allow-Origin: * 
Access-Control-Allow-Methods: OPTIONS,POST,PUT 
Access-Control-Allow-Headers: Content-Type 
Access-Control-Expose-Headers: Location 
Age: 0 
Via: 1.1 wsg.sanjose08
```

`Location:` 标头 - `/api/v1/` 部分提供 API 版本。`[…]sessions/` 之后的部分是会话 ID。

## 响应代码

| HTTP 响应代码 | 描述 |
|---|---|
| 201 | 会话已创建 |
| 400 | 错误请求 |
| 500 | 服务器错误 |
