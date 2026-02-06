---
title: 如何跟踪流媒体服务中的离线下载内容
description: 了解如何使用“下载的内容”功能在用户离线时跟踪媒体消费情况。
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
exl-id: 82d3e5d7-4f88-425c-8bdb-e9101fc1db92
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 98%

---

# 跟踪下载的内容{#track-downloaded-content}

## 概述 {#overview}

通过“下载的内容”功能，可在用户离线时跟踪媒体消费情况。例如，用户在移动设备上下载并安装某个应用程序，然后使用该应用程序将内容下载到设备上的本地存储中。为了跟踪下载的数据，Adobe 开发了“下载的内容”功能。通过使用此功能，当用户播放设备存储中的内容时，便会在设备中存储跟踪数据，无论设备是否连接到网络。当用户结束播放会话，并且设备重新联机时，存储的跟踪信息便会在单个负载内发送到媒体收集 API 后端。然后，可在 Media Collection API 中像往常一样处理和报告存储的跟踪信息。

对比两种方法：

* 联机

  使用这种实时方法时，媒体播放器会发送每个播放器事件的跟踪数据，每 10 秒（广告为每 1 秒）就会发送一次网络 ping，并且是逐一发送到后端。

* 脱机（“下载的内容”功能）

  使用这种批处理方法时，需要生成相同的会话事件，但是这些事件会存储在设备上，直至它们作为单个会话发送到后端为止（请参阅以下示例）。

每种方法各有其优点和缺点：
* 联机方案会实时跟踪；这要求在发出每次网络调用之前进行网络连接检查。
* 脱机方案（“下载的内容”功能）只需要进行一次网络连接检查，但却需要占用更大的设备内存。

## 实施 {#implementation}

### 支持的平台

iOS 和 Android 移动设备支持内容跟踪。

### 事件架构

“下载的内容”功能是（标准）联机媒体收集 API 的脱机版本，因此，播放器进行批处理并发送到后端的事件数据必须使用进行联机调用时所用的相同事件架构。有关这些架构的信息，请参阅：
* [概述;](/help/implementation/media-collection-api/mc-api-overview.md)
* [验证事件请求](/help/implementation/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 事件的顺序

* 与媒体收集 API 中的常规情况一样，批量负载中的第一个事件必须为 `sessionStart`。
* **您必须将`media.downloaded: true`** 包含在 `params` 事件的标准元数据参数（`sessionStart` 键）中，以向后端指示您正在发送下载的内容。当您发送下载的数据时，如果此参数不存在或设置为 false，则 API 将返回 400 响应代码（错误请求）。在将内容发送到后端时，此参数会将下载的内容与实时内容区分开。如果在实时会话中设置了 `media.downloaded: true`，则同样会导致 API 返回 400 响应。
* 实施负责按照播放器事件发生的顺序正确地对事件进行存储。

### 响应代码

* 201 - 已创建：请求成功；数据有效，且会话已创建并将进行处理。
* 400 - 错误请求；架构验证失败，所有数据都被丢弃，不会处理任何会话数据。

## 与 Adobe Analytics 集成 {#integration-with-adobe-analtyics}

在计算“下载的内容”方案的 Analytics 开始/结束调用时，后端会设置一个名为 `ts.` 的额外 Analytics 字段。这些是收到的第一个事件和最后一个事件（开始和结束）的时间戳。此机制可将已结束的媒体会话放置在正确的时间点（也就是说，即便用户几天都没有联机，也会报告在实际查看内容时所发生的媒体会话）。必须通过在 Adobe Analytics 端创建“可选时间戳报表包”来启用此机制。__&#x200B;要启用可选时间戳报表包，请参阅[可选时间戳](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/timestamp-optional.html?lang=zh-Hans)。

## 会话对比示例 {#sample-session-comparison}

### 联机内容

```
POST /api/v1/sessions HTTP/1.1

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
POST /api/v1/downloaded HTTP/1.1

[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },  
    params:{...},
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

### 弃用通知

>[!IMPORTANT]
>
>以前还可将“下载的内容”发送到 `/api/v1/sessions` API。已&#x200B;**弃用**&#x200B;此方式跟踪下载的内容，并且未来将&#x200B;**删除**&#x200B;此方式。


`/api/v1/sessions` API 将仅接受会话初始化事件。使用新 API 时不再需要以前强制的 `media.downloaded` 标志。我们强烈建议将 `/api/v1/downloaded` API 用于“下载的内容”的新实施，并且更新依赖旧 API 的现有实施。


```
POST /api/v1/sessions HTTP/1.1
[{
    eventType: "sessionStart",
    playerTime:{
      playhead: 0,
      ts: 1529997923478
    },
    params:{
        "media.downloaded": true,
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

## 媒体跟踪器 API 参考

有关如何配置已下载内容的信息，请参阅媒[体跟踪器 API 参考](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)。
