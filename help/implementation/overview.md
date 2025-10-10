---
title: 实施适用于Adobe Analytics或Customer Journey Analytics的流媒体服务
description: 了解Adobe流媒体服务的实施路径。
uuid: null
feature: Streaming Media
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 65%

---

# 实施适用于Adobe Analytics或Customer Journey Analytics的流媒体服务

可通过多种方法来实施Adobe流媒体服务。 有关本页描述的实施方法所支持的设备和平台的详细比较，请参阅[支持的设备和平台。](/help/getting-started/supported-devices.md)

## Edge 实施方法

我们建议在为所有新Adobe Analytics或Edge客户实施流媒体服务时使用Customer Journey Analytics。

Edge实施方法使用流媒体收集加载项。

* **Media for Edge Network SDK /扩展：**&#x200B;从Web、iOS和Android设备或Roku设备收集数据并将其发送到Edge Network。 然后，数据可以发送到 Customer Journey Analytics 或 Adob&#x200B;e Analytics。

  有关Media for Edge Network SDK /扩展的更多信息，请参阅[使用Edge Network实施流媒体收集](/help/implementation/edge/implementation-edge.md)。

* **Media Edge API：**&#x200B;可自定义为从任何设备或格式（包括移动设备、Web设备和过顶设备）收集数据并将数据发送到Edge Network。 然后，数据可以发送到 Customer Journey Analytics 或 Adob&#x200B;e Analytics。

  有关Media Edge API的更多信息，请参阅[Media Edge API概述](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/)。

![CJA 工作流](assets/streaming-media-edge.png)

## 仅限 Adob&#x200B;e Analytics 的实施方法

建议将上述 Edge 实施方法用于 Customer Journey Analytics 和 Adob&#x200B;e Analytics，特别是对于新的实施。

除了 Edge 实施方法之外，还有其他实施方法。这些实施方法专为与 Adob&#x200B;e Analytics 配合使用而设计。但是，采用以下任何实施方法的现有客户仍然可以通过创建[&#x200B; Analytics 源连接](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html)使数据在 Customer Journey Analytics 中可用。

仅限Adobe Analytics的实施方法使用Adobe Analytics for Streaming Media加载项。

* **带有标签的媒体扩展：**&#x200B;适用于音频和视频的 Adobe Media Analytics 扩展提供了将媒体跟踪器实例添加到启用标签的网站或项目的功能。数据发送到 Adobe Analytics。

  有关安装、配置和实施带有标签的媒体扩展的信息，请参阅[适用于音频和视频的 Adob&#x200B;e Media Analytics (3.x SDK) 扩展概述。](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html)

* **Media SDK：**&#x200B;通过 Media SDK 可测量多种媒体平台，包括网站、手机、联网电视、平板电脑、OTT 设备、机顶盒和游戏机。（有关详细信息，请参阅[支持的设备和平台](/help/getting-started/supported-devices.md)。）

  Media SDK 使用媒体收集 API 进行跟踪。数据发送到 Adobe Analytics。

  有关下载和安装 Media SDK 及扩展的信息，请参阅[获取 Media SDK、使用标记的扩展和 OTT SDK](/help/getting-started/download-sdks.md)。

* **媒体收集 API：**&#x200B;由于可自定义媒体收集 API，因此它们可用于需要自定义跟踪功能的应用程序以及不受 Media SDK 支持的设备。媒体收集 API 使用 RESTful HTTP 调用跟踪音频和视频事件。数据发送到 Adobe Analytics。

  有关使用 Media Collection API 的信息，请参阅[&#x200B; Media Collection API。](media-collection-api/mc-api-overview.md)


![Analytics 工作流](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
