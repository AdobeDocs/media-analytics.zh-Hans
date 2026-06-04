---
title: 设置适用于流媒体的Roku
description: 配置Adobe Experience Platform Roku SDK以将流媒体数据发送到Edge Network。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 设置适用于流媒体的Roku

[Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku) (BrightScript)在Roku渠道中收集媒体会话数据并将其发送到Edge Network。 Roku是在代码中配置的；它不使用标记。

* **先决条件**：
   * 完成[Edge实施概述](overview.md)（架构、数据集、启用了[!UICONTROL Media Analytics]的数据流）。
   * 从[GitHub版本](https://github.com/adobe/aepsdk-roku/releases)下载SDK并将其添加到您的渠道中，如[快速入门指南](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/getting-started.md)中所述。

## 配置适用于媒体的AEP Roku SDK

初始化SDK并设置数据流和媒体配置：

```brightscript
m.aepSdk = AdobeAEPSDKInit()
ADB_CONSTANTS = AdobeAEPSDKConstants()

configuration = {}
configuration[ADB_CONSTANTS.CONFIGURATION.EDGE_CONFIG_ID] = "<datastreamID>"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_CHANNEL] = "sample_channel"
configuration[ADB_CONSTANTS.CONFIGURATION.MEDIA_PLAYER_NAME] = "player_name"
m.aepSdk.updateConfiguration(configuration)
```

然后打开与`createMediaSession`的会话：

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": { "name": "video-123", "length": 128, "contentType": "vod", "streamType": "video" },
            "playhead": 0
        }
    }
})
```

>[!IMPORTANT]
>
>在播放期间，使用最新的播放头值至少每秒发送一次`media.ping`事件。 AEP Roku SDK依赖这些Ping才能正常运行。

有关配置密钥和完整API的信息，请参阅[AEP Roku SDK API参考](https://github.com/adobe/aepsdk-roku/blob/main/Documentation/api-reference.md)。

## 跟踪媒体事件

会话打开后，使用`sendMediaEvent`发送每个媒体事件。 有关确切负载，请参阅每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Roku**&#x200B;选项卡。

## 下一步

实施完成后，您可以[为Edge实施设置报表](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku)
>* [事件概述](/help/implementation/events/overview.md)
>* [变量概述](/help/implementation/variables/overview.md)
