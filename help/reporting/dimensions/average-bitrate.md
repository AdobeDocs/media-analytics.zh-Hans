---
title: 平均比特率（维度）
description: 报告每个会话在100 kbps时间间隔内的分段平均比特率。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 8%
---

# 平均比特率（维度）

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**平均比特率**&#x200B;维度，该维度报告每个会话的分段比特率。 请参阅原始加权平均指标的[平均比特率（指标）](/help/reporting/metrics/average-bitrate.md)。 有关如何收集此变量，请参阅[比特率](/help/implementation/variables/quality/bitrate.md)。*

>[!ENDSHADEBOX]

**平均比特率**&#x200B;维度报告每个会话的平均播放比特率，以100 kbps间隔进行分段。 后端将该值计算为会话中所有比特率值的加权平均值，然后将其分配给存储段。 使用维度可按比特率层划分参与度和质量。

## 如何填充此维度

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.bitrateAverageBucket`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## 维度项目

每个项目都是一个比特率存储段标签（例如，`800-899`、`3200-3299`）。 将[平均比特率（指标）](/help/reporting/metrics/average-bitrate.md)用于原始加权平均值，而不是分段维度。
