---
title: 为Edge实施设置报表
description: 配置Customer Journey Analytics以报告通过Edge Network收集的流媒体数据。
feature: Streaming Media
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 6%

---

# 为Edge实施设置报表

通过Edge Network实施流媒体收集后，配置Customer Journey Analytics以报告收集的数据。

>[!NOTE]
>
>本页介绍Customer Journey Analytics中的报表，这是Edge实施的推荐目标。 如果您的数据流将流媒体数据发送到Adobe Analytics，请参阅[为仅限Analytics的实施设置报表](analytics-reporting.md)。

* **先决条件**：完成Edge实施并收集一些数据。 请参阅[Edge实施概述](/help/implementation/edge/overview.md)和您选择的实施方法。

## 在 Customer Journey Analytics 中创建连接

1. 在Customer Journey Analytics中，按照[创建连接](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-connections/create-connection)中的说明创建连接。 创建连接时，请确保启用了&#x200B;**[!UICONTROL 导入所有新数据]**&#x200B;复选框。

## 在 Customer Journey Analytics 中创建数据视图

1. 在Customer Journey Analytics中，按照[创建或编辑数据视图](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/create-dataview)中的说明创建数据视图。

   1. 在&#x200B;**[!UICONTROL 连接]**&#x200B;字段中，选择您之前创建的连接。 新连接最多可能需要15分钟才能显示。

   1. 在&#x200B;**[!UICONTROL 组件]**&#x200B;选项卡的&#x200B;**[!UICONTROL 架构字段]**&#x200B;部分中，搜索下表中每个组件，并将其拖到相应的&#x200B;**[!UICONTROL 维度]**&#x200B;或&#x200B;**[!UICONTROL 量度]**&#x200B;面板中。 如果存在多个同名字段，请使用XDM路径确认正确的字段。 应用组件设置的&#x200B;**[!UICONTROL 上下文标签]**&#x200B;下拉列表中显示的上下文标签。

      | 组件 | 类型 | XDM 路径 | 上下文标签 |
      |---|---|---|---|
      | [内容](/help/reporting/dimensions/content.md) | 维度 | `mediaReporting.sessionDetails.name` | 媒体：内容ID |
      | [内容名称](/help/reporting/dimensions/content-name.md) | 维度 | `mediaReporting.sessionDetails.friendlyName` | 媒体：视频名称 |
      | [内容长度](/help/reporting/dimensions/content-length.md) | 维度 | `mediaReporting.sessionDetails.length` | 媒体：视频长度 |
      | [节目](/help/reporting/dimensions/show.md) | 维度 | `mediaReporting.sessionDetails.show` | 媒体：节目 |
      | [季](/help/reporting/dimensions/season.md) | 维度 | `mediaReporting.sessionDetails.season` | 媒体：季 |
      | [集](/help/reporting/dimensions/episode.md) | 维度 | `mediaReporting.sessionDetails.episode` | Media：集 |
      | 事件类型 | 维度 | `eventType` | 媒体：事件类型 |
      | [内容逗留时间](/help/reporting/metrics/content-time-spent.md) | 量度 | `mediaReporting.sessionDetails.timePlayed` | 媒体：内容逗留时间 |
      | [媒体逗留时间](/help/reporting/metrics/media-time-spent.md) | 量度 | `mediaReporting.sessionDetails.totalTimePlayed` | 媒体：媒体逗留时间 |
      | [总暂停持续时间](/help/reporting/metrics/total-pause-duration.md) | 量度 | `mediaReporting.sessionDetails.pauseTime` | 媒体：暂停总持续时间 |
      | [开始时间](/help/reporting/metrics/time-to-start.md) | 量度 | `mediaReporting.qoeDataDetails.timeToStart` | 媒体：开始时间 |
      | [总缓冲持续时间](/help/reporting/metrics/total-buffer-duration.md) | 量度 | `mediaReporting.qoeDataDetails.bufferTime` | 媒体：缓冲总持续时间 |
      | 媒体会话服务器超时 | 量度 | `mediaReporting.sessionDetails.secondsSinceLastCall` | 媒体：上次调用后经过的秒数 |

      >[!IMPORTANT]
      >
      >需要此表中的上下文标签才能使流媒体面板正常工作。 Customer Journey Analytics使用它们自动计算&#x200B;**并行查看者**&#x200B;和&#x200B;**播放耗时**&#x200B;派生指标（由[媒体并行查看者](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)和[媒体播放耗时](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)面板使用），并填充[媒体平均受众访问分钟数](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)面板中的报表选项。

      此时可以向数据视图添加任何其他[维度](/help/reporting/dimensions/overview.md)或[量度](/help/reporting/metrics/overview.md)。 每个页面都列出了该组件的XDM路径。

1. 选择&#x200B;**[!UICONTROL 保存并继续]** → **[!UICONTROL 保存并完成]**&#x200B;以保存更改。

## 在Customer Journey Analytics中创建并配置项目

1. 在Customer Journey Analytics的&#x200B;**[!UICONTROL Workspace]**&#x200B;选项卡的&#x200B;**[!UICONTROL 项目]**&#x200B;区域，选择&#x200B;**[!UICONTROL 创建项目]**。

1. 选择&#x200B;**[!UICONTROL 空白项目]**→**[!UICONTROL 创建]**。

1. 在新项目中，选择您之前创建的数据视图。

   在项目中创建面板时，您可以使用添加到数据视图的任何组件。

1. 选择左边栏中的&#x200B;**面板**&#x200B;图标，然后拖入&#x200B;**[!UICONTROL 媒体平均受众访问分钟数]**、**[!UICONTROL 媒体并行查看者]**&#x200B;和&#x200B;**[!UICONTROL 媒体播放耗时]**&#x200B;面板。

1. （视情况而定）如果将自定义元数据添加到架构，请按照Customer Journey Analytics指南中的[持久性组件设置](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)中的说明设置自定义字段的持久性。

1. 按照[共享项目](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en)中的说明共享项目。

   >[!NOTE]
   >
   >如果要与共享的用户不可用，请确保这些用户在Adobe Admin Console中拥有Customer Journey Analytics的用户和管理员访问权限。

## Customer Journey Analytics中的可用媒体面板

Customer Journey Analytics中的Analysis Workspace包括三个专用媒体面板，面向具有流媒体收集加载项的客户。 这些面板提供了预建的可视化图表，可满足最常见的流媒体报表需求。

* **[媒体平均受众访问分钟数](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/average-minute-audience-panel)**：比较任意长度或类型的程序的平均内容使用量。 支持特定内容（基于持续时间）和自定义时段模式，并允许事后更新持续时间分类。
* **[媒体并行查看者](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers)**：分析一段时间内的并行查看者，以确定并发峰值和流失点。 支持可配置的粒度和按区段、维度或日期范围划分的系列。
* **[媒体播放耗时](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-workspace/panels/media-playback-time-spent)**：分析一段时间的播放持续时间，提供关于高峰期和低谷期的详细信息。 支持可配置的粒度和输出格式（小时或分钟）。

>[!MORELIKETHIS]
>
>* [维度概述](/help/reporting/dimensions/overview.md)
>* [量度概述](/help/reporting/metrics/overview.md)
