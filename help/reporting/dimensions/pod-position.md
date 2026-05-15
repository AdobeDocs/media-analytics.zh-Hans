---
title: Pod位置
description: 报告内容中每个广告时间的偏移。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# Pod位置

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**面板位置**&#x200B;报告维度。 有关如何收集此变量，请参阅[广告时间开始时间](/help/implementation/variables/ads/ad-break-start-time.md)。*

>[!ENDSHADEBOX]

**Pod位置**&#x200B;维度报告内容内每个广告时间的偏移（以秒为单位）。 前置滚动具有位置`0`；中间滚动具有与其播放头开始时间对应的位置。

## 如何填充此维度

Pod位置是根据播放器在[广告时间开始](/help/implementation/events/ads/ad-break-start.md)上设置的[广告时间开始时间](/help/implementation/variables/ads/ad-break-start-time.md)值设置的。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.ad.podSecond`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | [广告面板](ad-pod.md)维度的分类 — 为报表包启用&#x200B;**[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.ad.podSecond`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |
| Audience Manager | `c_contextdata.a.media.ad.podSecond` |

## 分类方法

为报表包启用&#x200B;**[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)**&#x200B;时，Adobe会自动创建Pod位置分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个广告面板ID及其位置之间提供了保证的1:1关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改面板位置分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.ad.podSecond`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 此方法捕获面板位置作为每次点击值，而无需分类维护。

取舍是您丢失了面板位置和父[广告Pod](ad-pod.md)维度之间保证的1:1关系。 如果实施在不同事件间为同一面板ID发送的值不一致，则同一广告面板下可能会显示多个位置。 更新值仅适用于以后的数据。

## 维度项目

每个项目都是在[广告时间开始](/help/implementation/events/ads/ad-break-start.md)时报告的整数偏移值（以秒为单位）。
