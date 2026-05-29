---
title: JavaScript 3.x Media SDK API参考
description: Media SDK JavaScript 3.x （ADB.Media和ADB.MediaConfig类）的API参考。
feature: Streaming Media
role: User, Admin, Developer
exl-id: c3f8a2b5-1d4e-4f9a-8c7b-3a2d1f0e9b6c
source-git-commit: 1022e0851d58db0c9b523ebb7b52d379239a2e07
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 17%

---


# JavaScript 3.x Media SDK API参考

>[!BEGINSHADEBOX]

本页介绍了仅限Analytics的JavaScript 3.x SDK。 有关推荐的实施，请参阅[使用Edge Network实施流媒体](/help/implementation/edge/edge-web-sdk.md)。

>[!ENDSHADEBOX]

## ADB.Media

### 静态方法

+++configure

配置MediaSDK以进行跟踪。 应在页面中创建任何跟踪器实例之前调用一次此方法。

**语法**

```javascript
ADB.Media.configure(mediaConfig, appMeasurement);
```

| 变量名称 | 类型 | 描述 |
|---|---|---|
| `mediaConfig` | `ADB.MediaConfig` | 有效的媒体配置 |
| `appMeasurement` | 对象 | AppMeasurement实例 |

**示例**

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

+++

+++getInstance

创建媒体实例以跟踪播放会话。 如果在配置媒体之前调用，则返回`null`。

**语法**

```javascript
ADB.Media.getInstance(trackerConfig)
```

| 变量名称 | 类型 | 必需 | 描述 |
| :--- | :--- | :---: | :--- |
| `trackerConfig` | 跟踪器配置 | 否 | 跟踪器配置对象。 |

**示例**

```javascript
var tracker = ADB.Media.getInstance();
```

若要覆盖每个跟踪器实例的`channel`或`playerName`，请在跟踪器配置对象中传递覆盖值。

**跟踪器配置示例**

```javascript
const trackerConfig = {
  [Media.TrackerConfig.Channel]: "custom_channel_name",
  [Media.TrackerConfig.PlayerName]: "custom_player_name",
}
this._mediaTracker = Media.getInstance(trackerConfig);
```

+++

+++createMediaObject

创建包含媒体信息的对象。 如果传递的参数无效，则返回空对象。

**语法**

```javascript
ADB.Media.createMediaObject(name, id, length, streamType, mediaType)
```

| 变量名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| `name` | 字符串 | 表示媒体名称的非空字符串 |
| `id` | 字符串 | 表示唯一媒体标识符的非空字符串 |
| `length` | 数字 | 正数，表示媒体长度（秒）。 如果长度未知，请使用`0`。 |
| `streamType` | 字符串 | 流类型或表示媒体流类型的非空字符串。 |
| `mediaType` | 媒体类型 | 媒体类型（音频或视频） |

**示例**

```javascript
var mediaObject = ADB.Media.createMediaObject("video-name",
                                              "video-id",
                                              60.0,
                                              ADB.Media.StreamType.VOD,
                                              ADB.Media.MediaType.Video);
```

+++

+++createAdBreakObject

创建包含广告时间信息的对象。 如果传递的参数无效，则返回空对象。

**语法**

```javascript
ADB.Media.createAdBreakObject(name, position, startTime);
```

| 变量名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| `name` | 字符串 | 表示广告时间名称（前置式广告、中置式广告和后置式广告）的非空字符串 |
| `position` | 数字 | 广告时间在内容中的位置编号，从1开始编号 |
| `startTime` | 数字 | 广告时间开始的播放头值。 |

**示例**

```javascript
var adbreakObject = ADB.Media.createAdBreakObject("midroll", 2, 30.0);
```

+++

+++createAdObject

创建包含广告信息的对象。 如果传递的参数无效，则返回空对象。

**语法**

```javascript
ADB.Media.createAdObject(name, id, position, length);
```

| 变量名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| `name` | 字符串 | 表示广告名称的非空字符串 |
| `id` | 字符串 | 表示广告ID的非空字符串 |
| `position` | 数字 | 广告时间中广告的位置编号，从1开始编号 |
| `length` | 数字 | 正数，表示广告长度 |

