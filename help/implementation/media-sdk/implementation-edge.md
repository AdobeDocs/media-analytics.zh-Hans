---
title: 设置适用于流媒体的 Analytics实施的首要步骤
description: 了解如何实施Adobe流媒体。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 723cfab6dd2d63448f44dc535724ffe4fd0ec8a7
workflow-type: tm+mt
source-wordcount: '1960'
ht-degree: 10%

---

# 使用Experience Platform边缘安装Media Analytics

Adobe Experience Platform Edge 允许您将发送到多个产品的数据发送到一个集中的位置。 Experience Edge 将适当的信息转发给所需的产品。 此概念允许您整合实施工作，尤其是跨多个数据解决方案进行整合。

下图说明了使用Experience Platform边缘的Media Analytics实施：

![边缘实施](assets/media-analytics-implementation-overview.png)

>[!IMPORTANT]
>
>目前，您只能使用Adobe Experience Platform Mobile SDK将数据发送到Experience Edge。


<!-- Replace the above sentence with this after it web releases: You can send data to Experience Edge using any of the following implementation methods:

* Adobe Experience Platform Web SDK (Coming soon)
* Adobe Experience Platform Mobile SDK
* Edge Network Server API

Regardless of which Experience Edge implementation method you use for configuring media tracking, you must first complete the following sections:

-->

请完成以下部分以使用Experience Platform边缘实施Media Analytics:

