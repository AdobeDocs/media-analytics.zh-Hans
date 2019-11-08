---
title: 从独立的Media SDK迁移到Adobe Launch - Web(JS)
description: 帮助从Media SDK迁移到Launch的说明和代码示例。
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# 从独立的Media SDK迁移到Adobe Launch - Web(JS)

## 功能差异

* *Launch* - Launch为您提供了一个UI，指导您设置、配置和部署基于Web的媒体跟踪解决方案。 Launch改进了动态标签管理(DTM)。
* *Media SDK* - Media SDK为您提供了专为特定平台设计的媒体跟踪库(例如：Android、iOS等)。 Adobe建议使用Media SDK来跟踪移动应用程序中的媒体使用情况。

## 配置

### 独立Media SDK

在独立的Media SDK中，您可以在应用程序中配置跟踪配置，并在创建跟踪器时将其传递给SDK。

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

除了配置之 `MediaHeartbeat` 外，页面还必须配置和传递媒体跟踪 `AppMeasurement` 的实 `VisitorAPI` 例和实例，才能正常工作。

### 启动扩展

1. 在Experience Platform Launch中，单击Web属 [!UICONTROL 性的] “扩展”选项卡。
1. 在“目 [!UICONTROL 录] ”选项卡上，找到“Adobe Media Analytics for Audio andVideo”扩展，然后单击“安 [!UICONTROL 装”]。
1. 在扩展设置页面中，配置跟踪参数。
媒体扩展将使用已配置的参数进行跟踪。

   ![](assets/launch_config_js.png)

[启动用户指南——安装和配置媒体扩展](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

## 跟踪器创建差异

### Media SDK

1. 将媒体分析库添加到您的开发项目。
1. 创建配置对象(`MediaHeartbeatConfig`)。
1. 实施委托协议，公开 `getQoSObject()` 和功 `getCurrentPlaybackTime()` 能。
1. 创建媒体心跳实例(`MediaHeartbeat`)。

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

[Media SDK —— 创建跟踪器](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

### Launch

Launch提供了两种创建跟踪基础架构的方法。 这两种方法都使用Media Analytics Launch Extension:

1. 使用网页中的媒体跟踪API。

   在此方案中，媒体分析扩展将媒体跟踪API导出到全局窗口对象中的已配置变量：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 使用另一个启动扩展的媒体跟踪API。

   在此方案中，您使用由和共享模块公开的媒 `get-instance` 体跟 `media-heartbeat` 踪API。

   >[!NOTE]
   >
   >共享模块不可用于网页。 您只能从其他扩展使用共享模块。

   使用共 `MediaHeartbeat` 享模块创建 `get-instance` 实例。
将委托对象传递给公开 `get-instance` 和函数 `getQoSObject()` 的委 `getCurrentPlaybackTime()` 托对象。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   通过 `MediaHeartbeat` 共享模块访问 `media-heartbeat` 常量。

## 相关文档

### Media SDK

* [设置JS](/help/sdk-implement/setup/set-up-js.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [启动概述](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [媒体分析扩展](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
