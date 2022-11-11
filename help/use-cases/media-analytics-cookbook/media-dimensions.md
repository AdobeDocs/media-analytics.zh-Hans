---
title: 什么是媒体流归因？
description: 了解如何将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 39%

---

# 媒体流归因 {#media-stream-attribution}

借助媒体流归因，您可以将应用程序操作链接到媒体跟踪数据，而无需其他处理规则和自定义变量。

## 媒体跟踪之外的媒体维度

您可以向分析调用添加媒体维度，如页面查看次数和自定义链接。 在实施过程中，您必须将媒体上下文数据参数添加到 Analytics 跟踪调用。要查看用于媒体的可用上下文数据参数的完整列表，请参阅 [音频和视频参数。](/help/implementation/variables/audio-video-parameters.md)

要为特定报表启用此功能，请从管理控制台重新启用媒体跟踪配置。

>[!NOTE]
>
>媒体量度包括 _not_ 可在媒体跟踪之外使用，因为大多数媒体跟踪是由Streaming Media Analytics基于心率事件计算的。 此外，媒体量度不应被不同的实施夸大，这一点也很重要。

## 使用媒体流归因

以下JavaScript示例会生成一个名称设置为“Hero Banner”的自定义链接跟踪调用。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 报表中，您可以使用 `Show` eVar 来划分数据，并且将能够计数跟踪链接实例。报表将类似于：

![](/assets/myShow-rpt-1.png)

## 用例

以下示例显示了以下用例：

* 类别放置
* 主页版面
* 参与度
* 订阅

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
