---
title: 章节
description: 报告每个播放的唯一章节，由自动生成的章节ID作为键值。
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
source-wordcount: '196'
ht-degree: 9%
---

# 章节

**Chapter**&#x200B;维度报告每个播放的唯一章节，并以自动生成的章节ID作为键值。 ID由SDK或后端从内容ID、章节索引和章节开始时间构建，因此同一内容上同一章节的两个会话将汇总为单个行项目。 将维度用作章节级别分类（例如，章节名称、章节长度、章节偏移和章节位置）的联接键。

## 如何填充此维度

当触发[章节开始](/help/implementation/events/chapters/chapter-start.md)事件时，将自动生成章节ID。 该值不是直接设置的；它是从章节位置、偏移和内容ID派生的。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体章节]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.chapter.name`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 数据馈送 | `videochapter`, `post_videochapter` |
| Audience Manager | 不适用 |

## 维度项目

每个项目都是一个唯一的章节ID。 ID不透明（通常是内容ID +索引+偏移量的哈希），并且最可用作分组密钥。 与[章节名称](chapter-name.md)配对，以获得友好标签。
