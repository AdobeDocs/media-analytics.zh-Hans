---
seo-title: 跟踪下载的内容
title: 跟踪下载的内容
uuid: 0718689d-9602-4e3f-833c-8297aae1d909
translation-type: tm+mt
source-git-commit: b9298de98eeb85c0e2ea0a456c98eac479f43b51

---


# 跟踪下载的内容{#track-downloaded-content}

## 概述 {#section_hcy_3pk_cfb}

下载的内容功能可在用户离线时跟踪媒体消耗。例如，用户在移动设备上下载并安装了某个应用程序。然后，用户使用该应用程序将内容下载到设备上的本地存储中。为了跟踪下载的数据，Adobe开发了“下载的内容”功能。使用此功能，当用户从设备的存储播放内容时，跟踪数据存储在设备上，而不管设备的连接性如何。当用户完成播放会话，且设备在线返回时，存储的跟踪信息将发送到一个负载中的Media Collection API后端。从此处，处理和报告在Media Collection API中按常规进度进行。

对比两种方法：

* 在线

   通过这种实时方法，媒体播放器在每个播放器事件后发送跟踪数据，并且它每10秒发送一次网络ping，逐个发送到后端。

* 脱机(下载的内容功能)

   使用此批处理方法，需要生成相同的会话事件，但它们存储在设备上，直到它们作为单一会话发送到后端(请参阅下面的示例)。

每种方法都有其优缺点：
* 实时在线方案跟踪；这需要在每次网络调用之前进行连接检查。
* 脱机场景(下载的内容功能)仅需要一个网络连接检查，但设备上还需要较大的内存占用。

## 实施 {#section_jhp_jpk_cfb}

### 活动架构

下载的内容功能只是(标准)在线媒体收集API的脱机版本，因此玩家批次和发送到后端的活动数据必须使用与进行在线呼叫时使用的相同的事件架构。有关这些架构的信息，请参阅：
* [概述;](/help/media-collection-api/mc-api-overview.md)
* [验证事件请求](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

### 活动顺序

* 批有效负荷中的第一个事件必须与Media `sessionStart` Collection API相同。
* **您必须在`media.downloaded: true`** 活动的标准元数据参数(`params` 密钥) `sessionStart` 中包含以指示您正在发送下载内容的后端。如果在发送下载的数据时此参数不存在或设置为false，则API将返回400响应代码(不良请求)。此参数将下载的与实时内容区分开来。(Note that if `media.downloaded: true` is set on a live session, this will likewise result in a 400 response from the API.)
* 实施负责按照播放器事件发生的顺序正确地对事件进行存储。

### 响应代码

* 201 - Created: Successful Request；数据有效，已创建会话并且将对其进行处理。
* 400 - Bad Request；架构验证失败，所有数据均会被丢弃，并且不会处理任何会话数据。

## 与 Adobe Analytics 集成 {#section_cty_kpk_cfb}

在计算下载的内容情景的Analytics开始/关闭调用时，后端设置额外的Analytics字段，即 `ts.` 接收的第一个和最后一个事件的时间戳(开始和完成)。此机制允许将完成的媒体会话放置在正确的时间点(即，即使用户未在线返回几天，媒体会话也会在实际查看内容时进行报告)。必须通过在 Adobe Analytics 端创建“可选时间戳报表包”_来启用此机制。_ 要启用时间戳可选报告套件，请参阅 [时间戳可选。](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/timestamp-optional.html)

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

