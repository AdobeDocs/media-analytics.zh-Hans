---
seo-title: 在 JavaScript 中跟踪体验质量
title: 在 JavaScript 中跟踪体验质量
uuid: 3bc762a2-9706-4b62-aa91-747f461 dd13 d
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 JavaScript 中跟踪体验质量{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## 实现质量

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   QoSObject 变量：

   >[!TIP]
   >
   >仅当您计划跟踪QoS时，才需要这些变量。

   | 变量 | 描述 | 必需 |
   | --- | --- | :---: |
   | `bitrate` | 当前比特率 | 是 |
   | `startupTime` | 开始时间 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 丢帧的数量 | 是 |

   QoS 对象创建：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. 在播放期间，当比特率发生更改时，在 MediaHeartbeat 实例中调用 `BitrateChange` 事件。

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >更新QoS对象，并在每个比特率发生变化时调用比特率更改事件。这样将可以提供最为准确的 QoS 数据。

1. 确保 `getQoSObject()` 方法返回最新的 QoS 信息。
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](../../sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >跟踪媒体播放器错误不会停止媒体跟踪会话。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

