---
title: 资产 ID
description: 报告基础媒体资产的稳定行业标识符。
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# 资产 ID

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**资产ID**报告维度。 有关如何收集此变量，请参阅[资产ID](/help/implementation/variables/standard-metadata/asset-id.md)。*

>[!ENDSHADEBOX]

**资产ID**&#x200B;维度报告基础媒体资产的稳定行业标识符（通常为EIDR、TMS/Gracenote或Rovi ID，但也接受专有ID）。

## 如何填充此维度

资产ID由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.asset`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | [内容(ID)](content.md)维度的分类。 为报表包启用&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;后，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.asset`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |
| Audience Manager | `c_contextdata.a.media.asset` |

## 分类方法

为报表包启用了&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;时，Adobe会自动创建资产ID分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个内容ID与其资产ID之间提供了保证的1:1关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改资产ID分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.asset`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法将资产ID捕获为每次点击值，而无需分类维护。

取舍是您丢失了资产ID与父[内容(ID)](content.md)维度之间保证的1:1关系。 如果实施在事件中为同一内容ID发送的值不一致，则同一内容下可能会显示多个资产ID。 更新值仅适用于以后的数据。

## 维度项目

每个项目都是一个在报告期间报告的唯一资产ID值。 在所有分发平台中对每项资产使用一个稳定的标识符，以便相同的内容可以汇总到单个行项目。
