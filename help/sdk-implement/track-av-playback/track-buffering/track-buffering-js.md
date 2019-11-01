---
title: 在 JavaScript 中跟踪缓冲
description: 描述在浏览器应用程序(JS)中跟踪缓冲事件。
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 JavaScript 中跟踪缓冲{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 缓冲区跟踪常量

| 常量名称 | 描述     |
|---|---|
| `BufferStart` | 用于跟踪缓冲开始事件的常量 |
| `BufferComplete` | 用于跟踪缓冲结束事件的常量 |

## 实现缓冲

1. 监听媒体播放器中的播放缓冲事件，并在发出缓冲开始事件通知时，使用 `BufferStart` 事件跟踪缓冲。

   ```js
   _onBufferStart = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
   };
   ```

1. 在从媒体播放器发出缓冲结束通知时，使用 `BufferComplete` 事件跟踪缓冲的结束。

   ```js
   _onBufferComplete = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
   };
   ```

有关更多信息，请参阅跟踪方案[带有缓冲的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。
