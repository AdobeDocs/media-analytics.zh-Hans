---
title: 在 Android 中跟踪错误
description: 本主题介绍如何在 Android 中使用 Media SDK 实施错误跟踪。
uuid: 7d0c77e5-924c-4619-8e29-3484748ab736
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Android 中跟踪错误{#track-errors-on-android}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

1. 跟踪媒体播放器错误：

   ```java
   public void onPlayerError(Observable observable, Object data) {  
       _heartbeat.trackError("mediaErrorID"); 
   }
   ```

>[!NOTE]
>
>跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd` 后调用 `trackError` 来关闭媒体跟踪会话。

