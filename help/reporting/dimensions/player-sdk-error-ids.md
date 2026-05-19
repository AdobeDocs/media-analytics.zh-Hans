---
title: 播放器SDK错误ID
description: 报告内容播放器SDK生成的唯一错误标识符。
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

---


# 播放器SDK错误ID

**播放器SDK错误ID**&#x200B;维度报告内容播放器SDK在会话期间生成的唯一错误标识符。 播放器必须在实施时通过错误跟踪API提供代码或ID。 每个会话支持多个错误ID。

## 如何填充此维度

播放器在[错误](/help/implementation/events/error.md)事件时将播放器 — SDK错误ID传递到跟踪器。 后端在整个会话中收集唯一ID，并在关闭调用时报告这些ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.playerSdkErrors`收集。 |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## 维度项目

每个项目都是播放器SDK生成的错误代码或ID。 跨实施使用稳定的分类，以便错误ID可以在会话间正确汇总。
