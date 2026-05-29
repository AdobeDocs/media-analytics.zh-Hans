---
title: 跟踪播放器状态
description: 了解播放器状态事件以及如何跟踪全屏、静音、隐藏式字幕、画中画和聚焦状态。
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 12%

---


# 跟踪播放器状态

播放器状态事件跟踪查看者在整个会话期间与播放器控件的交互方式。 核心媒体跟踪实施不需要这些参数，但这是可选参数。 五个可跟踪的状态是： `fullscreen`、`mute`、`closedCaptioning`、`pictureInPicture`和`inFocus`。

播放器状态事件有助于了解辅助功能用法，例如查看器启用隐藏式字幕或静音的频率。 此外，它们还可揭示查看行为模式，例如全屏与内联查看以及画中画多任务处理。

## 播放器事件

| 播放器事件 | 操作 |
| --- | --- |
| 播放器进入状态 | 呼叫状态开始 |
| 播放器退出状态 | 呼叫状态结束 |

## 标准状态和自定义状态

有五个标准播放器状态可用，而且您可以添加自己的自定义状态。

| 标准状态名称 | Media SDK 常数 | 媒体收集 API 名称 |
|----|----|----|
| 全屏 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 隐藏字幕 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 静音 | `ADB.Media.PlayerState.Mute` | `mute` |
| 画中画 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 焦点 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

有关包括XDM路径和量度定义的完整变量引用，请参阅[播放器状态变量](/help/implementation/variables/player-state/)。

**自定义状态：**&#x200B;您可以创建自定义状态来捕获特定于您的应用程序的其他播放器行为。 有关创建自定义状态对象的详细信息，请参阅[媒体API引用： `createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)。

## 实施步骤

1. 当播放器进入五个可跟踪状态中的任意状态时，**调用[状态开始](state-start.md)**。 多个状态可以同时处于活动状态，并且可以在同一事件调用中启动多个状态。
1. 当播放器退出某个状态时，**调用[状态结束](state-end.md)**。 可以在同一事件调用中结束多个状态，并且可以在单个调用中一起开始和结束状态。

## 准则

* 一个视频会话仅限拥有 10 个播放器状态。
* 状态可以任意组合。
* 如果传递了多个播放器状态，则仅保留前10个状态并将其转发到媒体后端。
* 10个州的上限适用于所有州，无论它们是处于打开状态还是关闭状态。
* 一个状态可以多次开始和结束，并计为单个状态。 例如，`closedCaptioning`可以启动和停止五次，但计为一个状态。
* 播放器状态是跨所有播放状态计算的（无拆分）
* 捕获每个单独播放会话的播放器状态。 不会跨播放计算播放器状态。
* 状态停止后，不会保留有关应用程序状态的信息。 状态结束后，必须再次启动状态才能继续跟踪。

## 同时更新多个状态

在基于XDM的平台上，可以使用`statesStart`和`statesEnd`中的数组将多个状态更改批量处理为单个`statesUpdate`调用。 在Mobile SDK上，每个状态更改都需要单独的调用。

以下示例将静音和画中画结合使用，然后转换为全屏。

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

```javascript
// t0 — start mute and picture-in-picture together
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }, { name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t1 — end mute and picture-in-picture; start full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }, { name: "pictureInPicture" }],
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});

// t2 — end full screen
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Mobile SDK不支持批量处理 — 请为每个状态更改发送单独的调用。

```swift
// t0 — start mute and picture-in-picture
let muteState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)
let pipState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(event: MediaEvent.StateStart, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateStart, info: pipState, metadata: nil)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: muteState, metadata: nil)
tracker.trackEvent(event: MediaEvent.StateEnd, info: pipState, metadata: nil)
let fullscreenState = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(event: MediaEvent.StateStart, info: fullscreenState, metadata: nil)

