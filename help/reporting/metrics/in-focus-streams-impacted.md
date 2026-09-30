---
title: 受聚焦影响的流数量
description: 计算播放器至少聚焦一次的会话数。
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
source-wordcount: '177'
ht-degree: 8%
---

# 受聚焦影响的流数量

>[!BEGINSHADEBOX]

*本页涵盖受焦点影响的&#x200B;**流**报表量度。 请参阅[焦点](/help/implementation/variables/player-state/in-focus.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

受聚焦影响的&#x200B;**流**&#x200B;量度计算播放器至少一次聚焦的会话数。 量度是会话级别的布尔值；同一会话中的多个焦点事件计为一个受影响的流。 对于焦点事件总数量，请使用[焦点计数](in-focus-count.md)。

## 如何计算此指标

媒体后端在会话期间第一次收到焦点状态开始事件时设置此标志。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.states.infocus.set`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "inFocus"`，字段`isSet` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.infocus.set` |
