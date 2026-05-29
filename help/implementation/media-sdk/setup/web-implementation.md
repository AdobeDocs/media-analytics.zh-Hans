---
title: 如何设置适用于流媒体的 Analytics 的 Web 实施
description: 了解如何实施适用于 Web 应用程序的 Adobe Streaming Media。
feature: Streaming Media
role: User, Admin, Developer
exl-id: aed561d0-defc-4be5-87d3-0f331cdfab34
TQID: https://experienceleague.adobe.com/UBY26SeGZbGWHjwOm6-YZNET8fe5Gvvco7aIZ9Z7rZg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 78%

---

# 使用JavaScript安装Media SDK {#install-web-sdks}

>[!IMPORTANT]
>
>本页介绍了仅限Analytics的JavaScript Web SDK实施。 有关推荐的实施，请参阅[使用Edge Network实施流媒体](/help/implementation/edge/edge-web-sdk.md)。

本页上的信息描述如何安装 Web 独立 SDK 和设置 JavaScript。

或者，还可使用Adobe Media Analytics扩展实施流媒体服务，如[使用Media Analytics扩展安装流媒体服务](/help/implementation/media-sdk/setup/web-implementation-tags.md)中所述。

## 先决条件 {#prerequesites}

* **获取有效的配置参数**

  在设置分析帐户后，这些参数可以从 Adobe 代表获取。

* **在媒体应用程序中实施适用于 JavaScript 的 `AppMeasurement` 和 `Experience Cloud Identity Service`**

  有关详细信息，请参阅[使用JavaScript实施Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans)和使用AppMeasurement进行[访客识别](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/id/appmeasurement)。

* **在媒体播放器中包含以下 API**

   * *用于订阅播放器事件的 API* – Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* – 其中包括有关当前播放的媒体、广告和章节的信息。

## 设置 JavaScript 3.x {#set-up-javascript}

1. 将[下载](/help/getting-started/download-sdks.md)的库添加到您的项目中。 为方便起见，请创建对类的本地引用。

   1. 展开您下载的 `MediaSDK-js-v3*.zip` 文件。
   1. 验证 `MediaSDK.js` 文件存在于 `libs` 目录中。

   1. 托管 `MediaSDK.js` 文件。

      此核心 JavaScript 文件必须在一个您站点的所有页面都能访问的 Web 服务器上托管。 您需要具有这些文件的路径才能进行下一步操作。

   1. 在所有网站页面上引用 `MediaSDK.js`。

      通过将下面一行代码添加到每个页面的 `<head>` 或 `<body>` 标记中，加入适用于 JavaScript 的 `MediaSDK`。 例如：

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
   >在媒体会话结束前，请确保您的 `tracker` 实例可以访问且未被取消分配。 此实例将用于跟踪该会话的以下所有事件。

## 从 JavaScript 2.x 迁移到 3.x

有关从2.x迁移到3.x的详细信息，请参阅从JS SDK 2.x迁移到3.x[&#128279;](/help/implementation/media-sdk/setup/migrate-js-2x-to-3x.md)。
