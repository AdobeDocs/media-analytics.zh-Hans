---
title: 了解如何在 Roku 中跟踪错误
description: 了解如何在 Roku 中使用 Media SDK 实施错误跟踪。
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
exl-id: 6a6aae4c-60c3-43ea-9954-0bb31f6456f8
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/S18A1AAxOQYLn216PtfA3IyO6F9j-WAAeHzlQn5UKvI
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 97
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
>跟踪媒体播放器错误不会停止媒体跟踪会话。 如果媒体播放器错误导致无法继续播放，请确保通过调用 `trackSessionEnd` 后调用 `trackError` 来关闭媒体跟踪会话。
