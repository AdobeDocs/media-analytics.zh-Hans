---
title: 设置适用于流媒体的Chromecast
description: 为仅适用于Analytics的流媒体实施安装和配置Media SDK for Chromecast 。
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
source-wordcount: '180'
ht-degree: 10%
---
# 设置适用于流媒体的Chromecast

Media SDK for Chromecast将流媒体数据从Chromecast接收器应用程序直接发送到Adobe Analytics。 SDK及其文档托管在GitHub上。

* **先决条件**：
  * 完成[仅限Analytics的实施概述](overview.md)。
  * [下载Media SDK for Chromecast](/help/getting-started/download-sdks.md)。

## 安装和配置SDK

将SDK添加到Chromecast接收器应用程序，并配置跟踪器，如规范参考中所述：

* [设置Chromecast SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Chromecast SDK API参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## 跟踪媒体事件

在创建跟踪器后，使用其跟踪器方法跟踪每个媒体事件。 查看每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Chromecast**&#x200B;选项卡，了解确切的调用。

## 下一步

实施完成后，您可以[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [Chromecast SDK API引用](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [事件概述](/help/implementation/events/overview.md)
>* [变量概述](/help/implementation/variables/overview.md)
