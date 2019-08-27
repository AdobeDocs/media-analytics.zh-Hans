---
seo-title: 跟踪概述
title: 跟踪概述
uuid: 7b8e2f76-bc4 e-4721-8933-3e4453 b01788
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# 跟踪概述{#tracking-overview}

>[!IMPORTANT]
>
>此文档涵盖SDK的版本2.x跟踪。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK.](/help/sdk-implement/download-sdks.md)

## Player事件

跟踪核心播放包括跟踪媒体载入、媒体开始、媒体暂停和媒体结束。虽然跟踪缓冲和跟踪搜寻并不是强制性的，但它们也是用于跟踪内容播放的核心组件。在媒体播放器 API 中，识别与 Media SDK 跟踪调用相对应的播放器事件，对事件处理程序进行编码以调用跟踪 API，并填充必需和可选的变量。

### 在媒体加载时

* 创建媒体对象
* 填充元数据
* 调用 `trackSessionStart`；例如： `trackSessionStart(mediaObject, contextData)`

### 在媒体开始时

* 调用 `trackPlay`

### 暂停/恢复

* 调用 `trackPause`
* `trackPlay`_恢复回放时调用_

### 在媒体完成时

* 调用 `trackComplete`

### 在媒体中止上

* 调用 `trackSessionEnd`

### 当划动开始时

* 调用 `trackEvent(SeekStart)`

### 当划动结束时

* 调用 `trackEvent(SeekComplete)`

### 缓冲开始时

* 调用 `trackEvent(BufferStart);`

### 缓冲结束时

* 调用 `trackEvent(BufferComplete);`

