---
title: 媒体路径
description: 将内容ID捕获为流量变量，以进行路径分析。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# 媒体路径

**媒体路径**&#x200B;维度将内容ID捕获为流量变量(prop)，以便将其用于路径分析（例如，下一个内容和上一个内容流量报表）。 它是Adobe Analytics独有的：Customer Journey Analytics不存储流量变量，并且直接对内容(ID)维度执行路径分析。

## 如何填充此维度

媒体路径自动派生自会话开始时设置的内容ID。 没有要设置的单独变量；每当填充内容(ID)时，都会填充数据馈送列`videopath`。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.name`中收集流量变量(prop)。 |
| Customer Journey Analytics | 不适用 — 使用[内容](content.md)进行路径分析 |
| 数据馈送 | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>Adobe Analytics prop具有100字节的限制。 长度超过100字节的值会被截断。

>[!IMPORTANT]
>
>路径报表会比较同一次访问中点击之间的prop值。 如果访问中的内容(ID)发生更改（例如，当查看者从一段内容移动到另一段内容时），路径报表会显示该流量。

## 维度项目

每个项目都是访问期间报告的内容ID。 在Adobe Analytics中，使用“内容”>“媒体路径”下的“下一页面流量”和“上一页面流量”报表，可以查看内容到内容的导航路径。
