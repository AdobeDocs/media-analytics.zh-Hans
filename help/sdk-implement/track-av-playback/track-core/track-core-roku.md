---
title: 了解如何在 Roku 上跟踪核心播放
description: 了解如何使用 Roku 上的媒体 SDK 实施核心跟踪。
uuid: a8aa7b3c-2d39-44d7-8ebc-b101d130101f
exl-id: 5272c0ce-4e3d-48c6-bfa6-94066ccbf9ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 14329fab02e88cbad69ceea4ccd719b90f6555a6
workflow-type: ht
source-wordcount: '771'
ht-degree: 100%

---

# 在 Roku 中跟踪核心播放{#track-core-playback-on-roku}

本文档介绍 2.x 版本的 SDK 中的跟踪。

>[!IMPORTANT]
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)

1. **初始跟踪设置**

   识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启）并创建 `MediaObject` 实例。

   **`MediaObject`引用：**

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 视频名称 | 是 |
   | `mediaid` | 视频唯一标识符 | 是 |
   | `length` | 视频长度 | 是 |
   | `streamType` | 流类型（请参阅下面的 _StreamType 常量_） | 是 |
   | `mediaType` | 媒体类型（请参阅下面的 _MediaType 常量_） | 是 |

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

   **为包含 VOD 内容的视频创建媒体信息对象：**

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

   **为包含 AOD 内容的视频创建媒体信息对象：**

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

   （可选）通过上下文数据变量将标准和/或自定义元数据对象附加到跟踪会话。

   * **标准元数据**

[在 Roku 中实施标准元数据](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)

      >[!NOTE]
      >将标准视频元数据对象附加到媒体对象是可选的。

   * **自定义元数据**

      为自定义变量创建变量对象，然后使用此视频的数据进行填充。例如：

      ```
      mediaContextData = {}
      mediaContextData["cmk1"] = "cmv1"
      mediaContextData["cmk2"] = "cmv2"
      ```

1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请在媒体心率实例中调用 `trackSessionStart`：

   ```
   ADBMobile().mediaTrackSessionStart(mediaInfo,mediaContextData)
   ```

   >[!TIP]
   >第二个值是您在步骤 2 中创建的自定义视频元数据对象名称。

   >[!IMPORTANT]
   >`trackSessionStart` 跟踪的是用户的播放意图，而不是播放的开始。此 API 用于加载视频数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >如果不使用自定义视频元数据，则只需在 `trackSessionStart` 中为 `data` 参数发送一个空对象，如上面 iOS 示例中注释掉的行所示。

1. **跟踪播放的实际开始事件**

   识别视频播放器中的视频播放开始事件（视频的第一帧呈现在屏幕上）并调用 `trackPlay`：

   ```
   ADBMobile().mediaTrackPlay()
   ```

1. **更新播放头值**

   当媒体播放头发生变化时，通过调用`mediaUpdatePlayhead` API 通知 SDK。<br />对于视频点播 (VOD)，该值以从媒体项开头开始的秒数指定。<br />对于直播，如果播放器不提供有关内容持续时间的信息，则该值可以指定为自当天 UTC 午夜开始的秒数。<br />请注意：使用进度标记时，需要内容持续时间，并且播放头需要更新为从媒体项目开始的秒数，从 0 开始。


   ```
   ADBMobile().mediaUpdatePlayhead(position)
   ```

1. **跟踪播放的结束事件**

   识别视频播放器中的视频播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`：

   ```
   ADBMobile().mediaTrackComplete()
   ```

1. **跟踪会话的结束事件**

   识别视频播放器中的视频播放卸载/关闭事件（用户关闭视频和/或视频已结束并卸载）并调用 `trackSessionEnd`：

   ```
   ADBMobile().mediaTrackSessionEnd()
   ```

   >[!IMPORTANT]
   >`trackSessionEnd` 标记视频跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。在调用 `trackSessionEnd` 之后，任何其他 `track*` API 调用都将被忽略（除了用于新的视频跟踪会话的 `trackSessionStart` 之外）。

1. **跟踪所有可能的暂停方案**

   识别视频播放器中的视频暂停事件并调用 `trackPause`：

   ```
   ADBMobile().mediaTrackPause()
   ```

   **暂停方案**

   识别视频播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`：

   * 用户在应用程序中明确点击暂停。
   * 播放器将其置于“暂停”状态。
   * （*移动应用程序*）- 用户将应用程序放入后台，但您希望应用程序保持会话打开。
   * （*移动应用程序*）- 发生导致应用程序被置于后台运行的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续观看视频。

1. 识别播放器中的视频播放事件和/或视频在暂停后继续播放的事件并调用 `trackPlay`：

   ```
   ADBMobile().mediaTrackPlay()
   ```

   >[!TIP]
   >这可能与步骤 4 中所使用的事件源相同。请确保当视频播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

* 跟踪方案：[不含广告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Roku SDK 随附有示例播放器，用于提供完整的跟踪示例。
