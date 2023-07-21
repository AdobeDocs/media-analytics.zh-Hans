---
title: 跟踪内容播放说明
description: “了解如何跟踪核心播放，包括跟踪媒体载入、媒体开始、媒体暂停和媒体结束。”
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 0d53e62069a65b252e004e21943ecdbd011a3658
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 100%

---

# 跟踪概述{#tracking-overview}

本文档介绍 2.x 版本的 SDK 中的跟踪。

>[!IMPORTANT]
>
>如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/getting-started/download-sdks.md)。

## 播放器事件

跟踪核心播放包括跟踪媒体载入、媒体开始、媒体暂停和媒体结束。虽然跟踪缓冲和搜索不是强制的，但它们也是用于跟踪内容播放的核心组件。在您的媒体播放器 API 中，识别与 Media SDK 跟踪调用相对应的播放器事件，并编码事件处理程序以调用跟踪 API，并填充必需和可选变量。

### 在媒体载入时

* 创建媒体对象
* 填充元数据
* 调用 `trackSessionStart`；例如：`trackSessionStart(mediaObject, contextData)`

### 在媒体开始时

* 调用 `trackPlay`

### 在暂停/继续播放时

* 调用 `trackPause`
* _在继续播放时_，调用 `trackPlay`

### 在媒体结束时

* 调用 `trackComplete`

### 在媒体中止时

* 调用 `trackSessionEnd`

### 在推移开始时

* 调用 `trackEvent(SeekStart)`

### 在推移结束时

* 调用 `trackEvent(SeekComplete)`
取消更改

### 在缓冲开始时

* 调用 `trackEvent(BufferStart);`

### 在缓冲结束时

* 调用 `trackEvent(BufferComplete);`


## 实施 {#implement}

1. **初始跟踪设置 –**&#x200B;识别用户何时触发播放意图（用户点击“播放”和/或自动播放开启），并使用媒体的内容名称、内容 ID、内容时长和流类型信息，创建 `MediaObject` 实例。

   **`MediaObject`引用：**

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

   创建 `MediaObject` 的一般格式是 `MediaHeartbeat.createMediaObject(<MEDIA_NAME>, <MEDIA_ID>, <MEDIA_LENGTH>, <STREAM_TYPE>, <MEDIA_TYPE>);`

1. **附加元数据 -**（可选）通过上下文数据变量将标准和/或自定义元数据对象附加到跟踪会话。

   * **标准元数据 -**

     >[!NOTE]
     >
     >将标准元数据对象附加到媒体对象是可选的。

     实例化一个标准元数据对象，填充所需变量，并在媒体心跳对象中设置该元数据对象。

     请在此处查看元数据的完整列表：[音频和视频参数。](../../implementation/variables/audio-video-parameters.md)

   * **自定义元数据 -** 为自定义变量创建变量对象，然后使用此内容的数据进行填充。

1. **跟踪开始播放的意图 -**&#x200B;要开始跟踪会话，请在 MediaHeartbeat 实例中调用 `trackSessionStart`。

   >[!IMPORTANT]
   >
   >`trackSessionStart` 跟踪的是用户的播放意图，而不是播放的开始。此 API 用于加载数据/元数据并评估开启 QoS 量度的时间（`trackSessionStart` 和 `trackPlay` 之间的持续时间）。

   >[!NOTE]
   >
   >如果不使用自定义元数据，则只需在 `trackSessionStart` 中为 `data` 参数发送一个空对象。

1. **跟踪播放的实际开始事件 -**&#x200B;识别媒体播放器中的播放开始事件（内容的第一帧呈现在屏幕上）并调用 `trackPlay`。

1. **跟踪播放的结束事件 -**&#x200B;识别媒体播放器中的播放结束事件（用户一直观看至内容的结尾）并调用 `trackComplete`。

1. **跟踪会话的结束事件 -**&#x200B;识别媒体播放器中的播放卸载/关闭事件（用户关闭内容和/或内容已结束并卸载）并调用 `trackSessionEnd`。

   >[!IMPORTANT]
   >
   >`trackSessionEnd` 标记跟踪会话的结尾。如果会话成功观看至结束（用户一直观看内容至结尾），请确保先调用 `trackComplete`，之后再调用 `trackSessionEnd`。在调用 `trackSessionEnd` 之后，任何其他 `track*` API 调用都将被忽略（除了用于新的跟踪会话的 `trackSessionStart` 之外）。

1. **跟踪所有可能的暂停方案 -**&#x200B;识别媒体播放器中的暂停事件并调用 `trackPause`。

   **暂停方案 -**&#x200B;识别播放器将会暂停的任何方案，并确保正确调用了 `trackPause`。以下方案均要求应用程序调用 `trackPause()`：

   * 用户在应用程序中明确点击暂停。
   * 播放器将其置于“暂停”状态。
   * （*移动应用程序*）- 用户将应用程序放入后台，但您希望应用程序保持会话打开。
   * （*移动应用程序*）- 发生导致应用程序被置于后台运行的任何类型的系统中断。例如，用户接到电话，或其他应用程序出现弹出窗口，但您希望应用程序保持会话的活动状态，以便用户有机会从中断点恢复内容。

1. 识别播放器中的播放事件和/或在暂停后继续播放的事件并调用 `trackPlay`。

   >[!TIP]
   >
   >这可能与步骤 4 中所使用的事件源相同。请确保当播放继续时，每个 `trackPause()` API 调用均与随后的一个 `trackPlay()` API 调用相配对。

1. 监听媒体播放器中的播放搜寻事件。在发出搜寻开始事件通知时，使用 `SeekStart` 事件跟踪搜寻。
1. 在从媒体播放器发出搜寻结束通知时，使用 `SeekComplete` 事件跟踪搜寻的结束。
1. 监听媒体播放器中的播放缓冲事件，并在发出缓冲开始事件通知时，使用 `BufferStart` 事件跟踪缓冲。
1. 在从媒体播放器发出缓冲结束通知时，使用 `BufferComplete` 事件跟踪缓冲的结束。

查看以下平台特定主题中每个步骤的示例，并查看 SDK 附带的示例播放器。

有关播放跟踪的简单示例，请参阅在 HTML5 播放器中对 JavaScript 2.x SDK 的使用：

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
if (e.type == "buffering") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
};

/* Call on buffer complete */
if (e.type == "buffered") {
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
};
```

## 验证 {#validate}

有关验证&#x200B;*旧版*&#x200B;实施的信息，请参阅[旧版验证。](/help/legacy/validation/validation-overview.md)
