---
title: 流媒体量度概述
description: 了解如何在Adobe Analytics和Customer Journey Analytics中计算和组织流媒体量度。
feature: Metrics
role: User, Admin
source-git-commit: da289f8d425fcbaece42519a9ea7d061f80e4591
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 3%

---


# 流媒体量度概述

Streaming Media Analytics中的量度是由媒体后端计算的事件驱动计数和持续时间。 媒体播放器发送诸如会话开始、播放、ping和广告开始等事件；媒体后端处理这些事件并在会话关闭调用时最终确定量度值。

## 量度的计算方式

流媒体量度遵循四种主要计算模式：

* **事件触发的标志**：在符合条件的事件首次进入会话时设置此项。 主内容的[`play`](/help/implementation/events/playback/play.md)事件设置[[!UICONTROL 内容开始]](content-starts.md)标志；[`adStart`](/help/implementation/events/ads/ad-start.md)事件设置[[!UICONTROL 广告开始]](ad-starts.md)。 该标记在关闭调用中为每个会话报告一次，而不是为每个事件报告一次。

* **累计持续时间**：在特定播放状态为活动时，对Ping事件之间的间隔求和。 主内容播放时累积[[!UICONTROL 内容逗留时间]](content-time-spent.md)；广告播放时累积[[!UICONTROL 广告逗留时间]](ad-time-spent.md)。 Adobe建议的主内容ping间隔为10秒，广告期间为1秒，因此“逗留时间”量度的粒度与实施的ping间隔相同。

* **事件计数**：跟踪会话中的总发生次数。 质量量度，如[[!UICONTROL 缓冲事件]](buffer-events.md)、[[!UICONTROL 比特率更改]](bitrate-changes.md)、[[!UICONTROL 错误事件]](error-events.md)和[[!UICONTROL 暂停事件]](pause-events.md)等，会计算每次发生的情况，而不只是第一次发生的情况。

* **受影响的流**：如果相应的事件在会话期间的任何时间发生，则会话级别标志设置为1，而不管发生次数。 使用这些量度测量范围，同时使用事件计数量度测量严重性。 例如，您可以使用[[!UICONTROL 受缓冲影响的流]](buffer-impacted-streams.md)来确定所有播放会话中受缓冲影响的会话比例。

## 按报告系统显示的可用性

| 报告系统 | 量度如何到达 |
| --- | --- |
| Adobe Analytics | 使用[上下文数据变量](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/vars/page-vars/contextdata)填充。 某些量度会自动使用这些上下文数据变量填充解决方案事件，而其他量度必须使用[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)映射到自定义事件。 自动填充值的量度必须首先启用各自的[流媒体报表包设置](../../implementation/media-sdk/setup/media-reports-enable.md)。 |
| Customer Journey Analytics | `xdm.mediaReporting.sessionDetails`和相关节点中的XDM字段，源自任何包含流媒体数据的数据集。 您必须使用[数据视图组件设置](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-dataviews/component-settings/overview)中的所需设置创建每个量度。 |
| 数据馈送 | 量度将作为事件ID显示在`event_list`和`post_event_list`列中。 每个源文件都包含一个`events.csv`文件，其中包含所有量度（包括流媒体量度）的查找。 |

>[!MORELIKETHIS]
>
>* [维度概述](../dimensions/overview.md)：流媒体维度参考
>* [计算量度](/help/reporting/calculated-metrics.md)：从上述基本量度生成的比例和派生量度
>* [参数映射](/help/implementation/parameters-mapping.md)：完成事件到列到XDM的引用
>* [事件概述](/help/implementation/events/overview.md)：推动量度计算的播放器事件
