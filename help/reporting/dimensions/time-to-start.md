---
title: 开始时间（维度）
description: 报告呈现第一帧之前经过的时间。
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
source-wordcount: '190'
ht-degree: 7%
---

# 开始时间（维度）

>[!BEGINSHADEBOX]

*本页涵盖&#x200B;**开始时间**&#x200B;维度。 Adobe Analytics从同一`a.media.qoe.timeToStart`上下文数据变量自动填充配对的[开始时间（指标）](/help/reporting/metrics/time-to-start.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.timeToStart`字段，您可以将其用作维度或指标。 有关如何收集此变量，请参阅[开始时间](/help/implementation/variables/quality/time-to-start.md)。*

>[!ENDSHADEBOX]

**开始时间**&#x200B;维度报告从会话开始到第一帧渲染之间经过的时间。 使用维度可按启动时段划分参与度。 Adobe会以秒为单位存储该值，并在摄取时从播放器报表中转换。

## 如何填充此维度

播放器在会话开始触发之前对QoE对象设置`timeToStart`。 后端报告关闭调用中的值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.timeToStart`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## 维度项目

每个项目都是关闭调用中报告的文字启动时间值。
