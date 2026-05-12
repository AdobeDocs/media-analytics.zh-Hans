---
title: 联合数据
description: 联合数据计算通过联合数据共享而不是客户自己的实施接收的会话。
feature: Metrics
role: User, Admin
source-git-commit: c9c4287b4b330ebc1a1ec8b7197b42ee45f7ff48
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 5%

---


# 联合数据

>[!AVAILABILITY]
>
>Federated Analytics服务仅在通过Adobe Analytics使用流媒体功能时可用。 Federated Analytics在Customer Journey Analytics中不可用。

**联合数据**&#x200B;量度计数通过联合数据共享接收的会话，而不是从您自己的实施接收的会话。 使用它衡量合作伙伴共享会话的数量，并将参与度、完成度或质量与第一方会话进行比较。

有关详细信息，请参阅[联合媒体](/help/use-cases/federated-media.md)用例。

>[!TIP]
>
>如果要将联合数据用作维度，请创建一个[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)，该规则会将`a.media.federated`上下文数据变量映射到eVar。

## 如何计算此指标

当会话通过联合通道到达时，媒体后端设置`mediaReporting.sessionDetails.isFederated = true`。 该指标会在每个符合条件的会话中递增一次，并在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.federated`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
