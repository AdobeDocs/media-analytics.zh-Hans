---
title: 在 Android 中跟踪核心播放
description: 本主题介绍如何在Android上使用Media SDK实现核心跟踪。
uuid: ab5fab95-76ed-4ae6-aedb-2e66eece7607
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Android 中跟踪核心播放{#track-core-playback-on-android}

>[!IMPORTANT]
>本文档涵盖SDK版本2.x中的跟踪。 如果您实施的是 1.x 版本的 SDK，可以在此处下载适用于 Android 的 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)

1. **初始跟踪设置**

   Identify when the user triggers the intention of playback (the user clicks play and/or autoplay is on) and create a `MediaObject` instance.

   [createMediaObject API](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 媒体名称 | 是 |
   | `mediaId` | 媒体唯一标识符 | 是 |
   | `length` | 媒体长度 | 是 |
   | `streamType` | 流类型(请参阅 _下面的StreamType常量_ ) | 是 |
   | `mediaType` | 媒体类型(请参阅 _下面的MediaType常量_ ) | 是 |

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

   （可选）通过上下文数据变量将标准和／或自定义元数据对象附加到跟踪会话。

   * **标准元数据**

      [在 Android 中实施标准元数据](/help/sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)

      >[!NOTE]
      >
      >将标准元数据对象附加到媒体对象是可选的。

      * 媒体元数据键 API 引用 - [标准元数据键 - Android](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
      * 请在此处查看可用视频元数据的完整集合：[音频和视频参数](/help/metrics-and-metadata/audio-video-parameters.md)
   * **自定义元数据**

      为自定义变量创建字典并填充此媒体的数据。 例如：

      ```java
      HashMap<String, String> mediaMetadata =  
        new HashMap<String, String>(); 
      mediaMetadata.put("isUserLoggedIn", "false"); 
      mediaMetadata.put("tvStation", "Sample TV Station"); 
      mediaMetadata.put("programmer", "Sample programmer");
      ```


1. **跟踪开始播放的意图**

   要开始跟踪媒体会话，请调用 `trackSessionStart` 媒体心跳实例。 例如：

   ```java
   public void onVideoLoad(Observable observable, Object data) {  
       _heartbeat.trackSessionStart(mediaInfo, mediaMetadata); 
   }
   ```

   >[!TIP]
   >
   >第二个值是您在步骤2中创建的自定义媒体元数据对象名称。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪用户的播放意图，而不是播放的开始。 此 API 用于加载媒体数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >If you are not using custom media metadata, simply send an empty object for the second argument in `trackSessionStart`.

1. **跟踪实际播放开始**

   Identify the event from the media player for the beginning of the media playback, where the first frame of the media is rendered on the screen, and call `trackPlay`:

   ```java
   // Video is rendered on the screen) and call trackPlay.  
   public void onVideoPlay(Observable observable, Object data) { 
       _heartbeat.trackPlay(); 
   }
   ```

1. **跟踪播放的完成情况**

   Identify the event from the media player for the completion of the media playback, where the user has watched the content until the end, and call `trackComplete`:

   ```java
   public void onVideoComplete(Observable observable, Object data) { 
       _heartbeat.trackComplete(); 
   }
   ```

1. **跟踪会话结束**

   Identify the event from the media player for the unloading/closing of the media playback, where the user closes the media and/or the media is completed and has been unloaded, and call `trackSessionEnd`:

   ```java
   // Closes the media and/or the media completed and unloaded,  
   // and call trackSessionEnd().  
   public void onMainVideoUnload(Observable observable, Object data) {  
       _heartbeat.trackSessionEnd(); 
   }
   ```

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记媒体跟踪会话的结束。 如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new media tracking session.

1. **跟踪所有可能的暂停方案**

   识别媒体播放器中的事件以进行媒体暂停和呼叫 `trackPause`:

   ```java
   public void onVideoPause(Observable observable, Object data) {  
       _heartbeat.trackPause(); 
   }
   ```

   **暂停方案**

   Identify any scenario in which the Video Player will pause and make sure that `trackPause` is properly called. 以下方案均要求应用程序调用 `trackPause()`()：

   * 用户在应用程序中明确点击暂停。
   * 播放器自行进入暂停状态。
   * （*移动设备应用程序*）- 用户将应用程序置于后台，但您希望应用程序保持会话打开。
   * （*移动设备应用程序*）- 出现导致应用程序被置于后台的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续播放媒体。

1. 识别播放器中的媒体播放事件和/或媒体在暂停后继续播放的事件，并调用 `trackPlay`。

   ```java
   // trackPlay() 
   public void onVideoPlay(Observable observable, Object data) {  
       _heartbeat.trackPlay(); 
   }
   ```

   >[!TIP]
   >
   >这可能是步骤4中使用的同一事件源。 Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the media playback resumes.

有关跟踪核心播放的其他信息，请参阅以下内容：

* 跟踪方案：[不含广告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
* Android SDK 随附有示例播放器，用于提供完整的跟踪示例。

