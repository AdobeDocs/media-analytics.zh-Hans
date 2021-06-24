---
title: 了解如何使用JavaScript 3.x跟踪搜寻
description: 了解如何使用浏览器应用程序(JS 3.x)中的Media SDK跟踪搜寻开始和搜寻结束事件。
exl-id: b7152436-520e-4f38-a8ad-1027ca3f1f6c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 62%

---

# 使用JavaScript 3.x跟踪搜寻{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 3.x SDK 实施提供了指南。如果您实施的是SDK的先前版本，可以在此处下载开发人员指南：[下载SDK。](/help/sdk-implement/download-sdks.md)

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

有关更多信息，请参阅跟踪方案[在主内容中进行搜寻的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-seeking.md)。
