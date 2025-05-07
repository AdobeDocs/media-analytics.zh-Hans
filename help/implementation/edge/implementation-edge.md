---
title: 使用Edge Network实施流媒体收集
description: 了解如何使用Experience Platform Edge实施流媒体收集。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: dfdb1415-105e-4c41-bedc-ecb85ed1b1d9
source-git-commit: c7e9b7ca9dedbd0389240cb045d274ee6995ecbe
workflow-type: tm+mt
source-wordcount: '2146'
ht-degree: 9%

---

# 使用Edge Network实施流媒体收集

Adobe Experience Platform Edge Network 允许您将发送到多个产品的数据发送到一个集中的位置。 Experience Edge 将适当的信息转发给所需的产品。 此概念允许您整合实施工作，尤其是跨多个数据解决方案进行整合。

下图说明了如何实施Adobe流媒体收集，以便使用Experience Platform Edge在Adobe Analytics或Customer Journey Analytics中使Analysis Workspace中的数据可用：

![CJA 工作流](assets/streaming-media-edge.png)

有关所有实施选项的概述，包括不使用Experience Platform Edge的实施方法，请参阅[实施流媒体收集](/help/implementation/overview.md)。

无论您是使用Adobe Experience Platform Web SDK、Adobe Experience Platform Mobile SDK、Adobe Experience Platform Roku SDK还是API来使用Experience Edge实施流媒体收集，都必须首先完成以下部分：

## 在Adobe Experience Platform中设置架构

为了标准化数据收集以在利用 Adobe Experience Platform 的应用程序中使用，Adobe 创建了开放且公开记录的标准，即体验数据模型 (XDM)。

创建和设置方案：

1. 在Adobe Experience Platform中，按照[在UI中创建和编辑架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=zh-Hans)中的说明开始创建架构。

1. 在创建架构时，请在“架构详细信息”页面上，为架构选择基类时选择&#x200B;[!UICONTROL **体验事件**]。

   ![已添加字段组](assets/schema-experience-event.png)

1. 选择&#x200B;[!UICONTROL **下一步**]。

1. 指定架构显示名称和说明，然后选择&#x200B;[!UICONTROL **完成**]。

1. 在&#x200B;[!UICONTROL **构成**]&#x200B;区域的&#x200B;[!UICONTROL **字段组**]&#x200B;部分中，选择&#x200B;[!UICONTROL **添加**]，然后搜索并将以下新字段组添加到架构中：
   * `End User ID Details`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   添加字段组后，它们应显示在&#x200B;[!UICONTROL **字段组**]&#x200B;部分，如下所示：

   ![已添加字段组](assets/schema-field-groups-added.png)

1. 选择&#x200B;[!UICONTROL **保存**]&#x200B;以保存更改。

1. （可选）您可以隐藏Media Edge API未使用的某些字段。 隐藏这些字段使架构更易于阅读和理解，但并非必需。 这些字段仅引用`MediaAnalytics Interaction Details`字段组中的字段。

