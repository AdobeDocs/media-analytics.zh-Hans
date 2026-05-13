---
title: 从独立Media SDK迁移到Adobe Launch - Web (JS)
description: 了解如何从 Media SDK 迁移到适用于 JS 的 Launch。
exl-id: 19b506b2-3070-4a5e-9732-a5cd0867afde
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/N4Fcbg3R9tT9cjUcaw-kcUm6h-QT8TYwatdCe1IdsaM
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c069c44e-5426-4c1a-accc-8028662f2fde
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 466
ht-degree: 77%

---

# 从独立 Media SDK 迁移到 Adobe Launch - Web (JS)

>[!NOTE]
>Adobe Experience Platform Launch 已更名为 Experience Platform 中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=zh-Hans)。

## 功能差异

* *Launch* - Launch 为您提供了一个 UI，可引导您设置、配置和部署基于 Web 的媒体跟踪解决方案。 Launch 改进了 Dynamic Tag Management (DTM)。
* *Media SDK* - Media SDK 为您提供了针对特定平台（例如：Android、iOS 等）设计的媒体跟踪库。 Adobe 建议使用 Media SDK 来跟踪移动应用程序中的媒体使用情况。

## 配置

### 独立 Media SDK

在独立Media SDK中，您可以在应用程序中配置跟踪配置
并在创建跟踪器时将其传递给SDK。

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

除了`MediaHeartbeat`配置外，页面还必须配置并传递
用于按顺序跟踪媒体的`AppMeasurement`实例和`VisitorAPI`实例
才能正常工作。

### Launch 扩展

1. 在Experience Platform Launch中，单击的[!UICONTROL 扩展]选项卡，
Web属性。
1. 在[!UICONTROL 目录]选项卡上，找到Adobe Media Analytics for Audio并
视频扩展，然后单击[!UICONTROL 安装]。
1. 在扩展设置页面中，配置跟踪参数。
Media 扩展将使用已配置的参数进行跟踪。

   ![](assets/launch_config_js.png)

[Launch用户指南 — 安装和配置媒体扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html#install-and-configure-the-ma-extension)

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

### Launch

Launch 提供了两种创建跟踪基础结构的方法。 这两种方法都使用 Media Analytics Launch 扩展：

1. 从网页中使用媒体跟踪 API。

   在此方案中，Media Analytics 扩展将媒体跟踪 API 导出到全局窗口对象中的已配置变量：

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. 从另一个 Launch 扩展中使用媒体跟踪 API。

   在此方案中，您将使用由 `get-instance` 和 `media-heartbeat` 共享模块公开的媒体跟踪 API。

   >[!NOTE]
   >
   >共享模块不可用于网页。 您只能从其他扩展中使用共享模块。

   使用 `get-instance` 共享模块创建 `MediaHeartbeat` 实例。
将委派对象传递给公开 `getQoSObject()` 和 `getCurrentPlaybackTime()` 函数的 `get-instance`。

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   通过 `media-heartbeat` 共享模块访问 `MediaHeartbeat` 常量。

## 相关文档

### Media SDK

* [设置 JavaScript 2.x](/help/legacy/media-sdk/setup/setup-javascript/set-up-js-2.md)
* [Media SDK JS API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

### Launch

* [Launch概述](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html)
* [Media Analytics扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html)
