---
title: 了解如何从里程碑迁移到 Media Analytics
description: 了解如何将里程碑变量更改为 Media Analytics 量度，并将里程碑模块方法更改为 Media Analytics 语法。
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 96%

---

# 从里程碑迁移到 Media Analytics {#migrating-from-milestone-to-media-analytics}

## 概述 {#overview}

视频测量的核心概念与里程碑和 Media Analytics 相同，后者采用视频播放器事件并将其映射到分析方法，同时捕获播放器元数据和值并将它们映射到分析变量。Media Analytics 解决方案源自里程碑，因此许多方法和量度都与里程碑是相同的，但配置方法和代码发生了显著变化。也可以更新播放器事件代码以指向新的 Media Analytics 方法。有关实施 Media Analytics 的更多详细信息，请参阅 [SDK 概述](/help/legacy/setup/legacy-setup-overview.md)和[跟踪概述](/help/use-cases/track-av-playback/track-core-overview.md)。

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

| 里程碑 | 里程碑语法 | 媒体分析 | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | 不适用 | 所有 Media Analytics 数据仅使用上下文数据发送。 |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 不适用 | Media Analytics 上下文数据会自动填充到保留变量中。实施代码中不再需要映射到 eVar、prop 和事件。客户可以使用处理规则将上下文数据映射到变量。 |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | 不适用 | 不再需要，因为映射是通过保留变量和处理规则进行的。 |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | 不适用 | 不再需要，因为映射是通过保留变量和处理规则进行的。 |

### 可选变量

| 里程碑 | 里程碑语法 | 媒体分析 | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 不适用 | 我们不再提供预建的播放器映射。 |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 不适用 | 我们不再提供预建的播放器映射。 |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 不适用 | “内容结束”仅支持 100% 进度标记。 |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 不适用 | “内容结束”仅支持 100% 进度标记。 |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 不适用 | 对于内容，Media Analytics 设置为 10 秒；对于广告，设置为 1 秒。无其他选项可用。 |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 不适用 | Media Analytics始终跟踪10%、25%、50%、75%、95%进度标记。 |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 不适用 | Media Analytics始终跟踪10%、25%、50%、75%、95%进度标记。 |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用。 |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用。 |

### 广告跟踪变量

| 里程碑 | 里程碑语法 | 媒体分析 | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 不适用 | 对于内容，Media Analytics 设置为 10 秒；对于广告，设置为 1 秒。无其他选项可用。 |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 不适用 | 默认情况下，广告不提供进度标记。请使用计算量度来构建广告进度标记。 |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 不适用 | 对于广告，Media Analytics 设置为 1 秒。无其他选项可用。 |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用。 |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 不适用 | 自动跟踪不再可用。 |

### 媒体模块方法

| 里程碑 | 里程碑语法 | 媒体分析 | Media Analytics 语法 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`：（必需）您希望在视频报表中显示的视频名称。 | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`：（必需）视频的长度，以秒为单位。 | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`：（必需）您希望在视频报表中显示的用于查看视频的媒体播放器名称。 | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`：（必需）广告的名称或 ID。 | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`：（必需）广告的长度。 | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`：（必需）用于查看广告的媒体播放器名称。 | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`：嵌入了广告的主内容的名称或 ID。 | 不适用 | 自动继承。 |
| parentPod | `parentPod`：广告在主内容中播放的位置。 | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`：广告在面板中播放的位置。 | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`：应用于此播放的 CPM 或加密 CPM（以“~”为前缀）。 | 不适用 | 在 Media Analytics 中默认不可用。 |
| Media.click | `s.Media.click(name, offset)` | 不适用 | 使用自定义链接分析调用来跟踪点击次数。 |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> 或 <br>trackEvent | `trackPause()` <br> 或 `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> 或 <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | 使用自定义或标准元数据来设置其他变量。 | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | 不适用 | 跟踪调用频率是自动设置的。 |
