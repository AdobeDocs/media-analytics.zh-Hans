---
title: 了解如何使用 JavaScript v3.x 跟踪核心播放
description: 了解如何使用 JavaScript 3.x 应用程序在浏览器中使用 Media SDK 实施核心跟踪。
exl-id: f3145450-82ba-4790-91a4-9d2cc97bbaa5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: c308dba2d7cf07b89bf124bd6e5f972c253c9f18
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 87%

---

# 使用 JavaScript 3.x 跟踪核心播放{#track-core-playback-on-javascript}

本文档介绍 3.x 版本的 SDK 中的跟踪。

>[!IMPORTANT]
>
>如果您实施的是 SDK 之前的版本，可以在此处下载开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

1. **初始跟踪设置**

   识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启）并创建 `MediaObject` 实例。

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 变量名称 | 类型 | 描述 |
   | --- | --- | --- |
   | `name` | 字符串 | 表示媒体名称的非空字符串。 |
   | `id` | 字符串 | 表示唯一媒体标识符的非空字符串。 |
   | `length` | 数字 | 正数，表示媒体长度（秒）。如果长度未知，则使用 0 表示。 |
   | `streamType` | 字符串 |   |
   | `mediaType` | | 媒体类型（音频或视频）。 |

   **`StreamType`常量：**

   | 常量名称 | 描述   |
   |---|---|
   | `VOD` | 点播视频的流类型。 |
   | `AOD` | 点播音频的流类型。 |

   **`MediaType`常量：**

   | 常量名称 | 描述 |
   |---|---|
   | `Audio` | 音频流的媒体类型。 |
   | `Video` | 视频流的媒体类型。 |

   ```
   var mediaObject = ADB.Media.createMediaObject(<MEDIA_NAME>,
                                     <MEDIA_ID,
                                     <MEDIA_LENGTH>,
                                     <STREAM_TYPE>,
                                     <MEDIA_TYPE>);
   ```

1. **附加元数据**

   （可选）通过上下文数据变量将标准和/或自定义元数据附加到跟踪会话。

   * **标准元数据**

     >[!NOTE]
     >
     >附加标准元数据是可选操作。

      * 媒体元数据键 API 引用 - [标准元数据键 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

        请在此处查看可用元数据的完整集合：[音频和视频参数](/help/implementation/variables/audio-video-parameters.md)

   * **自定义元数据**

     为自定义变量创建变量对象，然后使用此媒体的数据进行填充。例如：

     ```js
     /* Set context data */
      var contextData = {};
     
      //Standard metadata
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
      contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
     
      //Custom metadata
      contextData["isUserLoggedIn"] = "false";
      contextData["tvStation"] = "Sample TV Station";
     ```

1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请在媒体心跳实例中调用 `trackSessionStart`：

   ```js
   var mediaObject = ADB.Media.createMediaObject("video-name",
                                                 "video-id",
                                                 60.0,
                                                 ADB.Media.StreamType.VOD,
                                                 ADB.Media.MediaType.Video);
   
   var contextData = {};
   
   //Standard metadata
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Episode";
   contextData[ADB.Media.VideoMetadataKeys] = "Sample Show";
   
   //Custom metadata
   contextData["isUserLoggedIn"] = "false";
   contextData["tvStation"] = "Sample TV Station";
   
   tracker.trackSessionStart(mediaObject, contextData);
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪的是用户的播放意图，而不是播放的开始。此 API 用于加载数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >如果不使用 contextData，则只需在 `trackSessionStart` 中为 `data` 参数发送一个空对象。

1. **跟踪播放的实际开始事件**

   识别媒体播放器中的播放开始事件（媒体的第一帧呈现在屏幕上）并调用 `trackPlay`：

   ```js
   tracker.trackPlay();
   ```

1. **更新播放头值**

   当媒体播放头发生变化时，通过调用`mediaUpdatePlayhead` API通知SDK。 <br />对于视频点播 (VOD)，该值以从媒体项开头开始的秒数指定。<br />对于直播，如果播放器不提供有关内容持续时间的信息，则该值可以指定为自当天UTC午夜开始的秒数。

   ```
   tracker.updatePlayhead(position)
   ```

   >[!NOTE]
   >
   >调用`tracker.updatePlayhead` API时，请考虑以下事项：
   >* 使用进度标记时，需要内容持续时间，并且播放头需要更新为从媒体项目开始的秒数，从0开始。
   >* 使用Media SDK时，必须每秒至少调用一次`tracker.updatePlayhead` API。

1. **跟踪播放的结束事件**

   识别媒体播放器中的播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`：

   ```js
   tracker.trackComplete();
   ```

1. **跟踪会话的结束事件**

   识别媒体播放器中的播放卸载/关闭事件（用户关闭媒体和/或媒体已结束并卸载）并调用 `trackSessionEnd`：

   ```js
   tracker.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。在调用 `trackSessionEnd` 之后，任何其他 `track*` API 调用都将被忽略（除了用于新的跟踪会话的 `trackSessionStart` 之外）。

1. **跟踪所有可能的暂停方案**

   识别媒体播放器中的暂停事件并调用 `trackPause`：

   ```js
   tracker.trackPause();
   ```

   **暂停方案**

   识别媒体播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`：

   * 用户在应用程序中明确点击暂停。
   * 播放器将其置于“暂停”状态。
   * （*移动应用程序*）- 用户将应用程序放入后台，但您希望应用程序保持会话打开。
   * （*移动应用程序*）- 发生导致应用程序被置于后台运行的任何类型的系统中断。例如，用户接到电话，或其他应用程序出现弹出窗口，但您希望应用程序保持会话的活动状态，以便用户有机会从中断点恢复媒体。

1. 识别播放器中的播放事件和/或在暂停后继续播放的事件并调用 `trackPlay`：

   ```js
   tracker.trackPlay();
   ```

   >[!TIP]
   >
   >这可能与步骤 4 中所使用的事件源相同。请确保当播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

* 跟踪场景：[不含广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript SDK 随附的示例播放器提供了完整的跟踪示例。
