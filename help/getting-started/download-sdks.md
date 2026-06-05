---
title: 获取媒体SDK、扩展和API
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
source-git-commit: b18eab3deb3d15a08adf2f7ecf61d73235bbc6e5
workflow-type: tm+mt
source-wordcount: 575
ht-degree: 32%

---

# 获取媒体SDK、扩展和API

## Edge实施（推荐） {#edge-sdks}

Edge实施收集数据一次，然后通过Adobe Experience Platform Edge Network将数据交付到多个目标：Adobe Analytics、Customer Journey Analytics、Adobe Journey Optimizer和Real-Time CDP。 对于没有本机SDK的平台（例如智能电视、游戏机和机顶盒），请使用Media Edge API。

| | 文档 | 示例 |
|:---:|---|---|
| [![JavaScript图标](assets/javascript-icon.png)](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/install/overview)<br>[Web SDK](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/install/overview) | [为流媒体设置Web SDK](/help/implementation/edge/web-sdk.md) | [样本](https://github.com/adobe/alloy-samples/blob/main/media-collection/STANDALONE.md) |
| [![扩展图标](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html)<br>[Web SDK标记扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/web-sdk/overview.html) | [为流媒体设置Web SDK标记扩展](/help/implementation/edge/web-sdk-tags.md) | [样本](https://github.com/adobe/alloy-samples/blob/main/media-collection/TAGS_IMPL.md) |
| [![Android图标](assets/android.png)](https://github.com/adobe/aepsdk-media-android)<br>[Android SDK](https://github.com/adobe/aepsdk-media-android) | [为流媒体设置Android](/help/implementation/edge/android.md) | [样本](https://github.com/adobe/aepsdk-media-android/tree/main/code/testapp) |
| [![Apple iOS图标](assets/apple.png)](https://github.com/adobe/aepsdk-media-ios)<br>[iOS / tvOS SDK](https://github.com/adobe/aepsdk-media-ios) | [为流媒体设置iOS](/help/implementation/edge/ios.md) | [样本](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| [![扩展图标](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[Android标记扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [为流媒体设置Android标记扩展](/help/implementation/edge/android-tags.md) | |
| [![扩展图标](assets/plug.svg)](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)<br>[iOS / tvOS标记扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [为流媒体设置iOS标记扩展](/help/implementation/edge/ios-tags.md) | |
| [![Roku图标](assets/roku-icon.png)](https://github.com/adobe/aepsdk-roku)<br>[Roku SDK](https://github.com/adobe/aepsdk-roku) | [为流媒体设置Roku](/help/implementation/edge/roku.md) | [样本](https://github.com/adobe/aepsdk-roku/tree/main/sample/simple-videoplayer-channel) |
| [![API图标](assets/api.png)](https://developer.adobe.com/data-collection-apis/docs/api/media-edge)<br>[Media Edge API](https://developer.adobe.com/data-collection-apis/docs/api/media-edge) | [设置Media Edge API](/help/implementation/edge/media-edge-api.md) | [样本](https://developer.adobe.com/data-collection-apis/docs/getting-started/media-edge-examples) |

## 仅限Analytics的实施 {#analytics-only-sdks}

这些SDK和扩展将数据直接发送到Adobe Analytics。 对于新的实施，请使用上面的Edge实施。 要将现有Analytics数据引入Customer Journey Analytics或其他Experience Platform应用程序，请使用[Analytics源连接器](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/analytics)。

| | 文档 | 示例 |
|:---:|---|---|
| [![JavaScript图标](assets/javascript-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2)<br>[Media SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [为流媒体设置JavaScript](/help/implementation/analytics-only/javascript.md) | [样本](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| [![扩展图标](assets/plug.svg)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hans)<br>[媒体扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hans) | [使用流媒体标记设置JavaScript](/help/implementation/analytics-only/javascript-tags.md) | [样本](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| [![Chromecast图标](assets/chromecast-icon.png)](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3)<br>[Chromecast SDK 3.x](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [为流媒体设置Chromecast](/help/implementation/analytics-only/chromecast.md) | [样本](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/chromecast/samples/BasicPlayerSample) |
| [![API图标](assets/api.png)](/help/implementation/media-collection-api/mc-api-overview.md)<br>[媒体收集API](/help/implementation/media-collection-api/mc-api-overview.md) | [设置媒体收集API](/help/implementation/analytics-only/media-collection-api.md) | |
