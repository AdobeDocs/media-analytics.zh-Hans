---
title: 隐藏字幕
description: 跟踪查看器打开和关闭隐藏式字幕的时间，以便后端能够报告字幕参与情况。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 5%

---


# 隐藏字幕

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**隐藏式字幕**&#x200B;播放器状态的数据收集。 查看受隐藏式字幕影响的流数量[&#128279;](/help/reporting/metrics/closed-captioning-streams-impacted.md)、[隐藏式字幕数量](/help/reporting/metrics/closed-captioning-count.md)和[隐藏式字幕总持续时长](/help/reporting/metrics/closed-captioning-total-duration.md)以了解相应的报表量度。*

>[!ENDSHADEBOX]

当查看器打开和关闭字幕时，将跟踪隐藏式字幕播放器状态。 在启用字幕时触发状态开始事件，并在禁用字幕时触发状态结束事件。 后端根据这些事件计算三个量度：受影响的流数、状态条目计数和状态停留的总时间。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **XDM集合字段** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-collection-details)和[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-collection-details) （带有`name: "closedCaptioning"`的条目） |
| **Audience Manager特征** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
| **必需** | 否 |
| **发送条件** | [状态开始](/help/implementation/events/player-state/state-start.md)，[状态结束](/help/implementation/events/player-state/state-end.md) |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

使用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)发送状态已添加到`statesStart`的`media.statesUpdate`事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

当查看器禁用字幕时，发送另一个状态为`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.CLOSED_CAPTION`常量一起使用。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.CLOSED_CAPTION`常量一起使用。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

使用`sendMediaEvent`发送状态已添加到`statesStart`的`media.statesUpdate`事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

当查看器禁用字幕时，发送另一个状态为`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

在`statesStart`中使用`closedCaptioning`调用[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)终结点（或者在查看器禁用字幕时`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.ClosedCaptioning`常量：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

直接将`ADBMobile.media.createStateObject`与`"closedCaptioning"`字符串一起使用，因为Chromecast没有命名`PlayerState`常量：

```javascript
var stateObject = ADBMobile.media.createStateObject("closedCaptioning");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer disables captions:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

播放器状态跟踪在Roku 2.x SDK中不可用。 要跟踪播放器状态，请使用[Roku Edge SDK](/help/implementation/edge/roku.md)。

>[!TAB 媒体收集API]

启用字幕时发送`stateStart` POST请求，禁用字幕时发送`stateEnd` POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
