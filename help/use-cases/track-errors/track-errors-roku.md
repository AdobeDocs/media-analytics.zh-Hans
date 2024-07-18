---
title: 了解如何在 Roku 中跟踪错误
description: 了解如何在 Roku 中使用 Media SDK 实施错误跟踪。
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 100%

---

# 在 Roku 中跟踪错误{#track-errors-on-roku}

以下说明为所有 2.x SDK 实施提供了指南。

>[!IMPORTANT]
>
> 如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 实施错误跟踪

1. 跟踪媒体播放器错误：

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(),
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>跟踪媒体播放器错误不会停止媒体跟踪会话。如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd` 后调用 `trackError` 来关闭媒体跟踪会话。
