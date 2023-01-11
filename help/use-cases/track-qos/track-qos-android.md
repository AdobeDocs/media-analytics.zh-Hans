---
title: 了解如何在 Android 中跟踪体验质量
description: “了解如何在 Android 中使用 Media SDK 实施体验质量（QoE、QoS）跟踪。”
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '156'
ht-degree: 100%

---

# 在 Android 中跟踪体验质量{#track-quality-of-experience-on-android}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施 QoS

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
   >请更新 QoS 对象并在每次比特率发生更改时调用比特率更改事件。这样将可以提供最为准确的 QoS 数据。
