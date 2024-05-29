---
title: 安装Media Analytics和Experience Platform边缘
description: 了解如何使用Experience Platform Edge实施Adobe流媒体。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: 39869d5eeea02e81c204d995ac158b3e7b7541c7
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 9%

---

# 安装Media Analytics和Experience Platform边缘

Adobe Experience Platform Edge 允许您将发送到多个产品的数据发送到一个集中的位置。 Experience Edge 将适当的信息转发给所需的产品。 此概念允许您整合实施工作，尤其是跨多个数据解决方案进行整合。

下图说明了Media Analytics实施可以如何使用Experience PlatformEdge在Analysis Workspace中使数据在Adobe Analytics或Customer Journey Analytics中可用：

![CJA 工作流](assets/streaming-media-edge.png)

有关所有实施选项(包括不使用Experience Platform边缘的实施方法)的概述，请参阅 [实施Streaming Media for Adobe Analytics或Customer Journey Analytics](/help/implementation/overview.md).

无论您是使用Adobe Experience Platform Web SDK、Adobe Experience Platform Mobile SDK、Adobe Experience Platform Roku SDK还是API来使用Experience Edge实施流媒体，都必须首先完成以下部分：

## 在Adobe Experience Platform中设置架构

为了标准化数据收集以在利用 Adobe Experience Platform 的应用程序中使用，Adobe 创建了开放且公开记录的标准，即体验数据模型 (XDM)。

创建和设置方案：

