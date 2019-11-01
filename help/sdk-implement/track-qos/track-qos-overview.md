---
title: 概述
description: 使用Media SDK跟踪体验质量(QoE、QoS)的概述。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 概述{#overview}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. 您可以使用媒体播放器API来标识与QoS和错误跟踪相关的变量。 以下是体验质量跟踪的关键元素：

## 播放器事件 {#player-events}

### 在任何 QoS 量度发生更改时：

为播放创建或更新 QoS 对象实例。[QoS API参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### 关于所有比特率更改事件

调用 `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## 实施QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

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

1. 确保 `getQoSObject()` 方法返回最新的 QoS 信息。
1. 在播放期间，当比特率发生更改时，在 MediaHeartbeat 实例中调用 `BitrateChange` 事件。

   >[!IMPORTANT]
   >
   >更新QoS对象，并在每个比特率更改时调用比特率更改事件。 这样将可以提供最为准确的 QoS 数据。

以下示例代码将JavaScript 2.x SDK用于HTML5媒体播放器。 应将此代码与核心媒体播放代码一起使用。

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```

