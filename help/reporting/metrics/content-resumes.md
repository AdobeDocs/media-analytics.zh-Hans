---
title: 内容继续
description: 计算恢复先前中断的播放的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 7%

---


# 内容继续

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容继续**报告量度。 有关如何收集此变量，请参阅[内容继续](/help/implementation/variables/core/content-resumes.md)。*

>[!ENDSHADEBOX]

**Content继续**&#x200B;指标计算继续先前中断的播放的会话数。 当播放器在`sessionStart`上将会话标记为恢复时（例如，在缓冲、暂停或停止超过30分钟后），此值将递增。 使用它可将同一查看者和资产的正版新会话与后续会话区分开。

## 如何计算此指标

当`media.sessionStart`事件中的`mediaCollection.sessionDetails.hasResume`为`true`时，媒体后端设置`mediaReporting.sessionDetails.hasResume = true`。 播放器必须将会话明确标记为恢复。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.resume`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
