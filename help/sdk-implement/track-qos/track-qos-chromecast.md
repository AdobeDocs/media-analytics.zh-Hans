---
title: 了解如何在Chromecast中跟踪体验质量
description: “了解如何在Chromecast中使用Media SDK实施体验质量(QoE、QoS)跟踪。”
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
exl-id: 04b9b888-2727-4aa6-a934-94a02c85a490
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 91%

---

# 在 Chromecast 中跟踪体验质量{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

## 概述 {#overview}

体验质量跟踪包括服务质量 (QoS) 和错误跟踪，在核心媒体跟踪实施中，这两项跟踪都是可选元素，而&#x200B;**不是**&#x200B;必需元素。您可以使用媒体播放器 API 来识别与 QoS 和错误跟踪相关的变量。

## 播放器事件 {#player-events}

### 在发生所有比特率更改事件时

* 为播放创建/更新 QoS 对象实例 `qosObject`
* 调用 `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### 在发生播放器错误时

调用 `trackError(“media error id”);`

## 实施 {#implement}

1. 识别在媒体播放期间比特率发生更改的时间，并使用 QoS 信息创建 `MediaObject` 实例。

   **QoSObject 变量：**

   >[!TIP]
   >
   >只有在您打算跟踪 QoS 的情况下，才需要使用这些变量。

   | 变量 | 描述 | 必需 |
   | --- | --- | :---: |
   | `bitrate` | 当前比特率 | 是 |
   | `startupTime` | 开始时间 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 丢帧的数量 | 是 |

   **QoS 对象创建：**[createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. 在播放期间，当比特率发生更改时，在 MediaHeartbeat 实例中调用 `BitrateChange` 事件：[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >请更新 QoS 对象并在每次比特率发生更改时调用比特率更改事件。这样将可以提供最为准确的 QoS 数据。

1. 确保 `getQoSObject()` 方法返回最新的 QoS 信息。
1. 当媒体播放器遇到错误，并且错误事件可用于播放器 API 时，使用 `trackError()` 来捕获错误信息。（请参阅[概述](/help/sdk-implement/track-errors/track-errors-overview.md)。）

   >[!TIP]
   >
   >跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd()` 后调用 `trackError()` 来关闭媒体跟踪会话。
