---
title: 剧集
description: 报告一季中的集数。
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
source-wordcount: '132'
ht-degree: 12%
---

# 剧集

>[!BEGINSHADEBOX]

*本页涵盖&#x200B;**集**报告维度。 有关如何收集此变量，请参阅[集](/help/implementation/variables/standard-metadata/episode.md)。*

>[!ENDSHADEBOX]

**Episode**&#x200B;维度报告一季中的剧集数量。 将其与[节目](show.md)和[季](season.md)一起使用可在单个剧集级别划分参与度。

## 如何填充此维度

剧集由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.episode`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## 维度项目

每个项目是在会话开始时报告的字面集值（通常是字符串整数，如`"13"`）。 单单剧集数量在各季并不独特，而是与“季节”搭配使用，以取得明确的分手。
