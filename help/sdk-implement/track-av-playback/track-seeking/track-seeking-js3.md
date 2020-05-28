---
title: 使用JavaScript 3.x跟踪搜索
description: 本主题介绍如何在浏览器应用程序 (JS) 中使用 Media SDK 实施搜寻跟踪。
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 76%

---


# 使用JavaScript 3.x跟踪搜索{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 3.x SDK 实施提供了指南。If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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
