---
title: 了解如何在 Android 中跟踪核心播放
description: 了解如何使用 Android 上的 Media SDK 实施核心跟踪。
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
exl-id: d5f5a3f0-f1e0-4d68-af7f-88a30faed0db
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '708'
ht-degree: 100%

---

# 在 Android 中跟踪核心播放{#track-core-playback-on-android}

本文档介绍 2.x 版本的 SDK 中的跟踪。
>[!IMPORTANT]
>如果您实施的是 1.x 版本的 SDK，可以在此处下载适用于 Android 的 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)

1. **初始跟踪设置**

   识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启）并创建 `MediaObject` 实例。

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 媒体名称 | 是 |
   | `mediaId` | 媒体唯一标识符 | 是 |
   | `length` | 媒体长度 | 是 |
   | `streamType` | 流类型（请参阅下面的 _StreamType 常量_） | 是 |
   | `mediaType` | 媒体类型（请参阅下面的 _MediaType 常量_） | 是 |

   **`StreamType`常量：**

   | 常量名称 | 描述 |
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
   MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
     <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);
   ```

1. **附加元数据**

   （可选）通过上下文数据变量将标准和/或自定义元数据对象附加到跟踪会话。

   * **标准元数据**

      [在 Android 中实施标准元数据](/help/use-cases/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >将标准元数据对象附加到媒体对象是可选的。

      * 媒体元数据键 API 引用 - [标准元数据键 - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * 请在此处查看可用视频元数据的完整集合：[音频和视频参数](/help/implementation/variables/audio-video-parameters.md)
   * **自定义元数据**

      为自定义变量创建字典，然后使用此媒体的数据进行填充。例如：

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>();
      mediaMetadata.put("isUserLoggedIn", "false");
      mediaMetadata.put("tvStation", "Sample TV Station");
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请在媒体心跳实例中调用 `trackSessionStart`。例如：

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata);
   }
   ```

   >[!TIP]
   >
   >第二个值是您在步骤 2 中创建的自定义媒体元数据对象名称。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪的是用户的播放意图，而不是播放的开始。此 API 用于加载媒体数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >如果不使用自定义媒体元数据，则只需在 `trackSessionStart` 中为第二个参数发送一个空对象。

1. **跟踪播放的实际开始事件**

   识别媒体播放器中的媒体播放开始事件（媒体的第一帧呈现在屏幕上）并调用 `trackPlay`：

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) {
       _heartbeat.trackPlay();
   }
   ```

1. **跟踪播放的结束事件**

   识别媒体播放器中的媒体播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`：

   ```java
   public void onVideoComplete(Observable observable, Object data) {
       _heartbeat.trackComplete();
   }
   ```

1. **跟踪会话的结束事件**

   识别媒体播放器中的媒体播放卸载/关闭事件（用户关闭媒体和/或媒体已结束并卸载）并调用 `trackSessionEnd`：

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd();
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记媒体跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。在调用 `trackSessionEnd` 之后，任何其他 `track*` API 调用都将被忽略（除了用于新的媒体跟踪会话的 `trackSessionStart` 之外）。

1. **跟踪所有可能的暂停方案**

   识别媒体播放器中的媒体暂停事件并调用 `trackPause`：

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause();
   }
   ```

   **暂停方案**

   识别视频播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`：

   * 用户在应用程序中明确点击暂停。
   * 播放器将其置于“暂停”状态。
   * （*移动应用程序*）- 用户将应用程序放入后台，但您希望应用程序保持会话打开。
   * （*移动应用程序*）- 发生导致应用程序被置于后台运行的任何类型的系统中断。例如，用户接到电话，或其他应用程序出现弹出窗口，但您希望应用程序保持会话的活动状态，以便用户有机会从中断点恢复媒体。

1. 识别播放器中的媒体播放事件和/或媒体在暂停后继续播放的事件并调用 `trackPlay`。

   ```java
   // trackPlay()
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay();
   }
   ```

   >[!TIP]
   >
   >这可能与步骤 4 中所使用的事件源相同。请确保当媒体播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

有关跟踪核心播放的其他信息，请参阅以下内容：

* 跟踪场景：[不含广告的 VOD 播放](/help/use-cases/tracking-scenarios/vod-no-intrs-details.md)
* Android SDK 随附有示例播放器，用于提供完整的跟踪示例。
