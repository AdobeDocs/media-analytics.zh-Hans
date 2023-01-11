---
title: 什么是媒体流归因？
description: 了解如何将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '231'
ht-degree: 100%

---

# 媒体流归因 {#media-stream-attribution}

利用流媒体归因，您可以将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。

## 媒体跟踪之外的媒体维度

您可以将媒体维度添加到分析调用中，例如页面查看次数和自定义链接。在实施过程中，您必须将媒体上下文数据参数添加到 Analytics 跟踪调用。要查看用于媒体的可用上下文数据参数的完整列表，请参阅[音频和视频参数](/help/implementation/variables/audio-video-parameters.md)。

要为特定报告启用此功能，请从 Admin console 重新启用媒体跟踪配置。

>[!NOTE]
>
>媒体量度在媒体跟踪之外&#x200B;_不_&#x200B;可用，因为大多数媒体量度是由适用于流媒体的 Analytics 基于心跳事件计算的。此外，媒体量度不应被不同的实施夸大，这一点也很重要。

## 使用媒体流归因

以下 JavaScript 示例生成一个名称设置为“Hero Banner”的自定义链接跟踪调用。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 报表中，您可以使用 `Show` eVar 来划分数据，并且将能够计数跟踪链接实例。报表将类似于：

![](/assets/myShow-rpt-1.png)

## 用例

以下示例显示了以下内容的用例：

* 类别投放位置
* 主页投放位置
* 参与
* 订阅

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
