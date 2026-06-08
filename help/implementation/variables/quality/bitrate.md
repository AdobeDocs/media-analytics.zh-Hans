---
title: 比特率
description: 在QoE对象中设置当前播放比特率（以kbps为单位），以便后端可以计算比特率量度。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 5%

---


# 比特率

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**Bitrate**&#x200B;变量的数据收集。 查看相应报表变量的[[!UICONTROL 平均比特率]（维度）](/help/reporting/dimensions/average-bitrate.md)和[[!UICONTROL 平均比特率]（量度）](/help/reporting/metrics/average-bitrate.md)。*

>[!ENDSHADEBOX]

bitrate变量是当前播放比特率（以千位/秒为单位）。 每当播放器协商比特率时，在QoE对象中设置它，并在比特率发生更改时更新QoE对象。 后端使用比特率值来计算[[!UICONTROL 平均比特率]](/help/reporting/metrics/average-bitrate.md)、每比特率存储桶维度和[[!UICONTROL 比特率更改]](/help/reporting/metrics/bitrate-changes.md)量度。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.qoe.bitrateAverageBucket` |
| **XDM集合字段** | [`xdm.mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **必需** | 否 |
| **发送条件** | 质量事件（[比特率更改](/help/implementation/events/playback/bitrate-change.md)，[缓冲开始](/help/implementation/events/playback/buffer-start.md)，[错误](/help/implementation/events/error.md)），会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`media.bitrateChange`（或任何与质量相关的事件）的`xdm.mediaCollection.qoeDataDetails`中设置`bitrate`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

将比特率作为第一个参数传递给`createQoEObject`。 在触发任何质量事件之前更新跟踪器上的QoE对象。

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

将比特率作为第一个参数传递给`createQoEObject`。 在触发任何质量事件之前更新跟踪器上的QoE对象。

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

为质量事件（如`media.bitrateChange`）调用`sendMediaEvent`时，在`xdm.mediaCollection.qoeDataDetails`中设置`bitrate`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.qoeDataDetails`中包含`bitrate`的[bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
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

将比特率作为第一个参数传递给`ADB.Media.createQoEObject`并更新跟踪器：

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

将以kbps为单位的比特率作为第一个参数传递给`ADBMobile.media.createQoSObject`并更新跟踪器：

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

将以kbps为单位的比特率作为第一个参数传递给`adb_media_init_qosinfo`，并使用`mediaUpdateQoS`更新跟踪器：

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB 媒体收集API]

在`bitrateChange` POST请求的`params`对象中包括`media.qoe.bitrate`：

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
