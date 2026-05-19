---
title: 测试 2：媒体中断
description: 了解验证中使用的标准中断测试。
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
exl-id: 3f22ce2d-4385-4a3b-8d1f-52e25a9b1101
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/gVEDMjM05nDnzCB6l-9CjyUzoArcmyN4jgsjmjllRiY
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 248
ht-degree: 100%

---

# 测试 2：媒体中断{#test-media-interruption}

此测试案例将验证移动中断行为。

## 测试步骤

您必须按照以下顺序完成并记录这些任务：

1. **启动媒体播放器**

   媒体播放器启动时，会按照以下顺序发送以下调用：

   1. Adobe Analytics (AppMeasurement) 开始
   1. Media Analytics（心跳）开始
   1. 请求的 Media Analytics（心跳）Adobe Analytics 开始调用

   上述前两个调用包含其他的元数据和变量。 有关调用参数和元数据，请参阅[测试调用详细信息](/help/legacy/validation/test-call-details.md#start-the-media-player)。

   上述第三个调用告知 Media Analytics 服务器，Media SDK 已请求将 Adobe Analytics 开始调用 (`pev2=ms_s`) 发送到 Adobe Analytics 服务器。

1. **无中断播放主内容至少 5 分钟**

   **内容播放**

   在内容播放期间，Media SDK 每 10 秒会向 Media Analytics 服务器发送播放调用（心跳）。

   有关调用参数和元数据，请参阅[测试调用详细信息](/help/legacy/validation/test-call-details.md#play-main-content)。

   另请参阅您平台的[跟踪广告](/help/use-cases/track-ads/track-ads-overview.md)说明，了解这些广告调用的其他相关信息。

1. **将应用程序或浏览器移至后台**

   从 VHL 版本 1.6.6 及更高版本开始，当应用程序在后台运行时，应该只将 `main:pause` 调用发送到 Media Analytics 服务器。

1. **将应用程序或浏览器调至前台**

   从后台返回时，应恢复内容播放。

1. **无中断播放主内容媒体至少 5 分钟**

   有关调用参数和元数据，请参阅[测试调用详细信息](/help/legacy/validation/test-call-details.md#play-main-content)。

1. **关闭媒体播放器**

   在媒体播放器关闭后，不应触发任何其他跟踪调用。
