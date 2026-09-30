---
title: 已授权
description: 计算用户已通过Adobe Pass获得授权的会话数。
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
source-wordcount: '137'
ht-degree: 12%
---

# 已授权

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**已授权**&#x200B;报告量度。 请参阅[Authorized](/help/implementation/variables/standard-metadata/authorized.md)以了解如何收集此变量。*

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
