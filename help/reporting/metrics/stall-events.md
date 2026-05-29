---
title: 停止事件
description: 计算各个会话的总和平均值的停滞事件。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 7%

---


# 停止事件

**Stall事件**&#x200B;量度计算跨会话的延迟事件，适用于总和、平均值和百分位数汇总。 使用该量度计算报告时段内的总停滞量，并比较内容、网络或播放器之间的停滞稳定性。

在Customer Journey Analytics中，`xdm.mediaReporting.qoeDataDetails.stallCount`可用作指标或维度，而无需单独的维度组件。

## 如何计算此指标

每次在主内容上至少三个连续事件没有记录播放头移动时，媒体后端递增计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.qoe.stallCount`映射到自定义事件的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （处理规则将`a.media.qoe.stallCount`映射到的自定义事件；请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

对于会话级别的布尔报表（无论是否发生任何停顿），请使用[受停顿影响的流](stall-impacted-streams.md)。
