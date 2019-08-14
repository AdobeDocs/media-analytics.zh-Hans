---
seo-title: Test Media中断
title: Test Media中断
uuid: eeccd534-63fd-4dd3-b096-0431bc9 a11 ff
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# 测试2：媒体中断{#test-media-interruption}

此测试案例是认证请求表单中所需的一部分，用于验证在移动设备上发生中断的行为。

Download the certification request here: [Certification Request Form.](cert_req_form.docx)

您必须按照以下顺序完成并记录这些任务：

1. **启动媒体播放器**

   媒体播放器启动时，按以下顺序发送下列调用：

   1. Media Analytics 开始
   1. 心率开始
   1. 心率分析开始
   以上两个调用包含额外的元数据和变量。有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md)

1. **播放主要内容媒体至少不间断分钟**

   **内容播放**

   在常规主内容播放期间，每十秒就会向心率服务器发送一次心率调用。

   有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **将应用程序或浏览器移至后台**

   从 VHL 版本 1.6.6 及更高版本开始，当应用程序在后台运行时，应该只将“main:pause”调用发送至心率服务器。

1. **将应用程序或浏览器调至后台**

   从后台返回时，应恢复内容播放。

1. **播放主要内容媒体至少不间断分钟**

   有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md)

1. **关闭媒体播放器**

   关闭媒体播放器后，不会触发其他跟踪调用。

