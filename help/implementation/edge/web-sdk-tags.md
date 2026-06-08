---
title: 设置适用于流媒体的Web SDK标记扩展
description: 在Adobe Experience Platform Web SDK标记扩展中配置流媒体收集。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 设置适用于流媒体的Web SDK标记扩展

Adobe Experience Platform Web SDK标记扩展允许您在数据收集UI中配置流媒体收集，而不使用`alloy.js`配置代码。 本页介绍标记配置。 若要改为在代码中配置Web SDK，请参阅[为流媒体设置Web SDK](web-sdk.md)。

* **先决条件**：
   * 完成[Edge实施概述](overview.md)（架构、数据集、启用了[!UICONTROL Media Analytics]的数据流）。
   * 安装和配置Web SDK标记扩展。 请参阅[Web SDK标记扩展概述](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)。

## 在扩展中配置流媒体

1. 在数据收集UI中，打开Web属性并选择&#x200B;**[!UICONTROL 扩展]**。
1. 在已安装的&#x200B;**Adobe Experience Platform Web SDK**&#x200B;扩展上，选择&#x200B;**[!UICONTROL 配置]**。
1. 展开&#x200B;**[!UICONTROL 流媒体]**&#x200B;部分并设置以下内容：
   * **[!UICONTROL 频道]**：每个会话报告的频道名称。
   * **[!UICONTROL 播放器名称]**：正在使用的媒体播放器名称。
   * **[!UICONTROL 应用程序版本]**：播放器应用程序的版本。
   * **[!UICONTROL 主Ping间隔]**&#x200B;和&#x200B;**[!UICONTROL 广告Ping间隔]**：主内容和广告的Ping频率（以秒为单位）。
1. 保存扩展配置并发布更改。

## 跟踪媒体事件

配置扩展后，使用&#x200B;**[!UICONTROL 发送事件]**&#x200B;操作（或`sendEvent`命令）发送每个媒体事件。 有关确切负载，请参阅每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Web SDK**&#x200B;选项卡。

## 下一步

实施完成后，您可以[为Edge实施设置报表](/help/reporting/setup/edge-reporting.md)。

>[!MORELIKETHIS]
>
>* [Web SDK标记扩展概述](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/overview)
>* [为流媒体设置Web SDK（代码）](web-sdk.md)
>* [事件概述](/help/implementation/events/overview.md)
