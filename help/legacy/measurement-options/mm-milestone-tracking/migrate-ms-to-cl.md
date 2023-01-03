---
title: 了解如何从里程碑迁移到自定义链接
description: 了解如何将里程碑变量更改为自定义链接，并将里程碑模块方法更改为自定义链接语法。
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 9ba64b68efec5dd8b52010ac1a13afd7703448d0
workflow-type: ht
source-wordcount: '596'
ht-degree: 100%

---

# 从里程碑迁移到自定义链接{#migrating-from-milestone-to-custom-link}

## 概述 {#overview}

视频测量的核心概念与里程碑和自定义链接跟踪的核心概念相同，即获取视频播放器事件并将其映射到分析方法，同时还获取播放器元数据和值并将其映射到分析变量。应将“自定义链接”方法视为对实施和所收集数据的精简和简化。使用“自定义链接”解决方案，不会为视频测量预定义任何变量或方法，它需要进行完整的自定义设置。应当可以更新播放器事件代码，以指向基本的播放器事件（例如开始和结束）的自定义链接跟踪调用。请参阅[《自定义链接实施指南》](/help/legacy/measurement-options/cl-in-aa/cl-impl-guide.md)，以了解更多详细信息。

下表提供了“里程碑”解决方案和“自定义链接”解决方案之间的转换。

## 迁移指南 {#migration-guide}

### 视频变量引用

| 里程碑量度 | 变量类型 | 自定义链接 |
| --- | --- | --- |
| 内容 | eVar <br>默认过期：访问 | 定义您自已的 eVar。 |
| 内容类型 | eVar <br>默认过期：页面查看 | 定义您自已的 eVar。 |
| 内容逗留时间 | 事件 <br>类型：计数器 | 定义您自已的事件。 |
| 视频初始化 | 事件 <br>类型：计数器 | 定义您自已的事件。 |
| 视频结束 | 事件 <br>类型：计数器 | 定义您自已的事件。 |

### 媒体模块变量

| 里程碑 | 里程碑语法 | 自定义链接 | 自定义链接语法 |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | 不适用 | 现已通过处理规则，完成了将上下文数据映射到 eVar、prop 和事件中。 |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### 可选变量

| 里程碑 | 里程碑语法 | 自定义链接 | 自定义链接语法 |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | 不适用 | 不可用。 |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | 不适用 | 不可用。 |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | 不适用 | 不可用。 |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | 不适用 | 不可用。 |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | 在链接调用中设置 eVar 或上下文数据变量。 | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | 不适用 | 不可用。 |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | 不适用 | 不可用。 |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | 不适用 | 不可用。 |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | 不适用 | 不可用。 |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | 不适用 | 不可用。 |

### 广告跟踪变量

| 里程碑 | 里程碑语法 | 自定义链接 | 自定义链接语法 |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | 不适用 | 不可用。 |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | 不适用 | 不可用。 |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | 不适用 | 不可用。 |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | 不适用 | 不可用。 |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | 不适用 | 不可用。 |

### 媒体模块方法

| 里程碑 | 里程碑语法 | 自定义链接 | 自定义链接语法 |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`：（必需）您希望在视频报表中显示的视频名称。 | 在链接调用中设置 eVar 或上下文数据变量。 | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`：（必需）视频的长度，以秒为单位。 | 在链接调用中设置 eVar 或上下文数据变量。 | `s.contextData['video.length']` <br> `  = "90";` |
| mediaPlayerName | `mediaPlayerName`：（必需）您希望在视频报表中显示的用于查看视频的媒体播放器名称。 | 在链接调用中设置 eVar 或上下文数据变量。 | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | 不适用 | 不可用。 |
| name | `name`：（必需）广告的名称或 ID。 | 不适用 | 不可用。 |
| length | `length`：（必需）广告的长度。 | 不适用 | 不可用。 |
| playerName | `playerName`：（必需）用于查看广告的媒体播放器名称。 | 不适用 | 不可用。 |
| parentName | `parentName`：嵌入了广告的主内容的名称或 ID。 | 不适用 | 不可用。 |
| parentPod | `parentPod`：广告在主内容中播放的位置。 | 不适用 | 不可用。 |
| parentPodPosition | `parentPodPosition`：广告在面板中播放的位置。 | 不适用 | 不可用。 |
| CPM | `CPM`：应用于此播放的 CPM 或加密 CPM（以“~”为前缀）。 | 不适用 | 不可用。 |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | 使用自定义链接分析调用来跟踪点击次数。 |
| Media.close | `s.Media.close(mediaName)` | 不适用 | 不可用。 |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | 不适用 | 不可用。 |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | 不适用 | 不可用。 |
| Media.monitor | `s.Media.monitor(s, media)` | 在链接调用中设置 eVar 或上下文数据变量。 | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | 不适用 | 不可用。 |
