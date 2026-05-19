---
title: 如何使用 JavaScript 2.x 设置 Media SDK
description: 执行以下步骤，在 JavaScript 2.x 上设置 Media SDK 应用程序。
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
exl-id: 33976096-8b86-4353-906b-e25bf4693471
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mYfKt95xUE59MuMFOzGro6fPsJsdy4wcy2F2J--JaW8
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 89%

---

# 设置 JavaScript 2.x{#set-up-javascript}

## 先决条件

* **获取有效的配置参数**
在设置Analytics帐户后，这些参数可以从Adobe代表获取。
* 在媒体应用程序中为JavaScript实施&#x200B;**的`AppMeasurement`**
有关Adobe Mobile SDK文档的更多信息，请参阅[使用JavaScript实施Analytics。](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=zh-Hans)

* **在媒体播放器中提供以下功能：**

   * *用于订阅播放器事件的 API* – Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* - 此信息包括媒体名称和播放头位置等详细信息。

1. 将[下载](/help/getting-started/download-sdks.md)的库添加到您的项目中。 为方便起见，请创建对类的本地引用。

   1. 展开您下载的 `MediaSDK-js-v2.*.zip` 文件。
   1. 验证 `MediaSDK.min.js` 文件存在于 `libs` 目录中：

   1. 托管 `MediaSDK.min.js` 文件。

      此核心 JavaScript 文件必须在一个您站点的所有页面都能访问的 Web 服务器上托管。 您需要具有这些文件的路径才能进行下一步操作。

   1. 在所有网站页面上引用 `MediaSDK.min.js`。

      通过将下面一行代码添加到每个页面的 `<head>` 或 `<body>` 标记中，加入适用于 JavaScript 的 `MediaSDK`。 例如：

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
   >在媒体会话结束前，请确保您的 `MediaHeartbeat` 实例可以访问且未被取消分配。 此实例将用于以下所有的跟踪事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要 `AppMeasurement` 的实例，才能向 Adobe Analytics 发送调用。 以下是 `AppMeasurement` 实例的示例：

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net";
   appMeasurement.account = <rsid>;
   appMeasurement.pageName = <page_name>;
   appMeasurement.charSet = "UTF­8";
   ```

## 从 JavaScript 1.x 迁移到 2.x

在版本 2.x 中，所有公共方法都已合并到 `ADB.va.MediaHeartbeat` 类中，从而更加便于开发人员使用。 此外，所有配置现在都已合并到 `ADB.va.MediaHeartbeatConfig` 类中。

有关从 1.x 迁移到 2.x 的信息，请参阅旧版实施文档。
