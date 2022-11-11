---
title: 实施与报表
description: 了解如何实施播放器状态跟踪功能，包括。
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 96%

---

# 实施与报表

在播放会话期间，必须单独跟踪每个状态的出现情况（从开始到结束）。Media SDK 和媒体收集 API 为实现这项功能提供了新的跟踪方法。

Media SDK 包含两种进行自定义状态跟踪的新方法：

`trackStateStart("state_name")`

`trackStateClose("state_name")`


媒体收集 API 包含两个新事件，它们将 `media.stateName` 作为必需参数：

`stateStart` 和 `stateEnd`

## Media SDK 实施

播放器状态开始

```
// StateStart (ex: Mute is switched on)
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
tracker.trackEvent(ADB.Media.Event.StateStart, stateObject);
```

播放器状态结束

```
// StateEnd (ex: Mute is switched off)
tracker.trackEvent(ADB.Media.Event.StateEnd, stateObject);
```


## 媒体收集 API 实施

播放器状态开始

```
// StateStart (ex: Mute is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

播放器状态结束

```
// StateEnd (ex: Mute is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events

{
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "mute"
  },
  "playerTime": {
    "playhead": 600,
    "ts": 1569999730638
  }
}
```

## 状态量度

会计算为每个单独状态提供的量度，并将其作为“上下文数据”参数推送到 Adobe Analytics，然后进行存储以用于生成报表。每个状态有三个可用量度：

* `a.media.states.[state.name].set = true` - 如果每次播放特定流时至少设置一次状态，则设置为 true。
* `a.media.states.[state.name].count = 4` - 标识在每次播放流时某种状态出现的次数
* `a.media.states.[state.name].time = 240` - 标识在每次播放流时持续的时长（以秒为单位）

## 报表

为播放器状态跟踪启用报表包后，所有播放器状态量度都可用于 Analysis Workspace 或组件（区段、计算量度）中提供的任何报告可视化。可以从 Admin Console 中使用“媒体报告设置”（“编辑设置”>“媒体管理”>“媒体报告”）为每个报告启用新量度。

![](assets/report-setup.png)

在 Analytics 工作区中，所有新属性都位于“量度”面板中。例如，您可以在“量度”面板中搜索 `full screen` 以查看全屏数据。

![](assets/full-screen-report.png)

## 将播放器规定的量度导入 Adobe Experience Platform

存储在 Analytics 中的数据可用于任何目的，并且可以使用 XDM 将播放器状态量度导入到 Adobe Experience Platform 中，用于 Customer Journey Analytics。标准状态属性具有特定属性，而自定义状态属性可使用自定义事件获得。有关标准状态属性的更多信息，请参阅[播放器状态参数](/help/implementation/variables/player-state-parameters.md)页面上的 *XDM 标识的属性列表*&#x200B;部分。
