---
title: 版面 ID
description: 报告每个广告的投放位置标识符。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 9%

---


# 版面 ID

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**版面ID**报告维度。 有关如何收集此变量，请参阅[版面ID](/help/implementation/variables/ads/placement-id.md)。*

>[!ENDSHADEBOX]

**版面ID**&#x200B;维度报告广告版面标识符（通常是广告服务器平台中定义的版面或区域）。 使用维度可比较投放位置空格的参与度和完成度。

## 如何填充此维度

播放器在每`media.adStart`个事件中设置一次投放ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.ad.placement`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.ad.placement`映射到的eVar） |

## 维度项目

每个项目都是在`media.adStart`上报告的文字版面值。
