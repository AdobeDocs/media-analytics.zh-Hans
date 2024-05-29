---
title: 使用Adobe Experience Platform Web SDK将Web数据发送到Edge
description: 了解如何使用Adobe Experience Platform Web SDK将Adobe流媒体数据发送到Experience Platform Edge。
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 4e6ae687175b45680d8de071dbc3011f18921a44
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 使用Adobe Experience Platform Web SDK将Web数据发送到Edge

从版本2.20.0开始， `streamingMedia` Adobe Experience Platform组件 [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/home) 使您能够收集与网站上的媒体会话相关的数据。 收集的数据可以包括有关媒体回放、暂停、完成和其他相关事件的信息。

收集数据后，您可以将其发送到Adobe Experience Platform和/或Adobe Analytics以生成报表。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

对于使用Media JS SDK的客户，Web SDK提供了从Media JS SDK迁移到Web SDK的迁移路径，同时包括对现有Media JS功能（如处理媒体事件）的支持。

## 先决条件 {#prerequisites}

要使用 `streamingMedia` 组件，您必须满足以下先决条件：

* 在将Media Analytics数据发送到Edge之前，请先完成中的步骤 [安装Media Analytics和Experience Platform边缘](/help/implementation/edge/implementation-edge.md).
* 确保您有权访问Adobe Experience Platform和/或Adobe Analytics。
* 您必须使用Web SDK版本2.20.0或更高版本。 请参阅 [Web SDK安装概述](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) 了解如何安装最新版本。
* 启用 **[[!UICONTROL 媒体分析]](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/configure)** 选项。
* 确保数据流使用的架构包括媒体收集架构字段。
* 在Web SDK配置中配置流媒体功能，如本页所示，通过 [标记扩展](#tag-extension) 或通过 [JavaScript库](#library).

按照此页面中描述的步骤，将Analytics for Streaming Media实施从Media JS迁移到Web SDK。

### 步骤1：安装Experience PlatformWeb SDK

请参阅 [专用文档](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/install/overview) 以了解如何在Web资产上安装Web SDK。

### 步骤2：配置Web SDK `streamingMedia` 组件。

**示例**

以下代码片段显示了如何在Media JS中配置媒体收集。

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "company.hb-api.omtrdc.net";
mediaConfig.playerName = "player_name";
mediaConfig.channel = "sample_channel";
mediaConfig.appVersion = "app_version";
mediaConfig.debugLogging = true;
mediaConfig.ssl = true;

ADB.Media.configure(mediaConfig, appMeasurement);
```

相反，您必须配置 `streamingMedia` Web SDK中的组件，如下例所示。

```js
alloy("configure", {
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

请参阅Web SDK `streamingMedia` 组件 [文档](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/streamingmedia) 以了解有关如何对其进行配置的完整详细信息。

### 步骤3：从Media JS SDK迁移时获取媒体跟踪器实例

对于使用Media JS SDK的客户，Web SDK提供了从Media JS SDK迁移到Web SDK的迁移路径，同时包括对现有Media JS功能（如处理媒体事件）的支持。

[!DNL Web SDK] 包括用于检索Media Analytics跟踪器的命令。 您可以使用此命令创建一个对象实例，然后使用与提供的相同API [Media JS库](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)，跟踪媒体事件。

请参阅 [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/getMediaAnalyticsTracker) 文档，以了解有关所支持方法的完整详细信息。

以下代码片段显示了如何在Media JS中检索媒体跟踪器实例。

```javascript
var tracker = ADB.Media.getInstance();
```

请改用 `getMediaAnalyticsTracker` 命令以获得相同的结果，如下所示。

```js
// aquire Media Analytics APIs
const Media = await window.alloy("getMediaAnalyticsTracker", {});
// create a media tracker instance
const trackerInstance = Media.getInstance();
```

所有帮助程序方法均可在 `Media` 对象。 跟踪器方法在tracker实例上可用，如下所示。

```js
const mediaInfo = Media.createMediaObject(
  "video name",
  "player video",
  60,
  Media.StreamType.VOD,
  Media.MediaType.Video
);

const contextData = {
  isUserLoggedIn: "false",
  tvStation: "Sample TV station",
  programmer: "Sample programmer",
  assetID: "/uri-reference"
};

// Set standard Video Metadata
contextData[Media.VideoMetadataKeys.Episode] = "Sample Episode";
contextData[Media.VideoMetadataKeys.Show] = "Sample Show";

trackerInstance.trackSessionStart(mediaInfo, contextData);
```
