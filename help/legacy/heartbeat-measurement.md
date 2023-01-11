---
title: 有关心跳测量
description: 了解如何使用心跳收集视频量度。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
source-git-commit: a7d897c6f6fbc6ed0d5b71f5801ab18ee21f0411
workflow-type: ht
source-wordcount: '311'
ht-degree: 100%

---

# 有关心跳测量

Adobe Analytics 使用“心跳”收集视频量度。在视频播放期间，心跳会发送到心跳跟踪服务器以测量播放时长。每十秒发送一次心跳调用。心跳会生成精细的视频参与量度，以及更准确的视频流失报表。适用于流媒体的 Adobe Analytics 使用包含 Media Analytics 扩展的 Adobe Launch、Media SDK 和媒体收集 API 来测量心跳。`AppMeasurement` 和 `VisitorID` 组件用于接收视频数据。

通过使用心跳，适用于流媒体的 Adobe Analytics 具备以下优势：

| 功能 | 描述 |
|---|---|
| 媒体事件 | 对于主内容，每 10 秒发送一次详细事件和自定义事件；对于广告，则每 1 秒发送一次。 |
| 量度和维度 | 跨供应商的明确标准化量度、维度和基准。通过跨所有平台的标准化解决方案，您可以跨所有媒体和平台使用一致的标准化变量，从而更有效地跨促销活动、设备和供应商进行比较。 |
| 集成 | Experience Cloud ID 已链接到 Adobe Experience Cloud，以便更轻松地执行交叉分析。通过自动 Adobe Experience Cloud 集成，您可以对媒体受众进行细分、定位这些受众，并根据用户偏好提供媒体推荐。 |
| 定价 | 透明的按媒体流跟踪（单个） |
| 实施和支持 | 通过不断更新和改进来简化配置。通过简化实施流程，您可以通过播放器 API 快速映射变量并使用 Adobe Debug Tool 验证实施，以确保准确跟踪所有必要变量。 |
| 合作伙伴共享 | Federated Analytics 和认证的量度。通过 Federated Analytics 共享数据，您可以利用我们业界领先的媒体共享功能，全面评估您的所有媒体分发合作伙伴（运营商、节目制作商和分发商）的数据。 |
| 高级跟踪 | 下载内容跟踪、错误恢复跟踪和并行查看者。您可以跟踪在设备上下载和播放的流媒体内容，而不论该设备是否联网。 |
