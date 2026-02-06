---
title: 具有连续跟踪的实时主内容
description: 查看有关如何使用 Media SDK 跟踪具有连续跟踪的实时内容的示例。
uuid: b03477b6-9be8-4b67-a5a0-4cef3cf262ab
exl-id: 277a72b8-453b-41e5-b640-65c43587baf8
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 100%

---

# 具有连续跟踪的实时主内容{#live-main-content-with-sequential-tracking}

## 场景 {#scenario}

在此方案中，有一个实时资源，在加入实时流后 40 秒内不播放任何广告。

此方案与[不含广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)方案相同，但是部分内容会被清除，并且会从主内容的一个点到另一个点完成搜寻。

| 触发器 | 心跳方法 |  网络调用  |  注释   |
| --- | --- | --- | --- |
| 用户点击[!UICONTROL 播放] | trackSessionStart | Analytics 内容开始，心跳内容开始 | 测量库不知道存在一个前置广告，因此这些网络调用与[不含广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)方案相同。 |
| 播放内容的第一帧。 | trackPlay | 心跳内容播放 | 当章节内容在主内容之前播放时，心跳在章节开始时开始。 |
| 内容播放 | | 内容心跳 | 此网络调用与[不含广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)方案完全相同。 |
| Session1 结束（Episode1 结束） | trackComplete / trackSessionEnd | 心跳内容结束 | “结束”是指第 1 集的 session1 已完全观看结束。在开始下一集的会话之前，必须结束此会话。 |
| Episode2 开始（Session2 开始） | trackSessionStart | Analytics 内容开始，心跳内容开始 | 这是因为用户观看了第 1 集并继续观看另一剧集 |
| 媒体的第 1 帧 | trackPlay | 心跳内容播放 | 此方法将触发计时器，从这一刻开始，只要继续播放，就会每 10 秒发送一次心跳。 |
| 内容播放 | | 内容心跳 | |
| 会话结束（Episode2 结束） | trackComplete / trackSessionEnd | 心跳内容结束 | “结束”是指第 2 集的 session2 已完全观看结束。在开始下一集的会话之前，必须结束此会话。 |

## 参数 {#parameters}

### 心跳内容开始

| 参数 | 值 | 注释 |
|---|---|---|
| `s:sc:rsid` | &lt;您的 Adobe 报表包 ID> |  |
| `s:sc:tracking_serve` | &lt;您的 Analytics 跟踪服务器 URL> |  |
| `s:user:mid` | `s:user:mid` | 应当匹配 Adobe Analytics 内容开始调用中的中间值 |
| `s:event:type` | `"start"` |  |
| `s:asset:type` | `"main"` |  |
| `s:asset:media_id` | &lt;您的媒体名称> |  |
| `s:stream:type` | `live` |  |
| `s:meta:*` | *可选* | 对媒体设置的自定义元数据 |

## 心跳内容播放 {#heartbeat-content-play}

这应当看起来与心跳内容开始调用几乎完全相似，但关键的区别在于“s:event:type”参数。所有参数仍应位于此处。

| 参数 | 值 | 注释 |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `s:asset:type` | `"main"` |  |

## 内容心跳 {#content-heartbeats}

在媒体播放期间，有一个计时器将会每 10 秒发送一次主内容的一个或多个心跳，每 1 秒发送一次广告的一个或多个心跳。这些心跳将包含有关播放、广告、缓冲和许多其他内容的信息。每个心跳的确切内容不在本文档涵盖的范围之内，验证的关键内容是在持续播放期间始终触发心跳。

在内容心跳中，查找一些特定的内容：

| 参数 | 值 | 注释 |
|---|---|---|
| `s:event:type` | `"play"` |  |
| `l:event:playhead` | &lt;播放头位置> 例如，50、60、70 | 这应该反映播放头的当前位置。 |

## 心跳内容结束 {#heartbeat-content-complete}

当任何给定剧集的播放结束时（播放头跨越剧集边界），将发送“心跳内容结束”调用。此调用看起来类似于其他心跳调用，但包含几个特定的参数：

| 参数 | 值 | 注释 |
|---|---|---|
| `s:event:type` | `"complete"` |  |
| `s:asset:type` | `"main"` |  |

## 示例代码 {#sample-code}

