---
title: 使用JavaScript 3.x跟踪错误
description: 本主题介绍如何在浏览器应用程序 (JS) 中使用 Media SDK 实施错误跟踪。
translation-type: tm+mt
source-git-commit: fa161e2d41629fdfe77100d87d6a44728e23d77f
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 69%

---


# 使用JavaScript 3.x跟踪错误{#track-errors-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 3.x SDK 实施提供了指南。If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

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
