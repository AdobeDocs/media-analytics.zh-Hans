---
seo-title: 跟踪下载的内容
title: 跟踪下载的内容
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: 501bbfe8b44a2a8e9b2ac2caab49b2317f9ea0f3

---


# 跟踪下载的内容{#track-downloaded-content}

## 概述 {#section_hcy_3pk_cfb}

Downloaded Content API 提供了在用户处于脱机状态时跟踪媒体使用情况的功能。例如，用户在移动设备上下载并安装了某个应用程序。然后，用户使用该应用程序将内容下载到设备上的本地存储中。为了跟踪这些下载的数据，Adobe 开发了 Downloaded Content API。通过使用此 API，当用户播放设备存储中的内容时，便会在设备中存储跟踪数据，而不考虑设备是否连接到网络。当用户完成播放会话且设备处于联机状态时，存储的跟踪信息将发送到一个负载中的Media Collection API后端。之后，将在此 API 所基于的媒体收集 API 中照常进行处理和报告。

对比两种方法：

* 媒体收集 API

   通过这种实时方法，媒体播放器在每个播放器事件后发送跟踪数据，并且它每10秒发送一次网络ping，逐个发送到后端。

* 下载的内容API

   通过这种批处理方法，需要生成相同的会话事件，但存储在设备上，直到它们作为单一会话发送到后端(请参阅下面的示例)。

每种方法都有其优缺点：媒体收集 API 可实时跟踪，但需要在每次网络调用之前检查网络连接性；Downloaded Content API 只需检查一次网络连接性，但却需要在设备上占用较大的内存。

## 实施 {#section_jhp_jpk_cfb}

### 活动架构

下载的内容API基于Media Collection API，因此您的播放器批次和发送的事件数据要求与Media Collection API中一样使用相同的事件架构。For information on these schemas, see: [Overview;](../media-collection-api/mc-api-overview.md) and [Validating event requests.](../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 活动顺序

* 批处理负载中的第一个事件必须是 `sessionStart`。
* You must include `media.downloaded: true` in the standard metadata parameters ( `params` key) on the `sessionStart` event. 如果此参数不存在或设置为 false，则 Downloaded Content API 将返回 400 响应代码（错误请求）。这样，后端可以区分下载的内容和实时内容，并相应地进行处理。（请注意，如果在实时会话中设置为 `media.downloaded: true`，也将同样导致媒体收集 API 返回 400 响应。）

* 实施负责按照播放器事件发生的顺序正确地对事件进行存储。

### 响应代码

* 201 - Created: Successful Request；数据有效，已创建会话并且将对其进行处理。
* 400 - Bad Request；架构验证失败，所有数据均会被丢弃，并且不会处理任何会话数据。

## 与 Adobe Analytics 集成 {#section_cty_kpk_cfb}

When computing the Analytics start/close calls for the downloaded content scenario, the back-end sets an extra Analytics field called `ts`. 这些是收到的第一个和最后一个事件(开始和完成)的时间戳。此机制允许将完成的媒体会话放置在正确的时间点(即，即使用户未在线返回几天，媒体会话也会在实际查看内容时进行报告)。必须通过在 Adobe Analytics 端创建“可选时间戳报表包”**&#x200B;来启用此机制。To enable a timestamp optional report suite, see [Timestamps Optional.](https://marketing.adobe.com/resources/help/en_US/reference/timestamp-optional.html)

## 会话对比示例 {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### 媒体收集 API

```
{ 
  eventType: "sessionStart", 
  playerTime: { 
    playhead: 0,  
    ts: 1529997923478},  
  params: { /* Standard metadata parameters as documented */ },  
  customMetadata: { /* Custom metadata parameters as documented */ },  
  qoeData: { /* QoE parameters as documented */ } 
}
```

### 下载的内容API

```
[{ 
    eventType: "sessionStart", 
    playerTime:{playhead: 0, ts: 1529997923478},  
    params:{
        "media.downloaded": true
    }, 
    customMetadata:{},  
    qoeData:{} 
}, 
    {eventType: "play", playerTime:
        {playhead: 0,  ts: 1529997928174}}, 
    {eventType: "ping", playerTime:
        {playhead: 10, ts: 1529997937503}}, 
    {eventType: "ping", playerTime:
        {playhead: 20, ts: 1529997947533}}, 
    {eventType: "ping", playerTime:
        {playhead: 30, ts: 1529997957545},}, 
    {eventType: "sessionComplete", playerTime:
        {playhead: 35, ts: 1529997960559} 
}]
```

