---
title: 总停滞持续时间
description: 报告跨会话总和平均值的累计停滞时间。
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
source-wordcount: '210'
ht-degree: 7%
---

# 总停滞持续时间

**总停滞持续时间**&#x200B;量度报告跨会话的累积停滞时间，适用于总计、平均值和百分位数汇总。 使用该量度可计算查看者在报表时段内等待停止播放所花费的总时间。

在Customer Journey Analytics中，`xdm.mediaReporting.qoeDataDetails.stallTime`可用作指标或维度，而无需单独的维度组件。

## 如何计算此指标

媒体后端加总每个停止间隔的持续时间，当在主内容上至少三个连续事件没有记录播放头移动时检测该持续时间。 该量度在结束调用时报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.qoe.stallTime`映射到自定义事件的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （处理规则将`a.media.qoe.stallTime`映射到的自定义事件；请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
