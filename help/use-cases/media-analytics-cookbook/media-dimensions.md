---
title: 什么是媒体流归因？
description: 了解如何将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。
exl-id: 75cc9088-776d-4b10-b358-9fff956a7eb7
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/G0RufpSDBB65tr4XJRvPU2keKgKxv1uDviyhqzxEVD4
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e4f5f438-eabb-4c54-9133-b817e3d125f5id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 215
ht-degree: 87%

---

# 媒体流归因 {#media-stream-attribution}

利用流媒体归因，您可以将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。

## 媒体跟踪之外的媒体维度

您可以将媒体维度添加到分析调用中，例如页面查看次数和自定义链接。 在实施过程中，您必须将媒体上下文数据参数添加到 Analytics 跟踪调用。

要为特定报告启用此功能，请从 Admin console 重新启用媒体跟踪配置。

>[!NOTE]
>
>媒体量度&#x200B;_不_&#x200B;可用于媒体跟踪之外，因为大多数媒体量度是由流媒体服务基于心率事件计算的。 此外，媒体量度不应被不同的实施夸大，这一点也很重要。

## 使用媒体流归因

以下 JavaScript 示例生成一个名称设置为“Hero Banner”的自定义链接跟踪调用。

```javascript
s.contextData["a.media.show"]="Mi Amore"
s.tl(this,'o','Hero Banner');
```

在 Analytics 报表中，您可以使用 `Show` eVar 来划分数据，并且将能够计数跟踪链接实例。 报表将类似于：

![](/assets/myShow-rpt-1.png)

## 用例

以下示例显示了以下内容的用例：

* 类别放置环境
* 主图投放
* 参与
* 订阅

![](/assets/vid-stream-attr-category.png)

![](/assets/vid-stream-attr-hero.png)

![](/assets/show-engagement.png)

![](/assets/vid-stream-attr-subs.png)
