---
title: 事件请求
description: null
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 事件请求{#events-request}

```
POST 
https://{uri}/api/v1/sessions/{sid}/events 
```

## URI参数

`sid`:会话ID从会话请求 [返回。](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)

## 请求主体

请求主体必须是JSON，且必须具有与此示例请求主体相同的结构：

```
{ 
    "playerTime": { 
        "playhead": 0, 
        "ts": 1509045324153 
    }, 
    "eventType": "{event-type}", 
    "params": {}, 
    "qoeData": {}, 
    "customMetadata": {} 
}
```

* `playerTime` (必需)
   * `playhead` - 必须以秒为单位，但它可以是一个浮点数。
   * `ts` - 时间戳，必须以毫秒为单位。
* `eventType` (必需)
* `params`（可选）
* `customMetadata` (可选；仅发送(含 `adStart` 和活 `chapterStart` 动类型)
* `qoeData`（可选）

For a list of valid event types for this release, see [Event types and descriptions.](/help/media-collection-api/mc-api-ref/mc-api-event-types.md)

>[!IMPORTANT]
>
>***广告跟踪**-您只能跟踪广告内部`adBreak`*。
>
>在广告头尾没有 `adBreakStart` 和 `adBreakComplete`“书挡”的情况下，`adStart` 和 `adComplete` 事件将被忽略，并且会将相应的广告持续时间作为主内容持续时间进行跟踪。这可能会对 Adobe Analytics 中可用的聚合数据产生重大影响。

## 响应

```
HTTP/1.1 204 No Content 
Server nginx/1.13.5 
Date Thu, 26 Oct 2017 19:15:24 GMT 
Connection keep-alive 
Access-Control-Allow-Origin * 
Access-Control-Allow-Methods OPTIONS,POST,PUT 
Access-Control-Allow-Headers Content-Type 
Access-Control-Expose-Headers Location
```

## HTTP 响应代码

| HTTP 响应代码 | 描述 | 客户端操作项 |
|---|---|---|
| **204** | **无内容。**<br/><br/>心率调用成功。 | 不适用 |
| **400** | **错误请求。**<br/><br/>请求格式不正确。 | 请查看 [JSON 验证架构](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)以了解请求类型。 |
| **404** | **未找到。** 在 <br/><br/>后端服务中找不到媒体会话的会话ID。 | 客户端应用程序应使用[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API 来创建另一个媒体会话，并报告对该会话的跟踪。 |
| **410** | **已过期。** 在后 <br/><br/>端服务中找到媒体会话，但客户端不再报告其活动。 | 客户端应用程序应使用[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) API 来创建另一个媒体会话，并报告对该会话的跟踪。 |
| **500** | **服务器错误** | 不适用 |

