---
title: 广告完成
description: 计入每个播放到结束的广告。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# 广告完成

**广告完成**&#x200B;量度计算每个播放到结束的广告。 将其与[广告开始](ad-starts.md)配对，以计算广告完成率。

## 如何计算此指标

媒体后端在收到[广告结束](/help/implementation/events/ads/ad-complete.md)事件时设置此标志。 该量度将在广告关闭调用中报告。 跳过或放弃的广告不计为已完成。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/setup/analytics-reporting.md)时，从上下文数据`a.media.ad.complete`自动收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
