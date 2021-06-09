---
title: 提供有哪些流媒体实施路径？
description: 了解 Adobe 流媒体实施路径，包括 Adobe Launch。
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 98%

---

# 实施路径 {#implementation-paths}

对于每个实施路径，由于 Streaming Media Analytics 具有独有的 SKU，其定价模型已由基于服务器调用的模型变为基于视频流的模型，因此客户将需要联系他们的销售代表/客户经理来签署新的销售订单。

* **包含 Adobe Media Analytics 扩展的 Adobe Launch**

   Adobe Launch 是 Adobe 推出的下一代标记管理解决方案。Launch 为客户提供了一种简单的方式来部署和管理有助于加强相关客户体验的所有分析、营销和广告标记。要自行构建并维护与 Launch 的集成，您需要使用扩展。扩展是一种 JavaScript、HTML 和 CSS 代码包，用于扩展 Launch UI 和客户端功能。有关更多信息，请参阅 [Experience Platform Launch 用户指南](https://experienceleague.adobe.com/docs/launch/using/overview.html)。

   Adobe Media Analytics (MA) 扩展添加了适用于音频和视频的核心 JavaScript Media SDK (Media 2.x SDK)。此扩展提供了将 `MediaHeartbeat` 跟踪器实例添加到 Launch 网站或项目的功能。

   包含 Media Analytics 扩展的 Adobe Launch 要求您必须满足以下条件：
   * 您必须是 Adobe Experience Cloud 客户。
   * 您必须在网页上部署 Launch 或 DTM 嵌入代码。
   * [Analytics 扩展](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Experience Cloud ID 扩展](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


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
