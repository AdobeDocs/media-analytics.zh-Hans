---
title: 设置适用于带标记的流媒体的iOS
description: 使用Adobe Streaming Media for iOS标记扩展配置Edge Network的流媒体收集。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 设置适用于带标记的流媒体的iOS

您可以通过Tags移动属性为iOS或tvOS应用程序配置流媒体收集，并在数据收集UI中管理媒体设置。 本页介绍标记配置。 要在代码中配置SDK，请参阅[为流媒体设置iOS](ios.md)。

* **先决条件**：
   * 完成[Edge实施概述](overview.md)（架构、数据集、启用了[!UICONTROL Media Analytics]的数据流）。
   * 在数据收集UI中创建移动属性。 请参阅[Adobe Streaming Media for Edge Network](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)。

## 配置扩展

1. 在数据收集UI中，打开您的移动属性，然后选择&#x200B;**[!UICONTROL 扩展]**。
1. 在&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡上，找到&#x200B;**Adobe Streaming Media for Edge Network**&#x200B;扩展并选择&#x200B;**[!UICONTROL 安装]**。
1. 设置以下内容，然后保存：
   * **[!UICONTROL 频道]**：每个会话报告的频道名称。
   * **[!UICONTROL 播放器名称]**：正在使用的媒体播放器名称。
   * **[!UICONTROL 应用程序版本]**：播放器应用程序的版本。
1. 发布更改，然后将`AEPCore`、`AEPEdge`、`AEPEdgeIdentity`和`AEPEdgeMedia`依赖项添加到您的应用程序并在移动核心中注册它们。

## 跟踪媒体事件

发布属性并创建跟踪器后，使用其跟踪器方法跟踪每个媒体事件。 查看每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**iOS**&#x200B;选项卡，了解确切的调用。

## 下一步

实施完成后，您可以[为Edge实施设置报表](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [适用于Edge Network的Adobe流媒体](https://developer.adobe.com/client-sdks/edge/media-for-edge-network/)
>* [为流媒体设置iOS（代码中）](ios.md)
>* [事件概述](/help/implementation/events/overview.md)
