---
title: 在 Android 中跟踪缓冲
description: 介绍在Android上跟踪缓冲事件。
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Android 中跟踪缓冲{#track-buffering-on-android}

>[!IMPORTANT]
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDks.](/help/sdk-implement/download-sdks.md)

## 缓冲区跟踪常量

| 常量名称 | 描述     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | 用于跟踪缓冲开始事件的常量 |
| `MediaHeartbeat.Event.BufferComplete` | 用于跟踪缓冲结束事件的常量 |

## 实现缓冲

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
