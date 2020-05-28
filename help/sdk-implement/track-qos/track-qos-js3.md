---
title: 使用JavaScript 3.x跟踪体验质量
description: 本主题介绍在使用JavaScript 3x的浏览器应用程序中使用Media SDK实现体验质量(QoE,QoS)跟踪。
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# 使用JavaScript 3.x跟踪体验质量{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 3.x SDK 实施提供了指南。If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 实施QOE

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   QoEObject变量：

   >[!TIP]
   >
   >只有在您打算跟踪 QoS 的情况下，才需要使用这些变量。

   | 变量 | 类型 | 描述 |
   | --- | --- | --- |
   | `bitrate` | number | 当前比特率 |
   | `startupTime` | number | 开始时间 |
   | `fps` | number | FPS 值 |
   | `droppedFrames` | number | 丢帧的数量 |

   QoE对象创建：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   ```

1. 在播放期间，当比特率发生更改时，在 MediaHeartbeat 实例中调用 `BitrateChange` 事件。

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >更新QoE对象，并在每次比特率更改时调用比特率更改事件。 这提供最准确的QoE数据。

1. 确保调用方 `updateQoEObject()` 法向SDK提供最新的QoE信息。
1. 当媒体播放器遇到错误，并且错误事件可用于播放器 API 时，使用 `trackError()` 来捕获错误信息。（请参阅[概述](/help/sdk-implement/track-errors/track-errors-overview.md)。）

   >[!TIP]
   >
   >跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd()` 后调用 `trackError()` 来关闭媒体跟踪会话。
