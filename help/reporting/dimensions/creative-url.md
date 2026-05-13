---
title: 创作 URL
description: 报告每个广告创意的资产URL。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 9%

---


# 创作 URL

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**Creative URL**&#x200B;报表维度。 有关如何收集此变量，请参阅[Creative URL](/help/implementation/variables/ads/creative-url.md)。*

>[!ENDSHADEBOX]

**Creative URL**&#x200B;维度报告每个广告创意的资源URL。 当URL本身对分析有意义（例如，区分CDN路径或创意版本）时，请使用维度。

## 如何填充此维度

Creative URL由播放器在每个`media.adStart`事件中设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.ad.creativeURL`映射到eVar的[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.ad.creativeURL`映射到的eVar） |

## 维度项目

每个项目都是在`media.adStart`上报告的文字URL字符串。
