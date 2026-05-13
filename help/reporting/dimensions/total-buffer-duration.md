---
title: 缓冲总持续时间（维度）
description: 报告每个会话缓冲所花费的累积秒数。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 5%

---


# 缓冲总持续时间（维度）

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**总缓冲持续时间**&#x200B;维度。 Adobe Analytics从同一`a.media.qoe.bufferTime`上下文数据变量自动填充配对的[总缓冲持续时间（指标）](/help/reporting/metrics/total-buffer-duration.md)。 Customer Journey Analytics公开单个`mediaReporting.qoeDataDetails.bufferTime`字段，您可以将其用作维度或指标。*

>[!ENDSHADEBOX]

**缓冲总持续时间**&#x200B;维度报告播放器在会话期间处于缓冲状态的累计时间（以秒为单位）。 使用维度可按精确的缓冲持续时间值划分参与度。

## 如何填充此维度

媒体后端计算每个缓冲时间间隔（从`media.bufferStart`到下一个状态更改）的持续时间总和。 此值在关闭调用中报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.bufferTime`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoebuffertimeevar, post_videoqoebuffertimeevar` |

## 维度项目

每个项目都是在关闭调用中报告的文字持续时间值（以秒为单位）。
