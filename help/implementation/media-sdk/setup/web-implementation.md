---
title: 如何设置适用于流媒体的 Analytics 的 Web 实施
description: 了解如何实施适用于 Web 应用程序的 Adobe Streaming Media。
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 92%

---

# 使用JavaScript安装Media SDK {#install-web-sdks}

本页上的信息描述如何安装 Web 独立 SDK 和设置 JavaScript。

或者，还可使用Adobe MediumAnalytics扩展实施Adobe流媒体收集加载项，如[使用Media Analytics扩展实施Analytics](/help/implementation/media-sdk/setup/web-implementation-tags.md)中所述。

## 先决条件 {#prerequesites}

* **获取有效的配置参数**

  在设置分析帐户后，这些参数可以从 Adobe 代表获取。

* **在媒体应用程序中实施适用于 JavaScript 的 `AppMeasurement` 和 `Experience Cloud Identity Service`**

  有关更多信息，请参阅[使用 JavaScript 实施 Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans) 和[实施 Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html?lang=zh-Hans)。

* **在媒体播放器中包含以下 API**

   * *用于订阅播放器事件的 API* – Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* – 其中包括有关当前播放的媒体、广告和章节的信息。

## 设置 JavaScript 3.x {#set-up-javascript}

1. 将[下载](/help/getting-started/download-sdks.md)的库添加到您的项目中。为方便起见，请创建对类的本地引用。

   1. 展开您下载的 `MediaSDK-js-v3*.zip` 文件。
   1. 验证 `MediaSDK.js` 文件存在于 `libs` 目录中。

   1. 托管 `MediaSDK.js` 文件。

      此核心 JavaScript 文件必须在一个您站点的所有页面都能访问的 Web 服务器上托管。您需要具有这些文件的路径才能进行下一步操作。

   1. 在所有网站页面上引用 `MediaSDK.js`。

      通过将下面一行代码添加到每个页面的 `<head>` 或 `<body>` 标记中，加入适用于 JavaScript 的 `MediaSDK`。例如：

      ```html
      <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.js"></script>
      ```

   1. 要快速验证是否成功导入了库，请检查 `ADB.Media` 是否已在窗口对象上导出。

      >[!NOTE]
      >
      >JavaScript SDK 遵循 AMD 和 CommonJS 模块规范，并且 `MediaSDK.js` 也可以与兼容的模块加载器一起使用。

1. 创建 `AppMeasurement` 实例并配置 `visitor`。

   Media SDK 配置需要一个已配置 `visitor` 的 `AppMeasurement` 实例。

   ```js
    var appMeasurement = new AppMeasurement("<rsid>");
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   ```

1. 配置 Media SDK

   应该为每个网页配置一次 Media SDK，并且该配置适用于创建的所有跟踪器实例。

   >[!IMPORTANT]
   >
   > Media SDK (3.x) 使用媒体收集 API 跟踪媒体，该 API 与 2.x SDK 中使用的 HB 端点不同。请与 Adobe 代表联系以获取更多信息。

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

   配置 Media SDK 后，可以使用 `getInstance` API 创建用于跟踪媒体内容的跟踪器实例。

   ```js
   var tracker = ADB.Media.getInstance();
   ```

   >[!IMPORTANT]
   >
   >在媒体会话结束前，请确保您的 `tracker` 实例可以访问且未被取消分配。此实例将用于跟踪该会话的以下所有事件。

## 从 JavaScript 2.x 迁移到 3.x

有关从 2.x 迁移到 3.x 的详细信息，请参阅[从 2.x 迁移到 3.x](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/MigrationGuide.html)。

有关旧版内容，请参阅[旧版实施](/help/legacy/media-sdk/setup/setup-overview.md)
