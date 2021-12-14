---
title: 提供有哪些流媒体实施路径？
description: 了解Adobe流媒体实施路径，包括Adobe Experience Platform数据收集。
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f88e8b02bc9723793822fa7647a2ceab9ada45e6
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 68%

---

# 实施路径 {#implementation-paths}

对于每个实施路径，由于 Streaming Media Analytics 具有独有的 SKU，其定价模型已由基于服务器调用的模型变为基于视频流的模型，因此客户将需要联系他们的销售代表/客户经理来签署新的销售订单。

## Adobe Experience Platform使用Adobe Medium分析扩展收集数据

>[!NOTE]
>Adobe Experience Platform Launch 已更名为 Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=zh-Hans)。


Adobe Experience Platform中的标记是Adobe推出的新一代标签管理功能。 标记为客户提供了一种简单的方式来部署和管理所有用来改善相关客户体验的分析、营销和广告标记。 标记作为随附的增值功能提供给Adobe Experience Cloud客户。

标记可让任何人自行构建并维护与自己相关的集成，这称为扩展。 Adobe Experience Cloud客户可在应用商店中获取这些扩展，以便能够快速安装、配置和部署其标记。

扩展是用于扩展标记功能的代码包(JavaScript、HTML和CSS)。 使用几乎自助的界面构建、管理和更新您的集成。您可以将扩展视为用于完成任务的应用程序。有关详细信息，请参阅 *标记概述* 文章(位于 [Adobe Experience Platform文档](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans)

Adobe Media Analytics (MA) 扩展添加了适用于音频和视频的核心 JavaScript Media SDK (Media 2.x SDK)。此扩展提供了用于添加 `MediaHeartbeat` 跟踪器实例添加到数据收集网站或项目。

使用Media Analytics扩展Adobe数据收集需要满足以下条件：
* 您必须是 Adobe Experience Cloud 客户。
* 您必须在网页上部署数据收集或DTM嵌入代码。
* [Analytics 扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=zh-Hans)
* [Experience Cloud ID 扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=zh-Hans)


## 客户端

这些是仅限Media Analytics的集成。 您可以选择视频心率 SDK 和/或媒体收集 API 集成。此路径可以跨任何播放器使用，包括客户和/或 OVP 播放器，如 Brightcove、Ooyala、thePlatform 等。

如果 Media Analytics 是您的预期路径，请参阅 [Media SDK 实施](/help/sdk-implement/setup/setup-overview.md)和[媒体收集 API](/help/media-collection-api/mc-api-overview.md)。

>[!IMPORTANT]
>要使用 Media Analytics，客户还必须使用 Adobe Analytics。

## Adobe Primetime

Adobe Primetime 是一款 Adobe Experience Cloud 解决方案，可帮助内容程序员和发行商从每一个连接屏幕上的媒体中盈利。

Primetime 通过提供用于视频发布、广告、个性化和分析的模块化平台，消除了跨设备吸引、货币化和激活全球受众的复杂性。此外，Primetime 还提供以下解决方案和值：

* 支持精确测量线性和 VOD 内容类型。
* 支持在包含（或不含）动态广告插入时测量广告时间。
* TVSDK 的无缝广告插入模型允许 Analytics 直接测量广告播放，从而提高准确性。
* 可靠的事件和元数据集可确保跨 QoS 缓冲或移动连接中断问题和最终用户交互（如搜索、暂停和后台）之间的准确性。
* 利用 ID3 元数据集成 Nielsen DTVR（线性）支持，利用 CMS 元数据集成 DCR 支持。


TVSDK 已与 Media Analtyics (Heartbeats) SDK 集成，这使得在所有受支持的平台上都可以更便捷地实施 TVSDK。要利用 Primetime，请遵循[客户端](/help/intro-to-ava/implementation-paths/client-side-path.md)中提供的相同准则和先决条件，以及以下适用于您的平台的文档：[《Primetime 用户指南》](https://helpx.adobe.com/cn/primetime/user-guide.html)。

您还应该与您的销售代表/客户经理联系，了解购买 TVSDK 所需的条件。
