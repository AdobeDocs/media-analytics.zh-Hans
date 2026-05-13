---
title: 流派
description: 报告内容流派。 多流派内容会跨行项目进行拆分，每个行项目会获得相同的量度权重。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 6%

---


# 流派

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**流派**&#x200B;报告维度。 有关如何收集此变量的信息，请参阅[流派](/help/implementation/variables/standard-metadata/genre.md)。*

>[!ENDSHADEBOX]

**流派**&#x200B;维度报告内容流派。 流派作为以逗号分隔的字符串收集，并存储为列表维度。 多流派内容会拆分到单独的行项目，每个行项目会获得相同的量度权重。 使用它来比较不同流派之间的参与度，而无需重复计算在单个多流派资源上花费的时间。

## 如何填充此维度

流派由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.genre`（存储为列表变量）收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.genreList`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting)或[`mediaReporting.sessionDetails.genre`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting)（旧版） |
| 数据馈送 | `videogenre, post_videogenre` |

## 维度项目

每个项目都是一个流派值。 多流派会话（例如，`"Drama,Action"`）显示为两个单独的行项目（`Drama`和`Action`），其中每个项目都接收会话的完整点数。
