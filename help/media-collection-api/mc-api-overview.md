---
seo-title: 概述
title: 概述
uuid: c14bdbef-5846-4d31-8a14-8e9e9e9c9861
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 概述{#overview}

媒体收集 API 是 Adobe 针对客户端 Media SDK 的 RESTful 替代方案。借助媒体收集 API，播放器可以使用 RESTful HTTP 调用跟踪音频和视频事件。Media Collection API提供了Media SDK的相同实时跟踪功能，此外还有一个功能：

* **下载的内容跟踪**

   此功能使您能够在用户脱机时跟踪媒体，通过本地存储事件数据，直至用户设备在线返回为止。（有关详细信息，请参阅[跟踪下载的内容](track-downloaded-content.md)。）

媒体收集 API 本质上是一个适配器，充当 Media SDK 的服务器端版本。这意味着媒体SDK文档的某些方面也与Media Collection API相关。For example, both solutions use the same [Audio and Video Parameters](/help/metrics-and-metadata/audio-video-parameters.md), and the collected Audio and Video tracking data leads to the same [Reporting and Analysis.](/help/media-reports/media-reports-enable.md)

## 媒体跟踪数据流 {#section_pwq_n34_qbb}

实现Media Collection API的媒体播放器直接将RESTful API跟踪调用定向到媒体跟踪后端服务器，而实现Media SDK的播放器则对播放器应用程序内的SDK API进行跟踪调用。通过 Web 进行调用的一个效果是，实施媒体收集 API 的播放器需要处理 Media SDK 自动处理的一些进程。(Details in [Media Collection Implementation.](mc-api-impl/mc-api-quick-start.md))

使用Media Collection API捕获的跟踪数据会发送并最初处理不同于Media SDK播放器中捕获的跟踪数据，但后端的同一处理引擎会用于这两种解决方案。

![](assets/col_api_overview_simple.png)

## API Overview {#section_y4n_mcl_kcb}

**URI：**&#x200B;从 Adobe 代表处获得此信息。

**HTTP 方法：** POST，带有 JSON 请求正文。

### API Calls {#mc-api-calls}

* **`sessions`-** 与服务器建立会话，并返回后续 `events` 调用中使用的会话ID。应用程序会在跟踪会话开始时调用一次。

   ```
   {uri}/api/v1/sessions
   ```

* **`events`-** 发送媒体跟踪数据。

   ```
   {uri}/api/v1/sessions/{session-id}/events
   ```

### Request Body {#mc-api-request-body}

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

* `playerTime` - 所有请求都必须具有强制项。
* `eventType` - 所有请求都必须具有强制项。
* `params` - 对某些 `eventTypes` 而言，它是必选项；请检查 [JSON 验证架构](mc-api-ref/mc-api-json-validation.md)以确定哪些 eventTypes 是必选的，哪些是可选的。

* `qoeData` - 对所有请求都可选。
* `customMetadata` - 可选为所有请求，但仅随 `sessionStart`和 `adStart``chapterStart` 事件类型一起发送。

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

