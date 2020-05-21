---
title: 媒体分析SDK支持终止常见问题解答
description: 本主题包括有关Media Analytics SDK支持终止的常见问题解答。
translation-type: tm+mt
source-git-commit: 300eb77858296f0246a2cb484386c0dcdf8b87b9
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---


# 媒体分析SDK支持终止常见问题解答

随着2021年8月31日停止对版本4 Mobile SDK的支持，Adobe还将结束对适用于iOS和Android的Media Analytics SDK的支持。 2021年8月31日之后，Adobe将不提供Media Analytics SDK的修复、操作系统相关更新或支持。  在迁移到这些新的Experience Platform SDK的过程中，请牢记，必 [须实施Media Analytics扩](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics) 展，才能启用Adobe Analytics的音频和视频分析。

## 五大要知

1. 2021年8月31日之后将不再支持移动v4 SDK。 您应迁移至适用于iOS和Android的Adobe Experience Platform(AEP)SDK。

1. 音频和视频分析实施需要AEP SDK以及使用Analytics和Media Analytics扩展。 从2021年9月1日起，您应使用新的AEP SDK和扩展。  媒体分析扩展是使用Adobe Launch配置的。  有关更多信息，请 [参阅从独立媒体SDK迁移到Adobe Launch](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration.html)

1. 适用于iOS和Android的Media Analytics SDK的功能开发已结束。  从2019年秋季开始引入的新功能已通过Media Analytics扩展和Media Collection API启用。

1. Roku和Chromecast SDK仍可供音频和视频客户使用。 Roku和Chromecast SDK将继续得到增强，并作为独立SDK受支持。  如果您使用用于媒体分析的JS SDK，则可继续使用独立SDK或使用Adobe Launch启用媒体分析扩展。

1. 2021年9月1日之前，Adobe可自行决定为技术影响或业务暴露的问题开发新的修复程序。 根据客户的意见，Adobe将确定影响和曝光程度以及由此产生的活动。

如有任何疑问，请联系您的Adobe客户成功经理。

## 常见问题解答

1. **对Roku和Chromecast SDK的支持是否会受到影响&#x200B;?**

   否.  Roku和Chromecast SDK将继续作为独立SDK受支持&#x200B;,
1. **Media Analytics JS SDK实施是否会受此更改影响&#x200B;?**

   否.  使用JS SDK for Media Analytics的客户可继续使用SDK或通过Adobe Launch启用它。
&#x200B;
1. **迁移到Media Analytics扩展的工作量是多少&#x200B;?**

   LOE取决于每位客户的实施，因此会有所不同。  查看下面的迁移文档后，请咨询和／或客户关怀以获得更多支持。

   [媒体分析扩展： Android迁移](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)

   [媒体分析扩展： iOS迁移](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)

   [媒体分析扩展： 新实施](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

1. **是否需要将Launch作为标签管理系统？ 如果我不想使用Launch怎么办？**

   对于移动设备，需要Launch来配置媒体扩展，如Mobile Services UI。 在移动应用用例中，它不用作标签管理系统。

1. **此支持终止是否会影响SDK for tvOS?**

   是，对于tvOS（版本10+），建议实施是迁移到媒体分析扩展。  AEP SDK支持和媒体分析扩展支持计划于2020年6月推出。  有关其他信息，请 [参阅从独立Media SDK迁移到Adobe Launch - iOS](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.html)。

1. **此支持终止是否会影响FireTV和AndroidTV的SDK&#x200B;?**

   是的，对于FireTV和AndroidTV，建议的实施是迁移到媒体分析扩展。  AEP SDK支持和媒体分析扩展支持计划于2020年6月推出。  有关其他信息，请 [参阅从独立Media SDK迁移到Adobe Launch - Android](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.html)。
