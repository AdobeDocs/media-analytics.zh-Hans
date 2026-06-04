---
title: 实施适用于Adobe Analytics或Customer Journey Analytics的流媒体服务
description: 了解Adobe流媒体服务的实施路径。
uuid: null
feature: Streaming Media
role: User, Admin, Developer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
TQID: https://experienceleague.adobe.com/aFrxbzBLlf1ngetaM-GsNFXz6TUXi6Pic3quLVI297c
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 518
ht-degree: 66%

---

# 实施适用于Adobe Analytics或Customer Journey Analytics的流媒体服务

可通过多种方法来实施Adobe流媒体服务。 有关本页描述的实施方法所支持的设备和平台的详细比较，请参阅[支持的设备和平台。](/help/getting-started/supported-devices.md)

## Edge 实施方法

Adobe建议对所有新的Adobe Analytics或Customer Journey Analytics客户使用Edge Network实施方法。

* **Media for Edge Network SDK /扩展：**&#x200B;从Web、iOS和Android设备或Roku设备收集数据并将其发送到Edge Network。 然后，数据可以发送到 Customer Journey Analytics 或 Adob&#x200B;e Analytics。

  有关Media for Edge Network SDK /扩展的更多信息，请参阅[Edge实施概述](/help/implementation/edge/overview.md)。

* **Media Edge API：**&#x200B;可自定义为从任何设备或格式（包括移动设备、Web设备和过顶设备）收集数据并将数据发送到Edge Network。 然后，数据可以发送到 Customer Journey Analytics 或 Adob&#x200B;e Analytics。

  有关Media Edge API的更多信息，请参阅[Media Edge API概述](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/)。

![CJA 工作流](assets/streaming-media-edge.png)

## 仅限 Adob&#x200B;e Analytics 的实施方法

建议将上述 Edge 实施方法用于 Customer Journey Analytics 和 Adob&#x200B;e Analytics，特别是对于新的实施。

除了 Edge 实施方法之外，还有其他实施方法。 这些实施方法专为与 Adob&#x200B;e Analytics 配合使用而设计。 但是，采用以下任何实施方法的现有客户仍然可以通过创建[ Analytics 源连接](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html)使数据在 Customer Journey Analytics 中可用。

仅限Adobe Analytics的实施方法使用Adobe Analytics for Streaming Media加载项。 有关先决条件和方法的列表，请参阅[仅限Analytics的实施概述](/help/implementation/analytics-only/overview.md)。

* **带有标签的媒体扩展：**&#x200B;适用于音频和视频的 Adobe Media Analytics 扩展提供了将媒体跟踪器实例添加到启用标签的网站或项目的功能。 数据发送到 Adobe Analytics。

  有关安装、配置和实施带有标签的媒体扩展的信息，请参阅[适用于音频和视频的 Adob&#x200B;e Media Analytics (3.x SDK) 扩展概述。](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html)

* **Media SDK：**&#x200B;通过 Media SDK 可测量多种媒体平台，包括网站、手机、联网电视、平板电脑、OTT 设备、机顶盒和游戏机。 （有关详细信息，请参阅[支持的设备和平台](/help/getting-started/supported-devices.md)。）

  Media SDK 使用媒体收集 API 进行跟踪。 数据发送到 Adobe Analytics。

  有关下载和安装 Media SDK 及扩展的信息，请参阅[获取 Media SDK、使用标记的扩展和 OTT SDK](/help/getting-started/download-sdks.md)。

* **媒体收集 API：**&#x200B;由于可自定义媒体收集 API，因此它们可用于需要自定义跟踪功能的应用程序以及不受 Media SDK 支持的设备。 媒体收集 API 使用 RESTful HTTP 调用跟踪音频和视频事件。 数据发送到 Adobe Analytics。

  有关使用 Media Collection API 的信息，请参阅[ Media Collection API。](media-collection-api/mc-api-overview.md)


![Analytics 工作流](assets/analytics-implementation.png)
