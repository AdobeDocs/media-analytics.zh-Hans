---
title: 状态结束
description: 表示媒体播放器已退出跟踪播放器状态的信号。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 状态结束

状态结束事件表示媒体播放器已退出跟踪状态，例如全屏、静音或隐藏式字幕。 发送它以关闭由[状态开始](state-start.md)打开的状态。 状态可以在同一事件调用中开始和结束。 播放器可以同时退出多个状态。

有效的状态名称： `fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`、`inFocus`

* **先决条件**： [会话开始](../session/session-start.md)，[状态开始](state-start.md)
* **关联的量度**：因状态而异；请参阅[跟踪播放器状态](/help/implementation/events/player-state/overview.md)

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

使用`eventType: "media.statesUpdate"`和`statesEnd`中的状态名称调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)：

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

状态可以在同一调用中开始和结束：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将`trackPlayerStateEnd`与通过相应的`MediaConstants.PlayerState`常量创建的状态对象一起使用。

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

>[!TAB Android]

将`trackPlayerStateEnd`与通过相应的`MediaConstants.PlayerState`常量创建的状态对象一起使用。

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

>[!TAB Roku]

使用`eventType: "media.statesUpdate"`和`statesEnd`中的状态名称调用`sendMediaEvent`：

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

在`statesEnd`中调用状态名称为[statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/)的终结点：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

将`ADB.Media.createStateObject`与相应的`ADB.Media.PlayerState`常量一起使用：

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

将`ADBMobile.media.createStateObject`与相应的`ADBMobile.media.PlayerState`常量一起使用：

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB 媒体收集API]

向[事件终结点](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)发送`stateEnd`帖子：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
