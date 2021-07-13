---
title: 如何使用JavaScript 3.x设置媒体SKD
description: 按照以下步骤在JavaScript 3.x中设置Media SDK应用程序。
exl-id: 35e27495-e480-4463-9f00-4b60a54d02c1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 87%

---

# 设置 JavaScript 3.x{#set-up-javascript}

## 先决条件

* **获取有效配置参数**
在设置 Analytics 帐户后，您可以从 Adobe 代表处获取这些参数。
* **在媒 `AppMeasurement` 体应 `Experience Cloud Identity Service` 用程序中实施和for**
JavaScript有关更多信息，请参 [阅使用JavaScript实](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans) 施Analytics和 [实施Experience Cloud身份服务](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html)。

* **在媒体播放器中提供以下功能：**

   * *用于订阅播放器事件的 API* - Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* - 其中包括有关当前播放的媒体、广告、章节的信息。

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

   1. 要快速验证是否成功导入了库，请检查 `ADB.Media` 是否已在窗口对象上导出。

      >[!NOTE]
      >
      >JavaScript SDK 遵循 AMD 和 CommonJS 模块规范，并且 `MediaSDK.js` 也可以与兼容的模块加载器一起使用。

1. 创建 `AppMeasurement` 实例并配置 `visitor`。

   Media SDK 配置需要一个已配置 `visitor` 的 `AppMeasurement` 实例。

   ```js
    var appMeasurement = new AppMeasurement(“<rsid>”);
    appMeasurement.visitor = visitor;
    appMeasurement.trackingServer = “<visitor_namespace>.sc.omtrdc.net”;
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
