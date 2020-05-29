---
title: 设置JavaScript 3.x
description: Media SDK应用程序设置，以在JavaScript 3.x上实现。
translation-type: tm+mt
source-git-commit: b642bd1a136e62901847f2a8cf004d05282fca01
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 47%

---


# 设置JavaScript 3.x{#set-up-javascript}

## 先决条件

* **获取有效配置参数**
在设置 Analytics 帐户后，您可以从 Adobe 代表处获取这些参数。
* **在媒`AppMeasurement`体应`Experience Cloud Identity Service`用程序中实施和实现JavaScript**&#x200B;有关详细信息，请参 [阅使用JavaScript实现分析](https://docs.adobe.com/content/help/zh-Hans/analytics/implementation/js/overview.html) 和实 [现Experience Cloud Identity Service。](https://docs.adobe.com/content/help/en/id-service/using/implementation/setup-analytics.html)

* **在媒体播放器中提供以下功能：**

   * *用于订阅播放器事件的 API* - Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的API* —— 其中包括有关当前播放的媒体、广告、章节的信息。

1. 将[下载](/help/sdk-implement/download-sdks.md#download-3x-sdks)的库添加到您的项目中。为方便起见，请创建对类的本地引用。

   1. 展开您下载的 `MediaSDK-js-v3*.zip` 文件。
   1. 验证 `MediaSDK.js` 文件存在于 `libs` 目录中。

   1. 托管 `MediaSDK.js` 文件。

      此核心 JavaScript 文件必须在一个您站点的所有页面都能访问的 Web 服务器上托管。您需要具有这些文件的路径才能进行下一步操作。

   1. 在所有网站页面上引用 `MediaSDK.js`。

      通过将下面一行代码添加到每个页面的 `<head>` 或 `<body>` 标记中，加入适用于 JavaScript 的 `MediaSDK`。例如：

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. 要快速验证库是否成功导入，请检查是否 `ADB.Media` 在Window对象上导出。

      >[!NOTE]
      >
      >The JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `MediaSDK.js` can also be used with compatible module loaders.

1. 创建并配 `AppMeasurement` 置实例 `visitor`。

   Media SDK配置需要一个已配置 `AppMeasurement` 的实 `visitor` 例。

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
   ```

1. 配置媒体SDK

   Media SDK应每个网页配置一次，该配置应用于所有创建的跟踪器实例。

   >[!IMPORTANT]
   >
   > Media SDK(3.x)使用Media Collection API跟踪媒体，该API与2.x SDK中使用的HB端点不同。 请与Adobe代表联系以获取更多信息。

   以下是 `MediaConfig` 初始化示例：

   ```js
    // Create MediaConfig object (same as above)
    var mediaConfig = new ADB.MediaConfig();
    mediaConfig.trackingServer = Configuration.MEDIA_COLLECTION_ENDPOINT;
    mediaConfig.playerName = Configuration.PLAYER_NAME;
    mediaConfig.channel = Configuration.CHANNEL;
    mediaConfig.appVersion = Configuration.APP_VERSION;
    mediaConfig.debugLogging = false;
    mediaConfig.ssl = true;
   
    ADB.Media.configure(mediaConfig, appMeasurement);
   ```

1. 创建 `MediaTracker` 实例。

   配置Media SDK后，可以使用API创建用于跟踪媒体内容的跟踪器 `getInstance` 实例。

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >在媒体会话结束前，请确保您的 `tracker` 实例可以访问且未被取消分配。此实例将用于跟踪该会话的以下所有事件。

## 从JavaScript 2.x迁移到3.x

有关从 2.x 迁移到 3.x 的详细信息，请参阅[从 2.x 迁移到 3.x](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)。
