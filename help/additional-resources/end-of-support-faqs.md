---
title: 了解 Media Analytics SDK 支持终止常见问题解答
description: 本主题包括关于终止支持 Media Analytics SDK 的常见问题解答。
exl-id: 9601ec17-8421-49d0-9d81-1cfa5e8f37cf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '690'
ht-degree: 100%

---

# Media Analytics 移动 SDK 终止支持常见问题解答

Adobe 将在 2021 年 8 月 31 日终止支持版本 4 移动 SDK，届时还将终止支持适用于 iOS 和 Android 的 Media Analytics 移动 SDK。2021 年 8 月 31 日之后，Adobe 将不再为 Media Analytics 移动 SDK 提供修复、与操作系统相关的更新或支持。在迁移到这些新 Experience Platform SDK 的过程中，请牢记，必须实施 [Media Analytics 扩展](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)，才能启用 Adobe Analytics for Streaming Media。

>[!NOTE]
>Adobe Experience Platform Launch 已更名为 Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=zh-Hans)。


## 五大须知要点

1. 2021 年 8 月 31 日之后，将不再支持 Mobile v4 SDK。您应该迁移到适用于 iOS 和 Android 的 Adobe Experience Platform (AEP) Mobile SDK。有关更多信息，请参阅[版本 4 Mobile SDK 支持终止常见问题解答](https://aep-sdks.gitbook.io/docs/version-4-sdk-end-of-support-faq)。

1. Analytics for Streaming Media 实施需要安装 AEP Mobile SDK 以及使用 Analytics 扩展和 Media Analytics 扩展。从 2021 年 9 月 1 日起，您应使用新的 AEP Mobile SDK 和扩展。使用 Adobe 标记（数据收藏集）配置 Media Analytics 扩展。有关更多信息，请参阅[从独立的 Media SDK 迁移到 Adobe Launch](/help/legacy/sdk-to-launch/sdk-to-launch-migration.md)

1. 已终止适用于 iOS 和 Android 的 Media Analytics SDK 的功能开发。从 2019 年秋季开始引入的新功能均通过 Media Analytics 扩展和媒体收集 API 启用。

1. Roku 和 Chromecast SDK 仍可供 Analytics for Streaming Media 客户使用。将继续以独立 SDK 的形式增强和支持 Roku SDK 和 Chromecast SDK。如果您使用 JS SDK for Media Analytics，则可继续使用独立的 SDK 或使用 Adobe 数据收藏集（以前称为 Adobe Launch）启用 Media Analytics 扩展。

1. 2021 年 9 月 1 日之前，Adobe 可能会自行决定是否为具有重大技术影响或业务泄露风险的问题开发新的修复程序。Adobe 将会根据客户的意见来确定影响程度和泄露等级，以及相应的后续开发活动。

如果您有任何问题，请联系您的 Adobe 客户成功经理。

## 常见问题解答

1. **是否会影响对 Roku SDK 和 Chromecast SDK 的支持？**

   否。目前，Roku SDK 和 Chromecast SDK 将继续作为独立的 SDK 进行支持。
1. **此更改是否会影响 Media Analytics JS SDK 实施？**

   否。使用 JS SDK for Media Analytics 的客户可继续使用 SDK，或通过 Adobe Launch 启用它。

1. **迁移到 Media Analytics 扩展需要耗费多少工作量？**

   LOE 取决于每位客户的实施，因此会有所不同。查看下面的迁移文档后，请咨询顾问和/或客户关怀团队以获得其他支持。

[Media Analytics 扩展：Android 迁移](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)

[Media Analytics 扩展：iOS 迁移](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)

   [Media Analytics 扩展：新实施](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **是否需要将 Launch 作为标签管理系统？如果我不想使用 Launch，应该怎么办？**

   对于移动应用程序用例，不能使用 Launch 作为标签管理系统，因为它适用于 Web 用例。配置 SDK 扩展需要使用 Launch UI。这与您使用 Adobe Mobile Services UI 配置 Mobile v4 SDK 的方式相似。对于安装而言，使用 Launch 的好处是它可以根据您选择的扩展为您提供自定义的安装说明。

1. **终止支持是否会影响适用于 tvOS 的 SDK？**

   是，对于 tvOS（版本 10+），建议的实施是迁移到 Media Analytics 扩展。有关其他信息，请参阅[从独立的媒体 SDK 迁移到 Adobe Launch - iOS](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)。

1. **此项终止支持是否影响适用于 Fire TV 和 AndroidTV 的 SDK？**

   是，对于 Fire TV 和 AndroidTV，建议的实施是迁移到 Media Analytics 扩展。有关其他信息，请参阅[从独立的媒体 SDK 迁移到 Adobe Launch - Android](/help/legacy/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)。
