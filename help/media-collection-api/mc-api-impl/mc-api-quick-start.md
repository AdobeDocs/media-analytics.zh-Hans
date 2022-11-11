---
title: “流媒体收集API — 快速入门”
description: 流媒体API入门。 了解如何快速验证请求数据。
uuid: ca20bad4-2c8f-406b-833e-b4883a9aa534
exl-id: 08bb5873-f69a-4fdd-8f27-69649b4acb17
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: d89b2af2e2ae5a170ce98f62656cdeed6fe31f19
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 92%

---

# 快速启动{#quick-start}

>[!TIP]
>
>收集必要的请求数据，以成功将[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)发送到 Media Analytics (MA) 收集 API 后端服务器。通过手动发送请求（使用 `curl` 或 Postman 等），您可以快速验证您的请求数据。这将对请求中是否存在与不正确数据类型或信息有关的任何问题立即提供反馈。使用 [JSON 验证架构](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md)验证您提供的请求数据是否正确。

1. 收集运行任何 Experience Cloud 应用程序必须提供的标准、所需 Adobe Analytics 和访客数据：

   * Visitor Experience Cloud 组织 ID
   * Visitor Experience Cloud 用户 ID
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
   >必须在 JSON 请求正文中使用正确的数据类型。例如，`analytics.enableSSL` 要求是布尔值，`media.length` 为数值等。通过查看 [JSON 验证架构](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)，您可以检查参数类型以及必选与可选要求。

1. 将会话请求发送到 MA 收集 API 端点。如果您的请求负载无效，请确定问题并重试，直到接收到 `201 Created` 响应。在此 `curl` 示例中，JSON 请求正文位于名为 `sample_data_session` 的文件中：

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

如果[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)成功，您将接收到与上述相同的 `201 Created` 响应。响应包含 Location 标头中的会话 ID。会话 ID 是响应中的关键信息，因为所有后续跟踪调用都需要该信息。成功返回[会话请求](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md)后，您可以放心地继续使用视频播放器中的 MA API 来实施视频跟踪。
