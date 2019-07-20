---
seo-title: 在 Android 中跟踪错误
title: 在 Android 中跟踪错误
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# 在 Android 中跟踪错误{#track-errors-on-android}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

1. 跟踪媒体播放器错误：

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>跟踪媒体播放器错误不会停止媒体跟踪会话。If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

