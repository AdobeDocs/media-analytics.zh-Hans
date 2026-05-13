---
title: 了解如何在 iOS 中跟踪体验质量
description: 了解如何在iOS中使用Media SDK实施体验质量(QoE、QoS)跟踪。
uuid: cae2c142-ed39-4234-a711-765dcabc5415
exl-id: 7f01e6eb-95bd-4e3d-93d0-8a2e68323313
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/37GAel-VlcHz-jmbicc1WphVs0y7-E8UDbBInmMT9LQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 159
ht-degree: 89%

---

# 在 iOS 中跟踪体验质量{#track-quality-of-experience-on-ios}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施QOS

1. 识别在媒体播放期间比特率发生更改的时间，并使用 QoS 信息创建 `MediaObject` 实例。

   QoSObject 变量：

   | 变量 | 描述 | 必需 |
   | --- | --- | :---: |
   | `bitrate` | 当前比特率 | 是 |
   | `startupTime` | 开始时间 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 丢帧的数量 | 是 |

   >[!TIP]
   >
   >只有在您打算跟踪 QoS 的情况下，才需要使用这些变量。

   QoS 对象创建：

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE]
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. 确保 `getQoSObject` 方法返回最新的 QoS 信息。
1. 在播放期间，当比特率发生更改时，在 MediaHeartbeat 实例中调用 `BitrateChange` 事件。

   ```
   - (void)onBitrateChange:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil];
   }
   ```

   >[!IMPORTANT]
   >
   >请更新 QoS 对象并在每次比特率发生更改时调用比特率更改事件。 这样将可以提供最为准确的 QoS 数据。
