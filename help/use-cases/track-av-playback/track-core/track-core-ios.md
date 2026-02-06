---
title: 了解如何在 iOS 上跟踪核心播放
description: 了解如何使用 iOS 上的 Media SDK 实施核心跟踪。
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
exl-id: 5c6b36b3-a421-45a4-a65e-4eb57513ca4a
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 90%

---

# 在 iOS 中跟踪核心播放{#track-core-playback-on-ios}

本文档介绍 2.x 版本的 SDK 中的跟踪。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)

1. **初始跟踪设置**

   识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启）并创建 `MediaObject` 实例。

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | 变量名称 | 描述 | 必需 |
   |---|---|---|
   | `name` | 视频名称 | 是 |
   | `mediaid` | 视频唯一标识符 | 是 |
   | `length` | 视频长度 | 是 |
   | `streamType` | 流类型（请参阅下面的 _StreamType 常量_） | 是 |
   | `mediaType` | 媒体类型（请参阅下面的 _MediaType 常量_） | 是 |

   **`StreamType`常量：**

   | 常量名称 | 描述 |
   |---|---|
   | `ADBMediaHeartbeatStreamTypeVOD` | 点播视频的流类型。 |
   | `ADBMediaHeartbeatStreamTypeLIVE` | 实时内容的流类型。 |
   | `ADBMediaHeartbeatStreamTypeLINEAR` | 线性内容的流类型。 |
   | `ADBMediaHeartbeatStreamTypeAOD` | 点播音频的流类型。 |
   | `ADBMediaHeartbeatStreamTypeAUDIOBOOK` | 有声读物的流类型。 |
   | `ADBMediaHeartbeatStreamTypePODCAST` | 播客的流类型。 |

   **`MediaType`常量：**

   | 常量名称 | 描述 |
   |---|---|
   | `ADBMediaTypeAudio` | 音频流的媒体类型。 |
   | `ADBMediaTypeVideo` | 视频流的媒体类型。 |

   创建 `MediaObject` 的一般格式：

   ```
   ADBMediaObject *mediaObject =  
     [ADBMediaHeartbeat createMediaObjectWithName:<MEDIA_NAME>
                                          mediaId:<MEDIA_ID>
                                           length:<MEDIA_LENGTH>                       
                                       streamType:<STREAM_TYPE>
                                        mediaType: <MEDIA_TYPE>];
   ```

1. **附加视频元数据**

   （可选）通过上下文数据变量将标准和/或自定义视频元数据对象附加到视频跟踪会话。

   * **标准视频元数据**

      * [在 iOS 中实施标准元数据](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **视频元数据键**
        [iOS 元数据键](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * 请在此处查看视频元数据的完整列表：[音频和视频参数](/help/implementation/variables/audio-video-parameters.md)

     >[!NOTE]
     >
     >将标准视频元数据对象附加到媒体对象是可选的。

   * **自定义元数据**

     为自定义变量创建变量对象，然后使用此视频的数据进行填充。例如：

     ```
     NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
     [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
     [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
     ```

1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请在媒体心跳实例中调用 `trackSessionStart`。

   >[!TIP]
   >
   >第二个值是您在步骤 2 中创建的自定义视频元数据对象名称。

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification {
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil];
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪的是用户的播放意图，而不是播放的开始。此 API 用于加载视频数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >如果不使用自定义视频元数据，则只需在 `trackSessionStart` 中为 `data` 参数发送一个空对象，如上面 iOS 示例中注释掉的行所示。

1. **跟踪播放的实际开始事件**

   识别视频播放器中的视频播放开始事件（视频的第一帧呈现在屏幕上）并调用 `trackPlay`：

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

1. **跟踪播放的结束事件**

   识别视频播放器中的视频播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`：

   ```
   - (void)onVideoComplete:(NSNotification *)notification {
       [_mediaHeartbeat trackComplete];
   }
   ```

1. **跟踪会话的结束事件**

   识别视频播放器中的视频播放卸载/关闭事件（用户关闭视频和/或视频已结束并卸载）并调用 `trackSessionEnd`：

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification {
       [_mediaHeartbeat trackSessionEnd];
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记视频跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。在调用 `trackSessionEnd` 之后，任何其他 `track*` API 调用都将被忽略（除了用于新的视频跟踪会话的 `trackSessionStart` 之外）。

1. **跟踪所有可能的暂停方案**

   识别视频播放器中的视频暂停事件并调用 `trackPause`：

   ```
   - (void)onVideoPause:(NSNotification *)notification {
       [_mediaHeartbeat trackPause];
   }
   ```

   **暂停方案**

   识别视频播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`：

   * 用户在应用程序中明确点击暂停。
   * 播放器将其置于“暂停”状态。
   * （*移动应用程序*）- 用户将应用程序放入后台，但您希望应用程序保持会话打开。
   * （*移动应用程序*）- 发生导致应用程序被置于后台运行的任何类型的系统中断。例如，用户接到电话，或其他应用程序出现弹出窗口，但您希望应用程序保持会话的活动状态，以便用户有机会从中断点恢复视频。

1. 识别播放器中的视频播放事件和/或视频在暂停后继续播放的事件并调用 `trackPlay`：

   ```
   - (void)onVideoPlay:(NSNotification *)notification {
       [_mediaHeartbeat trackPlay];
   }
   ```

   >[!TIP]
   >
   >这可能与步骤 4 中所使用的事件源相同。请确保当视频播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

有关跟踪核心播放的其他信息，请参阅以下内容：

* 跟踪场景：[不含广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* iOS SDK随附的示例播放器提供了完整的跟踪示例。