**示例**

```javascript
var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0)
```

+++

+++createChapterObject

创建包含章节信息的对象。 如果传递的参数无效，则返回空对象。

**语法**

```javascript
ADB.Media.createChapterObject(name, position, length, startTime)
```

| 变量名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| `name` | 字符串 | 表示章节名称的非空字符串 |
| `position` | 数字 | 内容中章节的位置，从1开始 |
| `length` | 数字 | 正数，表示章节长度 |
| `startTime` | 数字 | 章节开头的播放头值 |

**示例**

```javascript
var chapterObject = ADB.Media.createChapterObject("name", 1, 30.0, 0)
```

+++

+++createStateObject

创建包含状态信息的对象。 如果传递的参数无效，则返回空对象。

**语法**

```javascript
ADB.Media.createStateObject(name)
```

| 变量名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| `name` | 字符串 | 表示状态名称的播放器状态或非空字符串 |

**示例**

```javascript
var stateObject = ADB.Media.createStateObject("customstate");
```

+++

+++createQoEObject

创建包含QoE信息的对象。 如果传递的参数无效，则返回空对象。

**语法**

```javascript
ADB.Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)
```

| 变量名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| `bitrate` | 数字 | 表示当前比特率的正数（如果未知，则为0） |
| `startupTime` | 数字 | 表示启动时间的正数（如果未知，则为0） |
| `fps` | 数字 | 表示当前fps的正数（如果未知，则为0） |
| `droppedFrames` | 数字 | 正数，表示丢帧的数量（如果未知，则为0） |

**示例**

```javascript
qoeObject = ADB.Media.createQoEObject(10000000, 2, 23, 10);
```

+++

+++version

返回MediaSDK版本。

**语法**

```javascript
ADB.Media.version
```

**示例**

```javascript
console.log(ADB.Media.version);
```

+++

### 实例方法

+++trackSessionStart

跟踪开始播放的意图。 这将在媒体跟踪器实例上启动跟踪会话。 另请参阅媒体恢复。

**语法**

```javascript
ADB.Media.trackSessionStart(mediaObject, contextData);
```

| 变量名称 | 描述 | 必需 |
| :--- | :--- | :---: |
| `mediaObject` | 使用`createMediaObject`方法创建的媒体信息。 | 是 |
| `contextData` | 可选媒体上下文数据。 对于标准元数据键，请使用标准视频常量或标准音频常量。 | 否 |

**示例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[ADB.Media.VideoMetadataKeys.Show] = "Sample Show";
contextData["isUserLoggedIn"] = "false";
contextData["tvStation"] = "Sample TV Station";

tracker.trackSessionStart(mediaObject, contextData);
```

+++

+++trackPlay

跟踪上次暂停后的媒体播放或恢复。

**语法**

```javascript
ADB.Media.trackPlay();
```

**示例**

```javascript
tracker.trackPlay();
```

+++

+++trackPause

跟踪媒体暂停。

**语法**

```javascript
ADB.Media.trackPause();
```

**示例**

```javascript
tracker.trackPause();
```

+++

+++trackComplete

跟踪媒体结束。 仅当媒体已完全查看时才调用此方法。

**语法**

```javascript
ADB.Media.trackComplete();
```

**示例**

```javascript
tracker.trackComplete();
```

+++

+++trackSessionEnd

跟踪查看会话的结束。 即使用户没有查看至媒体结束，也调用此方法。

**语法**

```javascript
ADB.Media.trackSessionEnd();
```

**示例**

```javascript
tracker.trackSessionEnd();
```

+++

+++trackError

跟踪媒体播放中的错误。

**语法**

```javascript
ADB.Media.trackError(errorId);
```

| 变量名称 | 描述 | 必需 |
| :--- | :--- | :---: |
| `errorId` | 包含错误信息的非空字符串 | 是 |

**示例**

```javascript
tracker.trackError("errorId");
```

+++

+++trackEvent

跟踪媒体事件的方法。

| 变量名称 | 描述 |
| :--- | :--- |
| `event` | 媒体事件 |
| `info` | 对于`AdBreakStart`事件，使用`createAdBreakObject`方法创建adbreak信息。 对于`AdStart`事件，使用`createAdObject`方法创建广告信息。 对于`ChapterStart`事件，使用`createChapterObject`方法创建章节信息。 对于`StateStart`和`StateEnd`事件，状态信息是使用`createStateObject`方法创建的。 对于其他事件，不需要此操作。 |
| `contextData` | 可以为`AdStart`和`ChapterStart`事件提供可选的上下文数据。 对于其他事件，不需要此操作。 |

**语法**

```javascript
ADB.Media.trackEvent(event, info, contextData);
```

**示例**

**跟踪广告时间**

```javascript
// AdBreakStart
  var adBreakObject = ADB.Media.createAdBreakObject("preroll", 1, 0)
  tracker.trackEvent(ADB.Media.Event.AdBreakStart, adBreakObject);

