---
title: 受停滞影响的流
description: 计算播放期间至少发生一次停滞的会话数。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%
---

# 受停滞影响的流

**Stall影响的流**&#x200B;量度计算播放期间至少发生一次停止的会话数。 量度是会话级别的布尔值；同一会话中的多个停止计为一个受影响的流。 对于总停止量，请使用[停止事件](stall-events.md)。

## 如何计算此指标

当在会话期间至少三个连续事件没有在主内容上记录播放头移动时，媒体后端设置此标志。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.qoe.stall`映射到自定义事件的[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （处理规则将`a.media.qoe.stall`映射到的自定义事件；请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
