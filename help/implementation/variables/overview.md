---
title: 流媒体变量概述
description: 了解流媒体变量的组织方式以及它们如何跨Adobe Analytics和Customer Journey Analytics进行映射。
feature: Streaming Media
role: User, Admin, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%
---

# 流媒体变量概述

变量是媒体播放器提供的有关流的数据，如内容名称、流类型、广告名称和播放质量。 大多数变量是在会话开始时设置的，并由媒体后端执行到会话关闭，媒体后端会使用它们填充您在报表中使用的维度和量度。 每个变量页面都记录了如何在每种受支持的实施方法中设置该变量。

## 如何将变量发送到Adobe

单个变量将为每个Adobe应用程序或服务带来相同的值，但该值的格式取决于发送该值的位置。 下表列出了每个应用程序或服务及其所需的变量格式。 每个变量页上的属性表显示了要在每种格式中使用的确切值。

| 数据格式 | 描述 |
| --- | --- |
| 上下文数据变量 | 发送到Adobe Analytics的格式，以`a.media`为前缀命名（如`a.media.name`）。 |
| XDM收藏集字段 | 发送到Customer Journey Analytics的格式，以XDM字段路径表示（如`xdm.mediaCollection.sessionDetails.name`）。 |
| Audience Manager特征 | 转发到Audience Manager的格式，以`c_contextdata`为前缀（如`c_contextdata.a.media.name`）。 |

>[!MORELIKETHIS]
>
>* [事件概述](/help/implementation/events/overview.md)：包含变量的播放器事件
>* [维度概述](/help/reporting/dimensions/overview.md)：变量填充的报表维度
>* [量度概述](/help/reporting/metrics/overview.md)：变量填充的报表量度
