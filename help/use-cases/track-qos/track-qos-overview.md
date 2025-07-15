---
title: 解释跟踪体验质量
description: 有关使用 Media SDK 跟踪体验质量（QoE、QoS）的概述。
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 99%

---

# 概述{#overview}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

体验质量跟踪包括服务质量 (QoS) 和错误跟踪，在核心媒体跟踪实施中，这两项跟踪都是可选元素，而&#x200B;**不是**&#x200B;必需元素。您可以使用媒体播放器 API 来识别与 QoS 和错误跟踪相关的变量。以下是体验质量跟踪的关键元素：

## 播放器事件 {#player-events}

### 在任何 QoS 量度发生更改时：

为播放创建或更新 QoS 对象实例。[QoS API 引用](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### 在发生所有比特率更改事件时

调用 `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## 实施QOS

1. 识别在媒体播放期间任何 QoS 量度发生更改的时间，使用 QoS 信息创建 `MediaObject`，并更新新的 QoS 信息。

   QoSObject 变量：

   >[!TIP]
   >
   >只有在您打算跟踪 QoS 的情况下，才需要使用这些变量。

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
   >请更新 QoS 对象并在每次比特率发生更改时调用比特率更改事件。这样将可以提供最为准确的 QoS 数据。

以下代码示例为 HTML5 媒体播放器使用 JavaScript 2.x SDK。您应该结合使用此代码与核心媒体播放代码。

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
