---
title: 广告名称
description: 报告每个广告的可读标题。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 5%

---


# 广告名称

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**广告名称**&#x200B;报告维度。 有关如何收集此变量，请参阅[广告名称](/help/implementation/variables/ads/ad-name.md)。*

>[!ENDSHADEBOX]

**广告名称**&#x200B;维度报告每个广告的可读标题。

## 如何填充此维度

广告名称由播放器在每个`media.adStart`事件中设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.friendlyName`自动收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videoadname, post_videoadname` |

在Adobe Analytics中，此维度以两种方式显示：作为&#x200B;**广告名称（变量）**（直接从`a.media.ad.friendlyName`收集）和作为&#x200B;**广告名称**（从[广告](ad.md)维度派生的分类）。 如果使用分类，则您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护其值。 使用&#x200B;**广告名称（变量）**&#x200B;不需要分类维护，但您丢失了广告名称和父[广告](ad.md)维度之间保证的1:1关系。 使用实施工作流最支持的组件。

## 维度项目

每个项目都是`media.adStart`上报告的文字广告标题（例如，`"Ford F-150"`）。
