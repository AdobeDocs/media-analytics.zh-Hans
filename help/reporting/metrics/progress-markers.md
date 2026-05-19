---
title: 进度标记
description: 计算播放头超过五个固定阈值（10%、25%、50%、75%和95%）的会话数。
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 9%

---


# 进度标记

**进度标记**&#x200B;是五个单独的量度，用于计数播放头分别超过五个固定阈值（内容长度的10%、25%、50%、75%和95%）的会话。 使用它们绘制内容运行时中的流失图表；与[内容开始](content-starts.md)配对，以计算到达每个里程碑的已启动会话的份额。

每个标记器会在每个会话中触发一次，并且不会在回搜寻时触发。 向前搜索时跳过的标记不会被计数（例如，从5%跳转到60%的查看者同时触发10%、25%和50%标记）。

## 如何计算每个标记

媒体后端在每个事件后根据[内容长度](../dimensions/content-length.md)评估报告的播放头。 当播放头第一次超过阈值时，为会话的其余部分设置相应的标志。 这五个标记都会在收盘时报告。 从不在主内容上产生播放事件的会话（例如[开始前丢帧](/help/reporting/metrics/drops-before-start.md)）从不将播放头超过任何阈值，因此不设置标记。

>[!IMPORTANT]
>
>进度标记需要非零[内容长度](/help/reporting/dimensions/content-length.md)和准确的播放头报告。 如果内容长度未设置、为零或错误，则标记可能会在错误的时间触发，也可能根本不触发。

### 10%进度标记 {#progress-10}

当播放头首次达到内容长度的10%时触发。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.progress10`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.progress10` |

### 25%进度标记 {#progress-25}

当播放头首次达到内容长度的25%时触发。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.progress25`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.progress25` |

### 50%进度标记 {#progress-50}

在播放头首次达到内容长度的50%时触发。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.progress50`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.progress50` |

### 75%进度标记 {#progress-75}

当播放头首次达到内容长度的75%时触发。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.progress75`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.progress75` |

### 95%进度标记 {#progress-95}

当播放头首次达到内容长度的95%时触发。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.progress95`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.progress95` |
