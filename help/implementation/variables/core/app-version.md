---
title: 应用程序版本
description: 配置媒体播放器应用程序的版本字符串。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# 应用程序版本

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**应用程序版本**变量的数据收集。 有关相应的报表维度，请参阅[应用程序版本](/help/reporting/dimensions/app-version.md)。*

>[!ENDSHADEBOX]

应用程序版本变量可标识媒体播放器应用程序的版本。 在SDK初始化期间设置一次；该值自动包含在每个后续会话开始请求中。 使用与应用程序的发行周期匹配的版本字符串（例如，`"2.1.0"`或`"prod-YYYY-03-15"`）。

>[!NOTE]
>
>此字段捕获&#x200B;**媒体播放器应用程序**&#x200B;的版本，而不是Adobe的SDK库。 Adobe自己的SDK库版本将作为单独的内部字段自动收集。

| 属性 | 值 |
| --- | --- |
| **XDM集合字段** | [`xdm.mediaCollection.sessionDetails.appVersion`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **媒体收集API参数** | `media.sdkVersion` |
| **必需** | 否 |
| **发送条件** | [会话开始](/help/implementation/events/session/session-start.md) |

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

调用[`configure`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia)时，在`streamingMedia`配置对象中设置`appVersion`：

```javascript
alloy("configure", {
  streamingMedia: {
    channel: "Sports Channel",
    playerName: "HTML5 Player",
    appVersion: "2.1.0",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

>[!TAB iOS]

在初始化媒体跟踪器之前，在应用程序配置中设置`edgeMedia.appVersion`：

```swift
var config: [String: Any] = [:]
config["edgeMedia.channel"] = "sample_channel"
config["edgeMedia.playerName"] = "player_name"
config["edgeMedia.appVersion"] = "2.1.0"
MobileCore.updateConfiguration(config)
```

>[!TAB Android]

在初始化媒体跟踪器之前，在应用程序配置中设置`edgeMedia.appVersion`：

```kotlin
val config: Map<String, Any> = mapOf(
    "edgeMedia.channel" to "sample_channel",
    "edgeMedia.playerName" to "player_name",
    "edgeMedia.appVersion" to "2.1.0"
)
MobileCore.updateConfiguration(config)
```

>[!TAB Roku]

使用`ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION`在SDK配置中设置应用程序版本：

```brightscript
ADB_CONSTANTS = AdobeAEPSDKConstants()
configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<YOUR_CONFIG_ID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "channel_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_APP_VERSION] = "2.1.0"
m.aepSdk.updateConfiguration(configuration)
```

>[!TAB Media Edge API]

在[sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart)请求的`sessionDetails`对象中包括`appVersion`：

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "appVersion": "2.1.0"
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

在调用`ADB.Media.configure`之前对`MediaConfig`对象设置`appVersion`：

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "2.1.0";
ADB.Media.configure(mediaConfig, appMeasurement);
```

>[!TAB Chromecast]

在ADBMobile配置的`mediaHeartbeat`部分中设置`sdkVersion`。 此字段会捕获您的播放器应用程序版本，而不是Chromecast SDK库版本。

```javascript
var ADBMobileConfig = {
  "mediaHeartbeat": {
    "server": "obumobile5.hb-api.omtrdc.net",
    "publisher": "<YOUR_PUBLISHER_ID>@AdobeOrg",
    "channel": "sample-channel",
    "ssl": true,
    "playerName": "Chromecast Player",
    "sdkVersion": "2.1.0"
  }
};
```

>[!TAB 媒体收集API]

在`sessionStart` POST请求的`params`对象中包括`media.sdkVersion`：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.playerName": "sample-html5-api-player",
    "media.sdkVersion": "2.1.0",
    "media.channel": "sample-channel"
  }
}
```

有关完整请求结构，请参阅[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)。

>[!ENDTABS]
