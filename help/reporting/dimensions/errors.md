---
title: 错误数
description: 报告每个会话的错误事件计数。
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
source-wordcount: '235'
ht-degree: 6%
---

# 错误数

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**错误**维度。 Adobe Analytics从同一`a.media.qoe.errorCount`上下文数据变量自动填充配对的[错误事件指标](/help/reporting/metrics/error-events.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.errorCount`字段，您可以将其用作维度或指标。*

>[!ENDSHADEBOX]

**错误**&#x200B;维度报告会话期间收到的错误事件计数。 使用维度按确切错误计数划分参与度。

## 如何填充此维度

媒体后端会递增播放器报告的每个错误的计数。 此值在关闭调用中报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.errorCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## 维度项目

每个项目都是关闭调用中报告的文字错误计数值。 对于会话级别的布尔报表（无论是否发生任何错误），请使用[受错误影响的流](/help/reporting/metrics/error-impacted-streams.md)。 对于唯一的错误ID，请使用[外部错误ID](external-error-ids.md)和[播放器SDK错误ID](player-sdk-error-ids.md)。

>[!NOTE]
>
>如果您使用旧版心率SDK (Media SDK 1.5.x-2.x)，则由SDK内部生成的错误ID会自动收集在上下文数据键`a.media.qoe.mediaSdkErrors`下，并可通过自定义处理规则在Adobe Analytics中访问。 Audience Manager特征是`c_contextdata.a.media.qoe.mediaSdkErrors`。 此字段不适用于媒体收集API或Media Edge API实施。
