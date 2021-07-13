---
title: 了解如何在iOS中跟踪缓冲
description: 了解如何在iOS中跟踪缓冲事件。
uuid: 4f4db23a-489b-4b41-bb6e-393ec64d52a2
exl-id: 5f0a3c4b-7c9e-499d-98d0-6fcf316c4d9c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 87%

---

# 在 iOS 中跟踪缓冲{#track-buffering-on-ios}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

## 缓冲跟踪常量


| 常量名称 | 描述     |
|---|---|
| `ADBMediaHeartbeatEventBufferStart` | 用于跟踪缓冲开始事件的常量 |
| `ADBMediaHeartbeatEventBufferComplete` | 用于跟踪缓冲结束事件的常量 |

## 实施缓冲

1. 监听媒体播放器中的播放缓冲事件，并在发出缓冲开始事件通知时，使用 `BufferStart` 事件跟踪缓冲：

   ```
   - (void)onBufferStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 在从媒体播放器发出缓冲结束通知时，使用 `BufferComplete` 事件跟踪缓冲的结束：

   ```
   - (void)onBufferComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBufferComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

有关更多信息，请参阅跟踪方案[带有缓冲的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。