// AdBreakComplete
  tracker.trackEvent(ADB.Media.Event.AdBreakComplete);
```

**跟踪广告**

```javascript
// AdStart
  var adObject = ADB.Media.createAdObject("ad-name", "ad-id", 1, 15.0);

  var adMetadata = {};
  // Standard metadata keys provided by adobe.
  adMetadata[ADB.Media.AdMetadataKeys.Advertiser]  ="Sample Advertiser";
  adMetadata[ADB.Media.AdMetadataKeys.CampaignId] = "Sample Campaign";
  // Custom metadata keys
  adMetadata["affiliate"] = "Sample affiliate";

  tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);

// AdComplete
  tracker.trackEvent(ADB.Media.Event.AdComplete);

// AdSkip
  tracker.trackEvent(ADB.Media.Event.AdSkip);
```

**跟踪章节**

```javascript
// ChapterStart
  var chapterObject = ADB.Media.createChapterObject("chapter-name", 1, 60.0, 15.0);

  var chapterMetadata = {};
  chapterMetadata["segmentType"] = "Sample segment type";

  tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterObject, chapterMetadata);

// ChapterComplete
  tracker.trackEvent(ADB.Media.Event.ChapterComplete);

// ChapterSkip
  tracker.trackEvent(ADB.Media.Event.ChapterSkip);
```

**跟踪状态**

```javascript
// StateStart (ex: Mute is switched on)
  var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
  tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);

// StateEnd (ex: Mute is switched off)
  tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```

**跟踪播放事件**

```javascript
// BufferStart
  tracker.trackEvent(ADB.Media.Event.BufferStart);

// BufferComplete
  tracker.trackEvent(ADB.Media.Event.BufferComplete);

// SeekStart
  tracker.trackEvent(ADB.Media.Event.SeekStart);

// SeekComplete
  tracker.trackEvent(ADB.Media.Event.SeekComplete);
```

**跟踪比特率更改**

```javascript
// If the new bitrate value is available provide it to the tracker.
  var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
  tracker.updateQoEObject(qoeObject);

// Bitrate change
  tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

+++

+++updatePlayhead

向媒体跟踪器提供当前媒体播放头。 要准确跟踪，请在播放期间播放头发生更改时调用此方法。

**语法**

```javascript
ADB.Media.updatePlayhead(time);
```

| 变量名称 | 描述 |
| :--- | :--- |
| `time` | 当前播放头（秒）。 对于视频点播(VOD)，该值以秒为单位，从媒体项目的开头起计算。 对于直播，如果播放器不提供有关内容持续时间的信息，则该值可以指定为自当天UTC午夜开始的秒数。 请注意：使用进度标记时，需要内容持续时间，并且播放头需要更新为从媒体项目开始的秒数，从 0 开始。 |

**示例**

```javascript
tracker.updatePlayhead(13.3);

// For live streams
var UTCTimeInSeconds = Math.floor(Date.now() / 1000)
var timeFromMidnightInSecond = UTCTimeInSeconds % 86400

tracker.updatePlayhead(timeFromMidnightInSecond);
```

