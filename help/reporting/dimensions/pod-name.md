---
title: Pod名称
description: 报告每个广告时间的友好名称。 使用分类或自定义处理规则在Adobe Analytics中收集它。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Pod名称

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**面板名称**报告维度。 有关如何收集此变量，请参阅[广告时间名称](/help/implementation/variables/ads/ad-break-name.md)。*

>[!ENDSHADEBOX]

**面板名称**&#x200B;维度报告每个广告时间的友好名称（例如，`"pre-roll"`、`"mid-roll-1"`）。 在Customer Journey Analytics中，它是一个直接从implementation变量填充的离散维度。 在Adobe Analytics中，它可通过两种方法使用：[广告pod](ad-pod.md)维度的分类，或使用处理规则填充的eVar。

## 如何填充此维度

Pod名称源自播放器在[广告时间开始](/help/implementation/events/ads/ad-break-start.md)上设置的[广告时间名称](/help/implementation/variables/ads/ad-break-name.md)值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.ad.podFriendlyName`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | 广告面板维度的分类 — 为报表包启用&#x200B;**[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.ad.podFriendlyName`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |
| Audience Manager | `c_contextdata.a.media.ad.podFriendlyName` |

## 分类方法

为报表包启用&#x200B;**[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建Pod名称分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个面板ID及其友好名称之间提供了保证的1:1关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改Pod名称分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.ad.podFriendlyName`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法将友好名称捕获为每次点击值，而无需分类维护。

取舍是您丢失了面板名称和父[广告pod](ad-pod.md)维度之间保证的1:1关系。 如果实施在不同事件间为同一面板ID发送的值不一致，则同一广告面板下可能会显示多个名称。 更新值仅适用于以后的数据。

## 维度项目

每个项目都是在[广告时间开始](/help/implementation/events/ads/ad-break-start.md)上报告的文字广告时间名称。
