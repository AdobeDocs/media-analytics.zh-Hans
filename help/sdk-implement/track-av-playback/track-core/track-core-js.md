---
seo-title: 在 JavaScript 中跟踪核心播放
title: 在 JavaScript 中跟踪核心播放
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345 ab
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# 在 JavaScript 中跟踪核心播放{#track-core-playback-on-javascript}

>[!IMPORTANT]
>此文档涵盖SDK的版本2.x跟踪。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](../../../sdk-implement/download-sdks.md)

1. **初始跟踪设置**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 媒体名称 | 是 |
   | `mediaid` | 媒体唯一标识符 | 是 |
   | `length` | 媒体长度 | 是 |
   | `streamType` | Stream type (see _StreamType constants_ below) | 是 |
   | `mediaType` | Media type (see _MediaType constants_ below) | 是 |

   **`StreamType`常量：**

   | 常量名称 | 描述   |
   |---|---|
   | `VOD` | 点播视频的流类型。 |
   | `LIVE` | 实时内容的流类型。 |
   | `LINEAR` | 线性内容的流类型。 |
   | `AOD` | 点播音频的流类型。 |
   | `AUDIOBOOK` | 音频书籍的流类型。 |
   | `PODCAST` | 播客的流类型。 |

   **`MediaType`常量：**

   | 常量名称 | 描述 |
   |---|---|
   | `Audio` | 音频流的媒体类型。 |
   | `Video` | 视频流的媒体类型。 |

   ```
   var mediaObject =  
     MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                     <MEDIA_ID,  
                                     <MEDIA_LENGTH>, 
                                     MediaHeartbeat.StreamType.VOD,
                                     <MEDIA_TYPE>);
   ```

1. **附加元数据**

   (可选)通过上下文数据变量将标准和/或自定义元数据对象附加到跟踪会话。

   * **标准元数据**

      [在 JavaScript 中实施标准元数据](../../../sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >将标准元数据对象附加到媒体对象是可选的。

      * 媒体元数据键 API 引用 - [标准元数据键 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         See the comprehensive set of available metadata here: [Audio and video parameters](../../../metrics-and-metadata/audio-video-parameters.md)
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
   >`trackSessionEnd` 标记跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **跟踪所有可能的暂停场景**

   Identify the event from the media player for pause and call `trackPause`:

   ```js
   mediaHeartbeat.trackPause();
   ```

   **暂停场景**

   Identify any scenario in which the media player will pause and make sure that `trackPause` is properly called. 以下方案均要求应用程序调用 `trackPause()`()：

   * 用户在应用程序中明确点击暂停。
   * 播放器自行进入暂停状态。
   * （*移动设备应用程序*）- 用户将应用程序置于后台，但您希望应用程序保持会话打开。
   * （*移动设备应用程序*）- 出现导致应用程序被置于后台的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续播放媒体。

1. Identify the event from the player for play and/or resume from pause and call `trackPlay`:

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >这可能与在步骤中使用的相同。Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

* 跟踪方案：[不含广告的 VOD 播放](../../../sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript SDK 随附有示例播放器，用于提供完整的跟踪示例。

