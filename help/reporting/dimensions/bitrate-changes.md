---
title: 比特率更改（维度）
description: 报告每个会话的比特率更改事件计数。
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
source-wordcount: '205'
ht-degree: 6%
---

# 比特率更改（维度）

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**比特率更改**维度。 Adobe Analytics从同一`a.media.qoe.bitrateChangeCount`上下文数据变量自动填充配对的[比特率更改（指标）](/help/reporting/metrics/bitrate-changes.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`字段，您可以将其用作维度或指标。 有关如何触发比特率更改事件，请参阅[比特率更改](/help/implementation/variables/quality/bitrate-change.md)。*

>[!ENDSHADEBOX]

**比特率更改**&#x200B;维度报告会话期间发生的比特率更改事件计数。 使用维度可按确切的更改计数值划分参与度和质量（例如，“具有3个比特率更改的会话与具有0的会话”）。

## 如何填充此维度

媒体后端在会话期间每收到[比特率更改](/help/implementation/events/playback/bitrate-change.md)事件就递增计数。 此值在关闭调用中报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.bitrateChangeCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## 维度项目

每个项目都是关闭调用中报告的文字更改计数值。 对于会话级别的布尔报表（会话是否遇到任何比特率更改），请使用[受比特率更改影响的流](/help/reporting/metrics/bitrate-change-impacted-streams.md)。
