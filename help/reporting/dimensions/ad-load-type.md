---
title: 广告加载次数
description: 报告用于每个流媒体会话的广告加载类型。
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
source-wordcount: '161'
ht-degree: 8%
---

# 广告加载次数

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**广告加载**&#x200B;报告维度。 有关如何收集此变量，请参阅[广告加载类型](/help/implementation/variables/standard-metadata/ad-load-type.md)。*

>[!ENDSHADEBOX]

**广告加载**&#x200B;维度报告在每个流媒体会话开始时加载的广告类型。 该值由客户定义，允许组织按其广告投放机制（例如，`"linear"`、`"dynamic"`或`"programmatic"`）对会话进行分类。

## 如何填充此维度

广告加载类型由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 配置[[!UICONTROL 流媒体]](/help/reporting/setup/analytics-reporting.md)时自动从上下文数据`a.media.adLoad`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## 维度项目

每一项都是会话开始时设置的文字广告加载类型字符串。 值不受标准枚举的限制。 定义在您的实施中一致的分类，以便值可以预测地汇总在报表中。
