---
title: 了解如何使用JavaScript 2.x跟踪核心播放
description: 了解如何使用JavaScript 2.x应用程序在浏览器中使用Media SDK实施核心跟踪。
uuid: 3d6e0ab1-899a-43c3-b632-8276e84345ab
exl-id: d8af37a0-9048-4e6b-8cba-809386cbed5f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 94%

---

# 使用 JavaScript 2.x 跟踪核心播放{#track-core-playback-on-javascript}

以下说明为跨2.x SDK实施提供了指南。

>[!IMPORTANT]
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)

1. **初始跟踪设置**

   识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启）并创建 `MediaObject` 实例。

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 媒体名称 | 是 |
   | `mediaid` | 媒体唯一标识符 | 是 |
   | `length` | 媒体长度 | 是 |
   | `streamType` | 流类型（请参阅下面的 _StreamType 常量_） | 是 |
   | `mediaType` | 媒体类型（请参阅下面的 _MediaType 常量_） | 是 |

   **`StreamType`常量：**

   | 常量名称 | 描述   |
   |---|---|
   | `VOD` | 点播视频的流类型。 |
   | `LIVE` | 实时内容的流类型。 |
   | `LINEAR` | 线性内容的流类型。 |
   | `AOD` | 点播音频的流类型。 |
   | `AUDIOBOOK` | 有声读物的流类型。 |
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

   （可选）通过上下文数据变量将标准和/或自定义元数据对象附加到跟踪会话。

   * **标准元数据**

      [在 JavaScript 中实施标准元数据](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)

      >[!NOTE]
      >
      >将标准元数据对象附加到媒体对象是可选的。

      * 媒体元数据键 API 引用 - [标准元数据键 - JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript)

         请在此处查看可用元数据的完整集合：[音频和视频参数](/help/implementation/variables/audio-video-parameters.md)
   * **自定义元数据**

      为自定义变量创建变量对象，然后使用此媒体的数据进行填充。例如：

      ```js
      /* Set custom context data */
      var customVideoMetadata = {
          isUserLoggedIn: "false",
          tvStation: "Sample TV station",
          programmer: "Sample programmer"
      };
      ```


1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请在媒体心率实例中调用 `trackSessionStart`：

   ```js
   mediaHeartbeat.trackSessionStart(mediaObject, customVideoMetadata);
   ```

   >[!TIP]
   >
   >第二个值是您在步骤 2 中创建的自定义媒体元数据对象名称。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪的是用户的播放意图，而不是播放的开始。此 API 用于加载数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >如果不使用自定义元数据，则只需在 `trackSessionStart` 中为 `data` 参数发送一个空对象，如上面 iOS 示例中注释掉的行所示。

1. **跟踪播放的实际开始事件**

   识别媒体播放器中的播放开始事件（媒体的第一帧呈现在屏幕上）并调用 `trackPlay`：

   ```js
   mediaHeartbeat.trackPlay();
   ```

1. **跟踪播放的结束事件**

   识别媒体播放器中的播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`：

   ```js
   mediaHeartbeat.trackComplete();
   ```

1. **跟踪会话的结束事件**

   识别媒体播放器中的播放卸载/关闭事件（用户关闭媒体和/或媒体已结束并卸载）并调用 `trackSessionEnd`：

   ```js
   mediaHeartbeat.trackSessionEnd();
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。在调用 `trackSessionEnd` 之后，任何其他 `track*` API 调用都将被忽略（除了用于新的跟踪会话的 `trackSessionStart` 之外）。

1. **跟踪所有可能的暂停方案**

   识别媒体播放器中的暂停事件并调用 `trackPause`：

   ```js
   mediaHeartbeat.trackPause();
   ```

   **暂停方案**

   识别媒体播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`：

   * 用户在应用程序中明确点击暂停。
   * 播放器将其置于“暂停”状态。
   * （*移动应用程序*）- 用户将应用程序放入后台，但您希望应用程序保持会话打开。
   * （*移动应用程序*）- 发生导致应用程序被置于后台运行的任何类型的系统中断。例如，用户接到电话，或其他应用程序出现弹出窗口，但您希望应用程序保持会话的活动状态，以便用户有机会从中断点恢复媒体。

1. 识别播放器中的播放事件和/或在暂停后继续播放的事件并调用 `trackPlay`：

   ```js
   mediaHeartbeat.trackPlay();
   ```

   >[!TIP]
   >
   >这可能与步骤 4 中所使用的事件源相同。请确保当播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

* 跟踪方案：[不含广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* JavaScript SDK 随附的示例播放器提供了完整的跟踪示例。
