---
title: 了解Media Analytics SDK终止支持常见问题解答
description: 本主题包括关于终止支持 Media Analytics SDK 的常见问题解答。
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 78%

---

# Media Analytics SDK 终止支持常见问题解答

Adobe 将于 2021 年 8 月 31 日终止支持版本 4 Mobile SDK，届时还将终止对适用于 iOS 和 Android 的 Media Analytics SDK 的支持。2021 年 8 月 31 日之后，Adobe 将不再对 Media Analytics SDK 提供修复、操作系统相关的更新或支持。在迁移到这些新Experience PlatformSDK的过程中，请记住必须实施[Media Analytics扩展](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)才能启用适用于流媒体的Adobe Analytics。

## 五大须知要点

1. 2021 年 8 月 31 日之后，将不再支持 Mobile v4 SDK。您应该迁移到适用于iOS和Android的Adobe Experience Platform(AEP)Mobile SDK。 有关更多信息，请参阅[版本 4 Mobile SDK 支持终止常见问题解答](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)。

1. 适用于流媒体的Analytics实施需要安装AEP Mobile SDK以及使用Analytics和Media Analytics扩展。 从2021年9月1日开始，您应使用新的AEP Mobile SDK和扩展。  Media Analytics 扩展是使用 Adobe Launch 配置的。有关更多信息，请参阅[从独立的 Media SDK 迁移到 Adobe Launch](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. 已终止适用于 iOS 和 Android 的 Media Analytics SDK 的功能开发。从 2019 年秋季开始引入的新功能均通过 Media Analytics 扩展和媒体收集 API 启用。

1. Roku SDK和Chromecast SDK仍可供Analytics用于流媒体客户。 Roku SDK 和 Chromecast SDK 将继续作为独立的 SDK 进行增强和支持。如果您使用 JS SDK for Media Analytics，则可继续使用独立的 SDK 或通过 Adobe Launch 启用 Media Analytics 扩展。

1. 2021 年 9 月 1 日之前，Adobe 可能会自行决定是否为具有重大技术影响或业务泄露风险的问题开发新的修复程序。Adobe 将会根据客户的意见来确定影响程度和泄露等级，以及相应的后续开发活动。

如果您有任何问题，请联系您的 Adobe 客户成功经理。

## 常见问题解答

1. **是否会影响对 Roku SDK 和 Chromecast SDK 的支持？**

   否。目前，Roku SDK 和 Chromecast SDK 将继续作为独立的 SDK 进行支持。
1. **此更改是否会影响 Media Analytics JS SDK 实施？**

   否。使用 JS SDK for Media Analytics 的客户可继续使用 SDK，或通过 Adobe Launch 启用它。

1. **迁移到 Media Analytics 扩展需要耗费多少工作量？**

   LOE 取决于每位客户的实施，因此会有所不同。查看下面的迁移文档后，请咨询顾问和/或客户关怀团队以获得其他支持。

   [Media Analytics 扩展：Android 迁移](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [Media Analytics 扩展：iOS 迁移](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [Media Analytics 扩展：新实施](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **是否需要将 Launch 作为标签管理系统？如果我不想使用 Launch，应该怎么办？**

   对于移动应用程序用例，不能使用 Launch 作为标签管理系统，因为它适用于 Web 用例。配置 SDK 扩展需要使用 Launch UI。这与您使用 Adobe Mobile Services UI 配置 Mobile v4 SDK 的方式相似。对于安装而言，使用 Launch 的好处是它可以根据您选择的扩展为您提供自定义的安装说明。

1. **终止支持是否会影响适用于 tvOS 的 SDK？**

   是，对于 tvOS（版本 10+），建议的实施是迁移到 Media Analytics 扩展。有关更多信息，请参阅[从独立的 Media SDK 迁移到 Adobe Launch - iOS](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)。

1. **终止支持是否会影响适用于 FireTV 和 AndroidTV 的 SDK？**

   是，对于 FireTV 和 AndroidTV，建议的实施是迁移到 Media Analytics 扩展。有关更多信息，请参阅[从独立的 Media SDK 迁移到 Adobe Launch - Android](https://experienceleague.adobe.com/docs/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)。
