---
title: 静音
description: 跟踪查看器何时将音频静音和取消静音，以便后端可以报告静音参与情况。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 6%

---


# 静音

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**静音**&#x200B;播放器状态的数据收集。 查看受静音影响的[流](/help/reporting/metrics/mute-streams-impacted.md)、[静音计数](/help/reporting/metrics/mute-count.md)以及相应报表量度的[静音总持续时间](/help/reporting/metrics/mute-total-duration.md)。*

>[!ENDSHADEBOX]

静音播放器状态在查看器静音和取消静音时跟踪。 在查看器静音时触发状态开始事件，并在查看器取消静音时触发状态结束事件。 后端根据这些事件计算三个量度：受影响的流数、状态条目计数和状态停留的总时间。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **XDM集合字段** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-collection-details)和[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-collection-details) （带有`name: "mute"`的条目） |
| **Audience Manager特征** | `c_contextdata.a.media.states.mute.set`, `c_contextdata.a.media.states.mute.count`, `c_contextdata.a.media.states.mute.time` |
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
      statesStart: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

当查看器取消静音时，发送另一个状态为`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.MUTE`常量一起使用。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.MUTE`常量一起使用。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

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
            "statesStart": [{ "name": "mute" }],
            "playhead": 60
        }
    }
})
```

当查看器取消静音时，发送另一个状态为`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "mute" }],
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

在`statesStart`中使用`mute`调用[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)终结点（或在查看器取消静音时调用`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "mute" }],
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

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.Mute`常量：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

直接将`ADBMobile.media.createStateObject`与`"mute"`字符串一起使用，因为Chromecast没有命名`PlayerState`常量：

```javascript
var stateObject = ADBMobile.media.createStateObject("mute");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer unmutes:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

播放器状态跟踪在Roku 2.x SDK中不可用。 要跟踪播放器状态，请使用[Roku Edge SDK](/help/implementation/edge/roku.md)。

>[!TAB 媒体收集API]

在查看器静音时发送`stateStart` POST请求，并在查看器取消静音时发送`stateEnd` POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
