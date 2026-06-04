---
title: 已授权
description: 计算用户已通过Adobe Pass获得授权的会话数。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 12%

---


# 已授权

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**已授权**报告量度。 请参阅[Authorized](/help/implementation/variables/standard-metadata/authorized.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**Authorized**&#x200B;指标计算用户已通过Adobe Pass或TV-Everywhere获得授权的会话。 与[MVPD](/help/reporting/dimensions/mvpd.md)维度配对，以按提供程序划分身份验证卷。

## 如何计算此指标

当播放器在会话开始时将会话标记为已授权时，媒体后端会增加计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.pass.auth`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.authorized`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.pass.auth` |
