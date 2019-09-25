---
seo-title: 设置 JavaScript
title: 设置 JavaScript
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 设置 JavaScript{#set-up-javascript}

## 先决条件

* **获取有效的配**&#x200B;置参数在设置分析帐户后，可以从Adobe代表处获取这些参数。
* **在媒`AppMeasurement`体应用程序中实施JavaScript**&#x200B;有关Adobe Mobile SDK文档的详细信息，请参 [阅使用JavaScript实施分析。](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **在媒体播放器中提供以下功能：**

   * *可订阅播放器事件的 API -* Media SDK 要求您在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* - 此信息包括媒体名称和播放头位置等详细信息。

1. 将[下载](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)的库添加到您的项目中。为方便起见，请创建对类的本地引用。

   1. Expand the `MediaSDK-js-v2.*.zip` file that you downloaded.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      此核心 JavaScript 文件必须在一个您站点的所有页面都能访问的 Web 服务器上托管。下一步中需要使用这些文件的路径。

   1. 在所有站点页面上引用 `MediaSDK.min.js`

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. 例如：

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. 要快速验证是否成功导入了   库，请实例化 `ADB.va.MediaHeartbeatConfig` 类。

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. 为便于访问 API，请创建对 `MediaHeartbeat` 类的本地引用。

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

   本节将帮助您了解 `MediaHeartbeat` 配置参数以及如何在您的 `MediaHeartbeat` 实例中设置正确的配置值，以便进行准确跟踪。

   以下是 `MediaHeartbeatConfig` 初始化示例:

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

1. Implement the `MediaHeartbeatDelegate` protocol.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. 此实例将用于以下所有的跟踪事件。

   >[!TIP]
   >
   >`MediaHeartbeat` 需要一个实例 `AppMeasurement` 来向Adobe Analytics发送调用。 以下是 `AppMeasurement` 实例的示例：

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## 在 JavaScript 中从版本 1.x 迁移到 2.x

在版本 2.x 中，所有公共方法都已合并到 `ADB.va.MediaHeartbeat` 类中，从而更加便于开发人员使用。此外，所有配置现在都已合并到 `ADB.va.MediaHeartbeatConfig` 类中。

For detailed information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
