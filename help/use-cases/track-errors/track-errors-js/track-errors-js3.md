---
title: 了解如何使用 JavaScript 3.x 跟踪错误
description: 了解如何在浏览器应用程序 (JS) 中使用 Media SDK 实施错误跟踪。
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 100%

---

# 使用 JavaScript 3.x 跟踪错误{#track-errors-on-javascript}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
>如果您实施的是 SDK 之前的版本，可以在此处下载开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施错误跟踪

1. 跟踪媒体播放器错误：

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd` 后调用 `trackError` 来关闭媒体跟踪会话。