![](assets/ios-live-noads-multiplesessions.png)

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
//    i.e., when there is an intent to start playback.  
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the first  
//    frame of main content is rendered on the screen.  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing 1st episode/session.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2 /episode 2 of the same live stream.  
// There is no need to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 
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

// 5. Call trackSessionStart() when the playhead reaches a point that denotes the 
//    start of session 2 
_mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback  
_mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., the media completes and finishes playing.  
_mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
_mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue similarly tracking further sessions in the live stream if required 
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
//    frame of main content is rendered on the screen. 
[_mediaHeartbeat trackPlay]; 
....... 
....... 

// 3. Call trackComplete when the playback reaches the end of session,  
//    i.e., when the media completes and finishes playing the first 
//    episode/session. 
[_mediaHeartbeat trackComplete]; 
....... 
....... 

// 4. Call trackSessionEnd to end session 1 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Start tracking session 2 / episode 2 of the same live stream, No need to  
// reinstantiate mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
ADBMediaObject *mediaObject =  
[ADBMediaHeartbeat createMediaObjectWithName:MEDIA_NAME  
                   length:MEDIA_LENGTH  
                   streamType:ADBMediaHeartbeatStreamTypeLIVE]; 
 
NSMutableDictionary *mediaContextData = [[NSMutableDictionary alloc] init]; 
[mediaContextData setObject:CUSTOM_VAL_1 forKey:CUSTOM_KEY_1]; 
[mediaContextData setObject:CUSTOM_VAL_2 forKey:CUSTOM_KEY_2]; 
 
// 5. Call trackSessionStart when the playhead reaches a point that denotes  
//    start of session 2 
[_mediaHeartbeat trackSessionStart:mediaObject data:mediaContextData]; 
...... 
...... 
 
// 6. Call trackPlay to start tracking session 2 playback 
[_mediaHeartbeat trackPlay]; 
....... 
....... 
 
// 7. Call trackComplete when the playback reaches the end of session 2,  
//    i.e., when the media completes and finishes playing. 
[_mediaHeartbeat trackComplete]; 
........ 
........ 
 
// 8. Call trackSessionEnd to end the session 2 
[_mediaHeartbeat trackSessionEnd]; 
........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```

### JavaScript

以下是预期的 API 调用顺序：

```js
// Set up mediaObject 

var mediaInfo = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.VOD 
); 

var mediaMetadata = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 1. Call trackSessionStart() when Play is clicked or if autoplay is used,  
//    i.e., there's an intent to start playback. 
this._mediaHeartbeat.trackSessionStart(mediaInfo, mediaMetadata); 

...... 
...... 

// 2. Call trackPlay() when the playback actually starts, i.e., when the  
//    first frame of media is rendered on the screen. 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 3. Call trackComplete() when the playback reaches the end of a session,  
//    i.e., whn playback completes and finishes playing the 1st episode/session. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 4. Call trackSessionEnd() to end session 1 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Start tracking session 2/episode 2 of the same live stream. There is no need  
// to reinstantiate a mediaHeartbeat instance for tracking sesison 2. 

// Set up mediaObject 
var mediaInfo2 = MediaHeartbeat.createMediaObject( 
  Configuration.MEDIA_NAME,  
  Configuration.MEDIA_ID,  
  Configuration.MEDIA_LENGTH,  
  MediaHeartbeat.StreamType.LIVE 
); 

var mediaMetadata2 = { 
  CUSTOM_KEY_1 : CUSTOM_VAL_1,  
  CUSTOM_KEY_2 : CUSTOM_VAL_2,  
  CUSTOM_KEY_3 : CUSTOM_VAL_3 
}; 

// 5. Call trackSessionStart() when the playhead reaches a point that denotes  
//    the start of session 2 
this._mediaHeartbeat.trackSessionStart(mediaInfo2, mediaMetadata2); 

...... 
...... 

// 6. Call trackPlay() to start tracking session 2 playback 
this._mediaHeartbeat.trackPlay(); 

....... 
....... 

// 7. Call trackComplete() when the playback reaches the end of session 2,  
//    i.e., playback completes and finishes playing. 
this._mediaHeartbeat.trackComplete(); 

........ 
........ 

// 8. Call trackSessionEnd() to end session 2 
this._mediaHeartbeat.trackSessionEnd(); 

........ 
........ 

// Continue tracking further sessions in live stream similarly if required 
```
