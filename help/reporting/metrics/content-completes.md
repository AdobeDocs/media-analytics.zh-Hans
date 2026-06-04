---
title: 内容完成
description: 计算播放头到达内容结尾的会话数。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 10%

---


# 内容完成

**内容完成**&#x200B;指标计算播放头到达内容结尾的会话数。 将其与[Content starts](content-starts.md)配对，以计算完成率；将其与[Media starts](media-starts.md)配对，以计算端到端查看率。

## 如何计算此指标

当收到[会话完成](/help/implementation/events/session/session-complete.md)事件时，媒体后端会设置此标志。 该量度在结束调用时报告。 在没有显式`sessionComplete`的情况下超时的会话不计为完成。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.complete`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.complete` |
