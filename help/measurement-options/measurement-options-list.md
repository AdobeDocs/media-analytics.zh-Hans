---
title: 测量选项
description: null
uuid: null
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 96%

---


# 测量选项{#measurement-options}

您可以使用包含 Adobe Media Analytics 扩展的 Adobe Launch、Media SDK 或媒体收集 API 启用音频和视频跟踪。

## 包含 Adobe Media Analytics 扩展的 Adobe Launch

Adobe Launch 是 Adobe 推出的下一代标记管理解决方案。Launch 为客户提供了一种简单的方式来部署和管理有助于加强相关客户体验的所有分析、营销和广告标记。要自行构建并维护与 Launch 的集成，您需要使用扩展。扩展是一种 JavaScript、HTML 和 CSS 代码包，用于扩展 Launch UI 和客户端功能。有关更多信息，请参阅 [Experience Platform Launch 用户指南](https://experienceleague.adobe.com/docs/launch/using/overview.html)。

Adobe Media Analytics (MA) 扩展添加了适用于音频和视频的核心 JavaScript Media SDK (Media 2.x SDK)。此扩展提供了将 `MediaHeartbeat` 跟踪器实例添加到 Launch 网站或项目的功能。

包含 Media Analytics 扩展的 Adobe Launch 要求您必须满足以下条件：
* 您必须是 Adobe Experience Cloud 客户。
* 您必须在网页上部署 Launch 或 DTM 嵌入代码。
* [Analytics 扩展](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
* [Experience Cloud ID 扩展](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)

## Media SDK

Media SDK 集成了最常用的媒体播放器。

## 媒体收集 API (RESTful API)

与不支持 SDK 的播放器集成，或者在不需要 SDK 集成时实施该 API。<br>从 v2.2.0 版本开始，视频心率库 (VHL) SDK 将重命名为 Media Analytics SDK，以支持音频和视频跟踪。Media 2.2.0 SDK 可以完全向后兼容 VHL 2.x SDK 系列产品。名称更改只是命名约定的更改，不代表功能更改。
