---
title: 创作 ID
description: 设置每个广告的创意标识符。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 10%

---


# 创作 ID

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**Creative ID**&#x200B;变量的数据收集。 查看相应报表维度的[Creative ID](/help/reporting/dimensions/creative-id.md)。*

>[!ENDSHADEBOX]

创意ID变量可识别特定的广告创意。 可接受任何字符串值（通常是广告服务器平台中的创意ID）。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.creative` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingDetails.creativeID`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.creative` |
| **必需** | 否 |
| **发送条件** | [广告开始](/help/implementation/events/ads/ad-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingDetails`中设置`creativeID`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        creativeID: "creative-987"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将创意ID作为哈希映射参数中的元数据键传递给`trackEvent(AdStart)`。 使用 `MediaConstants.AdMetadataKeys.CREATIVE_ID`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

将创意ID作为哈希映射参数中的元数据键传递给`trackEvent(AdStart)`。 使用 `MediaConstants.AdMetadataKeys.CREATIVE_ID`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CREATIVE_ID] = "creative-987"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

为`media.adStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingDetails`中设置`creativeID`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "creativeID": "creative-987"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingDetails`中包含`creativeID`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.adStart",
      "mediaCollection": {
        "advertisingDetails": {
          "name": "ad-2125",
          "length": 15,
          "playerName": "Freewheel",
          "podPosition": 0,
          "creativeID": "creative-987"
        },
        "sessionID": "{sid}",
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

使用`ADB.Media.AdMetadataKeys.CreativeId`在`contextData`对象中传递创意ID：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CreativeId] = "creative-987";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

使用标准广告元数据对象中的`ADBMobile.media.AdMetadataKeys.CREATIVE_ID`设置创作ID：

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CREATIVE_ID] = "creative-987";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

使用标准广告元数据对象中的`MEDIA_AdMetadataKeyCREATIVE_ID`设置创作ID：

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCREATIVE_ID] = "creative-987"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.ad.creativeId`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.creativeId": "creative-987"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
