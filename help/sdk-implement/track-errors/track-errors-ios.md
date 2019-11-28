---
title: 在 iOS 中跟踪错误
description: 本主题介绍如何在 iOS 中使用 Media SDK 实施错误跟踪。
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 iOS 中跟踪错误{#track-errors-on-ios}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

## 实施错误跟踪

1. 跟踪媒体播放器错误：

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"mediaoErrorId"]; 
   }
   ```

>[!NOTE]
>
>跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd` 后调用 `trackError` 来关闭媒体跟踪会话。

