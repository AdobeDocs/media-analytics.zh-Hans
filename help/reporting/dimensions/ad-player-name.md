---
title: 广告播放器名称
description: 报告每个广告由哪个播放器呈现。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# 广告播放器名称

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**广告播放器名称**报告维度。 有关如何收集此变量，请参阅[广告播放器名称](/help/implementation/variables/ads/ad-player-name.md)。*

>[!ENDSHADEBOX]

**广告播放器名称**&#x200B;维度报告哪个播放器呈现了每个广告（例如，`"Freewheel"`、`"Google IMA"`）。 当服务器端广告插入服务拼合广告时，广告播放器可以不同于主内容播放器。

## 如何填充此维度

广告播放器名称由播放器在每个[广告开始](/help/implementation/events/ads/ad-start.md)事件中设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.playerName`自动收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## 维度项目

每个项目都是在[广告开始](/help/implementation/events/ads/ad-start.md)上报告的文字广告播放器名称。
