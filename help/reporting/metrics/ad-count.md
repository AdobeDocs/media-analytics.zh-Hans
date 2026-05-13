---
title: 广告计数
description: 报告在会话期间开始的广告数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# 广告计数

**广告计数**&#x200B;量度报告会话期间开始的广告数。 使用它可按内容、渠道或流类型了解广告加载。 对于由广告维度（广告商、促销活动、创意）透视的广告开始计数，请使用启用广告变量类别时可用的广告开始量度。

## 如何计算此指标

会话期间每收到`media.adStart`个事件，媒体后端就会递增`mediaReporting.sessionDetails.adCount`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.adCount`映射到自定义事件的[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （处理规则将`a.media.adCount`映射到的自定义事件；请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
