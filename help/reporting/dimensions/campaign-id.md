---
title: 营销活动 ID
description: 报告每个广告所属的营销活动。
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
source-wordcount: '122'
ht-degree: 14%
---

# 营销活动 ID

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**促销活动ID**&#x200B;报告维度。 有关如何收集此变量，请参阅[促销活动ID](/help/implementation/variables/ads/campaign-id.md)。*

>[!ENDSHADEBOX]

**促销活动ID**&#x200B;维度报告每个广告创意所属的广告促销活动。 使用维度可在共享营销策划的多个创意中汇总参与度。

## 如何填充此维度

播放器在每[个广告开始](/help/implementation/events/ads/ad-start.md)事件上设置促销活动ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/setup/analytics-reporting.md)时，从上下文数据`a.media.ad.campaign`自动收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## 维度项目

每个项目都是在[广告开始](/help/implementation/events/ads/ad-start.md)上报告的文字营销活动值。
