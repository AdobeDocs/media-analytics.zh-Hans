---
title: 了解如何使用 JavaScript 2.x 跟踪体验质量
description: 了解如何在使用JavaScript 2.x的浏览器应用程序中使用Media SDK实施体验质量(QoE、QoS)跟踪。
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 90%

---

# 使用 JavaScript 2.x 跟踪体验质量{#track-quality-of-experience-on-javascript}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施QOS

1. 识别在媒体播放期间比特率发生更改的时间，并使用 QoS 信息创建 `MediaObject` 实例。

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
   >请更新 QoS 对象并在每次比特率发生更改时调用比特率更改事件。这样将可以提供最为准确的 QoS 数据。

1. 确保 `getQoSObject()` 方法返回最新的 QoS 信息。
1. 当媒体播放器遇到错误，并且错误事件可用于播放器 API 时，使用 `trackError()` 来捕获错误信息。（请参阅[概述](/help/use-cases/track-errors/track-errors-overview.md)。）

   >[!TIP]
   >
   >跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd()` 后调用 `trackError()` 来关闭媒体跟踪会话。
