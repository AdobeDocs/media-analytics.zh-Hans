---
title: 全屏
description: 跟踪查看器进入和退出全屏播放的时间，以便后端可以报告全屏参与情况。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 7%

---


# 全屏

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**全屏**&#x200B;播放器状态的数据收集。 查看受全屏影响的[流](/help/reporting/metrics/full-screen-streams-impacted.md)、[全屏计数](/help/reporting/metrics/full-screen-count.md)和[全屏总持续时间](/help/reporting/metrics/full-screen-total-duration.md)以了解相应的报表量度。*

>[!ENDSHADEBOX]

全屏播放器状态将跟踪查看器进入和退出全屏播放的时间。 每当查看器进入全屏时触发状态开始事件，并在查看器退出时触发状态结束事件。 后端根据这些事件计算三个量度：受影响的流数、状态条目计数和状态停留的总时间。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **XDM集合字段** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details)和[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) （带有`name: "fullscreen"`的条目） |
| **Audience Manager特征** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
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
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

当查看器全屏退出时，发送另一个状态为`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.FULLSCREEN`常量一起使用。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.FULLSCREEN`常量一起使用。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku]

使用`sendMediaEvent`发送状态已添加到`statesStart`的`media.statesUpdate`事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

当查看器全屏退出时，发送另一个状态为`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

在`statesStart`中使用`fullscreen`调用[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)终结点（当查看器退出时，调用`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
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

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.FullScreen`常量：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

直接将`ADBMobile.media.createStateObject`与`"fullscreen"`字符串一起使用，因为Chromecast没有命名`PlayerState`常量：

```javascript
var stateObject = ADBMobile.media.createStateObject("fullscreen");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the user exits full-screen:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB 媒体收集API]

当查看者进入全屏时发送`stateStart`个POST请求，当他们退出时发送`stateEnd`个POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
