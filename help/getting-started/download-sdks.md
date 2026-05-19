---
title: 访问 Media Analytics SDK 的下载链接
description: 可用平台（包括 Android、iOS、JavaScript、Chromecast 和 Roku）的 SDK 下载链接。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c77ba355-6681-41fe-b719-563d3f507fdb
  - id: df312454-73c4-43f6-a90e-18f5043f074c
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 84%

---

# 获取 Media SDK、使用标记的扩展和 OTT SDK {#download-sdks}

此页面上的信息包括用于下载当前 Media SDK 和获取使用标记的媒体扩展的链接。

Adobe Experience Platform 中的标记是 Adobe 推出的新一代网站标记和移动 SDK 管理功能。 标记提供一种简单的方式以部署和管理强化相关客户体验所需的分析、营销和广告解决方案。 有关标记的其他信息，请参阅[标记概述](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=zh-Hans)。


>[!NOTE]
>
>有关下载旧版SDK的信息，请参阅[旧版 — 下载SDK](/help/legacy/legacy-download-sdks.md)。<br>
>有关终止支持的重要信息，请参阅[终止支持常见问题解答](/help/additional-resources/end-of-support-faqs.md)。

## Media SDK 和移动库 {#media-sdks-libraries}

### Web 实施 {#download-web-sdk}

| 支持的平台 | 支持的解决方案 | 实施方法 | 版本 |  API   |  文档  |  示例  |
|:---:|---|---|---|---| ---| ---|
| ![JavaScript图标&#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | 仅 Analytics | Web - [适用于 JS v3.0.2 的 Media SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API 参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [使用JavaScript安装Media SDK](/help/implementation/media-sdk/setup/web-implementation.md) | [适用于 JS 的 Media SDK v3.0.2 示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript图标&#x200B;](assets/javascript-icon.png)</br>**JavaScript API** | Adobe Analytics | 仅 Analytics | Web - 媒体扩展 |  | [Adobe Media Analytics (3.x SDK) for Audio and Video 扩展 - 使用标记（数据收集）](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hans) | [Adobe Media Analytics (3.x SDK) for Audio and Video 扩展示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web - Experience Platform Edge |  | [使用Edge Network实施Customer Journey Analytics流媒体收藏集](/help/implementation/edge/implementation-edge.md) <p>和</p><p>[使用Adobe Experience Platform Web SDK将Web数据发送到Edge](/help/implementation/edge/edge-web-sdk.md)</p> | |

### 移动实施 {#get-mobile-extension}

| 支持的平台 | 支持的解决方案 | 实施方法 | 版本 |  文档   |  示例  |
|:---:|---|---|---|---|---|
| ![Android图标&#x200B;](assets/android-icon.png)</br>**Android** | Adobe Analytics | 仅 Analytics | Android - 媒体扩展 | [移动 SDK 文档](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video 示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS 图标&#x200B;](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | 仅 Analytics | iOS / tvOS - 媒体扩展 | [移动 SDK 文档](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics - Media Analytics for Audio and Video 示例](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Android图标&#x200B;](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android - Experience Platform Edge | [使用JavaScript安装Media SDK](/help/implementation/edge/implementation-edge.md) | |
| ![Apple iOS 图标&#x200B;](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS - Experience Platform Edge | [使用JavaScript安装Media SDK](/help/implementation/edge/implementation-edge.md) |  |

### 过顶实施 {#download-ott-libraries}

| 支持的平台 | 支持的解决方案 | 实施方法 | 版本 |  API   |  文档  |
|:---:|---|---|---|---|---|
| ![Chromecast图标&#x200B;](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | 仅 Analytics | [适用于 Chromecast 的 SDK v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API 参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [设置适用于 Chromecast 的移动 SDK v3.x](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku图标&#x200B;](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | 仅 Analytics | [适用于 Roku 的 SDK v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [设置适用于 Roku 的移动 SDK v2.x](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Roku图标&#x200B;](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [使用JavaScript安装Media SDK](/help/implementation/edge/implementation-edge.md) |
