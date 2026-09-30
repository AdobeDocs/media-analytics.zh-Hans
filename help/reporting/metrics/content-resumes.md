---
title: 内容继续
description: 计算恢复先前中断的播放的会话数。
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
source-wordcount: '171'
ht-degree: 9%
---

# 内容继续

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容继续**报告量度。 有关如何收集此变量，请参阅[内容继续](/help/implementation/variables/core/content-resumes.md)。*

>[!ENDSHADEBOX]

**Content继续**&#x200B;指标计算继续先前中断的播放的会话数。 当播放器在`sessionStart`上将会话标记为恢复时（例如，在缓冲、暂停或停止超过30分钟后），此值将递增。 使用它可将同一查看者和资产的正版新会话与后续会话区分开。

## 如何计算此指标

当`xdm.mediaCollection.sessionDetails.hasResume`在[会话开始](/help/implementation/events/session/session-start.md)事件中为`true`时，媒体后端会设置此标志。 播放器必须将会话明确标记为恢复。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.resume`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | 不适用 |
