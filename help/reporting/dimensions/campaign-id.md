---
title: 营销活动 ID
description: 报告每个广告所属的营销活动。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# 营销活动 ID

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**促销活动ID**&#x200B;报告维度。 有关如何收集此变量，请参阅[促销活动ID](/help/implementation/variables/ads/campaign-id.md)。*

>[!ENDSHADEBOX]

**促销活动ID**&#x200B;维度报告每个广告创意所属的广告促销活动。 使用维度可在共享营销策划的多个创意中汇总参与度。

## 如何填充此维度

促销活动ID由播放器在每个`media.adStart`事件中进行设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.campaign`自动收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videocampaign, post_videocampaign` |

## 维度项目

每个项目是`media.adStart`上报告的文字营销活动值。
