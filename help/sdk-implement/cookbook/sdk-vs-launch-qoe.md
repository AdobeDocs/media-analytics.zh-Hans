---
seo-title: 了解Launch与Media SDK差异
title: 了解Launch与Media SDK差异
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# 了解Launch与Media SDK差异

## 功能差异

* *Launch* - Launch为您提供一个UI，可指导您设置、配置和部署基于Web的媒体跟踪解决方案。Launch改进了动态标签管理(DTM)。
* *Media SDK* - Media SDK为您提供专为特定平台设计的媒体跟踪库(例如：Android、iOS等)。Adobe建议媒体SDK跟踪移动应用程序中的媒体使用情况。

## 跟踪器创建差异

### Launch

Launch提供了两种创建跟踪基础结构的方法。这两种方法都使用Media Analytics Launch Extension：

1. 使用网页中的媒体跟踪API。

   在此方案中，Media Analytics Extension将媒体跟踪API导出到全局窗口对象中的已配置变量：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 使用其他Launch扩展中的媒体跟踪API。

   在此方案中，您将使用由和 `get-instance``media-heartbeat` 共享模块公开的媒体跟踪API。

   >[!NOTE]
   >
   >共享模块不可用于网页。您只能使用其他扩展中的共享模块。

   使用 `MediaHeartbeat``get-instance` 共享模块创建实例。
将委托对象传递给 `get-instance` 显示 `getQoSObject()` 和 `getCurrentPlaybackTime()` 函数。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   通过 `MediaHeartbeat``media-heartbeat` 共享模块访问常量。

### Media SDK

1. 将Media Analytics库添加到开发项目。
1. 创建配置对象(`MediaHeartbeatConfig`)。
1. 实施委托协议，暴露 `getQoSObject()` 和 `getCurrentPlaybackTime()` 功能。
1. 创建Media Heartbat实例(`MediaHeartbeat`)。

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

## 相关文档

### Launch

* [启动概述](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [设置JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

