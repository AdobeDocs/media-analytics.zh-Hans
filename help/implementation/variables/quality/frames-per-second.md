---
title: 每秒帧数
description: 在QoE对象上设置当前帧速率，以便后端具有用于质量报告的帧速率上下文。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 7%

---


# 每秒帧数

每秒帧数变量是流的当前帧速率。 在QoE对象上将其与比特率和丢帧一起设置，以使后端具有每个播放会话的全部质量上下文。 Adobe Analytics不会自动为帧速率创建报表变量；如果您希望它显示为报表，请创建自定义处理规则。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | 无（Adobe Analytics没有为帧速率分配保留的上下文数据键） |
| **XDM集合字段** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特征** | 不适用 |
| **必需** | 否 |
| **发送条件** | 质量事件（[比特率更改](/help/implementation/events/playback/bitrate-change.md)，[缓冲开始](/help/implementation/events/playback/buffer-start.md)，[错误](/help/implementation/events/error.md)），会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.qoeDataDetails`中设置`framesPerSecond`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将帧速率作为第三个参数(`fps`)传递给`createQoEObject`。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

将帧速率作为第三个参数(`fps`)传递给`createQoEObject`。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

调用`sendMediaEvent`时，在`xdm.mediaCollection.qoeDataDetails`中设置`framesPerSecond`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.qoeDataDetails`中包含`framesPerSecond`的[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

将帧速率作为第三个参数传递给`ADB.Media.createQoEObject`：

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

将帧速率作为第三个参数(`fps`)传递给`ADBMobile.media.createQoSObject`并更新跟踪器：

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

将帧速率作为第三个参数(`fps`)传递给`adb_media_init_qosinfo`，并使用`mediaUpdateQoS`更新跟踪器：

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.qoe.framesPerSecond`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
