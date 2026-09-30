---
title: 第一个数字日期
description: 设置内容在数字平台上首次播出的日期。 Adobe建议使用YYYY-MM-DD格式。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 7%
---

# 第一个数字日期

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**第一个数字日期**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[首次数字化日期](/help/reporting/dimensions/first-digital-date.md)。*

>[!ENDSHADEBOX]

第一个数字日期变量是内容首次在任何数字平台上播出的日期。 可接受任何日期格式，但Adobe建议使用`YYYY-MM-DD`以保持一致性。 与[首次播放日期](/help/implementation/variables/standard-metadata/first-air-date.md)一起使用比较数字发布时间与原始广播。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.digitalDate` |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.digitalDate` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md)，会话关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.sessionDetails`中设置`firstDigitalDate`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将第一个数字日期作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

将第一个数字日期作为HashMap参数中的元数据键传递给`trackSessionStart`。 使用 `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

使用`createMediaSession`在`sessionDetails`中设置`firstDigitalDate`：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.sessionDetails`中包含`firstDigitalDate`的[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "firstDigitalDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

使用`ADB.Media.VideoMetadataKeys.FirstDigitalDate`传递`contextData`对象中的第一个数字日期：

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

在调用`trackSessionStart`之前，使用`ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE`设置媒体对象的`StandardMediaMetadata`属性中的第一个数字日期：

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

在调用`mediaTrackSessionStart`之前，使用`MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE`在媒体对象的标准元数据中设置第一个数字日期：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE] = "2016-01-25"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.firstDigitalDate`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions)。

>[!ENDTABS]
