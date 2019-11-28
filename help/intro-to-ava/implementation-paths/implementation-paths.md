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

* **客户端 -** 这些是仅限 Media Analytics 的集成。您可以选择视频心率 SDK 和/或媒体收集 API 集成。此路径可在任何视频播放器中使用，包括客户和/或 OVP 的播放器，例如 Brightcove、Ooyala 和 thePlatform 等等。

   如果 Media Analytics 是您的预期路径，请参阅 [Media SDK 实施](/help/sdk-implement/setup/setup-overview.md)和[媒体收集 API](/help/media-collection-api/mc-api-overview.md)。

   >[!IMPORTANT]
   >
   >要使用 Media Analytics，客户还必须使用 Adobe Analytics。

* **Adobe Experience Platform Launch -** Adobe Experience Platform Launch 是 Dynamic Tag Management 的后续产品，具有 Media Analytics Launch 扩展功能，可帮助您在播放器中实施视频跟踪。

   您可以在此处了解有关 Experience Platform Launch 的更多信息：[Adobe Media Analytics for Audio and Video 扩展](https://docs.adobe.com/content/help/zh-Hans/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.translate.html)
* **Adobe Primetime -** Adobe Primetime 是一款 Adobe Experience Cloud 解决方案，可帮助内容程序员和发行商从每一个连接屏幕上的媒体中盈利。

   Primetime 为进行视频发布、广告投放、个性化和分析提供了模块化的平台，让客户可以更轻松地在各种各样的设备上联系和吸引全球客户并借以盈利。此外，Primetime 还在以下方面提供了解决方案，并带来了价值：

   * 支持精准地测量线性和 VOD 内容类型。
   * 支持测量含有（或不含）动态广告插入的广告时间。
   * TVSDK 的无缝广告插入模型允许分析工具直接测量广告播放，提高了准确性。
   * 利用强大的事件和元数据集，可确保在出现各种 QoS 缓冲或移动连接中断问题以及最终用户在移动设备上进行搜寻、暂停或后台播放时，测量数据仍然准确。
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK 已与 Media Analtyics (Heartbeats) SDK 集成，这使得在所有受支持的平台上都可以更便捷地实施 TVSDK。<!--Primetime also supports the partnership with Nielsen.-->要利用 Primetime，请遵循[客户端](/help/intro-to-ava/implementation-paths/client-side-path.md)中提供的相同准则和先决条件，以及以下适用于您的平台的文档：[Primetime 用户指南](https://helpx.adobe.com/cn/primetime/user-guide.html)。

您还应该与您的销售代表/客户经理联系，了解购买 TVSDK 所需的条件。
