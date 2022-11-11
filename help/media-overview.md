---
title: Adobe Analytics for Streaming Media概述
description: 使用流媒体分析，对内容、音频和广告获得强大的洞察力。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 16%

---

# Adobe Analytics for Streaming Media概述

![横幅](./assets/media_analytics_banner.png)

适用于流媒体的 Adobe Analytics 是 Adobe Analytics 的一个附加产品，可提供针对音频、视频和广告的强大测量工具。借助适用于流媒体的Analytics，您可以获得持续时间、停止次数和开始次数的近乎实时的精细详细信息，以便您评估和组合视频和音频量度。 通过这些洞察，您可以了解客户的查看和收听习惯，并通过高度个性化的推荐来提高参与度。

Adobe Analytics for Streaming Media让您能够跟踪客户在您的网站和流应用程序中的整个历程。 您可以将流媒体量度与其他Adobe Analytics功能(如Audience Analytics、移动设备或跨设备分析)结合使用。 这些量度可轻松集成到Adobe Analytics报表和其他Adobe Experience Platform产品中。 媒体测量让您可以将数据分类为多个维度和区段，从而捕获执行完整的详细分析所需的所有元数据。然后，您可以分析数据并将成功标准归因于充分使用的媒体、平均逗留时间和已完成的广告。

您可以测量与体验质量(QoE)相关的重要交付量度，例如丢帧、缓冲所用时间和平均比特率。 这些量度可以与您的网站或应用程序数据相结合，以可视化客户路径和兴趣 — 使用Adobe Experience Platform提供增强的推荐和个性化客户体验。

## 工作原理

使用Media SDK、媒体收集API或媒体扩展（包含标记）从播放器收集流媒体跟踪数据。 所有粒度数据（最多10秒）都会发送到Media Analytics服务，该服务会为每个单独的播放会话收集和处理数据。 播放会话结束后，计算的跟踪数据将发送到Adobe Analytics以进行存储和报告。 在Adobe Customer Journey Analytics(CJA)实施中，可以使用Analytics Data Connector(ADC)将数据发送到CJA，以便客户可以将CJA用作报表工具。

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="流媒体流程" width="75%">
</div>

## 功能

适用于流媒体的 Adobe Analytics 具备以下优势：实时监控、详细分析、切实可行的洞察信息以及盈利机会。

* **实时分析**:跨多个渠道利用关键绩效量度（如媒体开始）做出实时、可操作的决策。

* **推动参与**:通过减少缓冲事件，了解广告在内容中的播放位置和时间，以提供流畅、影响较小的体验来交付重复访问，从而充分吸引用户。

* **全面视角**:合并所有内容分发商的多个数据点，以全面了解所有媒体活动。通过Federated Analytics功能，跨所有可能的渠道衡量参与度和查看/收听次数。

* **增加了粒度**:在最精细的粒度级别评估查看行为，包括每天的单个访客时间、按分钟划分的并行查看者或收听者，以及使用内容的平均持续时间。

* **精确测量**:在用于媒体使用情况的多种设备（包括OTT、智能手机、平板电脑、台式机等）上进行测量，以监控用户参与模式和习惯。

* **分段**:将分类应用于您的播放器、设备、流派、章节和节目，以了解每个分类对内容、音频、广告和组合内容的整体查看/收听次数和客户参与度有何影响。
