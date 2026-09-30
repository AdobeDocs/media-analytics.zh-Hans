---
title: 预计的流
description: 近似于每个会话的音频或视频流数量。
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
source-wordcount: '190'
ht-degree: 10%
---

# 预计的流

**预计的流**&#x200B;量度与每个会话的音频或视频流数量相近，每30分钟播放一次就会计算一个流。 它旨在用于内容联合协议，并达到大约30分钟消费块计为单独“流”的状态。

## 如何计算此指标

媒体后端将此量度计算为`FLOOR(totalTimePlayed / 1800) + 1`，其中`totalTimePlayed`是[媒体逗留时间](media-time-spent.md)秒。 该量度在结束调用时报告。

| 媒体逗留时间 | 预计的流 |
| --- | --- |
| 0-29分钟 | 1 |
| 30-59分钟 | 2 |
| 60-89分钟 | 3 |
| 90分钟以上 | 4+ |

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.estimatedStreams`映射到自定义事件的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （处理规则将`a.media.estimatedStreams`映射到的自定义事件；请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
