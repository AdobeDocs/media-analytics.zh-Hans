---
title: 营销活动 ID
description: 设置每个广告的促销活动标识符，以便按促销活动汇总参与度。
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
source-wordcount: '256'
ht-degree: 9%
---

# 营销活动 ID

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**促销活动ID**&#x200B;变量的数据收集。 查看相应报表维度的[促销活动ID](/help/reporting/dimensions/campaign-id.md)。*

>[!ENDSHADEBOX]

促销活动ID变量可识别创意所属的广告促销活动。 可接受任何字符串值（通常是广告服务器平台中的促销活动ID）。 使用变量可在共享营销策划的多个创意中汇总参与度。

| 属性 | 值 |
| --- | --- |
| **上下文数据变量** | `a.media.ad.campaign` |
| **XDM集合字段** | [`xdm.mediaCollection.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-collection) |
| **Audience Manager特征** | `c_contextdata.a.media.ad.campaign` |
| **必需** | 否 |
| **发送条件** | [广告开始](/help/implementation/events/ads/ad-start.md)，广告关闭 |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)时，在`xdm.mediaCollection.advertisingDetails`中设置`campaignID`：

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adStart",
    mediaCollection: {
      advertisingDetails: {
        name: "ad-2125",
        campaignID: "fall-2024"
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

将促销活动ID作为哈希映射参数中的元数据键传递给`trackEvent(AdStart)`。 使用 `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`。

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(event: MediaEvent.AdStart, info: adObject, metadata: metadata)
```

>[!TAB Android]

将促销活动ID作为哈希映射参数中的元数据键传递给`trackEvent(AdStart)`。 使用 `MediaConstants.AdMetadataKeys.CAMPAIGN_ID`。

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024"

tracker.trackEvent(Media.Event.AdStart, adObject, metadata)
```

>[!TAB Roku Edge]

为`media.adStart`调用`sendMediaEvent`时，在`xdm.mediaCollection.advertisingDetails`中设置`campaignID`：

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adStart",
        "mediaCollection": {
            "advertisingDetails": {
                "name": "ad-2125",
                "campaignID": "fall-2024"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB Media Edge API]

调用`xdm.mediaCollection.advertisingDetails`中包含`campaignID`的[adStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adstart)终结点：

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
          "campaignID": "fall-2024"
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

使用`ADB.Media.AdMetadataKeys.CampaignId`在`contextData`对象中传递营销活动ID：

```javascript
var contextData = {};
contextData[ADB.Media.AdMetadataKeys.CampaignId] = "fall-2024";

tracker.trackEvent(ADB.Media.Event.AdStart, adInfo, contextData);
```

>[!TAB Chromecast]

使用标准广告元数据对象中的`ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID`设置促销活动ID：

```javascript
var adInfo = ADBMobile.media.createAdObject("Ford F-150", "ad-2125", 1, 30);
var standardAdMetadata = {};
standardAdMetadata[ADBMobile.media.AdMetadataKeys.CAMPAIGN_ID] = "fall-2024";
adInfo[ADBMobile.media.MediaObjectKey.StandardAdMetadata] = standardAdMetadata;
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdStart, adInfo, null);
```

>[!TAB Roku 2.x]

使用标准广告元数据对象中的`MEDIA_AdMetadataKeyCAMPAIGN_ID`设置促销活动ID：

```brightscript
adb = ADBMobile()
adInfo = adb_media_init_adinfo("Ford F-150", "ad-2125", 1, 30.0)

standardAdMetadata = {}
standardAdMetadata[adb.MEDIA_AdMetadataKeyCAMPAIGN_ID] = "fall-2024"
adInfo[adb.MEDIA_STANDARD_AD_METADATA] = standardAdMetadata

adb.mediaTrackEvent(adb.MEDIA_AD_START, adInfo)
```

>[!TAB 媒体收集API]

在`params`对象中包括`media.ad.campaignId`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adStart",
  "params": {
    "media.ad.campaignId": "fall-2024"
  }
}
```

有关完整请求结构，请参阅[媒体收集API事件引用](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events)。

>[!ENDTABS]
