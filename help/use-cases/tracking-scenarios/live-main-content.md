---
title: 实时主内容
description: 查看如何使用媒体 SDK 跟踪实时内容的示例。
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
exl-id: f6a00ffd-da6a-4d62-92df-15d119cfc426
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oOshJZEQmXqgNh5l10-qhLMO8dmph6Tz9mpH0a4FePU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 590
ht-degree: 98%

---

# 实时主内容{#live-main-content}

## 场景 {#scenario}

在此方案中，有一个实时资源，在加入实时流后 40 秒内不播放任何广告。

| 触发器 | 心跳方法 | 网络调用 | 注释   |
|---|---|---|---|
| 用户点击&#x200B;**[!UICONTROL 播放]** | `trackSessionStart` | Analytics 内容开始，心跳内容开始 | 这可以是用户点击&#x200B;**[!UICONTROL 播放]**&#x200B;或自动播放事件。 |
| 播放媒体的第一帧。 | `trackPlay` | 心跳内容播放 | 此方法将触发计时器。 只要继续播放，就会每 10 秒发送一次心跳。 |
| 播放内容。 |  | 内容心跳 |  |
| 会话结束。 | `trackSessionEnd` |  | `SessionEnd` 是指观看会话结束。 即使用户没有观看至媒体结束，也必须调用此 API。 |

## 参数 {#parameters}

您在 Adobe Analytics 内容开始调用中看到的很多值，同样也会在心率内容开始调用中看到。 您还会看到许多其他参数，Adobe 使用这些参数填充 Adobe Analytics 中的各种媒体报表。 我们不会在这里涵盖所有这些变量，而是只列出一些非常重要的变量。

### 心跳内容开始

| 参数 | 值 | 注释 |
|---|---|---|
| `s:sc:rsid` | &lt;您的 Adobe 报表包 ID> |  |
| `s:sc:tracking_serve` | &lt;您的 Analytics 跟踪服务器 URL> |  |
| `s:user:mid` | `s:user:mid` | 应当匹配 Adobe Analytics 内容开始调用中的中间值 |
| `s:event:type` | &quot;start&quot; |  |
| `s:asset:type` | &quot;main&quot; |  |
| `s:asset:mediao_id` | &lt;您的媒体名称> |  |
| `s:stream:type` | 实时 |  |
| `s:meta:*` | 可选 | 对媒体设置的自定义元数据 |

## 内容心率 {#content-heartbeats}

在媒体播放期间，有一个计时器将会每 10 秒发送一次主内容的一个或多个心率（或 ping），每 1 秒发送一次广告的一个或多个心率（或 ping）。 这些心跳将包含有关播放、广告、缓冲和许多其他内容的信息。 每个心跳的确切内容不在本文档涵盖的范围之内，验证的关键内容是在持续播放期间始终触发心跳。

在内容心跳中，查找一些特定的内容：

| 参数 | 值 | 注释 |
|---|---|---|
| `s:event:type` | &quot;play&quot; |  |
| `l:event:playhead` | &lt;播放头位置> 例如，50、60、70 | 这应该反映播放头的当前位置。 |

## 心跳内容结束 {#heartbeat-content-complete}

由于实时流从不结束，因此这种情况下不会有结束调用。

## 播放头值设置

对于 LIVE 流，您需要将播放头值设置为自当天 UTC 午夜开始的秒数，以便在报告中，分析人员可以确定用户在 24 小时视图内何时加入和离开 LIVE 流。

### 开始时

对于 LIVE 媒体，当用户开始播放流时，您需要将 `l:event:playhead` 设置为自当天 UTC 午夜以来的秒数。 这与 VOD 相反，在 VOD 中，您需要将播放头设置为“0”。 请注意：使用进度标记时，需要内容持续时间，并且播放头需要更新为从媒体项目开始的秒数，从 0 开始。

例如，假设实时流事件从午夜开始，并且持续 24 小时（`a.media.length=86400`；`l:asset:length=86400`）。 然后，假设用户在12:00pm开始播放该LIVE流。 在这种场景下，您应该将 `l:event:playhead` 设置为 43200（自当天 UTC 午夜起 12 小时，以秒为单位）。

### 暂停时

当用户暂停播放时，必须应用在播放开始时所应用的相同“实时播放头”逻辑。 当用户返回播放 LIVE 流时，您必须根据自午夜 UTC 以来的新秒数设置 `l:event:playhead` 值，_不是_&#x200B;到用户暂停 LIVE 流的点。

## 示例代码 {#sample-code}

![](assets/live-content-playback.png)

### Android

以下是预期的 API 调用顺序：

```java
// Set up mediaObject 
MediaObject mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

HashMap<String, String> mediaMetadata = new HashMap<String, String>(); 
mediaMetadata.put(CUSTOM_VAL_1, CUSTOM_KEY_1); 
mediaMetadata.put(CUSTOM_VAL_2, CUSTOM_KEY_2); 

// 1. Call trackSessionStart() when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen. 
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since the user does not watch live media to completion, there  
//    is no need to call trackComplete().  
_mediaHeartbeat.trackSessionEnd(); 
....... 
....... 
```

### iOS

以下是预期的 API 调用顺序：

```
// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 1. Call trackSessionStart when the user clicks Play or if autoplay is used,  
//    i.e., there is an intent to start playback. 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 2. Call trackPlay when the playback actually starts, i.e., when the first  
//    frame of the main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 3. Call trackSessionEnd when user ends the playback session. Since the user  
//    does not watch live media to completion, there is no need to call  
//    trackComplete. 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 
```

### JavaScript

以下是预期的 API 调用顺序：

```js
// Set up mediaObject 
var mediaInfo =  
MediaHeartbeat.createMediaObject(Configuration.MEDIA_NAME,  
                                 Configuration.MEDIA_ID,  
                                 Configuration.MEDIA_LENGTH,  
                                 MediaHeartbeat.StreamType.VOD); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay  
//    is used, i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackSessionEnd() when user ends the playback session.  
//    Since user does not watch live media to completion, there is  
//    no need to call trackComplete(). 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 
```
