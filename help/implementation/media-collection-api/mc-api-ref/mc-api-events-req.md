---
title: 流媒体收集 API – 事件请求端点
description: 媒体收集API事件请求端点参数和响应是什么？
uuid: b237f0a0-dc29-418b-89ee-04c596a27f39
exl-id: ee0dd8a6-1529-4258-af12-0e2f5948ec38
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 95%

---

# 事件请求{#events-request}

`POST https://{uri}/api/v1/sessions/{sid}/events`

## URI 参数

`sid`：从[会话请求](mc-api-sessions-req.md)返回的会话 ID。

## 请求正文

请求正文必须是 JSON，且还必须具有与此示例请求正文相同的结构：

```json
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

* `playerTime`（必需）
   * `playhead` - 必须以秒为单位，但它可以是一个浮点数。
   * `ts` - 时间戳，必须以毫秒为单位。
* `eventType`（必需）
* `params`（可选）
* `customMetadata`（可选，只通过 `adStart` 和 `chapterStart` 事件类型发送）
* `qoeData`（可选）

有关此版本的有效事件类型列表，请参阅[事件类型和描述](mc-api-event-types.md)。

>[!IMPORTANT]
>
>***广告跟踪 -**&#x200B;您只能跟踪`adBreak`* 内的广告。
>
>在广告头尾没有 `adBreakStart` 和 `adBreakComplete`“书挡”的情况下，`adStart` 和 `adComplete` 事件将被忽略，并且会将相应的广告持续时间作为主内容持续时间进行跟踪。这可能会对 Adobe Analytics 中可用的聚合数据产生重大影响。

## 响应

```text
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
| **204** | **无内容。**<br/><br/>心跳调用成功。 | 不适用 |
| **400** | **错误请求。**<br/><br/>请求格式不正确。 | 检查 [JSON 验证架构](mc-api-json-validation.md)以了解请求类型。 |
| **404** | **未找到。**<br/><br/>在后端服务中找不到媒体会话的会话 ID。 | 客户端应用程序应使用[会话请求](mc-api-sessions-req.md) API 创建另一个媒体会话并报告对它的跟踪。 |
| **410** | **不存在。**<br/><br/>在后端服务中找到媒体会话，但客户端无法再对该会话报告活动。 | 客户端应用程序应使用[会话请求](mc-api-sessions-req.md) API 创建另一个媒体会话并报告对它的跟踪。 |
| **500** | **服务器错误** | 不适用 |
