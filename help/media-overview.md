---
title: 在 Adobe Analytics 中测量音频和视频
description: 'Adobe Analytics for Media（也称为 Media Analytics）可为客户提供针对内容、音频和广告的可靠媒体测量。 '
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: ht
source-git-commit: 689b7d4ce632d3ddba6704bb8040eec52bfc326f

---


# 在 Adobe Analytics 中测量音频和视频{#measuring-audio-and-video-in-adobe-analytics}

![横幅](./assets/media_analytics_banner.png)

>[!IMPORTANT]
>
>此处提供的文档专门面向利用 Adobe 的 1.5 或更高版本 *Media SDK* 或者较新的&#x200B;*媒体收集 API* 进行心率测量的客户。该文档不包括有关旧版里程碑视频实施的说明。我们建议所有客户采用其中一种或同时采用这两种最新的媒体跟踪解决方案，以便充分利用改进功能，实现更广泛的测量。您可以阅读下方的[转换到最新解决方案的益处](media-overview.md#heartbeat-versus-milestone-benefits)。尽管我们会继续支持通过里程碑跟踪视频的方法，但将不会有任何计划的更新、修复或功能改进。如果您有任何进一步的问题，请联系您的 Adobe 帐户管理员。

## 概述 {#overview}

Adobe Analytics for Media（也称为 Media Analytics）是 Analytics 基础产品的附加组件，可为客户提供针对内容、音频和广告的可靠媒体测量。Media Analytics 为客户带来诸多益处，允许客户进行实时监测、详细分析、可操作分析及盈利商机挖掘。

可通过以下任一方法启用媒体跟踪：

* **Media SDK -**&#x200B;与最常用的媒体播放器集成。
* **媒体收集 API -**(RESTful API) 与没有 SDK 支持的播放器集成（或与不需要 SDK 集成的播放器集成）。

Adobe Analytics for Media 让用户可以跟踪客户在其网站中的整个活动历程（包括媒体使用情况），这些测量可以轻松地集成到 Analytics 报表及其他 Experience Cloud 产品中。媒体测量允许您将数据划分为多个维度和区段，捕获进行全面详尽的分析所需的全部元数据，并且还允许您将成功标准归因于完整使用媒体、平均逗留时间和完整播放广告。

媒体解决方案不仅可以测量与 QoS 相关的重要交付量度，例如丢帧、缓冲花费时间和平均比特率，而且还可以与您的网站或应用程序数据相结合，使客户的流量和兴趣可视化，从而让您能够通过 Adobe Experience Cloud 更有效地推荐内容，并提供个性化的客户体验。

## 优点 {#benefits}

Adobe 媒体测量解决方案的部分优点包括：

* **及时分析 -**&#x200B;利用跨多个渠道的关键效果量度（例如，持续时间）做出实时的可操作性决策。以 **10 秒**&#x200B;为间隔，测量主内容事件，可及时捕获发生的所有活动。广告跟踪事件的发生间隔为 **1 秒**。
* **促进参与度提升 -**&#x200B;通过较少缓冲事件并了解广告应在内容中播放的位置和时间，提供更顺畅、更友好的体验，从而吸引用户再次来访，提高回访率。
* **全面视角 -**&#x200B;通过 [Federated Analytics](/help/federated-analytics.md) 功能将所有内容传播方的多个数据点相结合，在所有可能的渠道中全面了解媒体的活动，测量参与度和查看/收听次数。
* **增加粒度 -**&#x200B;在极其精细的粒度级别上评估查看行为，包括具体访客的时间段、每分钟的并行查看者/收听者数量和使用内容的平均持续时长。
* **精准测量 -**&#x200B;在使用媒体的多种设备（包括 OTT、智能手机、平板电脑、台式机，等等）上测量数据以监测用户参与模式和习惯。
* **区段划分 -**&#x200B;对您的播放器、设备、流派、章节和节目应用分类，以了解每个分类对内容、音频、广告和组合元素的整体查看/收听量和客户参与度有何影响。

## 心率相比里程碑的优势 {#heartbeat-versus-milestone-benefits}

Adobe Analytics for Media 可通过两种方式进行测量：旧版的里程碑方法（仅限视频）和新版的心率方法（适用于音频和视频，包括 Media SDK 和媒体收集 API）。心率方法是首选的测量方法，我们建议所有尚未采用心率方法的客户迁移到此版本，以便充分利用下文所述的优点。

旧版的里程碑方法基于对 Analytics 服务器的以下单个服务器调用：视频开始、四分位点、持续时间和结束。心率方法则提供了更强大的媒体跟踪解决方案，能够以 10 秒为间隔测量主内容，从而提供增强的标准化量度。此外，Adobe 从里程碑方法中汲取了经验，在心率方法中通过利用 Media SDK 或媒体收集 API，使实施流程更为顺畅、更为简单。

心率方法具有诸多优点，其中包括：

