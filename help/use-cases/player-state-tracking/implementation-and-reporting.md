---
title: 实施与报表
description: 了解如何实施播放器状态跟踪功能，包括。
exl-id: 19a97c9b-14d1-4f11-bb0a-3a1ad6f949da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/NzekVHZYctiEjAWDpRhIdiw74amAX3wTX-z2nZDgvIw
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
  - id: f836f655-eebe-4b76-82bc-697955ec1ce3
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 308
ht-degree: 76%

---

# 实施与报表

在播放会话期间，必须单独跟踪每个状态的出现情况（从开始到结束）。 Media SDK和媒体收集API提供了针对此功能的跟踪方法。

Media SDK包括两种自定义状态跟踪方法：

`trackStateStart("state_name")`

`trackStateClose("state_name")`


媒体收集API包含两个事件，它们将`media.stateName`作为必需参数：

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

会计算为每个单独状态提供的量度，并将其作为“上下文数据”参数推送到 Adobe Analytics，然后进行存储以用于生成报表。 每个状态有三个可用量度：

* `a.media.states.[state.name].set = true` - 如果每次播放特定流时至少设置一次状态，则设置为 true。
* `a.media.states.[state.name].count = 4` - 标识在每次播放流时某种状态出现的次数
* `a.media.states.[state.name].time = 240` - 标识在每次播放流时持续的时长（以秒为单位）

## 报告

为播放器状态跟踪启用报表包后，所有播放器状态量度都可用于 Analysis Workspace 或组件（区段、计算量度）中提供的任何报告可视化。 可以使用“媒体报表设置”（“编辑设置”>“媒体管理”>“媒体报表”）从Admin Console为每个单独的报表启用这些指标。

![](assets/report-setup.png)

在Analysis Workspace中，所有新资产都位于“指标”面板中。 例如，您可以在“量度”面板中搜索 `full screen` 以查看全屏数据。

![](assets/full-screen-report.png)

## 将播放器规定的量度导入 Adobe Experience Platform

存储在 Analytics 中的数据可用于任何目的，并且可以使用 XDM 将播放器状态量度导入到 Adobe Experience Platform 中，用于 Customer Journey Analytics。 标准状态属性具有特定属性，而自定义状态属性可使用自定义事件获得。
