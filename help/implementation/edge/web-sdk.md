---
title: 设置适用于流媒体的Web SDK
description: 配置Adobe Experience Platform Web SDK (alloy.js)以将流媒体数据发送到Edge Network。
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
source-wordcount: '283'
ht-degree: 5%
---
# 设置适用于流媒体的Web SDK

Adobe Experience Platform [Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)（`alloy.js`，版本2.20.0或更高版本）的`streamingMedia`组件收集您网站上的媒体会话数据并将这些数据发送至Edge Network。 本页介绍代码内(`alloy.js`)配置。 要改为通过标记配置Web SDK，请参阅[为流媒体设置Web SDK标记扩展](web-sdk-tags.md)。

* **先决条件**：
  * 完成[Edge实施概述](overview.md)（架构、数据集、启用了[!UICONTROL Media Analytics]的数据流）。
  * 安装Web SDK 2.20.0或更高版本。 请参阅[安装Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/install/overview)。

## 配置流媒体组件

将`streamingMedia`组件添加到您的`alloy`配置：

```js
alloy("configure", {
  edgeConfigId: "<datastreamID>",
  streamingMedia: {
    channel: "sample_channel",
    playerName: "player_name",
    appVersion: "app_version",
    mainPingInterval: 10,
    adPingInterval: 10
  }
});
```

有关完整的配置详细信息，请参阅[`streamingMedia`命令](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/configure/streamingmedia)。

### 从Media JS SDK迁移

如果您从Media JS (3.x) SDK迁移，则Web SDK [`getMediaAnalyticsTracker`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/getmediaanalyticstracker)命令返回一个与[3.x Media SDK](/help/implementation/analytics-only/javascript.md)公开相同API的跟踪器实例，因此您的现有跟踪调用将继续工作。

## 跟踪媒体事件

配置SDK后，通过调用[`sendEvent`](https://experienceleague.adobe.com/cn/docs/experience-platform/collection/js/commands/sendevent/overview)发送每个媒体事件。 有关确切负载，请参阅每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Web SDK**&#x200B;选项卡。

## 下一步

实施完成后，您可以[为Edge实施设置报表](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Web SDK 概述](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/js-overview)
>* [事件概述](/help/implementation/events/overview.md)
>* [变量概述](/help/implementation/variables/overview.md)
