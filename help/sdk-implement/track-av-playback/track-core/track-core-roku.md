---
seo-title: 在 Roku 中跟踪核心播放
title: 在 Roku 中跟踪核心播放
uuid: a8aa7b3c-2d39-44d7-8eBC-b101 d130101 f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 Roku 中跟踪核心播放{#track-core-playback-on-roku}

>[!IMPORTANT]
>此文档涵盖SDK的版本2.x跟踪。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)

1. **初始跟踪设置**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   **`MediaObject`参考：**

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 视频名称 | 是 |
   | `mediaid` | 视频唯一标识符 | 是 |
   | `length` | 视频长度 | 是 |
   | `streamType` | Stream type (see _StreamType constants_ below) | 是 |
   | `mediaType` | Media type (see _MediaType constants_ below) | 是 |

   **`StreamType`常量：**

   | 常量名称 | 描述   |
   |---|---|
   | `MEDIA_STREAM_TYPE_VOD` | 点播视频的流类型。 |
   | `MEDIA_STREAM_TYPE_LIVE` | 实时内容的流类型。 |
   | `MEDIA_STREAM_TYPE_LINEAR` | 线性内容的流类型。 |
   | `MEDIA_STREAM_TYPE_AOD` | 点播音频的流类型。 |
   | `MEDIA_STREAM_TYPE_AUDIOBOOK` | 有声读物的流类型。 |
   | `MEDIA_STREAM_TYPE_PODCAST` | 播客的流类型。 |

   **`MediaType`常量：**

   | 常量名称 | 描述 |
   |---|---|
   | `MEDIA_STREAM_TYPE_AUDIO` | 音频流的媒体类型。 |
   | `MEDIA_STREAM_TYPE_VIDEO` | 视频流的媒体类型。 |

   **使用VOD内容创建视频的媒体信息对象：**

   ```
    mediaInfo = adb_media_init_mediainfo(
     "<MEDIA_NAME>",
     "<MEDIA_ID>",
     600,
     ADBMobile().MEDIA_STREAM_TYPE_VOD,
     ADBMobile().MEDIA_TYPE_VIDEO
   )
   ```

   或

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_VOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_VIDEO
   ```

   **使用AOD内容创建视频的媒体信息对象：**

   ```
   mediaInfo = adb_media_init_mediainfo(
    "<MEDIA_NAME>", 
    "<MEDIA_ID>", 
    600, 
    ADBMobile().MEDIA_STREAM_TYPE_AOD, 
    ADBMobile().MEDIA_TYPE_AUDIO
   )
   ```

   或

   ```
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.name = "<MEDIA_NAME>"
   mediaInfo.id = "<MEDIA_ID>"
   mediaInfo.length = 600
   mediaInfo.streamType = ADBMobile().MEDIA_STREAM_TYPE_AOD
   mediaInfo.mediaType = ADBMobile().MEDIA_TYPE_AUDIO
   ```

1. **附加元数据**

   (可选)通过上下文数据变量将标准和/或自定义元数据对象附加到跟踪会话。

   * **标准元数据**

      [在 JavaScript 中实施标准元数据](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >将标准元数据对象附加到媒体对象是可选的。

      * 媒体元数据键 API 引用 - [标准元数据键 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](/help/metrics-and-metadata/audio-video-parameters.md)
   * **自定义元数据**

      为自定义变量创建一个变量对象，然后填充该媒体的数据。例如：

      ```js
      /* Set custom context data */ 
      var customVideoMetadata = { 
          isUserLoggedIn: "false", 
          tvStation: "Sample TV station", 
          programmer: "Sample programmer" 
      };
      ```


1. **跟踪开始播放的目的**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >第二个值是您在步骤中创建的自定义媒体元数据对象名称。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪用户的播放意图，而不是播放开始。此 API 用于加载数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **跟踪实际播放开始**

   Identify the event from the media player for the beginning of the playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **跟踪播放完成**

   Identify the event from the media player for the completion of the playback, where the user has watched the content until the end, and call `trackComplete`:

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **跟踪会话结束**

   Identify the event from the media player for the unloading/closing of the playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >A `trackSessionEnd` marks the end of a tracking session. 如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.  用于跟踪媒体载入以及将当前会话设置为活动的媒体播放跟踪方法：

   ```
   ‘ Create a media info object
   mediaInfo = adb_media_init_mediainfo()
   mediaInfo.id = <MEDIA_ID>
   mediaInfo.playhead = "0"
   mediaInfo.length = "600"
   ```

1. **附加视频元数据**

   (可选)通过上下文数据变量将标准和/或自定义视频元数据对象附加到视频跟踪会话。

   * **标准视频元数据**

      [在 Roku 中实施标准元数据](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >将标准视频元数据对象附加到媒体对象是可选的。

   * **自定义元数据**

      为自定义变量创建一个变量对象，然后填充该视频的数据。例如：

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **跟踪开始播放的目的**

   To begin tracking a media session, call `trackSessionStart` on the Media Heartbeat instance:

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >第二个值是您在步骤中创建的自定义视频元数据对象名称。

   >[!IMPORTANT]
   >`trackSessionStart` 跟踪用户的播放意图，而不是播放开始。此 API 用于加载视频数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **跟踪实际播放开始**

   识别视频播放器中的视频播放开始事件（视频的第一帧呈现在屏幕上）并调用 `trackPlay`()：

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **跟踪播放完成**

   识别视频播放器中的视频播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`()：

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **跟踪会话结束**

   识别视频播放器中的视频播放卸载/关闭事件（用户关闭视频和/或视频已结束并卸载）并调用 `trackSessionEnd`()：

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` 标记视频跟踪会话的结束。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **跟踪所有可能的暂停场景**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   ADBMobile().mediaTrackPause()
   ```

   **暂停场景**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下方案均要求应用程序调用 `trackPause()`()：

   * 用户在应用程序中明确点击暂停。
   * 播放器自行进入暂停状态。
   * （*移动设备应用程序*）- 用户将应用程序置于后台，但您希望应用程序保持会话打开。
   * （*移动设备应用程序*）- 出现导致应用程序被置于后台的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续观看视频。

1. 识别播放器中的视频播放事件和/或视频在暂停后继续播放的事件，并调用 `trackPlay`：

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >这可能与在步骤中使用的相同。请确保当视频播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

* 跟踪方案：[不含广告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Roku SDK 随附有示例播放器，用于提供完整的跟踪示例。