+++

+++updateQoEObject

向媒体跟踪器提供当前QoE信息。 为了实现准确跟踪，请在媒体播放器提供更新的QoE信息时多次调用此方法。

**语法**

```javascript
ADB.Media.updateQoEObject(qoeObject);
```

| 变量名称 | 描述 |
| :--- | :--- |
| `qoeObject` | 使用`createQoEObject`方法创建的当前QoE信息。 |

**示例**

```javascript
var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
tracker.updateQoEObject(qoeObject);
```

+++

+++销毁

销毁跟踪器实例。

**语法**

```javascript
ADB.Media.destroy();
```

**示例**

```javascript
tracker.destroy();
```

+++

### 常量

+++跟踪器配置

定义每个跟踪器实例可以设置的配置键。

```javascript
ADB.Media.TrackerConfig = {
  Channel: "media.channel",
  PlayerName: "media.playerName"
}
```

+++

+++媒体类型

定义当前跟踪的媒体类型。

```javascript
ADB.Media.MediaType = {
  Video: "video",
  Audio: "audio"
}
```

+++

+++流类型

定义当前跟踪的内容的流类型。

```javascript
ADB.Media.StreamType = {
  VOD: "vod",
  Live: "live",
  Linear: "linear",
  Podcast: "podcast",
  Audiobook: "audiobook",
  AOD: "aod"
}
```

+++

+++标准元数据键

`ADB.Media.VideoMetadataKeys`、`ADB.Media.AudioMetadataKeys`和`ADB.Media.AdMetadataKeys`提供标准元数据的上下文数据键字符串。 有关键及其相应报表变量的完整列表，请参阅[标准元数据变量引用](/help/implementation/variables/standard-metadata/show.md)。

+++

+++媒体事件

定义跟踪事件的类型。

```javascript
ADB.Media.Event = {
  AdBreakStart: "adBreakStart",
  AdBreakComplete: "adBreakComplete",
  AdStart: "adStart",
  AdComplete: "adComplete",
  AdSkip: "adSkip",
  ChapterStart: "chapterStart",
  ChapterComplete: "chapterComplete",
  ChapterSkip: "chapterSkip",
  SeekStart: "seekStart",
  SeekComplete: "seekComplete",
  BufferStart: "bufferStart",
  BufferComplete: "bufferComplete",
  BitrateChange: "bitrateChange",
  StateStart: "stateStart",
  StateEnd: "stateEnd"
}
```

+++

+++播放器状态

定义用于跟踪播放器状态的标准值。

```javascript
ADB.Media.PlayerState = {
  FullScreen: "fullScreen",
  ClosedCaption: "closedCaptioning",
  Mute: "mute",
  PictureInPicture: "pictureInPicture",
  InFocus: "inFocus"
}
```

+++

+++媒体恢复播放

常量，表示当前跟踪会话正在恢复以前关闭的会话。 在启动跟踪会话时，必须提供此信息。

**语法**

```javascript
ADB.Media.MediaObjectKey = {
  MediaResumed: "resumed"
}
```

**示例**

```javascript
var mediaObject = ADB.Media.createMediaObject("media-name", "media-id", 60, ADB.Media.StreamType.VOD, ADB.Media.MediaType.Video);

mediaObject[ADB.Media.MediaObjectKey.MediaResumed] = true;

tracker.trackSessionStart(mediaObject);
```

+++

## ADB.MediaConfig

| 键 | 必需 | 描述 |
| :--- | :--- | :--- |
| `trackingServer` | 是 | 键入应将下载的媒体跟踪数据发送到的媒体收集API服务器的名称。 请联系您的Adobe客户代表以接收此信息。 |
| `channel` | 否 | 渠道名称属性 |
| `playerName` | 否 | 正在使用的媒体播放器的名称 |
| `appVersion` | 否 | 键入媒体播放器应用程序/SDK的版本 |
| `debugLogging` | 否 | 启用或禁用Media SDK日志（默认值： `false`） |
| `ssl` | 否 | 通过SSL发送ping（默认值： `true`） |
