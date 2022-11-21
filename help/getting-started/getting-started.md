---
title: 快速入门
description: 开始使用适用于流媒体的Adobe Analytics。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 快速入门 {#getting-started}

Adobe Analytics for Streaming Media提供了两种主要实施方法，即Media SDK和媒体收集API。

![方法](assets/getting-started2.png)

使用 **Media SDK**，您可以准确测量多个媒体平台，包括网站、移动电话、连接的电视、平板电脑、OTT设备、机顶盒和游戏机。 您甚至可以测量下载的内容。 您深入了解用户查看参与度的洞察信息，以便您了解查看者参与的时间、时间和位置。 Media SDK使用 **媒体收集API** 进行跟踪。 媒体收集API是可自定义的 — 如果您的应用程序需要自定义跟踪功能。 对于Media SDK不支持的设备，您可以使用媒体收集API。

Adobe Analytics流媒体解决方案针对以下媒体平台提供：

* Web
* 移动
* 过顶
* 可用于流媒体或服务器到服务器集成的任何连接设备

有关更多信息，请参阅 [支持的设备和平台](#_Supported_devices_and).

>[!IMPORTANT]
>
>要实施Adobe Analytics流媒体，请联系您的Adobe销售代表或客户经理，以确保流媒体是您的产品组合的一部分。

## 适用于流媒体的Media SDK {#media-sdks}

适用于流媒体的媒体SDK适用于JavaScript、Android、iOS、tvOS、Chromecast和Roku平台。

有关下载和安装Media SDK的信息，请参阅 [获取Media SDK、使用标记的扩展以及OTT SDK](/help/getting-started/download-sdks.md).


## 媒体收集API {#media-collection-apis}

的 **媒体收集API** 允许您自定义media analytics实施。 使用媒体收集API直接调用Adobe的服务器，以执行几乎任何您可以使用SDK执行的操作等。 自定义您的数据收集，以创建可探索、获得洞察或回答有关流媒体数据的重要问题的报表。

有关使用媒体收集API的信息，请参阅 [流媒体API文档](/help/implementation/media-collection-api/mc-api-overview.md).

## Adobe 扩展 {#adobe-extensions}

* 的 [**Adobe MediumAnalytics for Audio and Video扩展**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) （Media Analytics扩展），是iOS和tvOS实施的必需项。 它提供了将跟踪器实例添加到标记站点或项目的功能。 MA扩展还需要使用Analytics扩展和Experience CloudID扩展。

* [Analytics扩展v1.6或更高版本](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en) — 此扩展允许您加载Adobe Experience Platform Web SDK Javascript库，以将数据发送到Adobe解决方案。

* [Experience CloudID扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en) — 此扩展实施了Experience CloudID服务，在所有Experience Cloud解决方案中标识访客。 Experience CloudID服务是Adobe Experience Platform中的一个个性化扩展。
