---
title: 广告加载次数
description: 报告用于每个流媒体会话的广告加载类型。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## 维度项目

每一项都是会话开始时设置的文字广告加载类型字符串。 值不受标准枚举的约束 — 定义跨实施一致的分类，以便值在报表中以可预见的方式汇总。
