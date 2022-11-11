---
title: 关于心率测量
description: 了解如何使用心率收集视频量度。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 30%

---

# 关于心率测量

Adobe Analytics使用“心率”收集视频量度。 在视频播放期间，心率会发送到心率跟踪服务器以测量播放时长。每十秒发送一次心率调用。心率会生成精细的视频参与量度，以及更准确的视频流失报表。Adobe Analytics for Streaming Media使用包含Media Analytics扩展、Media SDK和媒体收集API的AdobeLaunch来测量心率。 `AppMeasurement` 和 `VisitorID` 组件用于接收视频数据。

通过使用心率，适用于流媒体的 Adobe Analytics 具备以下优势：

| 功能 | 描述 |
|---|---|
| 媒体事件 | 对于主内容，每 10 秒发送一次详细事件和自定义事件；对于广告，则每 1 秒发送一次。 |
| 量度和维度 | 跨供应商的明确标准化量度、维度和基准。通过跨所有平台的标准化解决方案，您可以跨所有媒体和平台使用一致的标准化变量，以便更有效地跨促销活动、设备和供应商进行比较。 |
| 集成 | Experience CloudID已链接到Adobe Experience Cloud，以便进行交叉分析。通过自动Adobe Experience Cloud集成，您可以对媒体受众进行分段、定位这些受众，并根据用户偏好提出媒体推荐。 |
| 定价 | 透明的按媒体流跟踪（单个） |
| 实施和支持 | 通过不断更新和改进来简化配置。通过简化的实施流程，您可以通过播放器API快速映射变量并使用Adobe调试工具验证实施，以确保准确跟踪所有必需变量。 |
| 合作伙伴共享 | Federated Analytics和认证量度。通过Federated Analytics共享数据，您可以利用我们业界领先的媒体共享功能，全面评估您的所有媒体分发合作伙伴（运营商、节目制作商和发行商）的数据。 |
| 高级跟踪 | 下载的内容跟踪、错误恢复跟踪和并行查看者。您可以跟踪在设备上下载和播放的流媒体内容，而不管该设备是否联网。 |
