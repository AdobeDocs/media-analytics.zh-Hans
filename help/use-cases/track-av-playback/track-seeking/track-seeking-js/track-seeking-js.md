---
title: 了解如何使用JavaScript 2.x跟踪搜寻
description: 了解如何使用浏览器应用程序(JS 2.x)中的Media SDK跟踪搜寻开始和搜寻结束事件。
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 76%

---

# 使用JavaScript 2.x跟踪搜寻{#track-seeking-on-javascript}

下面的说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 搜寻跟踪常量

| 常量名称 | 描述     |
|---|---|
| `SeekStart` | 用于跟踪搜寻开始事件的常量。 |
| `SeekComplete` | 用于跟踪搜寻结束事件的常量。 |

## 实施搜寻

1. 监听媒体播放器中的播放搜寻事件，并在发出搜寻开始事件通知时，使用 `SeekStart` 事件跟踪搜寻：

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. 在从媒体播放器发出搜寻结束通知时，使用 `SeekComplete` 事件跟踪搜寻的结束：

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

有关更多信息，请参阅跟踪方案[在主内容中进行搜寻的 VOD 播放](/help/use-cases/tracking-scenarios/vod-seeking.md)。
