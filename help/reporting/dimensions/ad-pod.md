---
title: 广告pod
description: 报告每个唯一的广告时间，由自动生成的面板ID作为密钥。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 广告pod

**广告面板**&#x200B;维度报告每个唯一的广告时间，并以自动生成的面板ID作为键值。 会话中的每个广告都属于一个父广告面板，该面板将多个广告背对背播放。 使用该维度通过广告时间中断参与并作为[Pod名称](pod-name.md)和[Pod位置](pod-position.md)分类的联接键。

## 如何填充此维度

当触发[广告时间开始](/help/implementation/events/ads/ad-break-start.md)事件时，SDK会自动生成广告面板ID。 直接API实施通过中断索引和开始时间构建它，或提供自定义面板ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.pod`自动收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 数据馈送 | `videoadpod`, `post_videoadpod` |
| Audience Manager | 不适用 |

## 维度项目

每个项目都是一个唯一的广告面板ID。 该ID不透明（通常是会话ID、内容ID和中断索引的哈希），在与[Pod name](pod-name.md)结合使用时作为友好标签的分组键最有用。
