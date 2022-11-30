---
title: 访问 Media Analytics SDK 的下载链接
description: 可用平台（包括 Android、iOS、JavaScript、Chromecast 和 Roku）的 SDK 下载链接。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '645'
ht-degree: 100%

---

# 获取媒体 SDK、使用标记的扩展和 OTT SDK {#download-sdks}

此页面上的信息包括用于下载当前媒体 SDK 和获取媒体扩展的链接。

此页面上的信息包括用于下载当前媒体 SDK 和获取使用标记的媒体扩展的链接。

Adobe Experience Platform 中的标记是 Adobe 推出的新一代网站标记和移动 SDK 管理功能。标记提供一种简单的方式以部署和管理强化相关客户体验所需的分析、营销和广告解决方案。有关标记的其他信息，请参阅[标记概述](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=zh-Hans)


>[!NOTE]
>
>有关下载旧版 SDK 的信息，请参阅[旧版 - 下载 SDK](/help/legacy/legacy-download-sdks.md)。<br>
>有关终止支持的重要信息，请参阅[终止支持常见问题解答](/help/additional-resources/end-of-support-faqs.md)。

## 媒体 SDK 和移动库 {#media-sdks-libraries}

### Web 实施 {#download-web-sdk}

| 支持的平台 | 版本 |  API   |  文档  | 示例 |
|:---:|---|---|---|---|
| ![JavaScript 图标](assets/javascript-icon.png) | Web - [适用于 JS v3.0.2 的媒体 SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API 参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [设置适用于 JavaScript 的媒体 SDK v3.x](/help/implementation/media-sdk/setup/web-implementation.md) | [适用于 JS 的媒体 SDK v3.0.2 示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript 图标](assets/javascript-icon.png) | Web - 媒体扩展 |  | [Adobe Media Analytics (3.x SDK) for Audio and Video 扩展 - 使用标记（数据收集）](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hans) | [Adobe Media Analytics (3.x SDK) for Audio and Video 扩展示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### 移动实施 {#get-mobile-extension}

| 支持的平台 | 版本 | 文档 | 示例 |
|:---:|---|---|---|
| ![Android 图标](assets/android-icon.png) | Android - 媒体扩展 | [移动 SDK 文档](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Media Analytics for Audio and Video 示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS 图标](assets/ios-icon.png)<br>添加 tvOS 图标 | iOS / tvOS - 媒体扩展 | [移动 SDK 文档](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics - Media Analytics for Audio and Video 示例](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### 过顶实施 {#download-ott-libraries}

| 支持的平台 | 版本 |  API   |  文档  |
|:---:|---|---|---|
| ![Chromecast 图标](assets/chromecast-icon.png) | [适用于 Chromecast 的 SDK v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API 参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [设置适用于 Chromecast 的移动 SDK v3.x](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku 图标](assets/roku-icon.png) | [适用于 Roku 的 SDK v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Roku API 参考](/help/implementation/media-sdk/setup/set-up-roku.md) | [设置适用于 Roku 的移动 SDK v2.x](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Adobe 扩展 {#adobe-extensions}

### 流媒体扩展 {#streaming-media-extension}

**Adobe Media Analytics for Audio and Video 扩展**&#x200B;需要 Adobe Analytics for Media 附加组件 SKU。要了解更多信息，请联系您的 Adobe 销售代表、客户经理或客户成功经理。

有关安装、配置和实施 **Adobe Media Analytics for Audio and Video 扩展**&#x200B;的详细信息，请参阅 [Adobe Media Analytics for Audio and Video 扩展概述](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=zh-Hans)和[配置 Media Analytics 扩展](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension)。

### Analytics 扩展 {#analytics-extension}

[Analytics 扩展 v1.6 或更高版本](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=zh-Hans) - 通过此扩展，可加载 Adobe Experience Platform Web SDK Javascript 库以将数据发送到 Adobe 解决方案。需要 **Analytics 扩展** v1.6 或更高版本。

有关配置此扩展的信息，请参阅[配置 Adobe Analytics 扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=zh-Hans)。

### Experience Cloud ID 扩展 {#cloud-id-extension}

[Experience Cloud ID 扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=zh-Hans) - 此扩展实施 Experience Cloud ID 服务，该服务在所有 Experience Cloud 解决方案间标识访客。Experience Cloud ID 服务是 Adobe Experience Platform 中的个性化扩展。

使用此扩展将 Experience Cloud Identity Service 融入您的财产。通过 Experience Cloud Identity Service，可为网站访客创建并存储唯一且永久的标识符。

有关配置此扩展的信息，请参阅[配置 Experience Cloud ID 扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=zh-Hans)。
