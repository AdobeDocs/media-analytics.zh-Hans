---
title: 面板中的广告位置
description: 报告每个广告在其父广告时间内的零索引位置。
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
source-wordcount: '156'
ht-degree: 8%
---

# 面板中的广告位置

>[!BEGINSHADEBOX]

*此页涵盖面板位置&#x200B;**报告维度中的**&#x200B;广告。 查看[面板位置](/help/implementation/variables/ads/ad-in-pod-position.md)中的广告，了解如何收集此变量。*

>[!ENDSHADEBOX]

面板位置&#x200B;**中的**&#x200B;广告维度报告每个广告在其父广告时间内的零索引位置。 面板中的第一个广告是`0`，第二个是`1`，依此类推。 使用维度可按广告时间内的位置比较参与和完成情况。

## 如何填充此维度

Pod中的广告位置由播放器在每个[广告开始](/help/implementation/events/ads/ad-start.md)事件时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/setup/analytics-reporting.md)时，从上下文数据`a.media.ad.podPosition`自动收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## 维度项目

每个项目都是整数值位置值(`0`、`1`、`2`、...) 在[广告开始](/help/implementation/events/ads/ad-start.md)报告。
