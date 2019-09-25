---
seo-title: 跟踪下载的内容
title: 跟踪下载的内容
uuid: 0718689d-9602-4e3f-833c-8297ae1d909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# 跟踪下载的内容{#track-downloaded-content}

## 概述 {#section_hcy_3pk_cfb}

“已下载内容”功能可在用户脱机时跟踪媒体使用情况。 例如，用户在移动设备上下载并安装了某个应用程序。然后，用户使用该应用程序将内容下载到设备上的本地存储中。为了跟踪此下载的数据，Adobe开发了“下载的内容”功能。 利用此功能，当用户从设备的存储中播放内容时，跟踪数据将存储在设备上，而不管设备的连接性如何。 当用户完成播放会话，并且设备返回联机状态时，存储的跟踪信息将在单个有效负荷内发送到Media Collection API后端。 在Media Collection API中，处理和报告会按正常方式进行。

对比两种方法：

* 在线

   使用这种实时方法，媒体播放器会在每个播放器事件上发送跟踪数据，并且每隔十秒（广告每隔一秒）向后端发送网络ping。

* 脱机（下载的内容功能）

   使用这种批处理方法，需要生成相同的会话事件，但这些事件会存储在设备上，直到它们作为单个会话发送到后端（请参阅以下示例）。

每种方法都有其优缺点：
* 在线场景实时跟踪；这要求在每次网络调用之前进行连接性检查。
* 脱机场景（“下载的内容”功能）只需要一个网络连接检查，但还需要设备上更大的内存占用。

## 实施 {#section_jhp_jpk_cfb}

### 事件架构

“下载的内容”功能只是（标准）在线Media Collection API的脱机版本，因此播放器批处理并发送到后端的事件数据必须使用与进行联机调用时使用的相同事件架构。 有关这些架构的信息，请参阅：
* [概述;](/help/media-collection-api/mc-api-overview.md)
* [验证事件请求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 活动顺序

* 批量有效负荷中的第一个事件必 `sessionStart` 须与Media Collection API中的常规情况一样。
* **必须在事`media.downloaded: true`** 件的标准元数据参数(`params` 键)中加入， `sessionStart` 以向后端指示您正在发送下载的内容。 如果发送下载的数据时此参数不存在或设置为false，则API将返回400个响应代码（错误请求）。 此参数将下载的内容与实时内容区分为后端。 (Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* 实施负责按照播放器事件发生的顺序正确地对事件进行存储。

### 响应代码

* 201 - Created: Successful Request；数据有效，已创建会话并且将对其进行处理。
* 400 - Bad Request；架构验证失败，所有数据均会被丢弃，并且不会处理任何会话数据。

## 与 Adobe Analytics 集成 {#section_cty_kpk_cfb}

在计算下载内容场景的Analytics启动／关闭调用时，后端会设置一个额外的Analytics字段，称为 `ts.` Theeses are timestamps for the first and last events received(start and complete)。 此机制允许将已完成的媒体会话放置在正确的时间点（即，即使用户连续数天未联机，媒体会话也会报告在实际查看内容时已发生）。 必须通过在 Adobe Analytics 端创建“可选时间戳报表包”_来启用此机制。_ 要启用时间戳可选报表包，请参阅 [可选时间戳。](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

## 会话对比示例 {#section_qnk_lpk_cfb}

```
[url]/api/v1/sessions
```

### 在线内容

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

