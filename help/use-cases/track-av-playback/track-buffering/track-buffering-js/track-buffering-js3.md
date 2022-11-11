---
title: 了解如何使用JavaScript 3.x跟踪缓冲
description: 了解如何在浏览器应用程序(JS)中跟踪缓冲事件。
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 65%

---

# 使用JavaScript 3.x跟踪缓冲{#track-buffering-on-javascript}

下面的说明为所有 3.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是SDK的先前版本，可以在此处下载开发人员指南： [下载SDK。](/help/getting-started/download-sdks.md)

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

有关更多信息，请参阅跟踪方案[带有缓冲的 VOD 播放](/help/use-cases/tracking-scenarios/vod-buffering.md)。
