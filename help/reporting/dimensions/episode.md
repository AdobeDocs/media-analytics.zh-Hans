---
title: 剧集
description: 报告一季中的集数。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 9%

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
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.episode`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoepisode, post_videoepisode` |

## 维度项目

每个项目是在会话开始时报告的字面集值（通常是字符串整数，如`"13"`）。 单单剧集数量在各季并不独特，而是与“季节”搭配使用，以取得明确的分手。
