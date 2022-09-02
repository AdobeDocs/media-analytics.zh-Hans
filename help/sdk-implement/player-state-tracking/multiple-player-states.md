---
title: 一次更新多个播放器状态
description: 本主题介绍多播放器状态跟踪功能。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: fdbb777547181422b81ff6f7874bec3d317d02e9
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 9%

---

# 多播放器状态跟踪

有时，两个播放器状态同时开始和结束，或者状态的结束也是另一个状态的开始，如下图所示：

![多个播放器状态](assets/multiple-player-states.svg)

当前实施允许两种情况：
- `stateStart(pictureInPicture)` - t0
- `stateStart(mute)` - t0
- `stateEnd(mute)` - t1
- `stateEnd(pictureInPicture)` - t1
- `stateStart(fullScreen)` - t1
- `stateEnd(fullScreen)` - t2

但是，这要求您发布多个 `stateStart` 和 `stateEnd` 事件来表示多个同时状态更改。 为了优化此常见行为，新 `statesUpdate` 已实施事件类型，该事件类型结束状态列表并开始新状态列表。

使用新 `statesUpdate` 事件时，上述事件列表将变为：
- `statesUpdate(statesEnd=[], statesStart=[pictureInPicture, mute])` - t0
- `statesUpdate(statesEnd=[mute, pictureInPicture], statesStart=[fullScreen])` - t1
- `statesUpdate(statesEnd=[fullScreen], statesStart=[])` - t2

对于相同行为，状态更新调用数量已从6个减少到3个。 最后一个事件可能也很简单 `stateEnd(fullScreen)`.

## 媒体收集 API 实施 {#mpst-api}

您可以使用媒体收集API实施多个播放器状态跟踪。

### 示例

以下显示了用于多播放器状态跟踪的媒体收集API实施示例。

```
// statesUpdate (ex: mute and pictureInPicture are switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesStart": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: mute and pictureInPicture are switched off, fullScreen is switched on)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "mute"
      },
      {
        "media.state.name": "pictureInPicture"
      }
    ],
    "statesStart": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

```
// statesUpdate (ex: fullScreen is switched off)
http(s)://<Analytics_Visitor_Namespace>.hb-api.omtrdc.net/api/v1/sessions/<SID>/events
{
  "eventType": "statesUpdate",
  "params": {
    "statesEnd": [
      {
        "media.state.name": "fullScreen"
      }
    ]
  },
  "playerTime": {
    "playhead": 0,
    "ts": 1569999130627
  }
}
```

## Media SDK 实施

没有Media SDK实施。
