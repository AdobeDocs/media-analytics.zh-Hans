---
title: 从里程碑迁移到 Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: aa2a230daa96b823f9963345ac4578799e59d3f5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 79%

---


# 从里程碑迁移到 Media Analytics {#migrating-from-milestone-to-media-analytics}

## 概述 {#overview}

视频测量的核心概念与里程碑和 Media Analytics 相同，后者采用视频播放器事件并将其映射到分析方法，同时捕获播放器元数据和值并将它们映射到分析变量。Media Analytics 解决方案源自里程碑，因此许多方法和量度都与里程碑是相同的，但配置方法和代码发生了显著变化。也可以更新播放器事件代码以指向新的 Media Analytics 方法。有关实施 Media Analytics 的更多详细信息，请参阅 [SDK 概述](/help/sdk-implement/setup/setup-overview.md)和[跟踪概述](/help/sdk-implement/track-av-playback/track-core-overview.md)。

下表提供了“里程碑”解决方案和“Media Analytics”解决方案之间的转换。

## 迁移指南 {#migration-guide}

### 变量引用

| 里程碑量度 | 变量类型 | Media Analytics 量度 |
| --- | --- | --- |
| 内容 | eVar <br>默认过期：访问 | 内容 |
| 内容类型 | eVar <br>默认过期：页面查看 | 内容类型 |
| 内容逗留时间 | 事件 <br>类型：计数器 | 内容逗留时间 |
| 视频初始化 | 事件 <br>类型：计数器 | 视频初始化 |
| 视频结束 | 事件 <br>类型：计数器 | 内容结束 |

### 媒体模块变量

| 里程碑 | 里程碑语法 | Media Analytics | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | 不适用 | 所有 Media Analytics 数据仅使用上下文数据发送。 |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 不适用 | Media Analytics 上下文数据会自动填充到保留变量中。实施代码中不再需要映射到 eVar、prop 和事件。客户可以使用处理规则将上下文数据映射到变量。 |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | 不适用 | 不再需要，因为映射是通过保留变量和处理规则进行的。 |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | 不适用 | 不再需要，因为映射是通过保留变量和处理规则进行的。 |

### 可选变量

| 里程碑 | 里程碑语法 | Media Analytics | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 不适用 | 我们不再提供预建的播放器映射。 |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 不适用 | 我们不再提供预建的播放器映射。 |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 不适用 | “内容结束”仅支持 100% 进度标记。 |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 不适用 | “内容结束”仅支持 100% 进度标记。 |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 不适用 | 对于内容，Media Analytics 设置为 10 秒；对于广告，设置为 1 秒。无其他选项可用。 |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 不适用 | Media Analytics 始终跟踪 10%、25%、50%、75%、95% 进度标记 |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 不适用 | Media Analytics 始终跟踪 10%、25%、50%、75%、95% 进度标记 |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用. |

### 广告跟踪变量

| 里程碑 | 里程碑语法 | Media Analytics | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 不适用 | 对于内容，Media Analytics 设置为 10 秒；对于广告，设置为 1 秒。无其他选项可用。 |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 不适用 | 默认情况下，广告不提供进度标记。请使用计算量度来构建广告进度标记。 |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 不适用 | 对于广告，Media Analytics 设置为 1 秒。无其他选项可用。 |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用. |

### 媒体模块方法

| 里程碑 | 里程碑语法 | Media Analytics | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName - (Required) <br> The name of the video as you want it to appear in video reports. | `mediaName` | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength - (Required) <br> The length of the video in seconds. | `mediaLength` | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName - (Required) <br> The name of the media player used to view the video, as you want it to appear in video reports. | `mediaPlayerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name - (Required) <br> The name or ID of the ad. | `name` | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length - (Required) <br> The length of the ad. | `length` | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName - (Required) <br> The name of the media player used to view the ad. | `playerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName <br> The name or ID of the primary content where the ad is embedded. | `parentName` | 不适用 | 自动继承 |
| parentPod <br> The position in the primary content the ad was played. | `parentPod` | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition <br> The position within the pod where the ad is played. | `parentPodPosition` | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM <br> The CPM or encrypted CPM (prefixed with a &quot;~&quot;) that applies to this playback. | `CPM` | 不适用 | 在 Media Analytics 中默认不可用. |
| Media.click | `s.Media.click(` <br> `  name,` <br> `  offset)` | 不适用 | 使用自定义链接分析调用来跟踪点击次数. |
| Media.close | `s.Media.close(` <br> `  mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | trackPause<br> 或 <br>trackEvent | `trackPause()` <br> 或 `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> 或 <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | 使用自定义或标准元数据来设置其他变量. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | 不适用 | 跟踪调用频率是自动设置的。 |

