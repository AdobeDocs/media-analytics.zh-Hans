---
seo-title: 在 Android 中跟踪搜寻
title: 在 Android 中跟踪搜寻
uuid: 65addd99-eef-4a80-8b4 a-d5 fbdff8 ab06
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# 在 Android 中跟踪搜寻{#track-seeking-on-android}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../../sdk-implement/download-sdks.md)

## 搜索跟踪常量

| 常量名称 | 描述     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | 用于跟踪搜寻开始事件的常量。 |
| `MediaHeartbeat.Event.SeekComplete` | 用于跟踪搜寻结束事件的常量。 |

## 实现搜寻

1. 监听媒体播放器中的播放搜寻事件，并在发出搜寻开始事件通知时，使用 `SeekStart` 事件跟踪搜寻：

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. 在从媒体播放器发出搜寻结束通知时，使用 `SeekComplete` 事件跟踪搜寻的结束：

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

有关更多信息，请参阅跟踪方案[在主内容中进行搜寻的 VOD 播放](../../../sdk-implement/tracking-scenarios/vod-seeking.md)。
