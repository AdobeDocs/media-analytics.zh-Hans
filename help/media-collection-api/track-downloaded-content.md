---
title: 跟踪下载的内容
description: null
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: be68a7abf7d5fd4cc725b040583801f2308ab066
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 56%

---


# 跟踪下载的内容{#track-downloaded-content}

## 概述 {#overview}

通过“下载的内容”功能，可以跟踪用户处于脱机状态下的媒体使用情况。例如，用户下载并在移动设备上安装应用程序，然后使用该应用程序将内容下载到设备上的本地存储。 为了跟踪下载的数据，Adobe开发了“下载的内容”功能。 利用此功能，当用户从设备存储播放内容时，跟踪数据将存储在设备上，而不管设备的连接性如何。 当用户完成播放会话并且设备返回联机状态时，存储的跟踪信息将在单个有效负荷内发送到Media Collection API后端。 然后，在Media Collection API中像往常一样处理和报告存储的跟踪信息。

对比两种方法：

* 联机

   使用这种实时方法，媒体播放器会为每个播放器事件发送跟踪数据，每十秒（广告每一秒）发送一次网络ping，逐个发送到后端。

* 脱机（“下载的内容”功能）

   使用这种批处理方法，需要生成相同的会话事件，但这些会话会存储在设备上，直到作为单个会话发送到后端（请参阅以下示例）。

每种方法各有其优点和缺点：
* 联机方案会实时跟踪；这要求在发出每次网络调用之前进行网络连接检查。
* 脱机方案（“下载的内容”功能）只需要进行一次网络连接检查，但却需要占用更大的设备内存。

## 实施 {#implementation}

### 支持的平台

iOS和Android移动设备支持内容跟踪。

### 事件架构

“下载的内容”功能是（标准）在线媒体集合API的脱机版本，因此您的播放器批处理并发送到后端的事件数据必须使用与进行在线调用时相同的事件模式。 有关这些架构的信息，请参阅：
* [概述；](/help/media-collection-api/mc-api-overview.md)
* [验证事件请求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件的顺序

* 与媒体收集 API 中的常规情况一样，批量负载中的第一个事件必须为 `sessionStart`。
* **您必须将`media.downloaded: true`**包含在`params`事件的标准元数据参数（`sessionStart`键）中，以向后端指示您正在发送下载的内容。当您发送下载的数据时，如果此参数不存在或设置为 false，则 API 将返回 400 响应代码（错误请求）。在将内容发送到后端时，此参数会将下载的内容与实时内容区分开。If`media.downloaded: true`is set on a live session, this will likewise result in a 400 response from the API.
* 实施负责按照播放器事件发生的顺序正确地对事件进行存储。

### 响应代码

* 201 - 已创建：请求成功；数据有效，且会话已创建并将进行处理。
* 400 - 错误请求；架构验证失败，所有数据都被丢弃，不会处理任何会话数据。

## 与 Adobe Analytics 集成 {#integration-with-adobe-analtyics}

在计算“下载的内容”方案的 Analytics 开始/结束调用时，后端会设置一个名为 `ts.` 的额外 Analytics 字段。这些是收到的第一个事件和最后一个事件（开始和结束）的时间戳。此机制可将已结束的媒体会话放置在正确的时间点（也就是说，即便用户几天都没有联机，也会报告在实际查看内容时所发生的媒体会话）。必须通过在 Adobe Analytics 端创建“可选时间戳报表包”来启用此机制。__&#x200B;要启用可选时间戳报表包，请参阅[可选时间戳](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/timestamp-optional.html)。

## 会话对比示例 {#sample-session-comparison}

```
[url]/api/v1/sessions
```

### 联机内容

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

### 下载的内容

```
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478},  
    params:{
        "media.downloaded": true
        ...
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

## 媒体跟踪器API参考

有关如何配置已下载内容的信息，请参阅媒 [体跟踪器API参考](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#media-api-reference)。
