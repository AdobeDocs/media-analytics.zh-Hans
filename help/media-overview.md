---
title: Adobe流媒体收集概述
description: 使用流媒体收藏集获得针对内容、音频和广告的强大insight。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 65%

---

# Adobe流媒体收集概述

![横幅](./assets/media_analytics_banner.png)

Adobe流媒体收藏集为流媒体内容（如适用于流媒体提供商的音频、视频和广告）提供强大的收藏集、测量和个性化工具。 您可以将流媒体量度与Audience Analytics、Mobile或Cross-Device Analytics等功能结合使用。

流媒体数据可轻松集成到以下Adobe Experience Platform产品中：

* Adobe Analytics

* Customer Journey Analytics

* Adobe Journey Optimizer

* Real-Time Customer Data Platform

>[!IMPORTANT]
>
>要实施流媒体收集，请联系您的Adobe销售代表或Adobe客户团队，以确保流媒体收集加载项是您的产品组合的一部分。

## 主要功能

流媒体收藏集的优势包括实时监控、详细分析、切实可行的见解、盈利机会等。

* **实时分析**：在多个渠道间利用关键性能指标（如媒体开始播放次数）做出实时、切实可行的决策。

  借助流媒体收集，您可以获得关于持续时间、停止和开始的近乎实时、精细的详细信息，以便您评估和组合视频和音频量度。 通过这些见解，可了解客户的观看和收听习惯，并通过高度个性化的推荐提高参与度。

* **促进参与**：通过减少缓冲事件以及通过了解应在内容中的何时何处播放广告以提供流畅、不那么令人反感的体验，促使用户重复访问，从而充分吸引用户参与。

* **一览无余**：整合所有内容传播方的多个数据点以全面了解所有媒体活动。在所有可能的渠道上测量参与度和观看/收听次数。

  流媒体收集使您能够跟踪整个网站和流媒体应用程序的客户历程，可视化客户路径和兴趣，提供增强的推荐并个性化客户体验。  媒体测量让您可以将数据分类为多个维度和区段，从而捕获执行完整的详细分析所需的所有元数据。然后，您可以分析数据并将成功标准归因于充分使用的媒体、平均逗留时间和已完成的广告。

* **重要指标**：测量与体验质量 (QoE) 相关的重要投放指标，如丢帧数、缓冲用时和平均比特率。

* **提高精细粒度**：在非常精细的粒度级别评估查看行为，包括个别访客的当天时间、各分钟同时存在的查看者或收听者以及使用内容的平均持续时间。

* **精确测量**：在用于媒体消费的多种设备（包括 OTT、智能手机、平板电脑、桌面计算机等等）上测量以监测用户参与模式和习惯。

* **分段**：将分类应用于您的播放器、设备、流派、章节和节目，以了解每个分类对于内容、音频、广告和这几项组合的总查看/收听次数和客户参与有多大影响。


## 工作原理

流媒体跟踪数据是使用 Media for Edge Network SDK/扩展、带标签的媒体扩展、Media SDK、Media Edge API 或 Media Collection API 从播放器收集的数据。

所有精细数据（最多 10 秒）都会发送到 Media Analytics Service 或 Experience Edge（取决于您选择的[实施方法](/help/implementation/overview.md)），并会收集和处理每个单独播放会话的数据。

播放会话结束后，计算出的跟踪数据将会发送到 Adob&#x200B;e Analytics 或 Customer Journey Analytics，以进行存储和报告。

>[!NOTE]
>
>通过实施 Customer Journey Analytics，可以使用 Experience Edge 或使用 Analytics Data Connector (ADC) 将数据发送到 Customer Journey Analytics。


有关各种实施方法的详细信息，请参阅[实施Adobe Analytics或Customer Journey Analytics的流媒体收藏集](/help/implementation/overview.md)。
