---
title: 快速启动
description: null
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 快速启动{#quick-start}

>[!TIP]
>
>收集完成对Media Analytics(MA)Collection API后端服 [务器的Session](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) request所需的请求数据。 通过手动发送请求（使用 `curl` 或 Postman 等），您可以快速验证您的请求数据。这将对请求中是否存在与不正确数据类型或信息有关的任何问题立即提供反馈。使用 [JSON 验证架构](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)来验证您是否提供了正确的请求数据。

1. 收集为运行任何 Experience Cloud 应用程序而必须提供的标准、必需的 Adobe Analytics 和访客数据：

   * Visitor Experience Cloud 组织 ID
   * 访客Experience cloud用户ID
   * Analytics 报表包 ID
   * Analytics 跟踪服务器 URL

1. 为 `sessions` 请求正文创建一个 JSON 对象，其中包含进行成功调用所需的最小数据。例如：

   ```
   { 
       "playerTime": { 
           "playhead": 0, 
           "ts": 1234560890123 
       }, 
       "eventType": "sessionStart", 
       "params": { 
           "media.playerName": "sample-html5-api-player", 
           "analytics.trackingServer": "[YOUR_TS]", 
           "analytics.reportSuite": "[YOUR_RSID]", 
           "media.contentType": "VOD", 
           "media.length": 60.39333333333333, 
           "media.id": "MA Collection API Sample Player", 
           "visitor.marketingCloudOrgId": "[YOUR_ORG_ID]", 
           "visitor.marketingCloudUserId": "[YOUR_ECID]",
           "media.name": "ClickMe", 
           "media.channel": "sample-channel", 
           "media.sdkVersion": "va-api-0.0.0", 
           "analytics.enableSSL": false 
       } 
   }
   ```

   >[!NOTE]
   >
   >您必须在JSON请求主体中使用正确的数据类型。 E.g., `analytics.enableSSL` requires a boolean, `media.length` is numeric, etc. You can check parameter types and mandatory versus optional requirements by checking the [JSON validation schemas.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)

1. 将会话请求发送到MA Collection API端点。 如果您的请求负载无效，请确定问题并重试，直到接收到 `201 Created` 响应。In this `curl` example, the JSON request body is in a file named `sample_data_session`:

   ```
   $ curl -i -d \ 
     @sample_data_session https://{uri}/api/v1/sessions \ 
     > curl.sessions.out 
   
   $ cat curl.sessions.out 
   HTTP/1.1 201 Created 
   Server: nginx/1.13.5 
   Date: Mon, 18 Dec 2017 22:34:12 GMT 
   Content-Type: application/octet-stream 
   Content-Length: 0 
   Connection: keep-alive 
   Location: /api/v1/sessions/a39c037641f[...]  # <== Session ID  
   Access-Control-Allow-Origin: * 
   Access-Control-Allow-Methods: OPTIONS,POST,PUT 
   Access-Control-Allow-Headers: Content-Type 
   Access-Control-Expose-Headers: Location
   ```

如果[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)成功，您将接收到与上述相同的 `201 Created` 响应。该响应将会话 ID 包含在 Location 标头中。会话 ID 是响应中的关键信息，因为所有后续跟踪调用都需要会话 ID。After a successful return of a [Sessions request](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md), you can confidently proceed with implementing video tracking using the MA API in your video player.
