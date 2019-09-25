---
seo-title: 在 Chromecast 中跟踪核心播放
title: 在 Chromecast 中跟踪核心播放
uuid: a9fc59d8-a2f4-4889-bdec-55c42a835d06
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 Chromecast 中跟踪核心播放{#track-core-playback-on-chromecast}

>[!IMPORTANT]
>
>This documentation covers tracking in version 2.x of the SDK. 如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)

1. **初始跟踪设置**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`API 引用:**

   [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

   ```
   mediaObject = ADBMobile.media.createMediaObject(<name>, <id>, <duration>, <streamType>, <mediaType>); 
   ```

   **`StreamType`常量：**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.StreamType)

   **`MediaType`constants:**

   [ADBMobile Media](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.MediaType)

1. **Attach video metadata**

   （可选）通过上下文数据变量将标准和／或自定义视频元数据对象附加到视频跟踪会话。

   * **标准视频元数据**

      [在 Chromecast 中实施标准元数据](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)

      >[!NOTE]
      >
      >将标准视频元数据对象附加到媒体对象是可选的。

   * **自定义元数据**

      为自定义变量创建一个变量对象，并填充此视频的数据。 例如：

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```

1. **跟踪开始播放的意图**

   To begin tracking a media session, call trackSessionStart on the  object.[](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionStart)`media`

   ```
   ADBMobile.media.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪用户的播放意图，而不是播放的开始。 此 API 用于加载视频数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >The second value is the custom video metadata object name that you created in step 2. If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **跟踪实际播放开始**

   Identify the event from the video player for the beginning of the video playback, where the first frame of the video is rendered on the screen, and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPlay)

   ```
   ADBMobile.media.trackPlay();
   ```

1. **Track the completion of playback**

   Identify the event from the video player for the completion of the video playback, where the user has watched the content until the end, and call [trackComplete:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackComplete();
   ```

1. **Track the end of the session**

   Identify the event from the video player for the unloading/closing of the video playback, where the user closes the video and/or the video is completed and has been unloaded, and call [trackSessionEnd:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackSessionEnd)

   ```
   ADBMobile.media.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` marks the end of a video tracking session. 如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **跟踪所有可能的暂停方案**

   Identify the event from the video player for video pause and call [trackPause:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackPause)

   ```
   ADBMobile.media.trackPause();
   ```

   **暂停方案**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下方案均要求应用程序调用 `trackPause()`()：

   * 用户在应用程序中明确点击暂停。
   * 播放器自行进入暂停状态。
   * （*移动设备应用程序*）- 用户将应用程序置于后台，但您希望应用程序保持会话打开。
   * （*移动设备应用程序*）- 出现导致应用程序被置于后台的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续观看视频。

1. Identify the event from the player for video play and/or video resume from pause and call [trackPlay:](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackComplete)

   ```
   ADBMobile.media.trackPlay();
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. 请确保当视频播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

* 跟踪方案：[不含广告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Chromecast SDK 随附有示例播放器，用于提供完整的跟踪示例。

