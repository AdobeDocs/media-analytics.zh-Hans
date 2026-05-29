---
title: 创作 URL
description: 报告每个广告创意的资产URL。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 10%

---


# 创作 URL

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**Creative URL**报表维度。 有关如何收集此变量，请参阅[Creative URL](/help/implementation/variables/ads/creative-url.md)。*

>[!ENDSHADEBOX]

**Creative URL**&#x200B;维度报告每个广告创意的资源URL。 当URL本身对分析有意义（例如，区分CDN路径或创意版本）时，请使用维度。

## 如何填充此维度

播放器在每个[广告开始](/help/implementation/events/ads/ad-start.md)事件中设置Creative URL。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.ad.creativeURL`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.ad.creativeURL`映射到的eVar） |
| Audience Manager | `c_contextdata.a.media.ad.creativeURL` |

## 维度项目

每个项目都是在[广告开始](/help/implementation/events/ads/ad-start.md)上报告的文字URL字符串。
