---
title: 缓冲事件（维度）
description: 报告每个会话的缓冲事件计数。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---


# 缓冲事件（维度）

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**缓冲事件**&#x200B;维度。 Adobe Analytics从同一`a.media.qoe.bufferCount`上下文数据变量自动填充配对的[缓冲事件（指标）](/help/reporting/metrics/buffer-events.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.bufferCount`字段，您可以将其用作维度或指标。*

>[!ENDSHADEBOX]

**缓冲事件**&#x200B;维度报告会话期间发生的缓冲事件计数。 使用维度可按确切缓冲计数划分参与度。

## 如何填充此维度

每次播放器进入`buffer`状态时，媒体后端都会递增计数。 此值在关闭调用中报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.bufferCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## 维度项目

每个项目都是关闭调用中报告的文字缓冲计数值。 对于会话级别的布尔报表（会话是否遇到任何缓冲），请使用[受缓冲影响的流](/help/reporting/metrics/buffer-impacted-streams.md)。
