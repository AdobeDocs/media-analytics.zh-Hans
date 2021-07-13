---
title: 了解如何在Android中跟踪缓冲
description: 了解如何在Android中跟踪缓冲事件。
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 87%

---

# 在 Android 中跟踪缓冲{#track-buffering-on-android}

>[!IMPORTANT]
>下面的说明为所有 2.x SDK 实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

## 缓冲跟踪常量

| 常量名称 | 描述     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | 用于跟踪缓冲开始事件的常量 |
| `MediaHeartbeat.Event.BufferComplete` | 用于跟踪缓冲结束事件的常量 |

## 实施缓冲

1. 监听媒体播放器中的播放缓冲事件，并在发出缓冲开始事件通知时，使用 `BufferStart` 事件跟踪缓冲：

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. 在从媒体播放器发出缓冲结束通知时，使用 `BufferComplete` 事件跟踪缓冲的结束：

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

有关更多信息，请参阅跟踪方案[带有缓冲的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。
