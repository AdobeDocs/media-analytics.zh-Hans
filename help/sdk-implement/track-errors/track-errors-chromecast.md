---
seo-title: 在 Chromecast 中跟踪错误
title: 在 Chromecast 中跟踪错误
uuid: efa9de8d-c626-4cb6-b46d-108495dd013a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 Chromecast 中跟踪错误{#track-errors-on-chromecast}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implement error tracking

1. Track media player errors: [trackError](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackError)

   ```
   trackError(errorId)
   ```

>[!NOTE]
>
>Tracking media player errors will not stop the media tracking session. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

