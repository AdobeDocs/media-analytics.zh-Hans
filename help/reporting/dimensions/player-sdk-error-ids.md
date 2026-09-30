---
title: 播放器SDK错误ID
description: 报告内容播放器SDK生成的唯一错误标识符。
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
source-wordcount: '159'
ht-degree: 8%
---

# 播放器SDK错误ID

**播放器SDK错误ID**&#x200B;维度报告内容播放器SDK在会话期间生成的唯一错误标识符。 播放器必须在实施时通过错误跟踪API提供代码或ID。 每个会话支持多个错误ID。

## 如何填充此维度

播放器在[错误](/help/implementation/events/error.md)事件时将播放器 — SDK错误ID传递到跟踪器。 后端在整个会话中收集唯一ID，并在关闭调用时报告这些ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.playerSdkErrors`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## 维度项目

每个项目都是播放器SDK生成的错误代码或ID。 跨实施使用稳定的分类，以便错误ID可以在会话间正确汇总。