+++ 展开此处可查看有关可隐藏字段的说明。

   1. 在&#x200B;[!UICONTROL **结构**]&#x200B;区域中，选择`Media Collection Details`字段，然后选择&#x200B;[!UICONTROL **管理相关字段**]。

      ![管理相关字段](assets/manage-related-fields.png)

   1. 启用该选项以&#x200B;[!UICONTROL **显示字段**]&#x200B;的显示名称，然后按如下方式更新架构：

      * 在`Media Collection Details` > `Advertising Details`字段中，隐藏以下报表字段： `Ad Completed`、`Ad Started`和`Ad Time Played`。

      * 在`Media Collection Details` > `Advertising Pod Details`字段中，隐藏以下报告字段： `Ad Break ID`

      * 在`Media Collection Details` > `Chapter Details`字段中，隐藏以下报告字段： `Chapter Completed`、`Chapter ID`、`Chapter Started`和`Chapter Time Played`。

      * 在`Media Collection Details`字段中，隐藏`List Of States`字段。

        ![隐藏媒体收集状态](assets/schema-hide-media-collection-states.png)

      * 在`Media Collection Details` > `List Of States End`和`Media Collection Details` > `List Of States Start`字段中，隐藏以下报告字段： `Player State Count`、`Player State Set`和`Player State Time`。

        要隐藏的![字段](assets/schema-hide-listofstates.png)

      * 在`Media Collection Details` > `Qoe Data Details`字段中，隐藏以下报告字段： `Average Bitrate`、`Average Bitrate Bucket`、`Bitrate Change Impacted Streams`、`Bitrate Changes`、`Buffer Impacted Streams`、`Buffer Events`、`Dropped Frame Impacted Streams`、`Drops Before Starts`、`Errors`、`External Error IDs`、`Error Impacted Streams`、`Media SDK Error IDs`、`Player SDK Error IDs`、`Stalling Impacted Streams`、`Stalling Events`、`Total Buffer Duration`和`Total Stalling Duration`。

      * 在`Media Collection Details` > `Session Details`字段中，隐藏以下报告字段： `10% Progress Marker`、`25% Progress Marker`、`50% Progress Marker`、`75% Progress Marker`、`95% Progress Marker`、`Ad Count`、`Average Minute Audience`、`Content Completes`、`Chapter Count`、`Content Starts`、`Content Time Spent`、`Estimated Streams`、`Federated Data`、`Media Segment Views`、`Media Downloaded Flag`、`Media Starts`、`Media Session ID`、`Media Session Server Timeout`、`Media Time Spent`、`Pause Events`、`Pause Impacted Streams`、`Pev3`、`Pccr`、`Total Pause Duration`、`Unique Time Played`和`Video Segment`。

   1. 选择&#x200B;[!UICONTROL **确认**]&#x200B;以保存更改。

   1. 在&#x200B;[!UICONTROL **结构**]&#x200B;区域中，启用选项&#x200B;[!UICONTROL **显示字段的显示名称**]，然后选择`List Of Media Collection Downloaded Content Events`字段。

   1. 选择&#x200B;[!UICONTROL **管理相关字段**]，然后按如下方式更新架构：


      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details`字段中，隐藏以下报告字段： `Ad Completed`、`Ad Started`和`Ad Time Played`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details`字段中，隐藏以下报告字段： `Ad Break ID`

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details`字段中，隐藏以下报告字段： `Chapter Completed`、`Chapter ID`、`Chapter Started`和`Chapter Time Played`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details`字段中，隐藏`List Of States`字段。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End`和`Media Collection Details` > `List Of States Start`字段中，隐藏以下报告字段： `Player State Count`、`Player State Set`和`Player State Time`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details`字段中，隐藏以下报告字段： `Average Bitrate`、`Average Bitrate Bucket`、`Bitrate Change Impacted Streams`、`Bitrate Changes`、`Buffer Events`、`Buffer Impacted Streams`、`Drops Before Starts`、`Dropped Frame Impacted Streams`、`Error Impacted Streams`、`Errors`、`External Error IDs`、`Media SDK Error IDs`、`Player SDK Error IDs`、`Stalling Events`、`Stalling Impacted Streams`、`Total Buffer Duration`和`Total Stalling Duration`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details`字段中，隐藏以下报告字段： `10% Progress Marker`、`25% Progress Marker`、`50% Progress Marker`、`75% Progress Marker`、`95% Progress Marker`、`Ad Count`、`Average Minute Audience`、`Chapter Count`、`Content Completes`、`Content Starts`、`Content Time Spent`、`Estimated Streams`、`Federated Data`、`Media Downloaded Flag`、`Media Segment Views`、`Media Session ID`、`Media Session Server Timeout`、`Media Starts`、`Media Time Spent`、`Pause Events`、`Pause Impacted Streams`、`Pccr`、`Pev3`、`Total Pause Duration`、`Unique Time Played`和`Video Segment`。

      * 在`List Of Media Collection Downloaded Content Events` > `Media Details`字段中，隐藏`Media Session ID`字段。

   1. 选择&#x200B;[!UICONTROL **确认**]&#x200B;以保存更改。

   1. 在&#x200B;[!UICONTROL **结构**]&#x200B;区域，选择`Media Reporting Details`字段，选择&#x200B;[!UICONTROL **管理相关字段**]。

   1. 启用该选项以&#x200B;[!UICONTROL **显示字段**]&#x200B;的显示名称，然后按如下方式更新架构：

      * 在`Media Reporting Details`字段中，隐藏以下字段： `Error Details`、`List Of States End`、`List of States Start`和`Media Session ID`。

   1. 选择&#x200B;[!UICONTROL **确认**] > [!UICONTROL **保存**]&#x200B;以保存更改。

+++

1. （可选）您可以将自定义元数据添加到架构中。 这允许您包含其他用户定义的元数据，这些元数据可以根据特定需求或上下文进行自定义。 在现有架构未涵盖所需数据点的情况下，此灵活性非常有用。 (您还可以将自定义元数据与Media Edge API结合使用。 有关详细信息，请参阅[使用Media Edge API创建自定义元数据](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/custom-metadata/)。)

+++ 展开此处可查看有关如何将自定义元数据添加到架构的说明。

   1. 通过选择&#x200B;[!UICONTROL **帐户信息**] > [!UICONTROL **分配的组织**] > [!UICONTROL _**组织名称**_] > [!UICONTROL **租户**]，找到组织租户的名称。

      将通过此路径接收这些自定义字段。 (例如，租户名称： _dcbl → myCustomField path： _dcbl.myCustomField。)

   1. 将自定义字段组添加到您定义的媒体架构。

      ![add-custom-metadata](assets/add-custom-metadata-fieldgroup.png)

   1. 将您要跟踪的任何自定义字段添加到字段组。

      ![add-custom-metadata](assets/add-custom-fields.png)

   1. [为请求有效负载中的自定义字段使用生成的路径](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/ui/fields/overview#type-specific-properties)。

      ![add-custom-metadata](assets/custom-fields-path.png)

+++

1. 继续[在Adobe Experience Platform](#create-a-dataset-in-adobe-experience-platform)中创建数据集。

## 在 Adobe Experience Platform 中创建数据集

1. 请确保按照[在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform)中所述设置架构。

1. 在Adobe Experience Platform中，按照[数据集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh_Hans#create)中的说明开始创建数据集。

   为数据集选择架构时，请选择您之前创建的架构，如[在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform)中所述。

1. 继续[在Customer Journey Analytics](#configure-a-datastream-in-adobe-experience-platform)中配置数据流。

## 在Adobe Experience Platform中配置数据流

1. 请确保按照[在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform)中的说明创建了数据集。

1. 按照[配置数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hans)中的说明创建新数据流。

   创建数据流时，请确保您进行了以下配置选择：

   * 创建数据流时，在&#x200B;[!UICONTROL **事件架构**]&#x200B;字段中，确保选择您在[中创建的架构。在Adobe Experience Platform](#set-up-the-schema-in-adobe-experience-platform)中设置架构。 选择&#x200B;[!UICONTROL **保存**]。

     >[!IMPORTANT]
     >
     >请勿选择&#x200B;[!UICONTROL **保存并添加映射**]，因为这样做会导致时间戳字段出现映射错误。

     ![创建数据流并选择架构](assets/datastream-create-schema.png)

   * 根据您使用的是Adobe Analytics还是Customer Journey Analytics，将以下任一服务添加到数据流：

      * [!UICONTROL **Adobe Analytics**] (如果使用Adobe Analytics)

        如果您使用的是Adobe Analytics，请确保定义报表包，如[创建报表包](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite)中所述。

      * [!UICONTROL **Adobe Experience Platform**] (如果使用Customer Journey Analytics)

     有关如何将服务添加到数据流的信息，请参阅[配置数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hans#view-details)中的“将服务添加到数据流”部分。

     ![添加Adobe Analytics服务](assets/datastream-add-service.png)

      * 展开&#x200B;[!UICONTROL **高级选项**]，然后启用&#x200B;[!UICONTROL **Media Analytics**]&#x200B;选项。

     ![Media Analytics选项](assets/datastream-media-check.png)

1. 您现在可以实施[Media Edge API](/help/implementation/edge/implementation-edge-api.md)或[Media Edge SDK](/help/implementation/edge/edge-mobile-sdk.md)以开始收集媒体分析数据。

   收集一些数据后，您可以[在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics)。

## 在 Customer Journey Analytics 中创建连接

>[!NOTE]
>
>只有在使用Customer Journey Analytics时，才需要执行以下过程。

1. 请确保按照[在Customer Journey Analytics中配置数据流](#configure-a-datastream-in-adobe-experience-platform)中的说明创建了数据流。

1. 在Customer Journey Analytics中，按照[创建连接](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=zh-Hans)中的说明创建连接。

   创建连接时，需要以下配置选择才能实施流媒体收集：

   1. 选择您之前创建的数据集，如[在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform)中所述。

   1. 确保已启用&#x200B;[!UICONTROL **导入所有新数据**]&#x200B;设置。

1. 继续[在Customer Journey Analytics](#create-a-new-data-view-in-customer-journey-analytics)中创建数据视图。

## 在 Customer Journey Analytics 中创建数据视图

>[!NOTE]
>
>只有在使用Customer Journey Analytics时，才需要执行以下过程。

1. 请确保您已按照[在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics)中的说明在Customer Journey Analytics中创建连接。

1. 在客户历程分析中，按照[创建或编辑数据视图](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=zh-Hans)中的说明创建数据视图。

   创建数据视图时，需要以下配置选择才能实施流媒体收集：

   1. 在&#x200B;[!UICONTROL **连接**]&#x200B;字段中，选择您之前创建的连接，如[在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics)中所述。

      最多可能需要15分钟才能选择您创建的连接。

   1. 在&#x200B;[!UICONTROL **组件**]&#x200B;选项卡的&#x200B;[!UICONTROL **架构字段**]&#x200B;部分中，搜索下表列出的每个组件，并将其拖到&#x200B;[!UICONTROL **量度**]&#x200B;面板中。 如果存在多个同名字段，请使用XDM路径以确保它是正确的字段。

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


   1. 更新下表中组件的标签（在&#x200B;[!UICONTROL **上下文标签**]&#x200B;下拉菜单中）。 搜索指标面板中尚未出现的任何组件，并将其拖到面板中。

      | 组件名称 | 上下文标签 |
      |---------|----------|
      | 媒体会话服务器超时 | 媒体：上次调用后经过的秒数 |
      | 平均逗留时间 | 媒体：媒体逗留时间 |
      | 缓冲总持续时间 | 媒体：缓冲总持续时间 |
      | 开始时间 | Media：开始时间 |
      | 暂停总持续时间 | 媒体：暂停总持续时间 |

   1. 要将划分添加到Customer Journey Analytics项目，请将以下维度添加到&#x200B;[!UICONTROL **维度**]&#x200B;面板：

      | XDM 路径 | 组件名称 |
      |---------|----------|
      | mediaReporting.states.name | 播放器状态名称 |
      | mediaReporting.sessionDetails.ID | 媒体会话 ID |

      除了此表中的维度外，您还可以添加任何其他要使其可用于在Customer Journey Analytics项目中过滤数据的维度。

1. 选择&#x200B;[!UICONTROL **保存并继续**] > [!UICONTROL **保存并完成**]&#x200B;以保存更改。

1. 继续[在Customer Journey Analytics](#create-and-configure-a-project-in-customer-journey-analytics)中创建并配置项目。

## 在Customer Journey Analytics中创建并配置项目

1. 请确保您已按照[在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics)中的说明在Customer Journey Analytics中创建数据视图。

1. 在Customer Journey Analytics的&#x200B;[!UICONTROL **Workspace**]&#x200B;选项卡的&#x200B;[!UICONTROL **项目**]&#x200B;区域，选择&#x200B;[!UICONTROL **创建项目**]。

1. 选择&#x200B;[!UICONTROL **空白项目**] > [!UICONTROL **创建**]。

1. 在新项目中，选择您之前创建的数据视图。

   在项目中创建面板时，您可以使用添加到数据视图的任何组件，如[在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics)中所述。

   以下4个面板是您可以创建的面板示例：

   ![主内容面板](assets/main-content-panel.png)

   ![章节和广告面板](assets/chapter-and-ads-panel.png)

   ![QoE面板](assets/qoe-panel.png)

   ![平板状态面板](assets/player-state-panel.png)

1. 选择左边栏中的&#x200B;**面板**&#x200B;图标，然后拖入&#x200B;[!UICONTROL **媒体并行查看者**]&#x200B;面板和&#x200B;[!UICONTROL **媒体播放耗时**]&#x200B;面板。

   这两个面板应当如下所示：

   ![媒体并行查看者面板](assets/media-concurrent-viewers-panels.png)

   ![媒体播放耗时面板](assets/media-playback-time-spent-panels.png)

1. （视情况而定）如果您向架构添加了自定义元数据，如[在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform)的步骤8中所述，那么您需要为自定义字段设置持久性，如Customer Journey Analytics指南中的[持久性组件设置](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-dataviews/component-settings/persistence)中所述。

   当数据到达Customer Journey Analytics时，自定义用户ID维度将可用。

   ![setup-custom-metadata](assets/custom-metadata-dimension.png)

   >[!NOTE]
   >
   >如果您将Adobe Analytics设置为数据流的上游，则自定义元数据也会出现在ContextData中，其名称为您在架构中设置的（不带租户前缀，例如myCustomField）。 这使得可以使用所有可用于ContextData的Adobe Analytics功能，例如[创建处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules)。

1. 按照[共享项目](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=zh-Hans)中的说明共享项目。

   >[!NOTE]
   >
   >   如果要与共享的用户不可用，请确保这些用户在Adobe Admin Console中拥有Customer Journey Analytics的用户和管理员访问权限。


1. 继续[将数据发送到Experience Platform Edge](#send-data-to-experience-platform-edge)。

## 将数据发送到Experience Platform Edge

根据要发送到Experience Platform Edge的数据类型，您可以使用以下任一方法：

### Web：使用Adobe Experience Platform Web SDK

* [入门指南](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [使用Adobe Experience Platform Web SDK将Web数据发送到Edge](/help/implementation/edge/edge-web-sdk.md)

* [迁移到Adobe Streaming Media for Edge Network扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Mobile：使用Adobe Experience Platform Mobile SDK

使用以下文档资源完成iOS和Android的实施：

* [入门指南](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [API 参考](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/api-reference/)

* [迁移到Adobe Streaming Media for Edge Network扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/)

### Roku： Adobe Experience Platform Roku SDK

* [入门指南](https://developer.adobe.com/client-sdks/documentation/media-for-edge-network/)

* [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main)

* [迁移到Adobe Streaming Media for Edge Network扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/migration-guide/) <!-- is the information here also applicable for Roku? -->

### API： Web和其他

此API是当前唯一受支持的将Web数据发送到Experience Platform Edge的方法。

如果您要使用Edge API的自定义实施，则该API也将可用。

有关media Edge API的更多信息，请参阅以下资源：

* [Media Edge API概述](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/overview.html?lang=zh-Hans)

* [Media Edge API快速入门](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/getting-started.html?lang=zh-Hans)

* [Media Edge API疑难解答指南](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/media-edge-apis/troubleshooting.html?lang=zh-Hans)

* [使用Media Edge API的Open API规范文件](https://developer.adobe.com/data-collection-apis/docs/api/media-edge/)
