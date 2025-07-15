---
title: 了解如何使用 JavaScript 3.x 跟踪搜寻
description: 了解如何在浏览器应用程序 (JS 3.x) 中使用 Media SDK 跟踪搜寻开始和搜寻结束事件。
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 100%

---

# 使用 JavaScript 3.x 跟踪搜寻{#track-seeking-on-javascript}

以下说明为所有 3.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 SDK 之前的版本，可以在此处下载开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 搜寻跟踪常量

| 常量名称 | 描述     |
|---|---|
| `SeekStart` | 用于跟踪搜寻开始事件的常量。 |
| `SeekComplete` | 用于跟踪搜寻结束事件的常量。 |

## 实施搜寻

1. 监听媒体播放器中的播放搜寻事件，并在发出搜寻开始事件通知时，使用 `SeekStart` 事件跟踪搜寻：

   ```js
   _onSeekStart = function() {
       tracker.trackEvent(ADB.Media.Event.SeekStart);
   };
   ```

1. 在从媒体播放器发出搜寻结束通知时，使用 `SeekComplete` 事件跟踪搜寻的结束：

   ```js
   _onSeekComplete = function() {
       tracker.trackEvent(ADB.Media.Event.SeekComplete);
   };
   ```

有关更多信息，请参阅跟踪场景[在主内容中进行搜寻的 VOD 播放](/help/use-cases/tracking-scenarios/vod-seeking.md)。
