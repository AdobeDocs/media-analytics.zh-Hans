---
title: 广告名称
description: 报告每个广告的可读标题。
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
source-wordcount: '194'
ht-degree: 7%
---

# 广告名称

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**广告名称**&#x200B;报告维度。 有关如何收集此变量，请参阅[广告名称](/help/implementation/variables/ads/ad-name.md)。*

>[!ENDSHADEBOX]

**广告名称**&#x200B;维度报告每个广告的可读标题。

## 如何填充此维度

广告名称由播放器在每个[广告开始](/help/implementation/events/ads/ad-start.md)事件中设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/setup/analytics-reporting.md)时，从上下文数据`a.media.ad.friendlyName`自动收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

在Adobe Analytics中，此维度以两种方式显示：作为&#x200B;**广告名称（变量）**（直接从`a.media.ad.friendlyName`收集）和作为&#x200B;**广告名称**（从[广告](ad.md)维度派生的分类）。 如果使用分类，则您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护其值。 使用&#x200B;**广告名称（变量）**&#x200B;不需要分类维护，但您将失去广告名称和父[广告](ad.md)维度之间保证的1:1关系。 使用实施工作流最支持的组件。

## 维度项目

每个项目都是在[广告开始](/help/implementation/events/ads/ad-start.md)上报告的文字广告标题（例如，`"Ford F-150"`）。
