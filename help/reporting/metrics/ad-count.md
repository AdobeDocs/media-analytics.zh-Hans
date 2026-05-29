---
title: 广告计数
description: 报告在会话期间开始的广告数。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 9%

---


# 广告计数

**广告计数**&#x200B;量度报告会话期间开始的广告数。 使用它可按内容、渠道或流类型了解广告加载。 对于由广告维度（广告商、促销活动、创意）透视的广告开始计数，请使用启用广告变量类别时可用的广告开始量度。

## 如何计算此指标

媒体后端在会话期间每收到[广告开始](/help/implementation/events/ads/ad-start.md)事件就递增此计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.adCount`映射到自定义事件的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （处理规则将`a.media.adCount`映射到的自定义事件；请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | 不适用 |
