---
seo-title: 在 JavaScript 中跟踪错误
title: 在 JavaScript 中跟踪错误
uuid: 5fc5fc-2677-4189-92aff-5cd074847b39
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 JavaScript 中跟踪错误{#track-errors-on-javascript}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## 实施错误跟踪

1. 跟踪媒体播放器错误：

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>跟踪媒体播放器错误不会停止媒体跟踪会话。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

