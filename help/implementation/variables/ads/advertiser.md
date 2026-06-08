---
title: 广告商
description: 设置每个广告中介绍的公司或品牌。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 10%

---


# 广告商

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告商**&#x200B;变量的数据收集。 有关相应的报表维度，请参阅[广告商](/help/reporting/dimensions/advertiser.md)。*

>[!ENDSHADEBOX]

广告商变量是广告中展现的公司或品牌（例如，`"Ford"`或`"Coca-Cola"`）。 使用变量可划分广告商的参与度和完成度。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.advertiser` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingDetails.advertiser`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.advertiser` |
| **必需** | 否 |
| **发送条件** | [广告开始](/help/implementation/events/ads/ad-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingDetails`中设置`advertiser`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        advertiser: "Ford"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将广告商作为HashMap参数中的元数据键传递给`trackEvent(AdStart)`。 使用 `MediaConstants.AdMetadataKeys.ADVERTISER`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

将广告商作为HashMap参数中的元数据键传递给`trackEvent(AdStart)`。 使用 `MediaConstants.AdMetadataKeys.ADVERTISER`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.ADVERTISER] = "Ford"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

为`media.adStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingDetails`中设置`advertiser`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "advertiser": "Ford"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingDetails`中包含`advertiser`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

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
          "advertiser": "Ford"
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

使用`ADB.Media.AdMetadataKeys.Advertiser`在`contextData`对象中传递广告商：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.Advertiser] = "Ford";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

在标准广告元数据对象中使用`ADBMobile.media.AdMetadataKeys.ADVERTISER`设置广告商：

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.ADVERTISER] = "Sample advertiser";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

在标准广告元数据对象中使用`MEDIA_AdMetadataKeyADVERTISER`设置广告商：

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyADVERTISER] = "Sample advertiser"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.ad.advertiser`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.advertiser": "Ford"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md)。

>[!ENDTABS]
