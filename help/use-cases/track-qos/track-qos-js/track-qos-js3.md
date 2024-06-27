---
title: 了解如何使用 JavaScript 3.x 跟踪体验质量
description: “了解如何使用 JavaScript 3.x 在浏览器应用程序中使用 Media SDK 实施体验质量（QoE、QoS）跟踪。”
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 99%

---

# 使用 JavaScript 3.x 跟踪体验质量{#track-quality-of-experience-on-javascript}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 SDK 之前的版本，可以在此处下载开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施QOE

1. 识别在媒体播放期间比特率发生更改的时间，并使用 QoE 信息创建 `qoeObject` 实例。

   QoEObject 变量：

   >[!TIP]
   >
   >只有在您打算跟踪 QoS 的情况下，才需要使用这些变量。

   | 变量 | 类型 | 描述 |
   | --- | --- | --- |
   | `bitrate` | 数字 | 当前比特率 |
   | `startupTime` | 数字 | 开始时间 |
   | `fps` | 数字 | FPS 值 |
   | `droppedFrames` | 数字 | 丢帧的数量 |

   QoE 对象创建：

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
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
   >请更新 QoE 对象并在每次比特率发生更改时调用比特率更改事件。这样将可以提供最为准确的 QoE 数据。

1. 确保调用 `updateQoEObject()` 方法以向 SDK 提供最新的 QoE 信息。
1. 当媒体播放器遇到错误，并且错误事件可用于播放器 API 时，使用 `trackError()` 来捕获错误信息。（请参阅[概述](/help/use-cases/track-errors/track-errors-overview.md)。）

   >[!TIP]
   >
   >跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd()` 后调用 `trackError()` 来关闭媒体跟踪会话。
