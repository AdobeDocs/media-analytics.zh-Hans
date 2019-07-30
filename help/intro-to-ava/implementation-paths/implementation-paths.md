---
seo-title: 实施路径
title: 实施路径
uuid: 8400c938-e77 e-4c88 b23 b-5977a5316 c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 实施路径 {#implementation-paths}

Media Analytics(HeartBeats)是Adobe的标准化视频解决方案。它取代了 Adobe 的旧式里程碑模型。

对于每个实施路径，客户需要联系销售代表/客户经理以签署新的销售订单，因为媒体分析具有独特的SKU和基于视频流的模型调用基于服务器调用的定价模式：

* **客户端-** 这些是仅限Media Analytics的集成。您可以选择视频心率 SDK 和/或媒体收集 API 集成。此路径可在任何视频播放器中使用，包括客户和/或 OVP 的播放器，例如 Brightcove、Ooyala 和 thePlatform 等等。

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >要使用Media Analytics，客户还必须使用Adobe Analytics。

* **Adobe Experience Platform Launch-** Adobe Experience Platform Launch是Dynamic Tag Management的后续产品，它提供了Media Analytics Launch Extension，可帮助您在播放器中实现视频跟踪。

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime-** Adobe Primetime是Adobe Experience Cloud解决方案，可帮助内容编排者和分销商在每个连接的屏幕上实现媒体货币化。

   Primetime 为进行视频发布、广告投放、个性化和分析提供了模块化的平台，让客户可以更轻松地在各种各样的设备上联系和吸引全球客户并借以盈利。此外，Primetime 还在以下方面提供了解决方案，并带来了价值：

   * 支持精准地测量线性和 VOD 内容类型。
   * 支持测量含有（或不含）动态广告插入的广告时间。
   * TVSDK 的无缝广告插入模型允许分析工具直接测量广告播放，提高了准确性。
   * 利用强大的事件和元数据集，可确保在出现各种 QoS 缓冲或移动连接中断问题以及最终用户在移动设备上进行搜寻、暂停或后台播放时，测量数据仍然准确。
   * 利用 ID3 元数据集成 Nielsen DTVR（线性）支持，利用 CMS 元数据集成 DCR 支持。
   TVSDK已经与Media Publishics(Heartbeats) SDK集成，这使得跨每个支持的平台实现更简单、更快速的实施变得更加简单快捷。Primetime 还支持与 Nielsen 的合作。为充分利用 Primetime，请遵循[客户端](/help/intro-to-ava/implementation-paths/client-side-path.md)中所述的指南和先决条件以及针对相应平台的以下文档：[Primetime用户指南。](https://helpx.adobe.com/primetime/user-guide.html)

   您还应该与您的销售代表/客户经理联系，了解购买 TVSDK 所需的条件。
