---
title: 广告商
description: 报告每个广告中展现的公司或品牌。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

---


# 广告商

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告商**&#x200B;报告维度。 有关如何收集此变量，请参阅[广告商](/help/implementation/variables/ads/advertiser.md)。*

>[!ENDSHADEBOX]

**广告商**&#x200B;维度报告每个广告中介绍的公司或品牌（例如，`"Ford"`或`"Coca-Cola"`）。 使用维度可划分广告商的参与度和完成度。

## 如何填充此维度

广告商由播放器在每个[广告开始](/help/implementation/events/ads/ad-start.md)事件中设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/setup/analytics-reporting.md)时，从上下文数据`a.media.ad.advertiser`自动收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## 维度项目

每个项目都是在[广告开始](/help/implementation/events/ads/ad-start.md)上报告的文字广告商名称。
