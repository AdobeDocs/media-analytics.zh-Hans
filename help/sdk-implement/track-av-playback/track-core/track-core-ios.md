---
seo-title: 在 iOS 中跟踪核心播放
title: 在 iOS 中跟踪核心播放
uuid: bdc0e05c-4fe5-430e-aee2-f331bc59ac6b
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 iOS 中跟踪核心播放{#track-core-playback-on-ios}

>[!IMPORTANT]
>This documentation covers tracking in version 2.x of the SDK. 如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)

1. **初始跟踪设置**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObjectWithName API](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)

   | 变量名称 | 描述 | 必需 |
   |---|---|---|
   | `name` | 视频名称 | 是 |
   | `mediaid` | 视频唯一标识符 | 是 |
   | `length` | 视频长度 | 是 |
   | `streamType` | 流类型(请参阅 _下面的StreamType常量_ ) | 是 |
   | `mediaType` | 媒体类型(请参阅 _下面的MediaType常量_ ) | 是 |

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

   （可选）通过上下文数据变量将标准和／或自定义视频元数据对象附加到视频跟踪会话。

   * **标准视频元数据**

      * [在 iOS 中实施标准元数据](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
      * **视频元数据键**
         [iOS 元数据键](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

      * 请在此处查看视频元数据的完整列表：[音频和视频参数](/help/metrics-and-metadata/audio-video-parameters.md)
      >[!NOTE]
      >
      >Attaching the standard video metadata object to the media object is optional.

   * **自定义元数据**

      Create a variable object for the custom variables and populate with the data for this video. 例如：

      ```
      NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init]; 
      [videoMetadata setObject:@"false" forKey:@"isUserLoggedIn"]; 
      [videoMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
      ```


1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请调用 `trackSessionStart` 媒体心跳实例。

   >[!TIP]
   >
   >第二个值是您在步骤2中创建的自定义视频元数据对象名称。

   ```
   - (void)onMainVideoLoaded:(NSNotification *)notification { 
   //    [_mediaHeartbeat trackSessionStart:mediaObject data:nil]; 
       [_mediaHeartbeat trackSessionStart:mediaObject data:videoMetadata]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪用户的播放意图，而不是播放的开始。 此 API 用于加载视频数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >If you are not using custom video metadata, simply send an empty object for the `data` argument in `trackSessionStart`, as shown in the commented out line in the iOS example above.

1. **跟踪实际播放开始**

   识别视频播放器中的视频播放开始事件（视频的第一帧呈现在屏幕上）并调用 `trackPlay`()：

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

1. **跟踪播放的完成情况**

   识别视频播放器中的视频播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`()：

   ```
   - (void)onVideoComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackComplete]; 
   }
   ```

1. **跟踪会话结束**

   识别视频播放器中的视频播放卸载/关闭事件（用户关闭视频和/或视频已结束并卸载）并调用 `trackSessionEnd`()：

   ```
   - void)onMainVideoUnloaded:(NSNotification *)notification { 
       [_mediaHeartbeat trackSessionEnd]; 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记视频跟踪会话的结束。 如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new video tracking session.

1. **跟踪所有可能的暂停方案**

   Identify the event from the video player for video pause and call `trackPause`:

   ```
   - (void)onVideoPause:(NSNotification *)notification { 
       [_mediaHeartbeat trackPause]; 
   }
   ```

   **暂停方案**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下方案均要求应用程序调用 `trackPause()`()：

   * 用户在应用程序中明确点击暂停。
   * 播放器自行进入暂停状态。
   * （*移动设备应用程序*）- 用户将应用程序置于后台，但您希望应用程序保持会话打开。
   * （*移动设备应用程序*）- 出现导致应用程序被置于后台的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续观看视频。

1. 识别播放器中的视频播放事件和/或视频在暂停后继续播放的事件，并调用 `trackPlay`：

   ```
   - (void)onVideoPlay:(NSNotification *)notification { 
       [_mediaHeartbeat trackPlay]; 
   }
   ```

   >[!TIP]
   >
   >This may be the same event source that was used in Step 4. 请确保当视频播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

有关跟踪核心播放的其他信息，请参阅以下内容：

* 跟踪方案：[不含广告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* iOS SDK 随附有示例播放器，用于提供完整的跟踪示例。

