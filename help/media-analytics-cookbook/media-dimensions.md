---
title: 媒体流归因
description: null
translation-type: ht
source-git-commit: cab9724476f7864ac23c4293e402e0443771cb1e
workflow-type: ht
source-wordcount: '209'
ht-degree: 100%

---


# 媒体流归因

利用此功能，可以将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。

## 媒体跟踪之外的媒体维度

借助媒体流归因，客户现在能够将任何媒体维度添加到所有其他分析调用，例如“页面查看次数”和“自定义链接”。在实施过程中，您必须将媒体上下文数据参数添加到 Analytics 跟踪调用。可在此处找到用于媒体的上下文数据参数的完整列表：[音频和视频参数](/help/metrics-and-metadata/audio-video-parameters.md)。

此外，您还需要从 Admin Console 为要启用此项功能的每个报表重新启用媒体跟踪配置。

>[!NOTE]
>
>媒体量度在媒体跟踪之外&#x200B;_不_&#x200B;可用，因为大多数媒体量度是由 Media Analytics 基于心率事件计算的。此外，媒体量度不应被不同的实施夸大，这一点也很重要。

## 方法

以下 JavaScript 示例将生成一个名称设置为“Hero Banner”的自定义链接跟踪调用。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 报表中，您可以使用 `Show` eVar 来划分数据，并且将能够计数跟踪链接实例。报表将类似于：

![](/assets/myShow-rpt-1.png)

## 用例

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

