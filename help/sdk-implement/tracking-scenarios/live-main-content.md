---
seo-title: 实时主内容
title: 实时主内容
uuid: e92e99f4-c395-48aa-8a30-cbdd2f5fc07c
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# 实时主内容{#live-main-content}

## 情景 {#scenario}

在此方案中，有一个加入实时流之后 40 秒不播放广告的实时资产。

| 触发器 | 心率方法 | 网络调用 | 注释   |
|---|---|---|---|
| User clicks **[!UICONTROL Play]** | `trackSessionStart` | Analytics 内容开始，心率内容开始 | 这可以是用户点击&#x200B;**[!UICONTROL 播放]或自动播放事件。** |
| 播放媒体的第一帧。 | `trackPlay` | 心率内容播放 | 此方法会触发计时器。只要播放继续，每 10 秒就会发送一次心率。 |
| 播放内容。 |  | 内容心率 |  |
| 会话结束。 | `trackSessionEnd` |  | `SessionEnd` 是指观看会话结束。即使用户不使用媒体完成，也必须调用此API。 |

## 参数 {#parameters}

您在 Adobe Analytics 内容开始调用中看到的很多值，同样也会在心率内容开始调用中看到。您还将看到许多其他参数，Adobe使用这些参数在Adobe Analytics中填充各种媒体报表。 我们不会在这里涵盖所有这些变量，而是只列出一些非常重要的变量。

### 心率内容开始

| 参数 | 值 | 注释 |
|---|---|---|
| `s:sc:rsid` | &lt;您的 Adobe 报表包 ID&gt; |  |
| `s:sc:tracking_serve` | &lt;您的 Analytics 跟踪服务器 URL&gt; |  |
| `s:user:mid` | `s:user:mid` | 应当匹配 Adobe Analytics 内容开始调用中的中间值 |
| `s:event:type` | "start" |  |
| `s:asset:type` | "main" |  |
| `s:asset:mediao_id` | &lt;您的媒体名称&gt; |  |
| `s:stream:type` | live |  |
| `s:meta:*` | 可选 | 媒体上的自定义元数据集 |

## 内容心率 {#content-heartbeats}

在媒体播放期间，有一个计时器将每10秒为主内容发送一个或多个心跳（或ping），每秒为广告发送一个或多个心跳。 这些心率将包含有关播放、广告、缓冲等的信息。本文档不包含各个心率的确切内容，但需要确认的一个关键点是，在继续播放时，将会持续触发心率。

在内容心率中，查找几个特定的参数：

| 参数 | 值 | 注释 |
|---|---|---|
| `s:event:type` | "play" |  |
| `l:event:playhead` | &lt;播放头位置&gt; 例如 50、60、70 | 这应该反映播放头的当前位置。 |

## 心率内容结束 {#heartbeat-content-complete}

此场景中不会有完整的调用，因为实时流从未完成。

## 播放头值设置

对于LIVE流，您需要将播放头设置为与开始编程时的偏移量，这样，在报告中，分析师可以确定用户在24小时视图内加入和离开LIVE流的时间点。

### 开始

对于实时媒体，当用户开始播放流时，您需要设置为当 `l:event:playhead` 前的偏移量（以秒为单位）。 这与VOD不同，在VOD中，您可以将播放头设置为“0”。

例如，假设LIVE流事件从午夜开始，持续24小时(`a.media.length=86400`; `l:asset:length=86400`)。 然后，假设用户在下午12:00开始播放该实时流。 在此方案中，您应设 `l:event:playhead` 置为43200（在流中停留12小时）。

### 暂停时

当用户暂停播放时，必须应用在播放开始时应用的相同“实时播放头”逻辑。 当用户返回播放LIVE流时，您必须将该值设置为新的偏移播放头位置，而 `l:event:playhead`__ 不是设置为用户暂停LIVE流的点。

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

