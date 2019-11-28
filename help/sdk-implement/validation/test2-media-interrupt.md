---
title: 测试 2：媒体中断
description: 本主题介绍验证中使用的媒体中断测试。
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 测试 2：媒体中断{#test-media-interruption}

此测试案例将验证移动中断行为。它是认证请求的必需元素。

## 认证请求表单

**可从此处下载认证请求表单：==&gt;**[认证请求表单。](cert_req_form.docx)

## 测试步骤

您必须按照以下顺序完成并记录这些任务：

1. **启动媒体播放器**

   媒体播放器启动时，会按照以下顺序发送以下调用：

   1. Adobe Analytics (AppMeasurement) 开始
   1. Media Analytics（心率）开始
   1. 请求的 Media Analytics（心率）Adobe Analytics 开始调用
   上述前两个调用包含其他的元数据和变量。有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)。

   上述第三个调用告知 Media Analytics 服务器，Media SDK 已请求将 Adobe Analytics 开始调用 (`pev2=ms_s`) 发送到 Adobe Analytics 服务器。

1. **无中断播放主内容至少 5 分钟**

   **内容播放**

   在内容播放期间，Media SDK 每 10 秒会向 Media Analytics 服务器发送播放调用（心率）。

   有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#play-main-content)。

   另请参阅您平台的[跟踪广告](/help/sdk-implement/track-ads/track-ads-overview.md)说明，了解这些广告调用的其他相关信息。

1. **将应用程序或浏览器移至后台**

   从 VHL 版本 1.6.6 及更高版本开始，当应用程序在后台运行时，应该只将 `main:pause` 调用发送到 Media Analytics 服务器。

1. **将应用程序或浏览器调至前台**

   从后台返回时，应恢复内容播放。

1. **无中断播放主内容媒体至少 5 分钟**

   有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#play-main-content)。

1. **关闭媒体播放器**

   在媒体播放器关闭后，不应触发任何其他跟踪调用。

