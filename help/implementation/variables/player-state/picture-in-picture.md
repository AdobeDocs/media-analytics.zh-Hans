---
title: 画中画
description: 跟踪查看者何时进入和退出画中画播放，以便后端可以报告PiP参与情况。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 5%

---


# 画中画

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**画中画**&#x200B;播放器状态的数据收集。 查看受画中画影响的流数量[&#128279;](/help/reporting/metrics/picture-in-picture-streams-impacted.md)、[画中画计数](/help/reporting/metrics/picture-in-picture-count.md)和[画中画总持续时间](/help/reporting/metrics/picture-in-picture-total-duration.md)以了解相应的报表量度。*

>[!ENDSHADEBOX]

当观看者进入和退出画中画播放时，画中画播放器状态进行跟踪。 在画中画开始时触发状态开始事件，并在画中画结束时触发状态结束事件。 后端根据这些事件计算三个量度：受影响的流数、状态条目计数和状态停留的总时间。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.states.pictureinpicture.set`, `a.media.states.pictureinpicture.count`, `a.media.states.pictureinpicture.time` |
| **XDM集合字段** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-collection-details)和[`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-collection-details) （带有`name: "pictureInPicture"`的条目） |
| **Audience Manager特征** | `c_contextdata.a.media.states.pictureinpicture.set`, `c_contextdata.a.media.states.pictureinpicture.count`, `c_contextdata.a.media.states.pictureinpicture.time` |
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
      statesStart: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

当查看器退出画中画时，发送另一个状态为`statesEnd`的事件：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.PICTURE_IN_PICTURE`常量一起使用。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

将`tracker.trackPlayerStateStart()`和`tracker.trackPlayerStateEnd()`与`MediaConstants.PlayerState.PICTURE_IN_PICTURE`常量一起使用。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku]

使用`sendMediaEvent`发送状态已添加到`statesStart`的`media.statesUpdate`事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "pictureInPicture" }],
            "playhead": 60
        }
    }
})
```

当查看器退出画中画时，发送另一个状态为`statesEnd`的事件：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "pictureInPicture" }],
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

在`statesStart`中使用`pictureInPicture`调用[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)终结点（或者，当查看器退出PiP时`statesEnd`）：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "pictureInPicture" }],
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

使用`ADB.Media.createStateObject`和`ADB.Media.PlayerState.PictureInPicture`常量：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

直接将`ADBMobile.media.createStateObject`与`"pictureInPicture"`字符串一起使用，因为Chromecast没有命名`PlayerState`常量：

```javascript
var stateObject = ADBMobile.media.createStateObject("pictureInPicture");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer exits picture-in-picture:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB 媒体收集API]

当画中画开始时，发送`stateStart`个POST请求；当画中画结束时，发送`stateEnd`个POST：

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "pictureInPicture"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
