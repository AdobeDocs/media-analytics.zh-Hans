---
title: 实施路径
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 64%

---


# 实施路径 {#implementation-paths}

对于每个实施路径，客户需要联系其销售代表／客户经理以签署新的销售订单，因为媒体分析具有唯一的SKU，并且从基于服务器调用的定价模型更改为基于视频流的模型。

* **带有Adobe Media Analytics扩展的Adobe Launch**

   Adobe Launch是Adobe的新一代标签管理解决方案。 Launch提供了部署和管理所有分析、营销和广告标签的简单方法，这些标签是提升相关客户体验所必需的。 要构建和维护您与Launch的集成，您需要使用扩展。 扩展是JavaScript、HTML和CSS包，它扩展了Launch UI和客户端功能。 有关详细信息，请参 [阅《Experience Platform Launch用户指南》](https://docs.adobe.com/content/help/zh-Hans/launch/using/overview.translate.html)

   Adobe Media Analytics(MA)扩展为音频和视频添加核心JavaScript Media SDK(Media 2.x SDK)。 此扩展提供了将 `MediaHeartbeat` 跟踪器实例添加到 Launch 网站或项目的功能。

   带有Media Analytics扩展的Adobe Launch需要：
   * 您必须是Adobe Experience Cloud客户。
   * 必须在网页上部署启动或DTM嵌入代码。
   * [Analytics 扩展](https://docs.adobe.com/content/help/zh-Hans/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID 扩展](https://docs.adobe.com/content/help/zh-Hans/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


* **客户端 -** 这些是仅限 Media Analytics 的集成。您可以选择视频心率 SDK 和/或媒体收集 API 集成。此路径可以跨任何播放器使用，包括客户和/或 OVP 播放器，如 Brightcove、Ooyala、thePlatform 等。

   如果 Media Analytics 是您的预期路径，请参阅 [Media SDK 实施](/help/sdk-implement/setup/setup-overview.md)和[媒体收集 API](/help/media-collection-api/mc-api-overview.md)。

   >[!IMPORTANT]
   >
   >要使用 Media Analytics，客户还必须使用 Adobe Analytics。

* **Adobe Primetime -** Adobe Primetime 是一款 Adobe Experience Cloud 解决方案，可帮助内容程序员和发行商从每一个连接屏幕上的媒体中盈利。

   Primetime 通过提供用于视频发布、广告、个性化和分析的模块化平台，消除了跨设备吸引、货币化和激活全球受众的复杂性。此外，Primetime 还提供以下解决方案和值：

   * 支持精确测量线性和 VOD 内容类型。
   * 支持在包含（或不含）动态广告插入时测量广告时间。
   * TVSDK 的无缝广告插入模型允许 Analytics 直接测量广告播放，从而提高准确性。
   * 可靠的事件和元数据集可确保跨 QoS 缓冲或移动连接中断问题和最终用户交互（如搜索、暂停和后台）之间的准确性。
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK 已与 Media Analtyics (Heartbeats) SDK 集成，这使得在所有受支持的平台上都可以更便捷地实施 TVSDK。<!--Primetime also supports the partnership with Nielsen.-->要利用 Primetime，请遵循[客户端](/help/intro-to-ava/implementation-paths/client-side-path.md)中提供的相同准则和先决条件，以及以下适用于您的平台的文档：[Primetime 用户指南](https://helpx.adobe.com/cn/primetime/user-guide.html)。

您还应该与您的销售代表/客户经理联系，了解购买 TVSDK 所需的条件。
