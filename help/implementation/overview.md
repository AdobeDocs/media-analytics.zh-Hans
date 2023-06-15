---
title: 实施Streaming Media for Adobe Analytics或Customer Journey Analytics
description: 了解有关流媒体实施路径的信息。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: ade20d7ae3cbb525b3a8390a27e1d93201d83003
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 实施 Streaming Media for Adobe Analytics 或Customer Journey Analytics

可通过多种方法来实施流媒体。 有关本页中介绍的实施方法支持的设备和平台的详细比较，请参阅 [支持的设备和平台](/help/getting-started/supported-devices.md).

## 边缘实施方法

在大多数情况下，我们建议为所有新的Adobe Analytics或Customer Journey Analytics (CJA)客户实施Media Analytics时使用Edge。

* **Media for Edge Network SDK/扩展：** 从iOS和Android设备收集数据并将其发送给Edge。 然后，可以将数据发送到CJA或Adobe Analytics。

  有关Media for Edge Network SDK/扩展的更多信息，请参阅 [安装Media Analytics和Experience Platform边缘](/help/implementation/implementation-edge.md).

  >[!NOTE]
  >
  >此实施方法当前不支持Web SDK或Roku。 但是，在使用Media Edge API实施时，这两种方法都受支持。

* **Media Edge API：** 可以自定义以从任何设备或格式（包括移动设备、Web设备和过顶设备）收集数据，并将数据发送到Edge。 然后，可以将数据发送到CJA或Adobe Analytics。

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![CJA 工作流](assets/cja-implementation.png)

## 其他实施方法

在大多数情况下，建议将上述边缘实施方法用于CJA和Adobe Analytics，尤其是新实施。

除了Edge实施方法之外，还可以使用其他实施方法。 这些实施方法最初旨在与Adobe Analytics结合使用。 但是，具有以下任何实施方法的客户仍然可以通过创建 [Analytics源连接](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=zh-Hans).

* **带有标记的Media扩展：** Adobe Medium Analytics for Audio and Video扩展提供了将媒体跟踪器实例添加到启用了标记的网站或项目的功能。 数据会发送到Adobe Analytics。

  有关安装、配置和实施带标记的媒体扩展的信息，请参阅 [Adobe Medium Analytics (3.x SDK) for Audio and Video扩展概述](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics-3x/overview.html).

* **Media SDK：**  数据会发送到Adobe Analytics。

  有关下载和安装 Media SDK 及扩展的信息，请参阅[获取 Media SDK、使用标记的扩展和 OTT SDK](/help/getting-started/download-sdks.md)。

* **媒体收集API：** 使用RESTful HTTP调用跟踪音频和视频事件。 数据会发送到Adobe Analytics。

  有关使用媒体收集 API 的信息，请参阅[媒体收集 API](media-collection-api/mc-api-overview.md)。


![Analytics工作流](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
