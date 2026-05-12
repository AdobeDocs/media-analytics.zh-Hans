---
title: 章节偏移
description: 报告内容中每个章节的偏移。
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---


# 章节偏移

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**章节偏移**&#x200B;报告维度。 有关如何收集此变量，请参阅[章节偏移](/help/implementation/variables/chapters/chapter-offset.md)。*

>[!ENDSHADEBOX]

**章节偏移**&#x200B;维度报告内容中每个章节的偏移，以秒为单位，从开始起计算。

## 如何填充此维度

播放器在每`media.chapterStart`个事件中设置章节偏移。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.chapter.offset`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | [Chapter](chapter.md)维度的分类 — 为报表包启用&#x200B;**[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.chapter.offset`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |

## 分类方法

为报表包启用了&#x200B;**[[!UICONTROL 媒体章节]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建章节偏移分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个章节ID及其偏移之间提供了保证的1:1关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改章节偏移分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.chapter.offset`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法将章节偏移捕获为每次点击值，而无需分类维护。

取舍是您丢失了章节偏移和父[Chapter](chapter.md)维度之间保证的1:1关系。 如果实施在不同事件间为同一章节ID发送的值不一致，则同一章节下可能会显示多个偏移。 更新值仅适用于以后的数据。

## 维度项目

每个项目是`media.chapterStart`上报告的整数偏移值（以秒为单位）。
