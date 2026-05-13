---
title: 播放器状态跟踪简介
description: 了解播放器状态跟踪功能，包括实现和报告播放器状态的要求和准则。
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/R4ByVgEI65JyN-LFdMX1CCBs4zVyppVgebN9OJxJNMM
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: c153fd90-23e1-4614-81d3-3cc7571227f7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 409
ht-degree: 100%

---

# 播放器状态跟踪简介

为了优化产品体验和提升业务价值，了解客户在观看视频时的行为非常重要。 这包括在不同播放器状态逗留的时间。  此外，根据需要灵活地创建和测量新的播放器状态和事件也很重要。

播放器状态跟踪使用一组标准的解决方案变量（全屏、隐藏式字幕、静音、画中画以及聚焦），提供了在播放过程中捕获查看者交互情况的功能。  此外，播放器状态跟踪还为创建自定义播放器状态提供了所需的灵活性。 可以在 Analysis Workspace 中使用“播放器状态跟踪”变量进行报告。

为了捕获播放器状态的变更，播放器状态跟踪会更新视频测量元数据。 例如，为确定“真正的”视频参与情况，“播放器状态跟踪”功能会测量开启音效时的观看时间与关闭音效条时被动或未参与的视频观看次数，或者测量在常规模式与全屏模式下的观看时间。

播放器状态跟踪具有以下优势：

* 提供用于测量全屏或隐藏式字幕等常见状态的标准变量
* 提供用于在播放会话期间测量自定义状态的自定义的变量
* 测量在自定义播放器状态中花费的时间
* 测量可能并发的多个状态

![播放器状态跟踪](assets/player_state_tracking.png)

## 要求

“播放器状态跟踪”需要以下数据集之一：
* Media JS SDK 3.0+
* 适用于 Adobe Marketing Cloud 解决方案的 Chromecast 3.0 SDK
* Media Analytics 扩展（与 Adobe Experience Platform (AEP) SDK 一起使用）
   * Web：Adobe Media Analytics (3.x SDK) for Audio and Video v1.0+
   * 移动设备：Adobe Media Analytics for Audio and Video v2.0+
* 媒体收集 API

## 准则

在实施播放器状态跟踪之前，请注意以下准则。

* 播放器状态是跨所有播放状态计算的（无拆分）
* 您可以同时测量多个播放器状态.
* 可在播放过程中跟踪的播放器状态上限为 10 个。
* 发送到 Analytics 的播放器状态量度仅用于生成“媒体关闭”调用报表。
* 状态停止后，不会保留有关应用程序状态的信息。 状态结束后，必须再次启动状态才能继续跟踪。 对于每个新播放状态，必须重新启动播放器的状态。
* 捕获每个单独播放会话的播放器状态 - 不会跨播放计算播放器状态。
