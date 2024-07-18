---
title: 了解如何在 iOS 中跟踪搜寻
description: 了解如何在 iOS 中使用 Media SDK 跟踪搜寻开始和搜寻结束事件。
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
exl-id: e8cb4962-2a14-4bfe-9a25-2405e503ba0b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 100%

---

# 在 iOS 中跟踪搜寻{#track-seeking-on-ios}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 搜寻跟踪常量

| 常量名称 | 描述     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | 用于跟踪搜寻开始事件的常量。 |
| `ADBMediaHeartbeatEventSeekComplete` | 用于跟踪搜寻结束事件的常量。 |

## 实施搜寻

1. 监听媒体播放器中的播放搜寻事件，并在发出搜寻开始事件通知时，使用 `SeekStart` 事件跟踪搜寻：

   ```
   - (void)onSeekStart:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil];
   }
   ```

1. 在从媒体播放器发出搜寻结束通知时，使用 `SeekComplete` 事件跟踪搜寻的结束：

   ```
   - (void)onSeekComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil];
   }
   ```

有关更多信息，请参阅跟踪场景[在主内容中进行搜寻的 VOD 播放](/help/use-cases/tracking-scenarios/vod-seeking.md)。
