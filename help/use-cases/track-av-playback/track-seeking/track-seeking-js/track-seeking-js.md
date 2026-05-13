---
title: 了解如何使用 JavaScript 2.x 跟踪搜寻
description: 了解如何在浏览器应用程序 (JS 2.x) 中使用 Media SDK 跟踪搜寻开始和搜寻结束事件。
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
exl-id: 90f35376-24d8-405d-82b4-d6b737acf7b9
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/wQkUvm0BhqYGd9q-k2YKe2f0kkhjkM3hpwDYuAIw3QU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 100%

---

# 使用 JavaScript 2.x 跟踪搜寻{#track-seeking-on-javascript}

以下说明为所有 2.x SDK 实施提供了指南。

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

有关更多信息，请参阅跟踪场景[在主内容中进行搜寻的 VOD 播放](/help/use-cases/tracking-scenarios/vod-seeking.md)。
