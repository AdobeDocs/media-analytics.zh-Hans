---
title: 访问 Media Analytics SDK 的下载链接
description: 可用平台（包括 Android、iOS、JavaScript、Chromecast 和 Roku）的 SDK 下载链接。
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 21%

---

# 获取Media SDK、使用标记的扩展以及OTT SDK {#download-sdks}

此页面上的信息包括用于下载当前媒体SDK和获取媒体扩展的链接。

此页面上的信息包括用于下载当前Media SDK以及获取使用标记的媒体扩展的链接。

Adobe Experience Platform中的标记是Adobe推出的新一代网站标记和移动SDK管理功能。 标记提供了一种简单的方式来部署和管理用来改善相关客户体验的分析、营销和广告解决方案。 有关标记的其他信息，请参阅 [标记概述](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=zh-Hans)


>[!NOTE]
>
>有关下载旧版SDK的信息，请参阅 [旧版 — 下载SDK](/help/legacy/legacy-download-sdks.md).<br>
>有关支持终止的重要信息，请参阅 [终止支持常见问题解答](/help/additional-resources/end-of-support-faqs.md).

## Media SDK和移动库 {#media-sdks-libraries}

### Web实施 {#download-web-sdk}

| 支持的平台 | 版本 |  API   |  文档  |  样例  |
|:---:|---|---|---|---|
| ![JavaScript图标](assets/javascript-icon.png) | Web - [适用于JS的Media SDK v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [JavaScript API参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [为JavaScript设置Media SDK v3.x](/help/implementation/media-sdk/setup/web-implementation.md) | [适用于JS的Media SDK v3.0.2示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![JavaScript图标](assets/javascript-icon.png) | Web — 媒体扩展 |  | [Adobe MediumAnalytics(3.x SDK)for Audio and Video扩展 — 使用标记（数据收集）](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=en) | [Adobe MediumAnalytics(3.x SDK)for Audio and Video扩展示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### 移动设备实施 {#get-mobile-extension}

| 支持的平台 | 版本 |  文档   |  示例  |
|:---:|---|---|---|
| ![Android图标](assets/android-icon.png) | Android — 媒体扩展 | [移动SDK文档](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics — 用于音频和视频的Media Analytics示例](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Apple iOS图标](assets/ios-icon.png)<br>添加tvOS图标 | iOS / tvOS — 媒体扩展 | [移动SDK文档](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics — 用于音频和视频的Media Analytics示例](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### 过顶实施 {#download-ott-libraries}

| 支持的平台 | 版本 |  API   |  文档  |
|:---:|---|---|---|
| ![Chromecast图标](assets/chromecast-icon.png) | [适用于 Chromecast v3.0.3 的 SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Chromecast API 引用](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [为Chromecast设置Mobile SDK v3.x](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Roku图标](assets/roku-icon.png) | [适用于Roku的SDK v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Roku API参考](/help/implementation/media-sdk/setup/set-up-roku.md) | [为Roku设置Mobile SDK v2.x](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Adobe 扩展 {#adobe-extensions}

### 流媒体扩展 {#streaming-media-extension}

的 **Adobe MediumAnalytics for Audio and Video扩展** 需要Adobe Analytics for Media附加组件SKU。 要了解更多信息，请联系您的Adobe销售代表、客户经理或客户成功经理。

有关安装、配置和实施的详细信息 **Adobe MediumAnalytics for Audio and Video扩展**，请参阅 [Adobe MediumAnalytics for Audio and Video扩展概述](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) 和 [配置Media Analytics扩展](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension).

### Analytics 扩展 {#analytics-extension}

[Analytics扩展v1.6或更高版本](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en) — 此扩展允许您加载Adobe Experience Platform Web SDK Javascript库，以将数据发送到Adobe解决方案。 的 **Analytics扩展** v1.6或更高版本是必需的。

有关配置此扩展的信息，请参阅 [配置Adobe Analytics扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en).

### Experience Cloud ID 扩展 {#cloud-id-extension}

[Experience CloudID扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en) — 此扩展实施了Experience CloudID服务，在所有Experience Cloud解决方案中标识访客。 Experience CloudID服务是Adobe Experience Platform中的一个个性化扩展。

使用此扩展可将Experience CloudIdentity Service与您的资产相集成。 通过Experience Cloud标识服务，您可以为网站访客创建并存储唯一的永久标识符。

有关配置此扩展的信息，请参阅 [配置Experience CloudID扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en)
