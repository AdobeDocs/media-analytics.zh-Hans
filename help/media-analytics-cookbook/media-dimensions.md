---
title: 媒体流归因
seo-title: 媒体流归因
translation-type: tm+mt
source-git-commit: cc067b31066aa5d7e254167e32429c6c56e40c77

---


# 媒体流归因

利用此功能，您无需附加处理规则和自定义变量即可将应用程序操作关联到媒体跟踪数据。

## 媒体跟踪之外的媒体维度

借助媒体流归因，客户现在可以将任何媒体维度添加到所有其他分析调用，如页面查看和自定义链接。 在实施过程中，您必须将媒体上下文数据参数添加到Analytics跟踪调用。 用于媒体的上下文数据参数的完整列表可在以下网址获得：音 [频和视频参数。](/help/metrics-and-metadata/audio-video-parameters.md)

您还需要从管理控制台为要启用此功能的每个报告重新启用媒体跟踪配置。

>[!NOTE]
>媒体指标在媒 _体跟踪_ 之外不可用，因为大部分指标都是由Media Analytics计算的
>基于心跳事件。 另外，媒体指标不要被不同的实施夸大也很重要。

## 如何

以下JavaScript示例将生成一个名称设置为“Hero Banner”的“自定义链接”跟踪调用。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在Analytics报告中，您可以使用 `Show` eVar来划分数据，并且您将能够计算跟踪链接实例。 报告将类似于：

![](/assets/myShow-rpt-1.png)

## 用例

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)

