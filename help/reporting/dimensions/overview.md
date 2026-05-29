---
title: 流媒体维度概述
description: 了解如何在Adobe Analytics和Customer Journey Analytics中填充和组织流媒体维度。
feature: Dimensions
role: User, Admin
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 6%

---


# 流媒体维度概述

通过Streaming Media Analytics中的维度，您可以按内容名称、流类型、广告名称和其他数十个属性对量度进行切片和过滤。 大多数由播放器在会话开始时设置，并持续到会话关闭。

## 维度的填充方式

流媒体维度遵循三个主要群体模式：

* **由媒体播放器提供**：大多数维度的源。 播放器在[会话开始](/help/implementation/events/session/session-start.md)调用中发送这些值，媒体后端将它们附加到会话中的每个后续事件。 播放器在会话开始时发送的内容是报表中显示的内容。 示例包括[[!UICONTROL 流类型]](/help/reporting/dimensions/stream-type.md)、[[!UICONTROL 内容名称]](/help/reporting/dimensions/content-name.md)和[[!UICONTROL 内容长度]](/help/reporting/dimensions/content-length.md)。

* **派生值**：媒体后端从累积播放状态而不是读取播放器提供的值计算的维度。 [[!UICONTROL 内容区段]](/help/reporting/dimensions/content-segment.md)是根据播放过程中的播放头位置计算的。 [[!UICONTROL 媒体路径]](/help/reporting/dimensions/media-path.md)在整个会话中跟踪内容和广告状态之间的过渡。 播放器无法覆盖这些维度。

* **分类**：可选。 您可以使用[分类集](https://experienceleague.adobe.com/zh-hans/docs/analytics/components/classifications/sets/overview) (Adobe Analytics)或[查找数据集](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/compare-aa-cja/upgrade-to-cja/create-datasets/cja-upgrade-dataset-lookup) (Customer Journey Analytics)来维护分类数据，而不是填充单独的维度。

## 按报告系统显示的可用性

| 报告系统 | 维度如何到达 |
| --- | --- |
| Adobe Analytics | 使用[上下文数据变量](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/vars/page-vars/contextdata)填充。 某些维度会自动使用这些上下文数据变量填充维度，而其他维度必须使用[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)填充。 自动填充值的维度必须首先启用各自的[流媒体报表包设置](../../implementation/media-sdk/setup/media-reports-enable.md)。 |
| Customer Journey Analytics | XDM字段通常位于`xdm.mediaReporting.sessionDetails`中，其来源为包含流媒体数据的任何数据集。 您必须使用[数据视图组件设置](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-dataviews/component-settings/overview)中的所需设置创建每个维度。 |
| 数据馈送 | 自动填充的维度具有其自己的数据馈送列名称（如`videostreamtype`、`videoname`或`videolength`）。 需要处理规则的维度使用`evar`列名。 |
| Audience Manager | 从Adobe Analytics转发的上下文数据。 仅在配置了Analytics到Audience Manager服务器端转发时可用。 |

>[!MORELIKETHIS]
>
>* [事件概述](/help/implementation/events/overview.md)：填充维度的播放器事件
>* [变量概述](/help/implementation/variables/overview.md)：事件携带到Adobe的数据
>* [量度概述](/help/reporting/metrics/overview.md)：变量填充的报表量度
