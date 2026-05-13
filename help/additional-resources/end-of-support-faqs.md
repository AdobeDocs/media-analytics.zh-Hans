---
title: 了解 Media Analytics SDK 支持终止常见问题解答
description: 本主题包括关于终止支持 Media Analytics SDK 的常见问题解答。
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/qfM2-x6s-SPf4gw2FpLlg7mPI-h-xZ3Y1TeeVALn3fQ
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 639
ht-degree: 62%

---

# Media Analytics 移动 SDK 终止支持常见问题解答

随着版本4 Mobile SDK于2021年8月31日停止支持，Adobe也终止了对适用于iOS和Android的Media Analytics Mobile SDK的支持。 (这不包括仍受支持的Media Analytics SDK for Web (JS)以及Chromecast和Roku等OTT平台。)

这意味着Adobe不再为Media Analytics Mobile SDK提供修复、与操作系统相关的更新或支持。 迁移到新的Experience Platform SDK时，请注意，必须实施[Media Analytics扩展](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)，才能启用Adobe流媒体服务。


## 五大须知要点

1. 自2021年8月31日起，将不再支持Mobile v4 SDK。 您应该迁移到适用于iOS和Android的Adobe Experience Platform (AEP) Mobile SDK。

1. Adobe流媒体服务实施需要AEP Mobile SDK，并且需要使用Analytics扩展和Media Analytics扩展。 自2021年9月1日起，您应使用新的AEP Mobile SDK和扩展。  使用 Adobe 标记（数据收藏集）配置 Media Analytics 扩展。 有关更多信息，请参阅[从独立的 Media SDK 迁移到 Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. 已终止适用于 iOS 和 Android 的 Media Analytics SDK 的功能开发。 从 2019 年秋季开始引入的新功能均通过 Media Analytics 扩展和媒体收集 API 启用。

1. 客户可以使用Roku SDK和Chromecast SDK以及Adobe Analytics for Streaming Media加载项和Customer Journey Analytics Streaming Media Collection加载项。 将继续以独立 SDK 的形式增强和支持 Roku SDK 和 Chromecast SDK。 如果您使用 JS SDK for Media Analytics，则可继续使用独立的 SDK 或使用 Adobe 数据收藏集（以前称为 Adobe Launch）启用 Media Analytics 扩展。

如果您有任何问题，请联系您的Adobe客户团队。

## 常见问题解答

1. **是否会影响对 Roku SDK 和 Chromecast SDK 的支持？**

   否。  目前，Roku SDK和Chromecast SDK将继续作为独立的SDK进行支持&#x200B;。

1. **此更改是否会影响 Media Analytics JS SDK 实施？**

   否。  使用JS SDK for Media Analytics的客户可以继续使用SDK，或通过Adobe Launch启用它。
 
1. **迁移到 Media Analytics 扩展需要耗费多少工作量？**

   LOE 取决于每位客户的实施，因此会有所不同。  查看下面的迁移文档后，请咨询顾问和/或客户关怀团队以获得其他支持。

   [Media Analytics 扩展：Android 迁移](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

   [Media Analytics 扩展：iOS 迁移](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics扩展：新实施](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/)

1. **是否需要将 Launch 作为标记管理系统？ 如果我不想使用 Launch，应该怎么办？**

   对于移动应用程序用例，不能使用 Launch 作为标记管理系统，因为它适用于 Web 用例。 配置 SDK 扩展需要使用 Launch UI。 这与您使用 Adobe Mobile Services UI 配置 Mobile v4 SDK 的方式相似。 对于安装而言，使用 Launch 的好处是它可以根据您选择的扩展为您提供自定义的安装说明。

1. **终止支持是否会影响适用于 tvOS 的 SDK？**

   是，对于 tvOS（版本 10+），建议的实施是迁移到 Media Analytics 扩展。 有关其他信息，请参阅[从独立的 Media SDK 迁移到 Adobe Launch - iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)。

1. **此项终止支持是否影响适用于 Fire TV 和 AndroidTV 的 SDK？**

   是，对于 Fire TV 和 AndroidTV，建议的实施是迁移到 Media Analytics 扩展。 有关其他信息，请参阅[从独立的 Media SDK 迁移到 Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)。
