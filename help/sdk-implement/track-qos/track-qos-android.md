---
seo-title: 在 Android 中跟踪体验质量
title: 在 Android 中跟踪体验质量
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 Android 中跟踪体验质量{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. 确保 `getQoSObject()` 方法返回最新的 QoS 信息。
1. 在播放期间，当比特率发生更改时，在 MediaHeartbeat 实例中调用 `BitrateChange` 事件。

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null); 
   } 
   ```

   >[!IMPORTANT]
   >
   >更新QoS对象，并在每个比特率发生变化时调用比特率更改事件。这样将可以提供最为准确的 QoS 数据。

