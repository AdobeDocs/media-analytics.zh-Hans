---
title: 广告
description: 报告每个播放的唯一广告，按广告ID进行键入。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 7%

---


# 广告

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**广告**&#x200B;报告维度。 有关如何收集此变量，请参阅[广告ID](/help/implementation/variables/ads/ad-id.md)。*

>[!ENDSHADEBOX]

**广告**&#x200B;维度报告每个播放的唯一广告，由[广告开始](/help/implementation/events/ads/ad-start.md)上设置的广告ID作为密钥。 维度是广告报表的主要细分，是广告级别分类（如广告名称、广告长度和Creative ID）的联接键。

## 如何填充此维度

广告由播放器在每个[广告开始](/help/implementation/events/ads/ad-start.md)事件中设置为广告的稳定标识符。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.name`自动收集。 在访问期间持续存在。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>广告ID为必填项。 如果未设置或为空，则将从流媒体广告报表中删除广告。

## 维度项目

每个项目都是一个在[广告开始](/help/implementation/events/ads/ad-start.md)报告的唯一广告ID。 为每个创意内容使用稳定的标识符，以便同一广告可以跨会话汇总为单个行项目。
