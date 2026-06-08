---
title: 第一个数字日期
description: 报告内容首次在数字平台上出现的日期。
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# 第一个数字日期

>[!BEGINSHADEBOX]

*本页涵盖&#x200B;**第一个数字日期**&#x200B;报告维度。 有关如何收集此变量的信息，请参阅[首次数字化日期](/help/implementation/variables/standard-metadata/first-digital-date.md)。*

>[!ENDSHADEBOX]

**第一个数字日期**&#x200B;维度报告内容首次在数字平台上出现的日期。 使用它与[首次播放日期](first-air-date.md)一起比较数字发布时间与原始广播。

## 如何填充此维度

播放器在会话开始时设置第一个数字日期。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.digitalDate`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | [内容(ID)](content.md)维度的分类。 为报表包启用&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;后，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.digitalDate`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## 分类方法

为报表包启用&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;后，Adobe会自动创建第一个数字日期分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个内容ID及其第一个数字日期之间提供了保证的1:1关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改第一个数字日期分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.digitalDate`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法将第一个数字日期捕获为每次点击值，而无需分类维护。

取舍是您丢失了第一个数字日期与父[内容(ID)](content.md)维度之间保证的1:1关系。 如果实施在事件间为同一内容ID发送的值不一致，则同一内容下可能会显示多个首次数字日期。 更新值仅适用于以后的数据。

## 维度项目

每一项都是会话开始时报告的文字日期字符串。 在实施中使用一致的格式。 Adobe建议`YYYY-MM-DD`。
