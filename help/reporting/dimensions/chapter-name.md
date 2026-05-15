---
title: 章节名称
description: 显示人类可读的章节标题。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---


# 章节名称

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**章节名称**报告维度。 有关如何收集此变量，请参阅[章节名称](/help/implementation/variables/chapters/chapter-name.md)。*

>[!ENDSHADEBOX]

**章节名称**&#x200B;维度显示每个章节的可读标题（例如，`"Pilot Episode - Opening"`）。

## 如何填充此维度

播放器在每个[章节开始](/help/implementation/events/chapters/chapter-start.md)事件上设置章节名称。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.chapter.friendlyName`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | [Chapter](chapter.md)维度的分类 — 为报表包启用&#x200B;**[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.chapter.friendlyName`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |
| Audience Manager | `c_contextdata.a.media.chapter.friendlyName` |

## 分类方法

为报表包启用了&#x200B;**[[!UICONTROL 媒体章节]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建章节名称分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个章节ID及其友好名称之间提供了保证的1:1关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改章节名称分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.chapter.friendlyName`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法将友好名称捕获为每次点击值，而无需分类维护。

取舍是您丢失了章节名称和父[Chapter](chapter.md)维度之间保证的1:1关系。 如果实施在不同事件间为同一章节ID发送的值不一致，则同一章节下可能会显示多个名称。 更新值仅适用于以后的数据。

## 维度项目

每个项目都是在[章节开始](/help/implementation/events/chapters/chapter-start.md)上报告的文字章节标题。
