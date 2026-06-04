---
title: 设置适用于流媒体的Android
description: 在Android上配置Adobe Experience Platform Mobile SDK以将流媒体数据发送到Edge Network。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 设置适用于流媒体的Android

Adobe Streaming Media for Edge Network扩展(`EdgeMedia`)收集Android应用程序中的媒体会话数据，并将其发送到Edge Network。 本页介绍代码内配置。 要改为通过Tags移动属性配置SDK，请参阅[为带有标记的Android设置](android-tags.md)。

* **先决条件**：
   * 完成[Edge实施概述](overview.md)（架构、数据集、启用了[!UICONTROL Media Analytics]的数据流）。
   * 将`Core`、`Edge`、`EdgeIdentity`和`EdgeMedia`扩展添加到您的应用程序中。 有关安装和注册，请参阅[Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)。

## 为Android配置媒体

在初始化SDK时设置媒体配置键：

```kotlin
val configuration = mapOf(
  "edgeMedia.channel" to "sample_channel",
  "edgeMedia.playerName" to "player_name",
  "edgeMedia.appVersion" to "app_version"
)
MobileCore.updateConfiguration(configuration)
```

然后，创建一个跟踪器来管理媒体会话：

```kotlin
val tracker = Media.createTracker()
```

有关配置密钥和完整的跟踪器API，请参阅[适用于Edge Network API的媒体](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/api-reference/)。

## 跟踪媒体事件

在创建跟踪器后，使用其跟踪器方法跟踪每个媒体事件。 查看每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Android**&#x200B;选项卡，了解确切的调用。

## 下一步

实施完成后，您可以[为Edge实施设置报表](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [适用于Edge Network的Adobe流媒体](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [为带有标记的流媒体设置Android](android-tags.md)
>* [事件概述](/help/implementation/events/overview.md)
