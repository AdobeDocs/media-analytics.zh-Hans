---
title: 测量选项
description: null
uuid: null
translation-type: tm+mt
source-git-commit: 47b4c7fe09da0d38c8faae1c3b4293ce48552bdc

---


# 测量选项

您可以通过Adobe Media Analytics扩展、Media SDK或Media Collection API使用Adobe Launch启用音频和视频跟踪。

## 带有Adobe Media Analytics扩展的Adobe Launch

Adobe Launch是Adobe的新一代标签管理解决方案。 Launch提供了部署和管理所有分析、营销和广告标签的简单方法，这些标签是提升相关客户体验所必需的。 要构建和维护您与Launch的集成，您需要使用扩展。 扩展是JavaScript、HTML和CSS包，它扩展了Launch UI和客户端功能。 有关详细信息，请参 [阅《Experience Platform Launch用户指南》](https://docs.adobe.com/content/help/zh-Hans/launch/using/overview.translate.html)

Adobe Media Analytics(MA)扩展为音频和视频添加核心JavaScript Media SDK(Media 2.x SDK)。 此扩展提供了将 `MediaHeartbeat` 跟踪器实例添加到 Launch 网站或项目的功能。

带有Media Analytics扩展的Adobe Launch需要：
* 您必须是Adobe Experience Cloud客户。
* 必须在网页上部署启动或DTM嵌入代码。
* [Analytics 扩展](https://docs.adobe.com/content/help/zh-Hans/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 扩展](https://docs.adobe.com/content/help/zh-Hans/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK与最常用的媒体播放器集成。

## Media Collection API(RESTful API)

与不支持SDK的播放器集成，或在不需要SDK集成时与播放器集成。<br>从v2.2.0版本开始，视频心跳库(VHL)SDK已更名为Media Analytics SDK，以支持音频和视频跟踪。 Media 2.2.0 SDK完全向后兼容VHL 2.x SDK系列。 名称更改只是命名约定的更改，不代表功能更改。
