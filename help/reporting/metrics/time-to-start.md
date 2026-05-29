---
title: 开始时间（量度）
description: 报告跨会话总和平均值的启动时间。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 7%

---


# 开始时间（量度）

>[!BEGINSHADEBOX]

*本页涵盖&#x200B;**开始时间**&#x200B;指标。 Adobe Analytics从同一`a.media.qoe.timeToStart`上下文数据变量自动填充配对的[开始时间（维度）](/help/reporting/dimensions/time-to-start.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.timeToStart`字段，您可以将其用作维度或指标。 有关如何收集此变量，请参阅[开始时间](/help/implementation/variables/quality/time-to-start.md)。*

>[!ENDSHADEBOX]

**开始时间**&#x200B;量度报告跨会话的启动时间，适用于总和、平均值和百分位数汇总。 使用该量度计算报告时段内的平均启动时间，并比较不同内容、网络或播放器之间的启动性能。 Adobe会以秒为单位存储该值，并在摄取时从播放器报表中转换。

## 如何计算此指标

播放器在会话开始触发之前对QoE对象设置`timeToStart`。 后端报告关闭调用中的值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.qoe.timeToStart`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
