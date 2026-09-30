---
title: 季
description: 报告情景内容的季编号。
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
source-wordcount: '140'
ht-degree: 11%
---

# 季

>[!BEGINSHADEBOX]

*本页涵盖&#x200B;**季**&#x200B;报告维度。 请参阅[季](/help/implementation/variables/standard-metadata/season.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**季节**&#x200B;维度报告偶发内容的季编号。 将它与[节目](show.md)和[剧集](episode.md)一起使用以进行完整的分段划分。

## 如何填充此维度

当内容属于某个系列时，播放器在会话开始时会设置季。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.season`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## 维度项目

每个项目是在会话开始时报告的文字季值（通常是字符串整数，如`"1"`、`"2"`）。 对于同一节目中的各个集数保持一致；维度不会将`"1"`和`"01"`标准化为相同的行项目。
