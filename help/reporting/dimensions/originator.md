---
title: 创作者
description: 报告内容的创建者或生产工作室。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---


# 创作者

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**发起人**&#x200B;报告维度。 有关如何收集此变量，请参阅[发起人](/help/implementation/variables/standard-metadata/originator.md)。*

>[!ENDSHADEBOX]

**创作者**&#x200B;维度报告内容的创建者或生产工作室（例如，`"Warner Brothers"`或`"Sony"`）。 使用它来比较内容所有者或权利所有者之间的参与情况。

## 如何填充此维度

发起者由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.originator`映射到eVar的[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | [内容(ID)](content.md)维度的分类 — 为报表包启用&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;时，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.originator`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |
| Audience Manager | `c_contextdata.a.media.originator` |

## 分类方法

为报表包启用&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;时，Adobe会自动创建创建创建者分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个内容ID及其发起方之间提供了保证的1:1关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改创建者分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.originator`映射到eVar的[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法将发起者捕获为每次点击值，而无需分类维护。

取舍是您丢失了发起者和父[内容(ID)](content.md)维度之间保证的1:1关系。 如果实施在事件之间为同一内容ID发送的值不一致，则同一内容下可能会显示多个创作者。 更新值仅适用于以后的数据。

## 维度项目

每一项都是会话开始时报告的文字创作者值。 每个演播室使用稳定、不同的名称，以便参与不会在非相关实体间折叠。
