---
seo-title: 从里程碑迁移到 Media Analytics
title: 从里程碑迁移到 Media Analytics
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: ffb97a0162e0bb609ea427afab81e4d8b532f20b

---


# 从里程碑迁移到 Media Analytics {#migrating-from-milestone-to-media-analytics}

## 概述 {#overview}

视频测量的核心概念与里程碑和 Media Analytics 的核心概念相同，即获取视频播放器事件并将其映射到分析方法，同时还获取播放器元数据和值并将其映射到分析变量。Media Analytics 解决方案源自里程碑解决方案，因此两种解决方案中的许多方法和量度都是相同的，但配置方法和代码发生了较大改变。应当可以更新播放器事件代码以指向新的 Media Analytics 方法。有关实 [施Media Analytics的更多详细信](/help/sdk-implement/setup/setup-overview.md)[](/help/sdk-implement/track-av-playback/track-core-overview.md) 息，请参阅SDK概述和跟踪概述。

下表提供了“里程碑”解决方案和“Media Analytics”解决方案之间的转换。

## 迁移指南 {#migration-guide}

### 变量引用

| 里程碑量度 | 变量类型 | Media Analytics 量度 |
| --- | --- | --- |
| 内容 | eVar默<br/><br/>认到期：访问 | 内容 |
| 内容类型 | eVar<br/><br/> Default expiration: Page view | 内容类型 |
| 内容逗留时间 | Event<br/><br/> Type: Counter | 内容逗留时间 |
| 视频初始化 | Event<br/><br/> Type: Counter | 视频初始化 |
| 视频结束 | 事件<br/><br/> 类型：计数器 | 内容结束 |

### 媒体模块变量

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑语法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 语法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>不适用
</td>
<td>所有 Media Analytics 数据仅使用上下文数据发送。
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = { "a.media.name":"eVar2,prop2", "a.media.segment":"eVar3", "a.contentType":"eVar1", "a.media.timePlayed":"event3", "a.media.view":"event1", "a.media.media.segmentView":"event2", "a.media.complete":"event7", "a.media.milestones":{ 25:"event4", 50:"event5", 75:"event6" }};
</pre>
</td>
<td>不适用
</td>
<td>Media Analytics 上下文数据会自动填充到保留变量中。实施代码中不再需要映射到 eVar、prop 和事件。客户可以使用处理规则将上下文数据映射到变量。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = "events, prop2, eVar1, eVar2, eVar3";
</pre>
</td>
<td>不适用
</td>
<td>不再需要，因为映射是通过保留变量和处理规则进行的。
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = "event1, event2, event3, event4, event5, event6, event7"
</pre>
</td>
<td>不适用
</td>
<td>不再需要，因为映射是通过保留变量和处理规则进行的。
</td>
</tr>
</tbody>
</table>

### 可选变量

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑语法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 语法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack = true;
</pre>
</td>
<td>不适用
</td>
<td>我们不再提供预先构建的播放器映射。
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams = true
</pre>
</td>
<td>不适用
</td>
<td>我们不再提供预先构建的播放器映射。
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset = true
</pre>
</td>
<td>不适用
</td>
<td>“内容结束”仅支持 100% 进度标记。
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold = 1
</pre>
</td>
<td>不适用
</td>
<td>“内容结束”仅支持 100% 进度标记。
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "自定义播放器名称"
</pre>
</td>
<td>
SDK密钥：playerName;API密钥：media.playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds = 15
</pre>
</td>
<td>不适用
</td>
<td>对于内容，Media Analytics 设置为 10 秒；对于广告，设置为 1 秒。无其他选项可用。
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestones = "25,50,75";
</pre>
</td>
<td>不适用
</td>
<td>Media Analytics 始终跟踪 10%、25%、50%、75%、95% 进度标记
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>不适用
</td>
<td>Media Analytics 始终跟踪 10%、25%、50%、75%、95% 进度标记
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>不适用
</td>
<td>自动跟踪不再可用
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones = true;
</pre>
</td>
<td>不适用
</td>
<td>自动跟踪不再可用
</td>
</tr>
</tbody>
</table>

### 广告跟踪变量

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑语法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 语法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds = 15
</pre>
</td>
<td>不适用
</td>
<td>对于内容，Media Analytics 设置为 10 秒；对于广告，设置为 1 秒。无其他选项可用。
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestones = "25,50,75";
</pre>
</td>
<td>不适用
</td>
<td>默认情况下，不会为广告提供进度标记。请使用计算量度来构建广告进度标记。
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>不适用
</td>
<td>对于广告，Media Analytics 设置为 1 秒。无其他选项可用。
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones = true;
</pre>
</td>
<td>不适用
</td>
<td>自动跟踪不再可用
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones = true;
</pre>
</td>
<td>不适用
</td>
<td>自动跟踪不再可用
</td>
</tr>
</tbody>
</table>

### 媒体模块方法

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑语法
</th>
<th>Media Analytics
</th>
<th>Media Analytics 语法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart(mediaObject, contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName -（必需）您希望视频显示在视频报告中的视频名称。
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject(name, mediaId, length, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength -（必需）视频秒数的长度。
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject(name, mediaId, length, streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName -（必需）用于查看视频的媒体播放器的名称，如您希望它显示在视频报告中一样。
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent(MediaHeartbeat。
    事件.
    AdBreakStart、adBreakObject);...trackEvent(MediaHeartbeat。
    事件.
    AdStart、adObject、adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name -（必需）广告的名称或ID。
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject(name, adId, position, length)
</pre>
</td>
</tr>
<tr>
<td>
长度（必需）广告的长度。
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject(name, adId, position, length)
</pre>
</td>
</tr>
<tr>
<td>
playerName -（必需）用于查看广告的mediaplayer的名称。
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName —— 嵌入广告的主要内容的名称或ID。
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>不适用
</td>
<td>自动继承
</td>
</tr>
<tr>
<td>
parentPod —— 广告播放的主要内容中的位置。
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject(name, position, startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition —— 播放广告的窗格内的位置。
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject(name, adId, position, length)
</pre>
</td>
</tr>
<tr>
<td>
CPMT适用于此播放的CPM或加密CPM（前缀为“~”）。
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>不适用
</td>
<td>默认情况下，在Media Analytics中不可用
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
</pre>
</td>
<td>不适用
</td>
<td>使用自定义链接分析调用来跟踪点击次数
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(name,offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment, segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> 或 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
或
<pre>
trackEvent(MediaHeartbeat。
  事件.
  SeekStart)
</pre> 或
<pre>
trackEvent(MediaHeartbeat。
  事件.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>使用自定义或标准元数据来设置其他变量
</td>
<td>
<pre>
var customVideoMetadata = { isUserLoggedIn:
    “false”,tvStation:
    节目编排者：
    “程序员范例”};...var standardVideoMetadata = {};standardVideoMetadata [MediaHeartbeat。
   VideoMetadataKeys.
   ISPOSE] = "Sample Ispose";standardVideoMetadata [MediaHeartbeat。
   VideoMetadataKeys.
   SHOW] = "Sample Show";...mediaObject.setValue(MediaHeartbeat。
  MediaObjectKey。
  StandardVideoMetadata、standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>不适用
</td>
<td>将自动设置跟踪调用频率。
</td>
</tr>
</tbody>
</table>

