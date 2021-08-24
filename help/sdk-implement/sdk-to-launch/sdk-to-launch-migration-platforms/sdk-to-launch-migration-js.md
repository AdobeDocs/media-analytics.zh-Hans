---
title: “从独立Media SDK迁移到AdobeLaunch - Web(JS)”
description: 了解如何从Media SDK迁移到Launch for JS。
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: ceef739641ae07ea05314fb2bc23028de6ee5efb
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 89%

---

# 从独立 Media SDK 迁移到 Adobe Launch - Web (JS)

## 功能差异

* *Launch* - Launch 为您提供了一个 UI，可引导您设置、配置和部署基于 Web 的媒体跟踪解决方案。Launch 改进了 Dynamic Tag Management (DTM)。
* *Media SDK* - Media SDK 为您提供了针对特定平台（例如：Android、iOS 等）设计的媒体跟踪库。Adobe 建议使用 Media SDK 来跟踪移动应用程序中的媒体使用情况。

## 配置

### 独立 Media SDK

在独立 Media SDK 中，您可以在应用程序中配置跟踪配置，并在创建跟踪器时将其传递给 SDK。

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channel";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

除了 `MediaHeartbeat` 配置外，页面还必须配置和传递用于媒体跟踪的 `AppMeasurement` 实例和 `VisitorAPI` 实例，才能正常工作。

### Launch 扩展

1. 在 Experience Platform Launch 中，单击适用于您的 Web 属性的[!UICONTROL 扩展]选项卡。
1. 在[!UICONTROL 目录]选项卡上，找到 Adobe Media Analytics for Audio and Video 扩展，然后单击[!UICONTROL 安装]。
1. 在扩展设置页面中，配置跟踪参数。
Media 扩展将使用已配置的参数进行跟踪。

   ![](assets/launch_config_js.png)

[Launch 用户指南 - 安装和配置媒体扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

## 跟踪器创建差异

### Media SDK

1. 将 Media Analytics 库添加到您的开发项目。
1. 创建配置对象 (`MediaHeartbeatConfig`)。
1. 实施委派协议，公开 `getQoSObject()` 和 `getCurrentPlaybackTime()` 函数。
1. 创建“媒体心率”实例 (`MediaHeartbeat`)。

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

<!--  Dead Link - from 2019 - can't locate where this should go
[Media SDK - Tracker Creation](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html) -->

### Launch

Launch 提供了两种创建跟踪基础结构的方法。这两种方法都使用 Media Analytics Launch 扩展：

1. 从网页中使用媒体跟踪 API。

   在此方案中，Media Analytics 扩展将媒体跟踪 API 导出到全局窗口对象中的已配置变量：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 从另一个 Launch 扩展中使用媒体跟踪 API。

   在此方案中，您将使用由 `get-instance` 和 `media-heartbeat` 共享模块公开的媒体跟踪 API。

   >[!NOTE]
   >
   >共享模块不可用于网页。您只能从其他扩展中使用共享模块。

   使用 `get-instance` 共享模块创建 `MediaHeartbeat` 实例。
将委派对象传递给公开 `getQoSObject()` 和 `getCurrentPlaybackTime()` 函数的 `get-instance`。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   通过 `media-heartbeat` 共享模块访问 `MediaHeartbeat` 常量。

## 相关文档

### Media SDK

* [设置 JavaScript 2.x](/help/sdk-implement/setup/setup-javascript/set-up-js-2.md)
* [设置 JavaScript 3.x](/help/sdk-implement/setup/setup-javascript/set-up-js-3.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Launch 概述](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans)
* [Media Analytics 扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
