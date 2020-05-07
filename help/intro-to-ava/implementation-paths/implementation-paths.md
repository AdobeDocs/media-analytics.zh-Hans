---
title: 实施路径
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 实施路径 {#implementation-paths}

Media Analytics (Heartbeats) 是 Adobe 的标准化视频解决方案。它取代了 Adobe 的旧式里程碑模型。

对于以下每种实施路径，由于 Media Analytics 具有独有的 SKU，其定价模型已由基于服务器调用的模型变为基于视频流的模型，因此客户将需要联系他们的销售代表/客户经理来签署新的销售订单：

* **客户端 -** 这些是仅限 Media Analytics 的集成。您可以选择视频心率 SDK 和/或媒体收集 API 集成。此路径可以跨任何播放器使用，包括客户和/或 OVP 播放器，如 Brightcove、Ooyala、thePlatform 等。

   如果 Media Analytics 是您的预期路径，请参阅 [Media SDK 实施](/help/sdk-implement/setup/setup-overview.md)和[媒体收集 API](/help/media-collection-api/mc-api-overview.md)。

   >[!IMPORTANT]
   >
   >要使用 Media Analytics，客户还必须使用 Adobe Analytics。

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch 是 Dynamic Tag Management 的后续产品，具有 Media Analytics Launch 扩展功能，可帮助您在播放器中实施视频跟踪。

   您可以在此处了解有关 Experience Platform Launch 的更多信息：[Adobe Media Analytics for Audio and Video 扩展](https://docs.adobe.com/content/help/zh-Hans/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.translate.html)
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
