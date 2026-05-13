---
title: 验证事件请求
description: 了解如何使用 JSON 验证架构来验证事件请求。
uuid: 1fc92f21-b510-4c96-8ea2-47e819f4a96e
exl-id: a78739da-9fc9-42e3-9181-1887fb3dd357
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/dJKiHSFFHaoCvHZQUgPJFZagzcM3tZdhji3DuYJZiMs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 121
ht-degree: 72%

---

# 验证事件请求{#validating-event-requests}

在后端使用JSON架构验证每个事件类型的JSON请求正文。 当API调用的验证失败时，会使用错误消息填充HTTP响应正文。

可在此处公开访问每个事件类型的 JSON 验证架构：`{uri}/api/v1/schemas/{eventType}`（例如，`{uri}/api/v1/schemas/sessionEnd`）。 这些 JSON 验证架构是绝对的权威，其可为每个事件类型确定正确的请求正文参数。

例如，对 `sessionStart` 验证架构的请求响应类似于此示例（为方便阅读，此处格式略有改动）：

```
HTTP/1.1 200 OK
Server: nginx/1.13.5
Date: Thu, 18 Jan 2018 15:44:50 GMT
Content-Type: application/json
Content-Length: 2716
Connection: keep-alive

{
  "$schema":"https://json-schema.org/draft-04/schema#",
  "id":"https://alpha.hb-api.omtrdc.net/api/v1/schemas/sessionStart",
  "definitions":
  {
    "playerTime":
    {
      "type":"object","properties":
      {
        "playhead":
        {"type":"number"},
        "ts":
        {"type":"integer"}
      },
      "required":["playhead","ts"],
      "additionalProperties":false
    },
    "eventType":
    {
      "type":"string",
      "enum":[
        "sessionStart",
        "play",
        "ping",
        "bufferStart",
        "pauseStart",
        "sessionComplete",
        "bitrateChange",
        "error",
        "adBreakStart",
        "adBreakComplete",
        "adStart",
        "adComplete",
        "adSkip",
        "sessionEnd"
      ]
    },
    "qoeData":
    {
      "type":"object","properties":
      {
        "media.qoe.bitrate":
        {"type":"integer"},
        "media.qoe.droppedFrames":
        {"type":"integer"},
        "media.qoe.framesPerSecond":
        {"type":"integer"},
        "media.qoe.timeToStart":
        {"type":"integer"}
      },
      "required":[],
      "additionalProperties":false
    },
    "customMetadata":
    {
      "type":"object",
      "patternProperties":
      {
        "^[a-zA-Z0-9_\\.]+$":
        {"type":"string"}
      },
      "additionalProperties":false
    },
    "sessionStart":
    {
      "properties":
      {
        "eventType":
        {"type":"string","enum":["sessionStart"]},
        "playerTime":
        {"$ref":"#/definitions/playerTime"},
        "params":
        {"type":"object",
          "properties":
          {
            "appInstallationId":
            {"type":"string"},
            "analytics.trackingServer":
            {"type":"string"},
            "analytics.reportSuite":
            {"type":"string"},
            <...>
            "visitor.marketingCloudOrgId"],
            "additionalProperties":false
          },
          "customMetadata":
          {"$ref":"#/definitions/customMetadata"},
          "qoeData":
          {"$ref":"#/definitions/qoeData"}
        },
        "required":["eventType","playerTime","params"],
        "additionalProperties":false
      }
    },
    "type":"object","$ref":"#/definitions/sessionStart"
  }
}
```

>[!NOTE]
>
>无法进行会话级别验证，因为会话上下文在收集层中不可用。
