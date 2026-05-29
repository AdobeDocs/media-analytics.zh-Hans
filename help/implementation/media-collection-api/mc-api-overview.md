---
seo-title: Overview
title: 流媒体收集 API 概述
description: 了解媒体收集 API 以及您的播放器如何使用 RESTful HTTP 调用跟踪音频和视频事件。
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/79XLYzuvi3neUuCrt3LcGEwnnaR038-mWHMuSrY797M
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: 347
ht-degree: 91%

---

# 媒体收集 API 概述 {#overview}

媒体收集 API 是 Adobe 的客户端 Media SDK 的 RESTful 替代方法。 借助媒体收集 API，您的播放器可以使用 RESTful HTTP 调用来跟踪音频和视频事件。

媒体收集 API 本质上是一个适配器，可充当 Media SDK 的服务器端版本。 收集的流媒体跟踪数据指向相同的[Reporting and Analysis](/help/implementation/media-sdk/setup/media-reports-enable.md)。

## 媒体跟踪数据流 {#media-tracking-data-flows}

实施媒体收集 API 的媒体播放器会直接对媒体跟踪后端服务器进行 RESTful API 跟踪调用，而实施 Media SDK 的播放器会对播放器应用程序内的 SDK API 进行跟踪调用。 通过 Web 进行调用的一个效果是，实施媒体收集 API 的播放器需要处理 Media SDK 自动处理的一些进程。 （[媒体收集实施](mc-api-impl/mc-api-quick-start.md)中的详细信息。）

与在 Media SDK 播放器中捕获的跟踪数据相比，虽然使用媒体收集 API 捕获的跟踪数据采用不同的方式进行发送和初始处理，但这两个解决方案在后端使用相同的处理引擎。

![](assets/col_api_overview_simple.png)

## API 概述 {#api-overview}

**URI：**&#x200B;从您的 Adobe 代表处获取此信息。

**HTTP 方法：** POST，包含 JSON 请求正文。

### API 调用 {#mc-api-calls}

* **`sessions`—** 与服务器建立会话，并返回在后续 `events` 调用中使用的会话 ID。 应用程序会在跟踪会话开始时调用一次。

  `{uri}/api/v1/sessions`

* **`events`—** 发送媒体跟踪数据。

  `{uri}/api/v1/sessions/{session-id}/events`

### 请求正文 {#mc-api-request-body}

```json
{
    "playerTime": {
        "playhead": "{playhead position in seconds}",
        "ts": "{timestamp in milliseconds}"
    },
    "eventType": "{event-type}",
    "params": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "qoeData" : {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    },
    "customMetadata": {
        "{parameter-name}": "{parameter-value}",
        "{parameter-name}": "{parameter-value}"
    }
}
```

* `playerTime` — 对于所有请求而言，它是必选项。
* `eventType` — 对于所有请求而言，它是必选项。
* `params` — 对某些 `eventTypes` 而言，它是必选项；请检查 [JSON 验证架构](mc-api-ref/mc-api-json-validation.md)以确定哪些 eventTypes 是必选的，哪些是可选的。

* `qoeData` — 对于所有请求而言，它是可选项。
* `customMetadata` — 对于所有请求而言，它是可选项，但只通过 `sessionStart`、`adStart` 和 `chapterStart` 事件类型发送。

对于每个 `eventType`，都有一个公开可用的 [JSON 验证架构](mc-api-ref/mc-api-json-validation.md)，您应该使用它来验证参数类型，以及参数是特定事件的可选参数还是必选参数。

### 事件类型 {#mc-api-event-types}

有关每个SDK实现示例的事件类型的完整列表，请参阅[事件概述](/help/implementation/events/overview.md)。
