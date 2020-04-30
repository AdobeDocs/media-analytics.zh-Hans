---
title: 从里程碑迁移到自定义链接
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a

---


# 从里程碑迁移到自定义链接{#migrating-from-milestone-to-custom-link}

## 概述 {#overview}

视频测量的核心概念与里程碑和自定义链接跟踪的核心概念相同，即获取视频播放器事件并将其映射到分析方法，同时还获取播放器元数据和值并将其映射到分析变量。应将“自定义链接”方法视为对实施和所收集数据的精简和简化。使用“自定义链接”解决方案，不会为视频测量预定义任何变量或方法，它需要进行完整的自定义设置。应当可以更新播放器事件代码，以指向基本的播放器事件（例如开始和结束）的自定义链接跟踪调用。有关更多详细信息，请参阅[自定义链接实施指南](/help/measurement-options/cl-in-aa/cl-impl-guide.md)和[使用自定义链接代码手动链接跟踪](https://docs.adobe.com/content/help/en/media-analytics/using/measurement-options/cl-in-aa/cl-impl-guide.html)。

下表提供了“里程碑”解决方案和“自定义链接”解决方案之间的转换。

## 迁移指南 {#migration-guide}

### 视频变量引用

<table>
<thead>
<tr>
<th><strong>里程碑量度</strong></th>
<th><strong>变量类型</strong></th>
<th><strong>自定义链接</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>内容</td>
<td>
<p>eVar</p>
<p>默认过期：访问</p>
</td>
<td>定义您自已的 eVar</td>
</tr>
<tr>
<td>内容类型</td>
<td>
<p>eVar</p>
<p>默认过期：页面查看</p>
</td>
<td>定义您自已的 eVar</td>
</tr>
<tr>
<td>内容逗留时间</td>
<td>
<p>Event</p>
<p>类型：计数器</p>
</td>
<td>定义您自已的事件</td>
</tr>
<tr>
<td>视频初始化</td>
<td>
<p>Event</p>
<p>类型：计数器</p>
</td>
<td>定义您自已的事件</td>
</tr>
<tr>
<td>视频结束</td>
<td>
<p>Event</p>
<p>类型：计数器</p>
</td>
<td>定义您自已的事件</td>
</tr>
</tbody>
</table>

### 媒体模块变量

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑语法
</th>
<th>自定义链接
</th>
<th>自定义链接语法
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
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  contextDataMapping = {
  "a.media.name":
    "eVar2,prop2",
  "a.media.segment":
    "eVar3",
  "a.contentType":
    "eVar1",
  "a.media.timePlayed":
    "event3",
  "a.media.view":
    "event1",
  "a.media.segmentView":
    "event2",
  "a.media.complete":
    "event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>不适用
</td>
<td>现已通过处理规则将上下文数据映射到 eVar、prop 和事件。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>里程碑
</th>
<th>里程碑语法
</th>
<th>自定义链接
</th>
<th>自定义链接语法
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
s.Media.
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>不适用
</td>
<td>现已通过处理规则将上下文数据映射到 eVar、prop 和事件。
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
</pre>
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
<th>自定义链接
</th>
<th>自定义链接语法
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
s.Media.autoTrack
  = true;
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams
  = true
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset
  = true
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold
    = 1
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName 
  = "Custom Player Name"
</pre>
</td>
<td>
在链接调用中设置 eVar 或上下文数据变量
</td>
<td>
<pre>
s.contextData['video.player']
  = "CustomPlayer Name";
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones 
  = "25,50,75";
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones 
  = "20,40,60";
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones
  = true;
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones
    = true;
</pre>
</td>
<td>不适用
</td>
<td>不可用
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
<th>自定义链接
</th>
<th>自定义链接语法
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
s.Media.adTrackSeconds 
  = 15 
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones 
  = "25,50,75";
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones 
    = "20,40,60";
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones
    = true;
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones
    = true;
</pre>
</td>
<td>不适用
</td>
<td>不可用
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
<th>自定义链接
</th>
<th>自定义链接语法
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(
  mediaName,
  mediaLength,
  mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.video.name,
     contextData.video.view';
s.linkTrackEvents 
  = 'event2';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event2';
s.contextData['video.name'] 
  = mediaName;
s.contextData['video.view'] 
  = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName：</b>（必需）您希望在视频报表中显示的视频名称。</td>
<td>在链接调用中设置 eVar 或上下文数据变量</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength：</b>（必需）视频的长度，以秒为单位。
</td>
<td>
在链接调用中设置 eVar 或上下文数据变量
</td>
<td>
<pre>
s.contextData['video.length']
  = "90";
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName：</b>（必需）您希望在视频报表中显示的用来查看视频的媒体播放器名称。
</td>
<td>
在链接调用中设置 eVar 或上下文数据变量
</td>
<td>
<pre>
s.contextData['video.player']
  = "CustomPlayer Name";
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(
  name,
  length,
  playerName,
  parentName,
  parentPod,
  parentPodPosition,
  CPM)
</pre>
</td>
<td>不适用
</td>
<td>不可用</td>
</tr>
<tr>
<td>name</td>
<td><b>name：</b>（必需）广告的名称或 ID。</td>
<td>不适用</td>
<td>不可用</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length：</b>（必需）广告的长度。
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>playerName：</b>（必需）用来查看广告的媒体播放器名称。
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName：</b>广告被嵌入到的主内容的名称或 ID。
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod：</b>广告在主内容中播放的位置。
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition：</b>广告在面板中播放的位置。
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM：</b>应用于此播放的 CPM 或加密 CPM（具有前缀“~”）。
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name, offset)
</pre>
</td>
<td>
<pre>
s.tl()
</pre>
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
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(
  name,
  offset)
</pre>
</td>
<td>
s.tl()
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.complete';
s.linkTrackEvents 
  = 'event3';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event3';
s.contextData['video.name']
 =  mediaName;
s.contextData['video.complete']
 = 'true';
s.tl(this,'o','Video Complete');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(
  name,
  offset,
  segmentNum,
  segment,
  segmentLength)
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(
  mediaName,
  mediaOffset)
</pre>
</td>
<td>不适用 
</td>
<td>不可用
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
在链接调用中设置 eVar 或上下文数据变量
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
s.linkTrackEvents = 'event2';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>不适用
</td>
<td>不可用
</td>
</tr>
</tbody>
</table>