1. 在Adobe Experience Platform中，开始创建架构，如中所述 [在UI中创建和编辑架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

1. 在创建方案时，在“方案详细资料”页上，选择 [!UICONTROL **体验事件**] 在为架构选择基类时。

   ![已添加字段组](assets/schema-experience-event.png)

1. 选择&#x200B;[!UICONTROL **下一步**]。

1. 指定架构显示名称和说明，然后选择 [!UICONTROL **完成**].

1. 在 [!UICONTROL **合成**] 区域，在 [!UICONTROL **字段组**] 部分，选择 [!UICONTROL **添加**]，然后搜索并将以下新字段组添加到该架构中：
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   添加字段组后，它们应显示在 [!UICONTROL **字段组**] 部分，如下所示：

   ![已添加字段组](assets/schema-field-groups-added.png)

1. 选择 [!UICONTROL **保存**] 以保存更改。

1. （可选）您可以隐藏Media Edge API未使用的某些字段。 隐藏这些字段使架构更易于阅读和理解，但并非必需。 这些字段仅指以下内容： `MediaAnalytics Interaction Details` 字段组。

+++ 展开此处可查看有关可隐藏字段的说明。

   1. 在 [!UICONTROL **结构**] 区域，选择 `Media Collection Details` 字段，然后选择 [!UICONTROL **管理相关字段**].

      ![管理相关字段](assets/manage-related-fields.png)

   1. 启用该选项 [!UICONTROL **显示字段的显示名称**]，然后更新架构，如下所示：

      * 在 `Media Collection Details` > `Advertising Details` 字段中，隐藏以下报表字段： `Ad Completed`， `Ad Started`、和 `Ad Time Played`.

      * 在 `Media Collection Details` > `Advertising Pod Details` 字段中，隐藏以下报表字段： `Ad Break ID`

      * 在 `Media Collection Details` > `Chapter Details` 字段中，隐藏以下报表字段： `Chapter Completed`， `Chapter ID`， `Chapter Started`、和 `Chapter Time Played`.

      * 在 `Media Collection Details` 字段，隐藏 `List Of States` 字段。

        ![隐藏媒体收集状态](assets/schema-hide-media-collection-states.png)

      * 在 `Media Collection Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 字段中，隐藏以下报表字段： `Player State Count`， `Player State Set`、和 `Player State Time`.

        ![要隐藏的字段](assets/schema-hide-listofstates.png)

      * 在 `Media Collection Details` > `Qoe Data Details` 字段中，隐藏以下报表字段： `Average Bitrate`， `Average Bitrate Bucket`， `Bitrate Change Impacted Streams`， `Bitrate Changes`， `Buffer Impacted Streams`， `Buffer Events`， `Dropped Frame Impacted Streams`， `Drops Before Starts`， `Errors`， `External Error IDs`， `Error Impacted Streams`， `Media SDK Error IDs`， `Player SDK Error IDs`， `Stalling Impacted Streams`， `Stalling Events`， `Total Buffer Duration`、和 `Total Stalling Duration`.

      * 在 `Media Collection Details` > `Session Details` 字段中，隐藏以下报表字段： `10% Progress Marker`， `25% Progress Marker`， `50% Progress Marker`， `75% Progress Marker`， `95% Progress Marker`， `Ad Count`， `Average Minute Audience`， `Content Completes`， `Chapter Count`， `Content Starts`， `Content Time Spent`， `Estimated Streams`， `Federated Data`， `Media Segment Views`， `Media Downloaded Flag`， `Media Starts`， `Media Session ID`， `Media Session Server Timeout`， `Media Time Spent`， `Pause Events`， `Pause Impacted Streams`， `Pev3`， `Pccr`， `Total Pause Duration`， `Unique Time Played`、和 `Video Segment`.

   1. 选择 [!UICONTROL **确认**] 以保存更改。

   1. 在 [!UICONTROL **结构**] 区域，启用选项 [!UICONTROL **显示字段的显示名称**]，然后选择 `List Of Media Collection Downloaded Content Events` 字段。

   1. 选择 [!UICONTROL **管理相关字段**]，然后更新架构，如下所示：


      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 字段中，隐藏以下报表字段： `Ad Completed`， `Ad Started`、和 `Ad Time Played`.

      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 字段中，隐藏以下报表字段： `Ad Break ID`

      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 字段中，隐藏以下报表字段： `Chapter Completed`， `Chapter ID`， `Chapter Started`、和 `Chapter Time Played`.

      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` 字段，隐藏 `List Of States` 字段。

      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 字段中，隐藏以下报表字段： `Player State Count`， `Player State Set`、和 `Player State Time`.

      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 字段中，隐藏以下报表字段： `Average Bitrate`， `Average Bitrate Bucket`， `Bitrate Change Impacted Streams`， `Bitrate Changes`， `Buffer Events`， `Buffer Impacted Streams`， `Drops Before Starts`， `Dropped Frame Impacted Streams`， `Error Impacted Streams`， `Errors`， `External Error IDs`， `Media SDK Error IDs`， `Player SDK Error IDs`， `Stalling Events`， `Stalling Impacted Streams`， `Total Buffer Duration`、和 `Total Stalling Duration`.

      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 字段中，隐藏以下报表字段： `10% Progress Marker`， `25% Progress Marker`， `50% Progress Marker`， `75% Progress Marker`， `95% Progress Marker`， `Ad Count`， `Average Minute Audience`， `Chapter Count`， `Content Completes`， `Content Starts`， `Content Time Spent`， `Estimated Streams`， `Federated Data`， `Media Downloaded Flag`， `Media Segment Views`， `Media Session ID`， `Media Session Server Timeout`， `Media Starts`， `Media Time Spent`， `Pause Events`， `Pause Impacted Streams`， `Pccr`， `Pev3`， `Total Pause Duration`， `Unique Time Played`、和 `Video Segment`.

      * 在 `List Of Media Collection Downloaded Content Events` > `Media Details`  字段，隐藏 `Media Session ID` 字段。

   1. 选择 [!UICONTROL **确认**] 以保存更改。

   1. 在 [!UICONTROL **结构**] 区域，选择 `Media Reporting Details` 字段，选择 [!UICONTROL **管理相关字段**].

   1. 启用该选项 [!UICONTROL **显示字段的显示名称**]，然后更新架构，如下所示：

      * 在 `Media Reporting Details` 字段中，隐藏以下字段： `Error Details`， `List Of States End`， `List of States Start`、和 `Media Session ID`.

   1. 选择 [!UICONTROL **确认**] > [!UICONTROL **保存**]  以保存更改。

1. 继续 [在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform).

## 在Adobe Experience Platform中创建数据集

1. 请确保按照中的说明设置架构 [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform).

1. 在Adobe Experience Platform中，按照中的说明开始创建数据集 [数据集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh_Hans#create).

   为数据集选择架构时，请选择之前创建的架构，如中所述 [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform).

1. 继续 [在Customer Journey Analytics中配置数据流](#configure-a-datastream-in-adobe-experience-platform).

## 在Adobe Experience Platform中配置数据流

1. 请确保已按照中的说明创建数据集 [在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform).

1. 创建新数据流，如中所述 [配置数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hans).

   创建数据流时，请确保您进行了以下配置选择：

   * 在 [!UICONTROL **事件架构**] 字段创建数据流时，请确保选择您在中创建的架构 [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform). 选择&#x200B;[!UICONTROL **保存**]。

     >[!IMPORTANT]
     >
         >不选择 [!UICONTROL **保存并添加映射**] 因为这样做会导致时间戳字段出现映射错误。
     
     ![创建数据流并选择架构](assets/datastream-create-schema.png)

   * 根据您使用的是Adobe Analytics还是Customer Journey Analytics，将以下任一服务添加到数据流：

      * [!UICONTROL **Adobe Analytics**] (如果使用Adobe Analytics)

        如果您使用的是Adobe Analytics，请确保您定义了报表包，如中所述 [创建报表包](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

      * [!UICONTROL **Adobe Experience Platform**] (如果使用Customer Journey Analytics)

     有关如何将服务添加到数据流的信息，请参阅中的“将服务添加到数据流”部分 [配置数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

     ![添加Adobe Analytics服务](assets/datastream-add-service.png)

   * 展开 [!UICONTROL **高级选项**]，然后启用 [!UICONTROL **媒体分析**] 选项。

     ![媒体分析选项](assets/datastream-media-check.png)

1. 您现在可以实施 [Media Edge API](/help/implementation/edge/implementation-edge-api.md) 或 [Media Edge SDK](/help/implementation/edge/edge-mobile-sdk.md) 以开始收集media analytics数据。

   收集一些数据后，您可以 [在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics).

## 在 Customer Journey Analytics 中创建连接

>[!NOTE]
>
>只有在使用Customer Journey Analytics时，才需要执行以下过程。


1. 确保已按照中的说明创建数据流 [在Customer Journey Analytics中配置数据流](#configure-a-datastream-in-adobe-experience-platform).

1. 在Customer Journey Analytics中，创建连接，如中所述 [创建连接](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=zh-Hans).

   创建连接时，需要以下配置选择才能实施流媒体：

   1. 选择您之前创建的数据集，如中所述 [在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform).

   1. 确保 [!UICONTROL **导入所有新数据**] 设置已启用。

1. 继续 [在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics).

## 在Customer Journey Analytics中创建数据视图

>[!NOTE]
>
>只有在使用Customer Journey Analytics时，才需要执行以下过程。

1. 请确保在Customer Journey Analytics中创建了连接，如中所述 [在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics).

1. 在客户历程分析中，创建数据视图，如中所述 [创建或编辑数据视图](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=zh-Hans).

   创建数据视图时，需要以下配置选择才能实施流媒体：

   1. 在 [!UICONTROL **连接**] 字段中，选择您之前创建的连接，如中所述 [在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics).

      最多可能需要15分钟才能选择您创建的连接。

   1. 在 [!UICONTROL **组件**] 选项卡，在 [!UICONTROL **架构字段**] 部分，搜索下表列出的每个组件，并将其拖到 [!UICONTROL **量度**] 面板。 如果存在多个同名字段，请使用XDM路径以确保它是正确的字段。

      **主要内容 — 内容量度**

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


   1. 更新标签(在 [!UICONTROL **上下文标签**] 下拉菜单)中列出的所有组件。 搜索指标面板中尚未出现的任何组件，并将其拖到面板中。

      | 组件名称 | 上下文标签 |
      |---------|----------|
      | 媒体会话服务器超时 | 媒体：上次调用后经过的秒数 |
      | 平均逗留时间 | 媒体：媒体逗留时间 |
      | 缓冲总持续时间 | 媒体：缓冲总持续时间 |
      | 开始时间 | Media：开始时间 |
      | 暂停总持续时间 | 媒体：暂停总持续时间 |

   1. 要将划分添加到Customer Journey Analytics项目，请将以下维度添加到 [!UICONTROL **Dimension**] 面板：

      | XDM 路径 | 组件名称 |
      |---------|----------|
      | mediaReporting.states.name | 播放器状态名称 |
      | mediaReporting.sessionDetails.ID | 媒体会话 ID |

      除了此表中的维外，您还可以添加任何其他要用于在Customer Journey Analytics项目中过滤数据的维。

1. 选择 [!UICONTROL **保存并继续**] > [!UICONTROL **保存并完成**] 以保存更改。

1. 继续 [在Customer Journey Analytics中创建并配置项目](#create-and-configure-a-project-in-customer-journey-analytics).

## 在Customer Journey Analytics中创建并配置项目

1. 确保您已按照中的说明在Customer Journey Analytics中创建数据视图 [在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics).

1. 在Customer Journey Analytics中，在 [!UICONTROL **工作区**] 选项卡，在 [!UICONTROL **项目**] 区域，选择 [!UICONTROL **创建项目**].

1. 选择 [!UICONTROL **空白项目**] > [!UICONTROL **创建**].

1. 在新项目中，选择您之前创建的数据视图。

   在项目中创建面板时，您可以使用添加到数据视图的任何组件，如中所述 [在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics).

   以下4个面板是您可以创建的面板示例：

   ![主内容面板](assets/main-content-panel.png)

   ![章节和广告面板](assets/chapter-and-ads-panel.png)

   ![QoE面板](assets/qoe-panel.png)

   ![平板状态面板](assets/player-state-panel.png)

1. 选择 **面板** 图标，然后拖入 [!UICONTROL **媒体并行查看者**] 面板和 [!UICONTROL **媒体播放耗时**] 面板。

   这两个面板应当如下所示：

   ![“媒体并行查看者”面板](assets/media-concurrent-viewers-panels.png)

   ![“媒体播放耗时”面板](assets/media-playback-time-spent-panels.png)

1. 按照中的说明共享项目 [共享项目](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   如果要与共享的用户不可用，请确保这些用户具有在Adobe Admin Console中Customer Journey Analytics的用户和管理员访问权限。

1. 继续 [将数据发送到Experience Platform边缘](#send-data-to-experience-platform-edge).

## 将数据发送到Experience Platform边缘

根据要发送到Experience Platform边缘的数据类型，您可以使用以下任一方法：

### Web：使用Adobe Experience Platform Web SDK



### Mobile：使用Adobe Experience Platform Mobile SDK

使用以下文档资源完成iOS和Android的实施：

* [入门指南](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API 参考](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [迁移到Adobe Streaming Media for Edge Network扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku：Adobe Experience Platform Roku SDK

* [入门指南](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main)

* [迁移到Adobe Streaming Media for Edge Network扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API： Web和其他

API是当前唯一受支持的将Web数据发送到Experience Platform边缘的方法。

如果您要使用Edge API的自定义实施，则该API也可用。

有关media Edge API的更多信息，请参阅以下资源：

* [Media Edge API概述](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html)

* [Media Edge API快速入门](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html)

* [Media Edge API疑难解答指南](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html)

* [使用适用于Media Edge API的Open API规范文件](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/swagger.html)
