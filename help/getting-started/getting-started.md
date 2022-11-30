---
title: 快速入门
description: Adobe Analytics for Streaming Media 快速入门。
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# 快速入门 {#getting-started}

Adobe Analytics for Streaming Media 提供两种主要的实施方法，媒体 SDK 和媒体收集 API。

![方法](assets/getting-started2.png)

使用&#x200B;**媒体 SDK** 的内置逻辑，即可准确地测量多种媒体平台，包括网站、手机、联网电视、平板电脑、OTT 设备、机顶盒和游戏机。甚至还可测量下载的内容。您获得的洞察深入到用户观看参与度，因此您可以了解观众参与的时长、时间和地点。媒体 SDK 使用&#x200B;**媒体收集 API** 进行跟踪。如果您的应用程序需要自定义跟踪功能，可自定义媒体收集 API。对于媒体 SDK 不支持的设备，您可以使用媒体收集 API。

为以下媒体平台提供了 Adobe Analytics Streaming Media 解决方案：

* Web
* 移动
* 过顶
* 任何可用于流媒体或服务器到服务器集成的联网设备

有关详细信息，请参阅[支持的设备和平台](#_Supported_devices_and)。

>[!IMPORTANT]
>
>要实施 Adobe Analytics Streaming Media，请联系您的 Adobe 销售代表或客户经理以确您的产品组合包含流媒体。

## 适用于流媒体的媒体 SDK {#media-sdks}

为 JavaScript、Android、iOS、tvOS、Chromecast 和 Roku 平台提供适用于流媒体的媒体 SDK。

有关下载和安装媒体 SDK 的信息，请参阅[获取媒体 SDK、使用标记的扩展和 OTT SDK](/help/getting-started/download-sdks.md)。


## 媒体收集 API {#media-collection-apis}

通过&#x200B;**媒体收集 API**，可自定义您的媒体分析实施。使用媒体收集 API 直接调用 Adobe 的服务器以执行您可使用 SDK 执行的几乎任何操作。自定义您的数据收藏集以创建报表，这些报表探索您的流媒体数据、获取关于您的流媒体数据的见解或回答关于您的流媒体数据的重要问题。

有关使用媒体收集 API 的信息，请参阅[流媒体 API 文档 ](/help/implementation/media-collection-api/mc-api-overview.md)。

## Adobe 扩展 {#adobe-extensions}

* iOS 和 tvOS 实施需要 [**Adobe Media Analytics for Audio and Video 扩展**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=zh-Hans)（Media Analytics 扩展）。它提供将跟踪器实例添加到标记网站或项目的功能。MA 扩展还需要 Analytics 扩展和 Experience Cloud ID 扩展。

* [Analytics 扩展 v1.6 或更高版本](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=zh-Hans) - 通过此扩展，可加载 Adobe Experience Platform Web SDK Javascript 库以将数据发送到 Adobe 解决方案。

* [Experience Cloud ID 扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=zh-Hans) - 此扩展实施 Experience Cloud ID 服务，该服务在所有 Experience Cloud 解决方案间标识访客。Experience Cloud ID 服务是 Adobe Experience Platform 中的个性化扩展。
