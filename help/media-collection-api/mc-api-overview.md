---
seo-title: 概述
title: 流媒体收集 API 概述
description: 了解媒体收集 API 以及您的播放器如何使用 RESTful HTTP 调用跟踪音频和视频事件。
uuid: c14bdbef-5846-4d31-8a14-8e9e0e9c9861
exl-id: 58430636-7fab-433a-8ead-52ccaa45d920
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '357'
ht-degree: 100%

---

# 概述{#overview}

媒体收集 API 是 Adobe 的客户端 Media SDK 的 RESTful 替代方法。借助媒体收集 API，您的播放器可以使用 RESTful HTTP 调用来跟踪音频和视频事件。

媒体收集 API 本质上是一个适配器，可充当 Media SDK 的服务器端版本。这意味着，Media SDK 文档的某些方面也与媒体收集 API 相关。例如，两个解决方案使用了相同的[流媒体参数](/help/metrics-and-metadata/audio-video-parameters.md)，并且收集的流媒体跟踪数据最终获得相同的[报表和分析](/help/media-reports/media-reports-enable.md)。

## 媒体跟踪数据流 {#media-tracking-data-flows}

实施媒体收集 API 的媒体播放器会直接对媒体跟踪后端服务器进行 RESTful API 跟踪调用，而实施 Media SDK 的播放器会对播放器应用程序内的 SDK API 进行跟踪调用。通过 Web 进行调用的一个效果是，实施媒体收集 API 的播放器需要处理 Media SDK 自动处理的一些进程。（[媒体收集实施](mc-api-impl/mc-api-quick-start.md)中的详细信息。）

与在 Media SDK 播放器中捕获的跟踪数据相比，虽然使用媒体收集 API 捕获的跟踪数据采用不同的方式进行发送和初始处理，但这两个解决方案在后端使用相同的处理引擎。

![](assets/col_api_overview_simple.png)

## API 概述 {#api-overview}

**URI：**&#x200B;从您的 Adobe 代表处获取此信息。

**HTTP 方法：** POST，包含 JSON 请求正文。

### API 调用 {#mc-api-calls}

* **`sessions`—** 与服务器建立会话，并返回在后续 `events` 调用中使用的会话 ID。应用程序会在跟踪会话开始时调用一次。

   ```
   {uri}/api/v1/sessions
   ```

* **`events`—** 发送媒体跟踪数据。

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### 请求正文 {#mc-api-request-body}

```
{
    "playerTime": {
        "playhead": {playhead position in seconds},
        "ts": {timestamp in milliseconds}
    },
    "eventType": {event-type},
    "params": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "qoeData" : {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
    },
    "customMetadata": {
        {parameter-name}: {parameter-value},
        ...
        {parameter-name}: {parameter-value}
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

* `sessionStart`
* `play`
* `ping`
* `pauseStart`
* `bufferStart`
* `adStart`
* `adComplete`
* `adSkip`
* `adBreakStart`
* `adBreakComplete`
* `chapterStart`
* `chapterSkip`
* `chapterComplete`
* `sessionEnd`
* `sessionComplete`
