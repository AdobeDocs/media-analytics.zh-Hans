---
title: 外部错误Id
description: 报告来自外部源的唯一错误标识符，如CDN错误。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# 外部错误Id

**外部错误ID**&#x200B;维度报告来自播放器SDK之外的任何源的唯一错误标识符（例如，CDN错误）。 播放器必须在实施时通过错误跟踪API提供代码或ID。 每个会话支持多个错误ID。

## 如何填充此维度

播放器在`media.error`事件时将外部错误ID传递到跟踪器。 后端在整个会话中收集唯一ID，并在关闭调用时报告这些ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.externalErrors`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoeextneralerrors` |

## 维度项目

每个项目都是播放器提供的错误代码或ID。 跨实施使用稳定的分类，以便错误ID可以在会话间正确汇总。
