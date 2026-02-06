---
title: 播放器状态跟踪简介
description: 了解播放器状态跟踪功能，包括实现和报告播放器状态的要求和准则。
exl-id: c678e182-74e4-4f46-8596-7be57e645c66
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 100%

---

# 播放器状态跟踪简介

为了优化产品体验和提升业务价值，了解客户在观看视频时的行为非常重要。这包括在不同播放器状态逗留的时间。此外，根据需要灵活地创建和测量新的播放器状态和事件也很重要。

播放器状态跟踪使用一组标准的解决方案变量（全屏、隐藏式字幕、静音、画中画以及聚焦），提供了在播放过程中捕获查看者交互情况的功能。此外，播放器状态跟踪还为创建自定义播放器状态提供了所需的灵活性。可以在 Analysis Workspace 中使用“播放器状态跟踪”变量进行报告。

为了捕获播放器状态的变更，播放器状态跟踪会更新视频测量元数据。例如，为确定“真正的”视频参与情况，“播放器状态跟踪”功能会测量开启音效时的观看时间与关闭音效条时被动或未参与的视频观看次数，或者测量在常规模式与全屏模式下的观看时间。

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
* 状态停止后，不会保留有关应用程序状态的信息。状态结束后，必须再次启动状态才能继续跟踪。对于每个新播放状态，必须重新启动播放器的状态。
* 捕获每个单独播放会话的播放器状态 - 不会跨播放计算播放器状态。
