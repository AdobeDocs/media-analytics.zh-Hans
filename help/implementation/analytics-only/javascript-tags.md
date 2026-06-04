---
title: 设置Media Analytics标记扩展
description: 使用Adobe Media Analytics (3.x SDK) for Audio and Video标记扩展实施仅限Analytics的流媒体。
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
