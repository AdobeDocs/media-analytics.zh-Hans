---
title: 网站 ID
description: 报告每个广告的广告网站标识符。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# 网站 ID

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**站点ID**&#x200B;报告维度。 有关如何收集此变量，请参阅[站点ID](/help/implementation/variables/ads/site-id.md)。*

>[!ENDSHADEBOX]

**网站ID**&#x200B;维度报告广告网站标识符（通常是广告服务器平台的ID）。 使用维度可划分广告投放网站的参与度。

## 如何填充此维度

播放器在每个[广告开始](/help/implementation/events/ads/ad-start.md)事件中设置网站ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.ad.site`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.ad.site`映射到的eVar） |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## 维度项目

每个项目都是在[广告开始](/help/implementation/events/ads/ad-start.md)上报告的文字网站ID值。
