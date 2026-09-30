---
title: 创作 URL
description: 报告每个广告创意的资产URL。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 10%
---

# 创作 URL

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**Creative URL**&#x200B;报表维度。 有关如何收集此变量，请参阅[Creative URL](/help/implementation/variables/ads/creative-url.md)。*

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