* **简化的实施流程 -**&#x200B;利用您的播放器 API 更轻松地映射变量，通过 Adobe Debug 工具验证实施以确保准确跟踪所有必需的变量。
* **自动集成 Adobe Experience Cloud -**&#x200B;通过 Experience Cloud ID 充分利用与 Adobe Experience Cloud 的自动集成，对媒体受众进行分段和定位，并根据用户的偏好推荐媒体内容。
* **利用 Federated Analytics 共享数据 -**&#x200B;利用我们在业界首开先河的媒体共享功能，全面评估您的所有媒体传播合作平台的数据：运营商、节目制作方和发行方。
* **所有平台通用的标准化解决方案 -**&#x200B;针对所有媒体和平台采用一致的标准化变量，可以更高效地对不同营销活动、设备和供应商的数据进行对比。
* **下载的内容跟踪 -**&#x200B;跟踪从设备中下载和播放的媒体内容（视频和音频），无论是否连接到网络。

### 对比图表

|  | Video Analytics - 里程碑 | Media Analytics - 心率 |
|---|---|---|
| **媒体事件** | 高级别的标准事件 | 每 10 秒执行一次主内容的详细自定义事件，每 1 秒执行一次广告的详细自定义事件。 |
| **量度和维度** | 在不同供应商之间存在差异，非标准化的量度和维度 | 针对所有供应商采用清晰的标准化量度、维度和基准 |
| **与 Adobe 产品集成** | 单一会话，支持部分映射和集成 | 利用集成的 Experience Cloud ID 与整个 Adobe Experience Cloud 相关联，使交叉分析更简便 |
| **定价** | 按每次服务器调用进行跟踪和计费 | 按媒体流（单个）进行透明的跟踪 |
| **实施与支持** | 实施集成所需的时间较长，对旧版本的支持有限，不会提供升级 | 简化配置，持续更新和改进 |
| **合作伙伴共享** | 不适用 | Federated Analytics 和经过认证的量度 |
| **高级跟踪** | 不适用 | 错误恢复跟踪和并行查看者 |

## 支持的设备 {#devices-supported}

Adobe Analytics for Media 契合行业发展趋势，提供了强大的数据收集工具，可确保在所有具有统计意义的设备上收集和报告每个媒体流。我们的 Media SDK 针对所有常用的设备而开发，这些设备包括：

* iOS 和 Android 智能手机和平板电脑
* 适用于 ROKU、AppleTV、FireTV 和 Android TV 的 OTT 设备
* 适用于台式机和笔记本电脑的 JavaScript 浏览器

当设备有新版本发布时，Adobe 会对 SDK 进行常规更新，您可以利用这些 SDK 与当今的大多数主流媒体播放器进行集成，包括 Brightcove 和 Ooyala。

对于目前不支持 SDK 的设备或平台（甚至对于支持 SDK 的设备和平台），您都可以实施媒体收集 API；通过使用该 API，您可以直接从设备/平台对 Media Analytics 后端进行 RESTful API 调用。

下表列出了目前可通过实施我们的 Media SDK 和媒体收集 API 支持的设备。要下载最新版本的 SDK，请参阅[下载 SDK。](sdk-implement/download-sdks.md)如果您希望实施测量的设备不在此列表中，请联系客户关怀或您的解决方案顾问来了解该设备的支持状态。

|      | Media SDK | 媒体收集 API |
|---|:---:|:---:|
| **JavaScript 浏览器** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **iOS 设备** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android 设备** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Unified Windows Platforms (UWP)** |  | ![](assets/icon-blue-check.png) |
| **Blackberry** |  | ![](assets/icon-blue-check.png) |
| **Apple TV（新版/旧版）** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU (JS)** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **ROKU（本机应用程序）** |  | ![](assets/icon-blue-check.png) |
| **OSX** |  | ![](assets/icon-blue-check.png) |
| **Fire TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Android TV** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Chromecast** | ![](assets/icon-blue-check.png) | ![](assets/icon-blue-check.png) |
| **Xbox One/360** |  | ![](assets/icon-blue-check.png) |
| **Sony PS3/PS4** |  | ![](assets/icon-blue-check.png) |
| **(其他/新连接设备）** |  | ![](assets/icon-blue-check.png) |

有关 Media SDK 的信息，另请参阅[最低平台版本支持](./sdk-implement/setup/setup-overview.md#minimum-platform-version)

## 传输层安全性 {#transport-layer-security}

**TLS 声明 --** Adobe 制定了要求终止使用旧版安全协议的安全合规标准。为了继续满足不断演变的安全协议标准，Adobe 正逐渐转为使用 TLS 1.2，以便使用最新的安全协议版本。从 2019 年 2 月 20 日起，Adobe 将仅支持 TLS 1.1 或更高版本。伴随这项变化，对于使用部署了 TLS 1.0 的较旧设备或 Web 浏览器的最终用户，Adobe 将不再收集他们的数据。迁移到 TLS 1.2 可提高安全性。您应务必了解具体细节，并且针对更改做出规划以实现顺利迁移。

>[!NOTE]
>
>TLS 是目前最广泛部署的安全协议，适用于 Web 浏览器和其他需要通过网络安全交换数据的应用程序。

