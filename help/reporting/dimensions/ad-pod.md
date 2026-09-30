---
title: 广告pod
description: 报告每个唯一的广告时间，由自动生成的面板ID作为密钥。
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
source-wordcount: '197'
ht-degree: 8%
---

# 广告pod

**广告面板**&#x200B;维度报告每个唯一的广告时间，并以自动生成的面板ID作为键值。 会话中的每个广告都属于一个父广告面板，该面板将多个广告背对背播放。 使用该维度通过广告时间中断参与并作为[Pod名称](pod-name.md)和[Pod位置](pod-position.md)分类的联接键。

## 如何填充此维度

当触发[广告时间开始](/help/implementation/events/ads/ad-break-start.md)事件时，SDK会自动生成广告面板ID。 直接API实施通过中断索引和开始时间构建它，或提供自定义面板ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/setup/analytics-reporting.md)时，从上下文数据`a.media.ad.pod`自动收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 数据馈送 | `videoadpod`, `post_videoadpod` |
| Audience Manager | 不适用 |

## 维度项目

每个项目都是一个唯一的广告面板ID。 该ID不透明（通常是会话ID、内容ID和中断索引的哈希），在与[Pod name](pod-name.md)结合使用时作为友好标签的分组键最有用。
