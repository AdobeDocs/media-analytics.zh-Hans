---
title: 了解如何在 Roku 中跟踪体验质量
description: 了解如何在Roku中使用Media SDK实施体验质量(QoE、QoS)跟踪。
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
exl-id: cd84c26d-ad91-4179-9532-83408030ff3e
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-e2JKBn8IB9Kk-MEVIlQq6IY5Wuevlp6GrpkM96xuX4
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 200
ht-degree: 91%

---

# 在 Roku 中跟踪体验质量{#track-quality-of-experience-on-roku}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施QOS

1. 识别在媒体播放期间比特率发生更改的时间，并使用 `mediaUpdateQoS` API 来更新 Media SDK 中的 QoS 信息。

   QoSObject 变量：

   >[!TIP]
   >
   >只有在您要跟踪 QoS 的情况下，才需要使用这些变量。

   | 变量 | 描述 | 必需 |
   | --- | --- | :---: |
   | `bitrate` | 当前比特率 | 是 |
   | `startupTime` | 开始时间 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 丢帧的数量 | 是 |

   例如：

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:

    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. 当播放切换比特率时，调用 `trackEvent(BitrateChange)` 来通知 Media SDK 比特率已发生更改。

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >您需要使用更新的比特率值调用 `updateQoSObject`。

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```

    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. 当媒体播放器遇到错误，并且错误事件可用于播放器 API 时，使用 `trackError()` 来捕获错误信息。 （请参阅[概述](/help/use-cases/track-errors/track-errors-overview.md)。）

   >[!TIP]
   >
   >跟踪媒体播放器错误不会停止媒体跟踪会话。 如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd()` 后调用 `trackError()` 来关闭媒体跟踪会话。
