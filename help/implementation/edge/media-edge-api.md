---
title: 设置适用于流媒体的Media Edge API
description: 使用Media Edge API将流媒体数据直接发送到Edge Network。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 设置适用于流媒体的Media Edge API

如果您无法使用Web SDK、Mobile SDK或Roku Edge SDK（例如，在自定义或不支持的运行时上），则可以使用Media Edge API直接将流媒体数据发送到Edge Network。 该API使用RESTful HTTP调用，是完全可自定义的。

* **先决条件**：完成[Edge实施概述](overview.md)（架构、数据集、启用[!UICONTROL Media Analytics]的数据流）。

## 将媒体事件发送到Edge Network

媒体事件将发送到`/ee/va/v1/`端点，通过`configId`查询参数作为您的数据流的键值。 例如，会话以`sessionStart`的POST开头：

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionStart?configId=<datastreamID>" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": { "name": "video-123", "playerName": "player_name", "contentType": "vod", "length": 128, "channel": "sample_channel" },
        "playhead": 0
      }
    }
  }]
}'
```

响应将返回所有后续事件都必须包含的会话ID。 有关完整的端点集、请求/响应格式和OpenAPI规范，请参阅[Media Edge API参考](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)。

## 跟踪媒体事件

有关确切负载，请参阅每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Media Edge API**&#x200B;选项卡。

## 下一步

实施完成后，您可以[为Edge实施设置报表](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Media Edge API引用](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)
>* [事件概述](/help/implementation/events/overview.md)
>* [变量概述](/help/implementation/variables/overview.md)
