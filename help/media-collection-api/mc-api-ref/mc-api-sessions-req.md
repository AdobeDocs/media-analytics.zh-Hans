---
title: 会话请求
description: null
uuid: 9609192d-4f7f-4fb5-844f-ea89d47c4e30
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 会话请求{#sessions-request}

```
POST 
https://{uri}/api/v1/sessions
```

## URI参数

无

## 请求主体

请求主体必须是JSON，且必须具有与此示例请求主体相同的结构：

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

* `playerTime` (必需)
   * `playhead` - 必须以秒为单位，但它可以是一个浮点数。
   * `ts` - 时间戳，必须以毫秒为单位。
* `eventType` (必需)

   **有效值：**`sessionStart`
* `params` (必需)
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

`Location:` header —— 该部 `/api/v1/` 分提供API版本。 之后的部 `[…]sessions/` 分是会话ID。

## 响应代码

| HTTP 响应代码 | 描述 |
|---|---|
| 201 | 会话已创建 |
| 400 | 错误请求 |
| 500 | 服务器错误 |