* [定义报表包](#define-a-report-suite)
* [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform)
* [在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform)
* [在Adobe Experience Platform中配置数据流](#configure-a-datastream-in-adobe-experience-platform)
* [在 Customer Journey Analytics 中创建连接](#create-a-connection-in-customer-journey-analytics)
* [在Customer Journey Analytics中创建数据视图](#create-a-data-view-in-customer-journey-analytics)
* [在Customer Journey Analytics中创建和配置项目](#create-and-configure-a-project-in-customer-journey-analytics)
* [使用Edge扩展将数据发送到Experience PlatformEdge](#send-data-to-experience-platform-edge-with-the-edge-extension)

## 定义报表包

>[!NOTE]
>
>仅当您使用的是Adobe Analytics时，才需要提供报表包。 如果您计划使用Customer Journey Analytics进行报表，则不需要报表包。

如果您计划使用Adobe Analytics进行报告，则需要具有一个报表包才能与流媒体实施结合使用。 有关定义报表包的信息，请参阅 [报表包管理器](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html?lang=en).

定义报表包后，继续 [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform).

## 在Adobe Experience Platform中设置架构

为了标准化数据收集以在利用 Adobe Experience Platform 的应用程序中使用，Adobe 创建了开放且公开记录的标准，即体验数据模型 (XDM)。

要创建和设置架构，请执行以下操作：

1. 在Adobe Experience Platform中，按照 [在UI中创建和编辑架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=en).

   创建架构时，选择 [!UICONTROL **XDM ExperienceEvent**] 从 [!UICONTROL **创建架构**] 下拉菜单。

1. 在 [!UICONTROL **组合物**] 区域，在 [!UICONTROL **字段组**] 选择 [!UICONTROL **添加**]，然后搜索以下新字段组并将其添加到架构中：
   * `Adobe Analytics ExperienceEvent Template`
   * `Implementation Details`
   * `MediaAnalytics Interaction Details`

   添加字段组后，这些字段组应显示在 [!UICONTROL **字段组**] 部分，如下所示：

   ![添加了字段组](assets/schema-field-groups-added.png)

1. 在 [!UICONTROL **结构**] 区域，选择 `endUserIds` > `_experience` 字段组，然后选择 [!UICONTROL **管理相关字段**].

   ![“管理相关字段”按钮](assets/manage-related-fields.png)

1. 按如下方式更新架构：

   * 在 `Adobe Analytics ExperienceEvent Template` 字段组，隐藏除 `EndUserIDs`.

   * 在 `endUserIds` > `_experience` > `Adobe Advertising Cloud end user IDs` 字段组，隐藏除 `Identifier` 字段。

   * 在 `endUserIds` > `_experience` > `Adobe Analytics Cloud Custom end user IDs` 字段组，隐藏除 `Identifier` 字段。

      ![隐藏字段](assets/schema-hide-fields.png)

1. 选择 [!UICONTROL **确认**] 以保存更改。

1. 在 [!UICONTROL **结构**] 区域，选择 `Implementation Details` 字段组，选择 [!UICONTROL **管理相关字段**]，然后按如下方式更新架构：

   * 在 `Implementation Details` > `Implementation details` 字段组，隐藏除 `version`.

      ![隐藏字段](assets/schema-hide-fields2.png)

1. 选择 [!UICONTROL **确认**] 以保存更改。

1. 在 [!UICONTROL **结构**] 区域，选择 `Media Collection Details` 字段组，选择 [!UICONTROL **管理相关字段**]，然后按如下方式更新架构：

   * 在 `Media Collection Details` 字段组，隐藏 `List Of States` 字段组。

      ![隐藏媒体收集状态](assets/schema-hide-media-collection-states.png)

   * 在 `Media Collection Details` > `Advertising Details` 字段组，隐藏以下报表字段： `Ad Completed`, `Ad Started`和 `Ad Time Played`.

   * 在 `Media Collection Details` > `Advertising Pod Details` 字段组，隐藏以下报表字段： `Ad Break ID`

   * 在 `Media Collection Details` > `Chapter Details` 字段组，隐藏以下报表字段： `Chapter ID`, `Chapter Completed`, `Chapter Started`和 `Chapter Time Played`.

   * 在 `Media Collection Details` > `Qoe Data Details` 字段组，隐藏以下报表字段： `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`和 `Total Stalling Duration`.

   * 在 `Media Collection Details` > `Session Details` 字段组，隐藏以下报表字段： `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`和 `Pccr`.

   * 在 `Media Collection Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 字段组，隐藏以下报表字段： `Player State Count`, `Player State Set`和 `Player State Time`.

      ![隐藏字段](assets/schema-hide-listofstates.png)

1. 选择 [!UICONTROL **确认**] 以保存更改。

1. 在 [!UICONTROL **结构**] 区域，选择 `List Of Media Collection Downloaded Content Events` 字段组，选择 [!UICONTROL **管理相关字段**]，然后按如下方式更新架构：

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` 字段组，隐藏 `List Of States` 字段组。

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Details` 字段组，隐藏以下报表字段： `Ad Completed`, `Ad Started`和 `Ad Time Played`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Advertising Pod Details` 字段组，隐藏以下报表字段： `Ad Break ID`

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Chapter Details` 字段组，隐藏以下报表字段： `Chapter ID`, `Chapter Completed`, `Chapter Started`和 `Chapter Time Played`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Qoe Data Details` 字段组，隐藏以下报表字段： `Average Bitrate`, `Average Bitrate Bucket`, `Bitrate Changes`, `Buffer Events`, `Total Buffer Duration`, `Errors`, `External Error IDs`, `Bitrate Change Impacted Streams`, `Buffer Impacted Streams`, `Dropped Frame Impacted Streams`, `Error Impacted Streams`, `Stalling Impacted Streams`, `Drops Before Starts`, `Media SDK Error IDs`, `Player SDK Error IDs`, `Stalling Events`和 `Total Stalling Duration`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `Session Details` 字段组，隐藏以下报表字段： `Media Session ID`, `Ad Count`, `Average Minute Audience`, `Chapter Count`, `Estimated Streams`, `Pause Impacted Streams`, `10% Progress Marker`, `25% Progress Marker`, `50% Progress Marker`, `75% Progress Marker`, `95% Progress Marker`, `Media Segment Views`, `Content Completes`, `Media Downloaded Flag`, `Federated Data`, `Content Starts`, `Media Starts`, `Pause Events`, `Total Pause Duration`, `Media Session Server Timeout`, `Video Segment`, `Content Time Spent`, `Media Time Spent`, `Unique Time Played`, `Pev3`和 `Pccr`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details` > `List Of States End` 和 `Media Collection Details` > `List Of States Start` 字段组，隐藏以下报表字段： `Player State Count`, `Player State Set`和 `Player State Time`.

   * 在 `List Of Media Collection Downloaded Content Events` > `Media Details`  字段组，隐藏 `Media Session ID` 字段。

1. 选择 [!UICONTROL **确认**] 以保存更改。

1. 在 [!UICONTROL **结构**] 区域，选择 `Media Reporting Details` 字段组，选择 [!UICONTROL **管理相关字段**]，然后按如下方式更新架构：

   * 在 `Media Reporting Details` 字段组，隐藏以下字段组： `Error Details`, `List Of States End`, `List of States Start`, `Playhead`和 `Media Session ID`.

1. 选择 [!UICONTROL **确认**] > [!UICONTROL **保存**]  以保存更改。

1. 继续 [在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform).

## 在Adobe Experience Platform中创建数据集

1. 确保按照 [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform).

1. 在Adobe Experience Platform中，按照 [数据集UI指南](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=zh_Hans#create).

   选择数据集的架构时，请选择之前创建的架构，如 [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform).

1. 继续 [在Customer Journey Analytics中配置数据流](#configure-a-datastream-in-adobe-experience-platform).

## 在Adobe Experience Platform中配置数据流

1. 确保您按照 [在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform).

1. 创建新数据流，如 [配置数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hans).

   创建数据流时，请确保进行以下配置选择：

   * 在 [!UICONTROL **事件架构**] 字段，请确保选择在中创建的架构 [在Adobe Experience Platform中设置架构](#set-up-the-schema-in-adobe-experience-platform). 选择&#x200B;[!UICONTROL **保存**]。

      >[!IMPORTANT]
          >
      >不选择 [!UICONTROL **保存并添加映射**] 因为这样做会导致“时间戳”字段的映射错误。
      

      ![创建数据流并选择模式](assets/datastream-create-schema.png)

   * 根据您使用的是Adobe Analytics还是Customer Journey Analytics，将以下任一服务添加到数据流：

      * [!UICONTROL **Adobe Analytics**] (如果使用Adobe Analytics)

         如果您使用的是Adobe Analytics，请确保定义一个报表包，如部分中所述 [定义报表包](#define-a-report-suite) 在本文中。

      * [!UICONTROL **Adobe Experience Platform**] (如果使用Customer Journey Analytics)
      有关如何向数据流添加服务的信息，请参阅 [配置数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#view-details).

      ![添加Adobe Analytics服务](assets/datastream-add-service.png)

   * 展开 [!UICONTROL **高级选项**]，然后启用 [!UICONTROL **Media Analytics**] 选项。

      ![Media Analytics选项](assets/datastream-media-check.png)


1. 继续 [在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics).

## 在 Customer Journey Analytics 中创建连接

>[!NOTE]
>
>仅当您使用Customer Journey Analytics时，才需要执行以下过程。


1. 确保您创建了数据流，如 [在Customer Journey Analytics中配置数据流](#configure-a-datastream-in-adobe-experience-platform).

1. 在Customer Journey Analytics中，按照 [创建连接](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-connections/create-connection.html?lang=zh-Hans).

   创建连接时，需要选择以下配置来实施流媒体：

   1. 选择您之前创建的数据集，如 [在Adobe Experience Platform中创建数据集](#create-a-dataset-in-adobe-experience-platform).

   1. 确保 [!UICONTROL **导入所有新数据**] 设置。

1. 继续 [在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics).

## 在Customer Journey Analytics中创建数据视图

>[!NOTE]
>
>仅当您使用Customer Journey Analytics时，才需要执行以下过程。

1. 确保在Customer Journey Analytics中创建连接，如 [在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics).

1. 在Customer Analytics中，创建历程视图，如 [创建或编辑数据视图](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=zh-Hans).

   创建数据视图时，需要选择以下配置来实施流媒体：

   1. 在 [!UICONTROL **连接**] 字段中，选择您之前创建的连接，如 [在Customer Journey Analytics中创建连接](#create-a-connection-in-customer-journey-analytics).

      最长可能需要15分钟才能选择您创建的连接。

   1. 在 [!UICONTROL **组件**] 选项卡 [!UICONTROL **架构字段**] 部分，搜索下表中列出的每个组件，并将其拖动到 [!UICONTROL **量度**] 的上界。 如果存在多个同名字段，请使用XDM路径确保该字段正确。

      **主内容 — 内容量度**

      | 组件名称 | XDM路径 |
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

      | 组件名称 | XDM路径 |
      |----------|---------|
      | 章节开始 | mediaReporting.chapterDetails.isStarted |
      | 章节结束 | mediaReporting.chapterDetails.isCompleted |
      | 章节播放时间 | mediaReporting.chapterDetails.timePlayed |
      | 广告开始 | mediaReporting.advertisingDetails.isStarted |
      | 广告结束 | mediaReporting.advertisingDetails.isCompleted |
      | 广告播放时间 | mediaReporting.advertisingDetails.timePlayed |


      **QoE - QoE量度**

      | 组件名称 | XDM路径 |
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

      | 组件名称 | XDM路径 |
      |----------|---------|
      | 播放器状态集 | mediaReporting.states.isSet |
      | 播放器状态计数 | mediaReporting.states.count |
      | 播放器状态时间 | mediaReporting.states.time |


   1. 更新标签(在 [!UICONTROL **上下文标签**] 下拉菜单)。 搜索并将“量度”面板中尚未包含的任何组件拖到面板中。

      | 组件名称 | 上下文标签 |
      |---------|----------|
      | 媒体会话服务器超时 | 媒体：自上次调用后经过的秒数 |
      | 平均逗留时间 | 媒体：媒体逗留时间 |
      | 缓冲总持续时间 | 媒体：缓冲总持续时间 |
      | 开始时间 | 媒体：开始时间 |
      | 暂停总持续时间 | 媒体：暂停总持续时间 |

   1. 要向Customer Journey Analytics项目添加划分，请将以下维度添加到 [!UICONTROL **Dimension**] 面板：

      | XDM路径 | 组件名称 |
      |---------|----------|
      | mediaReporting.states.name | 播放器状态名称 |
      | mediaReporting.sessionDetails.ID | 媒体会话 ID |

      除了此表中的维度之外，您还可以添加任何其他维度，以便您能够在Customer Journey Analytics项目中按维度过滤数据。

1. 选择 [!UICONTROL **保存并继续**] > [!UICONTROL **保存并完成**] 以保存更改。

1. 继续 [在Customer Journey Analytics中创建和配置项目](#create-and-configure-a-project-in-customer-journey-analytics).

## 在Customer Journey Analytics中创建和配置项目

1. 确保您按照 [在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics).

1. 在Customer Journey Analytics中，在 [!UICONTROL **工作区**] 选项卡 [!UICONTROL **项目**] 区域，选择 [!UICONTROL **创建项目**].

1. 选择 [!UICONTROL **空白项目**] > [!UICONTROL **创建**].

1. 在新项目中，选择您之前创建的数据视图。

   在项目中创建面板时，您可以使用添加到数据视图的任何组件，如 [在Customer Journey Analytics中创建数据视图](#create-a-new-data-view-in-customer-journey-analytics).

   以下4个面板是可以创建的面板示例：

   ![“主内容”面板](assets/main-content-panel.png)

   ![章节和广告面板](assets/chapter-and-ads-panel.png)

   ![QoE面板](assets/qoe-panel.png)

   ![播放器状态面板](assets/player-state-panel.png)

1. 选择 **面板** 图标，然后在 [!UICONTROL **媒体并行查看者**] 面板和 [!UICONTROL **媒体播放逗留时间**] 的上界。

   这2个面板应当如下所示：

   ![“媒体并行查看者”面板](assets/media-concurrent-viewers-panels.png)

   ![“媒体播放逗留时间”面板](assets/media-playback-time-spent-panels.png)

1. 按照 [共享项目](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/curate-share/share-projects.html?lang=en).

   >[!NOTE]
   >
   >   如果要与共享的用户不可用，请确保这些用户具有在Adobe Admin Console中访问Customer Journey Analytics的用户和管理员权限。

1. 继续 [将数据发送到Experience Platform边缘](#send-data-to-experience-platform-edge).

## 使用AEP Mobile SDK将数据发送到Experience Platform边缘

您可以使用Adobe Experience Platform Mobile SDK将移动数据发送到Experience Platform Edge。 (或者，您也可以使用边缘API的自定义实施。<!-- I guess we don't need/want to document this? -->)

使用以下文档资源完成实施：


| 移动操作系统 | 资源 |
|---------|----------|
| **iOS** | 以下资源可用于发送iOS移动数据： <ul><li>[使用数据收集UI配置Mobile SDK](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/getting-started.md)</li><li>[从Media SDK迁移到Edge Media SDK](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/migration-guide.md)</li><li>[Edge Media API引用](https://github.com/adobe/aepsdk-edgemedia-ios/blob/dev/Documentation/api-reference.md)</li></ul> |
| **Android** | 以下资源可用于发送Android移动数据： <ul><li>[使用数据收集UI配置Mobile SDK](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/getting-started.md)</li><li>[从Media SDK迁移到Edge Media SDK](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/migration-guide.md)</li><li>[Edge Media API引用](https://github.com/adobe/aepsdk-edgemedia-android/blob/dev/Documentation/api-reference.md)</li></ul> |


<!--

+++Adobe Experience Platform Mobile SDK

If you plan to use the Mobile SDK extension in Adobe Experience Platform Data Collection to send data to Edge, complete the following sections:

### Create a mobile property

Create a mobile property, as described in [Set up a mobile property](https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/). 

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/mobile-sdk/overview.html?lang=en 

The Adobe Experience Platform Mobile SDK helps power Adobe's Experience Cloud solutions and services in your mobile apps. It is available for Android, iOS, and various cross-platform development frameworks. Configuration is handled through Adobe Experience Platform Data Collection.
>[!IMPORTANT]
>
>An Adobe Analytics extension is also available in Adobe Experience Platform Data Collection. If you install this extension, you do not take advantage of XDM or the Edge Network.

### Register the extensions and load your tag configuration

Use code in your app to register the necessary extensions and load your tag configuration. For more information, see [Set up the configuration](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Implement and test fuctionality

Implement and test app functionality using a combination of tags data elements, rules, additional extensions, and SDK API calls. Inspect, validate, and debug data collection and experiences for your mobile application.

For more information, see [Use the sample application](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application) in [Getting started with Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration).

### Extend and validate your mobile app implementation

Before pushing the mobile app extension to your production environment, first validate that it works.

(What are the steps to do this?)

-->

<!--

+++Adobe Experience Platform Web SDK (Coming soon)

>[!NOTE]
>
>The Adobe Experience Platform Web SDK is not yet available. This page will be updated when it becomes available.

<!-- Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/web-sdk/overview.html?lang=en -->

<!-- Use the Web SDK extension in Adobe Experience Platform Data Collection to send data to Edge.

You can use the [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html) to send data to Adobe Analytics. This implementation method works by translating the [Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) into a format used by Analytics.

You can send data to Experience Edge directly using the Web SDK, or through the Web SDK extension in Tags. -->

<!-- ### Web SDK

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK workflow](../../assets/websdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td> 4</td>
<td><b>Install the prebuilt standalone version</b>. You can reference the library (<code>alloy.js</code>) on the CDN directly on your page or download and host it on your own infrastructure. Alternatively, you can use the NPM package.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-2%3A-installing-the-prebuilt-standalone-version">Installing the prebuilt standalone version</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=en#option-3%3A-using-the-npm-package">Using the NPM package</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>6</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>7</td>
<td><b>Configure the Web SDK</b>. Ensure the library that you installed in step 4 is properly configured with the datastream ID (formerly known as edge configuration id (<code>edgeConfigId</code>)), organization id (<code>orgId</code>), and other available options.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en">Configure the Web SDK</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Execute commands</b> and/or <b>track events</b>. After the base code has been implemented on your webpage, you can begin executing commands and tracking events with the SDK.
</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/executing-commands.html?lang=en">Execute commands</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en">Track events</a></td>
</tr>

<tr>
<td>9</td><td><b>Extend and validate your implementation</b> before pushing it out to production.</td><td></td> 
</tr>
</table>


### Web SDK extension

A high-level overview of the implementation tasks:

![Implement Adobe Analytics using Web SDK extension workflow](../../assets/websdk-extension-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Create a data layer</b> to manage the tracking of the data on your website.</td>
<td><a href="../../prepare/data-layer.md">Create a data layer</a></td>
</tr>

<tr>
<td>4</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<tr>
<td>5</td> 
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>6</td>
<td><b>Create a tag property</b>. Properties are overarching containers used to reference tag management data.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#for-web">Create or configure a tag property for web</a></td>
</tr>

<tr>
<td>7</td> 
<td><b>Install and configure the Web SDK extension</b> in your tag property. Configure the Web SDK extension to send data to the datastream configured in step 4.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/sdk/overview.html?lang=en">Adobe Experience Platform Web SDK extension overview</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Iterate, validate, and publish</b> to production. Add the tag property to your web site. Then use data elements, rules, and so on, to customize your implementation.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=en">Publishing overview</a></td>
</tr>

</table>


### Additional resources

Tags can be highly customized. Learn more about how you can get the most out of Adobe Analytics by including the right data in your implementation.

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#): Learn how the interface works and what extensions are available.

-   [Adobe Experience Platform Web SDK documentation](https://experienceleague.adobe.com/docs/web-sdk.html?lang=en)


+++

-->


<!--

### Adobe Experience Platform SDK

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Configure a datastream</b>. A datastream represents the server-side configuration when implementing the Adobe Experience Platform Web SDK.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en">Configure a datastream<a></td> 
</tr>

<td>4</td>
<td><b>Add an Adobe Analytics service</b> to your datastream. That service controls whether and how data is sent to Adobe Analytics.</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=en#analytics">Add Adobe Analytics service to a datastream</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Create a mobile property</b>. A property is a container that you fill with extensions, rules, data elements, and libraries.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/getting-started/create-a-mobile-property/">Set up a mobile property</a></tr>

<tr>
<td>6</td>
<td><b>Install the Adobe Experience Platform Edge Network extension</b> in the mobile tag property and configure the datastream in the extension.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/edge-network/">Adobe Experience Platform Edge Network</a>
</tr>

<tr>
<td>7</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>8</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>9</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>


### Adobe Analytics extension.

A high-level overview of the implementation tasks:

![Adobe Analytics using the Analytics extension workflow](../../assets/mobilesdk-analytics-annotated.png)

<table style="width:100%">

<tr>
<th style="width:5%"></th><th style="width:60%"><b>Task</b></th><th style="width:35%"><b>More Information</b></th>
</tr>

<tr>
<td>1</td>
<td>Ensure you have <b>defined a report suite</b>.</td>
<td><a href="../../../admin/admin/c-manage-report-suites/report-suites-admin.md">Report Suite Manager</a></td>
</tr>

<tr>
<td>2</td>
<td><b>Setup schemas and datasets</b>. To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented standard, Experience Data Model (XDM).</td>
<td><a href="https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/overview.html?lang=en">Schemas UI overview</a> and <a href="https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=en">Datasets UI overview</a></td>
</tr>

<tr>
<td>3</td>
<td><b>Install the Adobe Analytics extension</b> in the mobile tag property and configure the extension to point to your report suite.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/adobe-analytics/">Adobe Analytics extension for mobile property</a>
</tr>

<tr>
<td>4</td>
<td><b>Use code in your app</b> to register the necessary extensions and load your tag configuration.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#set-up-the-configuration">Set up the configuration</a></td>
</tr>

<tr>
<td>5</td>
<td><b>Implement and test functionality</b> using combination of tag's data elements, rules, additional extensions, and SDK API calls in your app. Inspect, validate, and debug data collection and experiences for your mobile application.</td>
<td><a href="https://developer.adobe.com/client-sdks/documentation/user-guides/getting-started-with-platform/overview/#use-the-sample-application">Use the sample application</a>
</tr>

<tr>
<td>6</td>
<td><b>Extend and validate your mobile app implementation</b> before pushing it out to production.</td>
<td></td> 
</tr>

</table>

### Additional resources

-   [Tags documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html#)

-   [Mobile SDK documentation](https://developer.adobe.com/client-sdks/documentation/)

-->

<!--

+++

+++Edge Network Server API

Send data directly to Edge using an API.

Content initially copied from here: https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/edge-api/overview.html?lang=en 

If you are unable to use the Adobe Experience Platform [Web SDK](../web-sdk/overview.md) or [Mobile SDK](../mobile-sdk/overview.md), you can send data to the Edge Network directly through an API.

See [Edge Network Server API documentation](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html), and an example [integrating with Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/interacting-other-adobe-solutions/interacting-adobe-analytics.html).

+++ 

-->

