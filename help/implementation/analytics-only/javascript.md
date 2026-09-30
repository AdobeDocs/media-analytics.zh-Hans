---
title: 设置适用于流媒体的JavaScript
description: 为仅限Analytics的流媒体实施安装和配置Media SDK for JavaScript (3.x) 。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 3%
---
# 设置适用于流媒体的JavaScript

Media SDK for JavaScript (3.x)将流媒体数据直接发送到Adobe Analytics。 本页介绍手动JavaScript安装。 要改为通过标记部署SDK，请参阅[设置Media Analytics标记扩展](javascript-tags.md)。 对于新的实施，请考虑使用[Web SDK](/help/implementation/edge/web-sdk.md)通过Edge Network数据流将数据发送到Adobe Analytics。

* **先决条件**：
  * 完成[仅限Analytics的实施概述](overview.md)。
  * 实施[AppMeasurement](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/js/overview)和[访客ID服务](https://experienceleague.adobe.com/zh-hans/docs/analytics/implementation/id/appmeasurement)。
  * [下载适用于JavaScript的Media SDK](/help/getting-started/download-sdks.md)。

## 安装和配置SDK

1. 在所有页面均可访问的Web服务器上安装主机`MediaSDK.js`（来自下载的`libs`目录），并在每个页面上引用它：

   ```html
   <script type="text/javascript" src="https://INSERT-DOMAIN-AND-PATH/MediaSDK.js"></script>
   ```

1. 每页配置一次Media SDK，传递您设置为先决条件的`appMeasurement`实例：

   ```js
   var mediaConfig = new ADB.MediaConfig();
   mediaConfig.trackingServer = "<media_collection_server>";
   mediaConfig.playerName = "player_name";
   mediaConfig.channel = "sample_channel";
   mediaConfig.appVersion = "app_version";
   mediaConfig.ssl = true;
   
   ADB.Media.configure(mediaConfig, appMeasurement);
   ```

   >[!NOTE]
   >
   >`mediaConfig.trackingServer`变量是您的&#x200B;**媒体收集服务器**（例如，`[namespace].hb-api.omtrdc.net`）。 此收集服务器不同于AppMeasurement实例中配置的Analytics跟踪服务器。

1. 创建具有`getInstance`的跟踪器实例。 使实例在整个媒体会话中保持可访问状态：

   ```js
   var tracker = ADB.Media.getInstance();
   ```

## 跟踪媒体事件

在创建跟踪器后，使用其跟踪器方法跟踪每个媒体事件。 查看每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Media SDK JS 3.x**&#x200B;选项卡，了解确切的调用。

## 下一步

实施完成后，您可以[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [适用于JavaScript 3.x API的Media SDK参考](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/APIReference.md)
>* [从JS SDK 2.x迁移到3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/sdks/js/3.x/docs/MigrationGuide.md)
>* [设置Media Analytics标记扩展](javascript-tags.md)
>* [事件概述](/help/implementation/events/overview.md)
