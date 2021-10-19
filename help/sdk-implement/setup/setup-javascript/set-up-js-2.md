---
title: 如何使用 JavaScript 2.x 设置 Media SDK
description: 执行以下步骤，在 JavaScript 2.x 上设置 Media SDK 应用程序。
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e10f705e135cc6b9c630059596994d12fc787866
workflow-type: ht
source-wordcount: '401'
ht-degree: 100%

---

# 设置 JavaScript 2.x{#set-up-javascript}

## 先决条件

* **获取有效配置参数**
在设置 Analytics 帐户后，您可以从 Adobe 代表处获取这些参数。
* **在媒体应用程序中实施适用于 JavaScript 的 `AppMeasurement`**
有关 Adobe Mobile SDK 文档的更多信息，请参阅[使用 JavaScript 实施 Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans)。

* **在媒体播放器中提供以下功能：**

   * *用于订阅播放器事件的 API* - Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* - 此信息包括媒体名称和播放头位置等详细信息。

1. 将[下载](/help/sdk-implement/download-sdks.md#download-2x-sdks)的库添加到您的项目中。为方便起见，请创建对类的本地引用。

   1. 展开您下载的 `MediaSDK-js-v2.*.zip` 文件。
   1. 验证 `MediaSDK.min.js` 文件存在于 `libs` 目录中：

   1. 托管 `MediaSDK.min.js` 文件。

      此核心 JavaScript 文件必须在一个您站点的所有页面都能访问的 Web 服务器上托管。您需要具有这些文件的路径才能进行下一步操作。

   1. 在所有网站页面上引用 `MediaSDK.min.js`。

      通过将下面一行代码添加到每个页面的 `<head>` 或 `<body>` 标记中，加入适用于 JavaScript 的 `MediaSDK`。例如：

      ```
      <script type="text/javascript"
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. 要快速验证是否成功导入了库，请实例化 `ADB.va.MediaHeartbeatConfig` 类。

      >[!NOTE]
      >
      >从版本 2.1.0 开始，JavaScript SDK 遵循 AMD 和 CommonJS 模块规范，并且 `VideoHeartbeat.min.js` 也可以与兼容的模块加载器一起使用。

1. 为便于访问 API，请创建对 `MediaHeartbeat` 类的本地引用。

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   ```

1. 创建一个 `MediaHeartbeatConfig` 实例。

   本节将帮助您了解 `MediaHeartbeat` 配置参数以及如何在您的 `MediaHeartbeat` 实例中设置正确的配置值，以便进行准确跟踪。

   以下是 `MediaHeartbeatConfig` 初始化示例：

   ```js
   //Media Heartbeat initialization
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
   mediaConfig.playerName = Configuration.PLAYER.NAME;
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL;
   mediaConfig.debugLogging = true;
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK;
   mediaConfig.ssl = false;
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP;
   ```

1. 实施 `MediaHeartbeatDelegate` 协议。

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate();
   
   // Replace <currentPlaybackTime> with the video player current playback time
   mediaDelegate.getCurrentPlaybackTime = function() {
       return <currentPlaybackTime>;
   };
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() {
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
   };
   ```

1. 创建 `MediaHeartbeat` 实例。

   使用 `MediaHeartbeatConfig` 和 `MediaHeartbeatDelegate` 创建 `MediaHeartbeat` 实例。

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >在媒体会话结束前，请确保您的 `MediaHeartbeat` 实例可以访问且未被取消分配。此实例将用于以下所有的跟踪事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要 `AppMeasurement` 的实例，才能向 Adobe Analytics 发送调用。以下是 `AppMeasurement` 实例的示例：

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## 从 JavaScript 1.x 迁移到 2.x

在版本 2.x 中，所有公共方法都已合并到 `ADB.va.MediaHeartbeat` 类中，从而更加便于开发人员使用。此外，所有配置现在都已合并到 `ADB.va.MediaHeartbeatConfig` 类中。

有关从 1.x 迁移到 2.x 的详细信息，请参阅[从 VHL 1.x 迁移到 2.x](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)。
