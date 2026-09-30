---
title: 媒体馈送类型
description: 在通过多个馈送交付相同内容时，报告广播馈送（例如，East-HD或West-SD）。
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
source-wordcount: '159'
ht-degree: 8%
---

# 媒体馈送类型

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**媒体馈送类型**&#x200B;报告维度。 有关如何收集此变量，请参阅[媒体馈送类型](/help/implementation/variables/standard-metadata/media-feed-type.md)。*

>[!ENDSHADEBOX]

**媒体馈送类型**&#x200B;维度报告每个会话的广播馈送（例如，`"East-HD"`、`"West-SD"`或`"4K"`）。 当通过多个区域或质量馈送交付相同内容，并且需要为每个馈送报告参与时，可使用它。

## 如何填充此维度

媒体馈送类型由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.feed`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## 维度项目

每个项目都是会话开始时报告的文字信息源值。 根据区域或质量拆分使用一组稳定的信息源标识符。
