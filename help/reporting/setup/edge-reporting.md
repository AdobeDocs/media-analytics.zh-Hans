---
title: 为Edge实施设置报表
description: 配置Customer Journey Analytics以报告通过Edge Network收集的流媒体数据。
feature: Streaming Media
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 17%

---

# 为Edge实施设置报表

通过Edge Network实施流媒体收集后，配置Customer Journey Analytics以报告收集的数据。 本页介绍如何为流媒体创建连接、数据视图和项目。

>[!NOTE]
>
>本页介绍Customer Journey Analytics中的报表，这是Edge实施的推荐目标。 如果您的数据流将流媒体数据发送到Adobe Analytics，请参阅[为仅限Analytics的实施设置报表](analytics-reporting.md)。

* **先决条件**：完成Edge实施并收集一些数据。 请参阅[Edge实施概述](/help/implementation/edge/overview.md)和您选择的实施方法。

## 在 Customer Journey Analytics 中创建连接

1. 在Customer Journey Analytics中，按照[创建连接](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=zh-Hans)中的说明创建连接。

   创建连接时，流媒体需要以下选择：

   1. 选择在实施期间创建的数据集。

   1. 确保已启用&#x200B;**[!UICONTROL 导入所有新数据]**&#x200B;设置。

1. 继续[在Customer Journey Analytics](#create-a-data-view-in-customer-journey-analytics)中创建数据视图。

## 在 Customer Journey Analytics 中创建数据视图

1. 在Customer Journey Analytics中，按照[创建或编辑数据视图](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=zh-Hans)中的说明创建数据视图。

   1. 在&#x200B;**[!UICONTROL 连接]**&#x200B;字段中，选择您之前创建的连接。

      新连接可供选择之前最多可能需要15分钟。

   1. 在&#x200B;**[!UICONTROL 组件]**&#x200B;选项卡的&#x200B;**[!UICONTROL 架构字段]**&#x200B;部分中，搜索下表中每个组件并将其拖到&#x200B;**[!UICONTROL 量度]**&#x200B;面板中。 如果存在多个同名字段，请使用XDM路径确认正确的字段。

      **主内容 — 内容量度**

      | 组件名称 | XDM 路径 |
      |----------|---------|
      | 媒体开始 | mediaReporting.sessionDetails.isViewed |
      | 媒体区段查看次数 | mediaReporting.sessionDetails.hasSegmentView |
      | 内容开始 | mediaReporting.sessionDetails.isPlayed |
      | 内容结束 | mediaReporting.sessionDetails.isCompleted |
      | 内容逗留时间 | mediaReporting.sessionDetails.timePlayed |
      | 平均逗留时间 | mediaReporting.sessionDetails.totalTimePlayed |
      | 不重复播放时间 | mediaReporting.sessionDetails.uniqueTimePlayed |
      | 10% 进度标记 | mediaReporting.sessionDetails.hasProgress10 |
      | 平均受众访问分钟数 | mediaReporting.sessionDetails.averageMinuteAudience |

      **章节和广告 — 章节和广告量度**

      | 组件名称 | XDM 路径 |
      |----------|---------|
      | 章节开始 | mediaReporting.chapterDetails.isStarted |
      | 章节已完成 | mediaReporting.chapterDetails.isCompleted |
      | 章节播放时间 | mediaReporting.chapterDetails.timePlayed |
      | 广告开始 | mediaReporting.advertisingDetails.isStarted |
      | 广告已完成 | mediaReporting.advertisingDetails.isCompleted |
      | 广告播放时间 | mediaReporting.advertisingDetails.timePlayed |

      **QoE - QoE量度**

      | 组件名称 | XDM 路径 |
      |----------|---------|
      | 开始时间 | mediaReporting.qoeDataDetails.timeToStart |
      | 开始前丢帧 | mediaReporting.qoeDataDetails.isDroppedBeforeStart |
      | 受缓冲影响的流 | mediaReporting.qoeDataDetails.hasBufferImpactedStreams |
      | 受比特率更改影响的流 | mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams |
      | 比特率更改 | mediaReporting.qoeDataDetails.bitrateChangeCount |
      | 平均比特率 | mediaReporting.qoeDataDetails.bitrateAverage |
      | 丢帧 | mediaReporting.qoeDataDetails.droppedFrames |
      | 错误数 | mediaReporting.qoeDataDetails.errorCount |
      | 受错误影响的流 | mediaReporting.qoeDataDetails.hasErrorImpactedStreams |
      | 受丢帧影响的流 | mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams |

      **播放器状态 — 播放器状态量度**

      | 组件名称 | XDM 路径 |
      |----------|---------|
      | 播放器状态设置 | mediaReporting.states.isSet |
      | 播放器状态计数 | mediaReporting.states.count |
      | 播放器状态时间 | mediaReporting.states.time |

   1. 更新下表中组件的标签（在&#x200B;**[!UICONTROL 上下文标签]**&#x200B;下拉菜单中）。 搜索指标面板中尚未出现的任何组件，并将其拖到面板中。

      | 组件名称 | 上下文标签 |
      |---------|----------|
      | 媒体会话服务器超时 | 媒体：上次调用后经过的秒数 |
      | 平均逗留时间 | 媒体：媒体逗留时间 |
      | 缓冲总持续时间 | 媒体：缓冲总持续时间 |
      | 开始时间 | Media：开始时间 |
      | 暂停总持续时间 | 媒体：暂停总持续时间 |

   1. 要在项目中添加划分，请将以下维度添加到&#x200B;**[!UICONTROL 维度]**&#x200B;面板：

      | XDM 路径 | 组件名称 |
      |---------|----------|
      | mediaReporting.states.name | 播放器状态名称 |
      | mediaReporting.sessionDetails.ID | 媒体会话 ID |

      除了此表中的维度外，您还可以添加要在项目中按其筛选数据的任何其他维度。

1. 选择&#x200B;**[!UICONTROL 保存并继续]** > **[!UICONTROL 保存并完成]**&#x200B;以保存更改。

1. 继续[在Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics)中创建并配置项目。

## 在Customer Journey Analytics中创建并配置项目

1. 在Customer Journey Analytics的&#x200B;**[!UICONTROL Workspace]**&#x200B;选项卡的&#x200B;**[!UICONTROL 项目]**&#x200B;区域，选择&#x200B;**[!UICONTROL 创建项目]**。

1. 选择&#x200B;**[!UICONTROL 空白项目]** > **[!UICONTROL 创建]**。

1. 在新项目中，选择您之前创建的数据视图。

   在项目中创建面板时，您可以使用添加到数据视图的任何组件。

1. 选择左边栏中的&#x200B;**面板**&#x200B;图标，然后拖入&#x200B;**[!UICONTROL 媒体并行查看者]**&#x200B;面板和&#x200B;**[!UICONTROL 媒体播放耗时]**&#x200B;面板。

1. （视情况而定）如果将自定义元数据添加到架构，请按照Customer Journey Analytics指南中的[持久性组件设置](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)中的说明设置自定义字段的持久性。

1. 按照[共享项目](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=zh-Hans)中的说明共享项目。

   >[!NOTE]
   >
   >如果要与共享的用户不可用，请确保这些用户在Adobe Admin Console中拥有Customer Journey Analytics的用户和管理员访问权限。

>[!MORELIKETHIS]
>
>* Workspace中的[媒体面板](/help/reporting/workspace/media-concurrent-viewers-overview.md)
>* [维度概述](/help/reporting/dimensions/overview.md)
>* [量度概述](/help/reporting/metrics/overview.md)
