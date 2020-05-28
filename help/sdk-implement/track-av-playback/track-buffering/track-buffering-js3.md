---
title: 使用JavaScript 3.x跟踪缓冲
description: 介绍如何在浏览器应用程序 (JS) 中跟踪缓冲事件。
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 74%

---


# 使用JavaScript 3.x跟踪缓冲{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 3.x SDK 实施提供了指南。If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 缓冲跟踪常量

| 常量名称 | 描述     |
|---|---|
| `BufferStart` | 用于跟踪缓冲开始事件的常量 |
| `BufferComplete` | 用于跟踪缓冲结束事件的常量 |

## 实施缓冲

1. 监听媒体播放器中的播放缓冲事件，并在发出缓冲开始事件通知时，使用 `BufferStart` 事件跟踪缓冲。

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. 在从媒体播放器发出缓冲结束通知时，使用 `BufferComplete` 事件跟踪缓冲的结束。

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

有关更多信息，请参阅跟踪方案[带有缓冲的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-buffering.md)。
