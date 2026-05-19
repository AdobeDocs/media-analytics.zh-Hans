---
title: 恢复不活动的会话
description: 了解如何恢复不活动的会话。
uuid: 3ff1205d-7bbe-4016-9bd7-6e34b7862c4c
exl-id: ee4cf7f5-5788-4d35-a04d-4ed714ccd663
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/KT7NfrYlagrMwAjsrbSNR8YUbj5d-ihU8AfJ6wcbgOA
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 37%

---

# 恢复不活动的会话{#resuming-inactive-sessions}

## 长时间暂停

Media SDK 会自动跟踪媒体播放处于下列某个不活动状态的时长：

* 已暂停
* 搜寻
* 已搁置
* 缓冲

如果媒体跟踪会话保持不活动状态超过 30 分钟，则该会话将被自动关闭。 如果用户恢复之前不活动的视频跟踪会话 (`trackPlay`)，媒体心跳会使用先前使用的视频信息和元数据自动创建新的视频会话，并发送恢复心跳事件。

## 使用恢复标志的跨设备切换

处理单应用程序会话继续的恢复机制也适用于查看器在设备之间传输播放时，例如，将视频从手机播放到电视或Chromecast接收器。 由于每个设备运行其自己的Media SDK实例，因此默认情况下，切换会创建多个会话。 使用恢复标记将它们拼合到逻辑连续项中，以便Analytics将合并查看报告为单次参与，而不是单独的媒体开始。

**如何实施：**

1. 在&#x200B;**源设备**（例如电话）上，当查看器启动转换时，请致电`trackSessionEnd`。 不要调用`trackComplete` — 内容未完成，正在移动到其他设备。
2. 在&#x200B;**目标设备**（例如，Chromecast）上，调用`trackSessionStart`，恢复标志设置为`true`并在源设备上使用相同的内容元数据（名称、ID、长度）。 传递观看器在源设备上停止播放的位置。
3. 如果查看器稍后将播放返回到源设备，请在目标设备上重复相同的模式： `trackSessionEnd`，并在源设备上使用恢复标志重复`trackSessionStart`。

设置恢复标志会导致Adobe Analytics在切换的第二个和后续分支中递增[内容恢复](/help/reporting/metrics/content-resumes.md)，而不是[媒体开始](/help/reporting/metrics/media-starts.md)。 由于没有内置机制可在SDK实例之间共享会话ID，因此恢复标志是客户端声明 — 当您知道查看器正在继续上一个会话时，可根据应用程序逻辑传递它。

## 手动恢复之前关闭的会话

Media SDK 仅在应用程序未关闭的情况下才会自动恢复会话。 如果应用程序存储了用户数据，并且能够恢复之前关闭的媒体，则可以手动触发恢复事件。 启动视频跟踪会话时，请设置可选的“视频已恢复”属性。

### Android

```java
// Set MediaHeartbeat.MediaObjectKey.mediaResumed to true
public void onmediaLoad(Observable observable, Object data) {

  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  MediaObject mediaInfo = MediaHeartbeat.createMediaObject(  
      <MEDIA_NAME>,  
      <MEDIA_ID>,  
      <MEDIA_LENGTH>,  
      MediaHeartbeat.StreamType.VOD
  );

  // Set to true if this is a resume playback scenario
  mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.mediaResumed, true);

  _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
}
```

### iOS

```
- (void)onMainmediaLoaded:(NSNotification *)notification {
  //Replace <MEDIA_NAME> with the media name.
  //Replace <MEDIA_ID> with a media unique identifier.
  //Replace <MEDIA_LENGTH> with the media length.     
  ADBMediaObject *mediaObject =  
    [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                       mediaId:<MEDIA_ID>
                       length:<MEDIA_LENGTH>
                       streamType:ADBMediaHeartbeatStreamTypeVOD];

  //Set to YES if this user is resuming a previously closed media session
  [mediaObject setValue:@(YES) forKey:ADBMediaObjectKeymediaResumed];

  [_mediaHeartbeat trackSessionStart:mediaObject data:mediaMetadata];
}
```

### JavaScript

```js
_onmediaLoad = function () {
  // Replace <MEDIA_NAME> with the media name.
  // Replace <MEDIA_ID> with a media unique identifier.
  // Replace <MEDIA_LENGTH> with the media length.  
  var mediaObject =  
    MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>,  
                                     MediaHeartbeat.StreamType.VOD);

  // Set to true if this user is resuming a previously closed media session
  mediaObject.setValue(MediaObjectKey.mediaResumed, true);
  this._mediaHeartbeat.trackSessionStart(mediaObject, contextData);
};
```