>[!TIP]
>
>播放头位置设置为设置和配置代码的一部分。有关详细信息， `getCurrentPlayheadTime`请参阅 [概述：一般实施准则。](/help/sdk-implement/setup/setup-overview.md#section_965A3B699A8248DDB9B2B3EA3CC20E41)

## 实施 {#section_BB217BE6585D4EDEB34C198559575004}

1. **初始跟踪设置 -**&#x200B;识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启），并使用媒体的内容名称、内容 ID、内容时长和流类型信息，创建 `MediaObject` 实例。

   **`MediaObject`参考：**

   | 变量名称 | 描述 | 必需 |
   |---|---|---|
   | `name` | 内容名称 | 是 |
   | `mediaid` | 内容唯一标识符 | 是 |
   | `length` | 内容时长 | 是 |
   | `streamType` | 流类型 | 是 |
   | `mediaType` | 媒体类型（音频或视频内容） | 是 |

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

   The general format for creating the `MediaObject` is `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **附加元数据 -**（可选）通过上下文数据变量将标准和/或自定义元数据对象附加到跟踪会话。

   * **标准元数据 -**

      >[!NOTE]
      >
      >将标准元数据对象附加到媒体对象是可选的。

      实例化一个标准元数据对象，填充所需变量，并在媒体心率对象中设置该元数据对象。

      请在此处查看元数据的完整列表：[音频和视频参数.](/help/metrics-and-metadata/audio-video-parameters.md)

   * **自定义元数据 -** 为自定义变量创建变量对象，然后使用此内容的数据进行填充。

1. **跟踪开始播放的意图 -**&#x200B;要开始跟踪会话，请在 MediaHeartbeat 实例中调用 `trackSessionStart`。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪用户的播放意图，而不是播放开始。此 API 用于加载数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >If you are not using custom metadata, simply send an empty object for the `data` argument in `trackSessionStart`.

1. **跟踪播放的实际开始事件 -**&#x200B;识别媒体播放器中的播放开始事件（内容的第一帧呈现在屏幕上）并调用 `trackPlay`。

1. **跟踪播放的结束事件 -**&#x200B;识别媒体播放器中的播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`。

1. **跟踪会话的结束事件 -**&#x200B;识别媒体播放器中的播放卸载/关闭事件（用户关闭内容和/或内容已结束并卸载）并调用 `trackSessionEnd`。

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。Any other `track*` API call is ignored after `trackSessionEnd`, except for `trackSessionStart` for a new tracking session.

1. **跟踪所有可能的暂停方案 -**&#x200B;识别媒体播放器中的暂停事件并调用 `trackPause`。

   **暂停方案 -**&#x200B;识别播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`()：

   * 用户在应用程序中明确点击暂停。
   * 播放器自行进入暂停状态。
   * （*移动设备应用程序*）- 用户将应用程序置于后台，但您希望应用程序保持会话打开。
   * （*移动设备应用程序*）- 出现导致应用程序被置于后台的任何类型的系统中断。例如，用户接收到一个调用，或者出现来自其他应用程序的弹出窗口，但您希望应用程序将会话保持活动状态，以便用户有机会从中断点继续播放内容。

1. 识别播放器中的播放事件和/或在暂停后继续播放的事件，并调用 `trackPlay`。

   >[!TIP]
   >
   >这可能与在步骤中使用的相同。Ensure that each `trackPause()` API call is paired with a following `trackPlay()` API call when the playback resumes.

1. 监听媒体播放器中的播放搜寻事件。在发出搜寻开始事件通知时，使用 `SeekStart` 事件跟踪搜寻。
1. 在从媒体播放器发出搜寻结束通知时，使用 `SeekComplete` 事件跟踪搜寻的结束。
1. 监听媒体播放器中的播放缓冲事件，并在发出缓冲开始事件通知时，使用 `BufferStart` 事件跟踪缓冲。
1. 在从媒体播放器发出缓冲结束通知时，使用 `BufferComplete` 事件跟踪缓冲的结束。

请参阅以下特定于平台的主题中每个步骤的示例，并查看 SDK 随附的示例播放器。

有关跟踪播放的简单示例，请参阅以下在 HTML5 播放器中使用 JavaScript 2.x SDK：

```js
/* Call on media start */ 
if (e.type == "play") { 
 
    // Check for start of media 
    if (!sessionStarted) { 
        /* Set media info */     
        /* MediaHeartbeat.createMediaObject(<MEDIA_NAME>,  
                                            <MEDIA_ID>,  
                                            <MEDIA_LENGTH>, 
                                            <MEDIA_STREAMTYPE>,
                                            <MEDIA_MEDIATYPE>);*/ 
        var mediaInfo = MediaHeartbeat.createMediaObject( 
          document.getElementsByTagName('video')[0].getAttribute("name"),  
          document.getElementsByTagName('video')[0].getAttribute("id"),  
          video.duration, 
          MediaHeartbeat.StreamType.VOD); 
 
        /* Set custom context data */ 
        var customVideoMetadata = { 
            isUserLoggedIn: "false", 
            tvStation: "Sample TV station", 
            programmer: "Sample programmer" 
        }; 
 
        /* Set standard video metadata */     
        var standardVideoMetadata = {}; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.EPISODE] = "Sample Episode"; 
        standardVideoMetadata[MediaHeartbeat.VideoMetadataKeys.SHOW] = "Sample Show"; 
        mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata,  
                           standardVideoMetadata);     
 
        // Start Session 
        this.mediaHeartbeat.trackSessionStart(mediaInfo, customVideoMetadata);    
 
        // Track play 
        this.mediaHeartbeat.trackPlay();  
        sessionStarted = true;     
 
    } else { 
        // Track play for resuming playack    
        this.mediaHeartbeat.trackPlay();  
    } 
}; 
 
/* Call on video complete */ 
if (e.type == "ended") { 
    console.log("video ended"); 
    this.mediaHeartbeat.trackComplete(); 
    this.mediaHeartbeat.trackSessionEnd(); 
    sessionStarted = false;     
}; 
 
/* Call on pause */ 
if (e.type == "pause") { 
    this.mediaHeartbeat.trackPause(); 
}; 
 
/* Call on scrub start */ 
if (e.type == "seeking") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart); 
}; 
     
/* Call on scrub stop */ 
if (e.type == "seeked") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete); 
}; 
 
/* Call on buffer start */ 
if (e.type == “buffering”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart); 
}; 
 
/* Call on buffer complete */ 
if (e.type == “buffered”) { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete); 
};
```

## 验证 {#section_ABCFB92C587B4CAABDACF93452EFA78F}

有关验证实施的信息，请参阅 [验证。](/help/sdk-implement/validation/validation-overview.md)

