---
seo-title: Test Video中断
title: Test Video中断
uuid: eeccd534-63fd-4dd3-b096-0431bc9 a11 ff
translation-type: tm+mt
source-git-commit: ee6eebac803410c1c4da1ccb80083025a9c817df

---


# 测试 2：视频中断{#test-video-interruption}

此测试案例是认证请求表单中所需的一部分，用于验证在移动设备上发生中断的行为。

Download the certification request here: [Certification Request Form.](cert_req_form_nielsen.docx)

您必须按照以下顺序完成并记录这些任务：

1. **启动视频播放器**

   视频播放器启动时，会按照以下顺序发送以下调用：

   1. Media Analytics 开始
   1. 心率开始
   1. 心率分析开始
   以上两个调用包含额外的元数据和变量。For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

1. **无中断播放主内容视频至少 5 分钟**

   **内容播放**

   在常规主内容播放期间，每十秒就会向心率服务器发送一次心率调用。

   For call parameters and metadata, see [Test call details.](../../sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](../../sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **将应用程序或浏览器移至后台**

   从 VHL 版本 1.6.6 及更高版本开始，当应用程序在后台运行时，应该只将“main:pause”调用发送至心率服务器。

1. **将应用程序或浏览器调至后台**

   从后台返回时，应恢复内容播放。

1. **无中断播放主内容视频至少 5 分钟**

   For call parameters and metadata, see [Test Call Details.](../../sdk-implement/validation/test-call-details.md)

1. **关闭视频播放器**

   在视频播放器关闭后，不应触发任何其他跟踪调用。

