---
title: 了解如何在Chromecast中跟踪核心播放
description: 了解如何在Chromecast中使用Media SDK实施核心跟踪。
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
exl-id: 9812d06d-9efd-460c-a626-6a15f61a4c35
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 96%

---

# 在 Chromecast 中跟踪核心播放{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>本文档介绍 2.x 版本的 SDK 中的跟踪。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)

1. **初始跟踪设置**

   识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启）并创建 `MediaObject` 实例。

   **`MediaObject`API 引用：**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`常量：**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`常量：**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **附加视频元数据**

   （可选）通过上下文数据变量将标准和/或自定义视频元数据对象附加到视频跟踪会话。

   * **标准视频元数据**

      [在 Chromecast 中实施标准元数据](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >将标准视频元数据对象附加到媒体对象是可选的。

   * **自定义元数据**

      为自定义变量创建变量对象，然后使用此视频的数据进行填充。例如：

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请在 `media` 对象中调用 [trackSessionStart](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart)。

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪的是用户的播放意图，而不是播放的开始。此 API 用于加载视频数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >第二个值是您在步骤 2 中创建的自定义视频元数据对象名称。如果不使用自定义视频元数据，则只需在 `trackSessionStart` 中为 `data` 参数发送一个空对象，如上面 iOS 示例中注释掉的行所示。

1. **跟踪播放的实际开始事件**

   识别视频播放器中的视频播放开始事件（视频的第一帧呈现在屏幕上）并调用 [trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)：

   ```
   ADBMobile.media.trackPlay();
   ```

1. **跟踪播放的结束事件**

   识别视频播放器中的视频播放结束事件（用户一直观看至内容的结尾）并调用 [trackComplete](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)：

   ```
   ADBMobile.media.trackComplete();
   ```

1. **跟踪会话的结束事件**

   识别视频播放器中的视频播放卸载/关闭事件（用户关闭视频和/或视频已结束并卸载）并调用 [trackSessionEnd](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)：

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记视频跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。在调用 `trackSessionEnd` 之后，任何其他 `track*` API 调用都将被忽略（除了用于新的视频跟踪会话的 `trackSessionStart` 之外）。

1. **跟踪所有可能的暂停方案**

   识别视频播放器中的视频暂停事件并调用 [trackPause](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)：

   ```
   ADBMobile.media.trackPause();
   ```

   **暂停方案**

   识别视频播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`：

   * 用户在应用程序中明确点击暂停。
   * 播放器将其置于“暂停”状态。
   * （*移动应用程序*）- 用户将应用程序放入后台，但您希望应用程序保持会话打开。
   * （*移动应用程序*）- 发生导致应用程序被置于后台运行的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续观看视频。

1. 识别播放器中的视频播放事件和/或视频在暂停后继续播放的事件并调用 [trackPlay](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)：

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >这可能与步骤 4 中所使用的事件源相同。请确保当视频播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

* 跟踪方案：[不含广告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Chromecast SDK 随附有示例播放器，用于提供完整的跟踪示例。