// t2 — end full screen
tracker.trackEvent(event: MediaEvent.StateEnd, info: fullscreenState, metadata: nil)
```

>[!TAB Android]

Mobile SDK不支持批量处理 — 请为每个状态更改发送单独的调用。

```kotlin
// t0 — start mute and picture-in-picture
val muteState = Media.createStateObject(MediaConstants.PlayerState.MUTE)
val pipState = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)
tracker.trackEvent(Media.Event.StateStart, muteState, null)
tracker.trackEvent(Media.Event.StateStart, pipState, null)

// t1 — end mute and picture-in-picture; start full screen
tracker.trackEvent(Media.Event.StateEnd, muteState, null)
tracker.trackEvent(Media.Event.StateEnd, pipState, null)
val fullscreenState = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)
tracker.trackEvent(Media.Event.StateStart, fullscreenState, null)

// t2 — end full screen
tracker.trackEvent(Media.Event.StateEnd, fullscreenState, null)
```

>[!TAB Roku]

```brightscript
' t0 — start mute and picture-in-picture together
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "playhead": 0
        }
    }
})

' t1 — end mute and picture-in-picture; start full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
            "statesStart": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})

' t2 — end full screen
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{"name": "fullscreen"}],
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

```sh
# t0 — start mute and picture-in-picture together
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:00:00+00:00"
    }
  }]
}'

# t1 — end mute and picture-in-picture; start full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "mute"}, {"name": "pictureInPicture"}],
        "statesStart": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:01:00+00:00"
    }
  }]
}'

# t2 — end full screen
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesEnd": [{"name": "fullscreen"}],
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-01-01T00:02:00+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

多个状态更改需要单独的调用。

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);
var pipState = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);
tracker.trackPlayerStateStart(muteState);
tracker.trackPlayerStateStart(pipState);

// t1 — end mute and picture-in-picture; start full screen
tracker.trackPlayerStateEnd(muteState);
tracker.trackPlayerStateEnd(pipState);
var fullscreenState = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);
tracker.trackPlayerStateStart(fullscreenState);

// t2 — end full screen
tracker.trackPlayerStateEnd(fullscreenState);
```

>[!TAB Chromecast]

多个状态更改需要单独的调用。

```javascript
// t0 — start mute and picture-in-picture
var muteState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.Mute);
var pipState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.PictureInPicture);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, pipState, null);

// t1 — end mute and picture-in-picture; start full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, muteState, null);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, pipState, null);
var fullscreenState = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, fullscreenState, null);

// t2 — end full screen
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, fullscreenState, null);
```

>[!TAB 媒体收集API]

```json
// t0 — start mute and picture-in-picture together
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999130627 }
}

// t1 — end mute and picture-in-picture; start full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      { "media.state.name": "mute" },
      { "media.state.name": "pictureInPicture" }
    ],
    "statesStart": [
      { "media.state.name": "fullScreen" }
    ]
  },
  "playerTime": { "playhead": 0, "ts": 1569999230627 }
}

// t2 — end full screen
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [{ "media.state.name": "fullScreen" }]
  },
  "playerTime": { "playhead": 0, "ts": 1569999330627 }
}
```

>[!ENDTABS]

## 长时间暂停

当视频会话的暂停持续时间超过30分钟时，API需要启动新会话。 生成新的会话ID并保留所有活动状态，以便在新的`sessionStart`调用之后立即通过`stateStart`事件还原这些状态。

`sessionStart → stateStart (fullscreen) → stateStart (mute) → pauseStart → (pings for 30 minutes) → sessionEnd`

发送`sessionEnd`后，启动新会话并立即重新发送活动状态：

`sessionStart → stateStart (fullscreen) → stateStart (mute) → ... other API events`

## 状态量度

系统会为每个跟踪的状态计算三个量度，并在媒体关闭调用时发送到Adobe Analytics：

| 量度 | 上下文数据键 | 描述 |
| --- | --- | --- |
| 状态集 | `a.media.states.[state.name].set = true` | 如果在播放期间至少设置过一次状态，则为`true` |
| 状态计数 | `a.media.states.[state.name].count = 4` | 播放期间出现该状态的次数 |
| 状态时间 | `a.media.states.[state.name].time = 240` | 播放期间处于状态所花费的总时间（秒） |
