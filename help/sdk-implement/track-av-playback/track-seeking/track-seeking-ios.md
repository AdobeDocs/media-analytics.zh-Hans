---
seo-title: 在 iOS 中跟踪搜寻
title: 在 iOS 中跟踪搜寻
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 iOS 中跟踪搜寻{#track-seeking-on-ios}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Seek tracking constants

| 常量名称 | 描述     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | 用于跟踪搜寻开始事件的常量。 |
| `ADBMediaHeartbeatEventSeekComplete` | 用于跟踪搜寻结束事件的常量。 |

## Implement seeking

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

有关更多信息，请参阅跟踪方案[在主内容中进行搜寻的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-seeking.md)。
