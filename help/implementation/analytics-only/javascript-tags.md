---
title: 设置Media Analytics标记扩展
description: 使用Adobe Media Analytics (3.x SDK) for Audio and Video标记扩展实施仅限Analytics的流媒体。
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 12%
---
# 设置Media Analytics标记扩展

Adobe Media Analytics (3.x SDK) for Audio and Video标记扩展通过标记部署Media SDK for JavaScript (3.x)，而无需手动安装JavaScript。 本页介绍标记配置。 要在代码中安装SDK，请参阅[为流媒体设置JavaScript](javascript.md)。 对于新的实施，请考虑推荐的[Web SDK标记扩展](/help/implementation/edge/web-sdk-tags.md) Edge路径。

* **先决条件**：完成[仅限Analytics的实施概述](overview.md)。

## 安装和配置扩展

通过在数据收集UI中安装和配置扩展，将媒体跟踪器实例添加到启用了标记的站点。 有关安装和配置详细信息，请参阅[Adobe Media Analytics (3.x SDK) for Audio and Video扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hans)。

## 跟踪媒体事件

配置扩展后，使用其跟踪器方法跟踪每个媒体事件。 查看每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Media SDK JS 3.x**&#x200B;选项卡，了解确切的调用。

## 下一步

实施完成后，您可以[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [Adobe Media Analytics (3.x SDK) for Audio and Video扩展](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=zh-Hans)
>* [为流媒体设置JavaScript（代码中）](javascript.md)
>* [事件概述](/help/implementation/events/overview.md)
