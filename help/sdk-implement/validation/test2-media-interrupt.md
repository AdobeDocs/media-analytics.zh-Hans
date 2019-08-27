---
seo-title: Test Media中断
title: Test Media中断
uuid: eeccd534-63fd-4dd3-b096-0431bc9 a11 ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# 测试2：媒体中断{#test-media-interruption}

此测试用例验证移动中断行为。它是认证请求的必需元素。

## 认证申请表

**请在此处下载认证申请表：==&gt;**[认证请求表。](cert_req_form.docx)

## 测试过程

您必须按照以下顺序完成并记录这些任务：

1. **启动媒体播放器**

   媒体播放器启动时，按以下顺序发送下列调用：

   1. Adobe Analytics(AppMeasurement)开始
   1. 媒体分析(心跳)开始
   1. 已请求Media Analytics(心跳) Adobe Analytics开始电话
   以上两个调用包含额外的元数据和变量。有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上面的第三个调用告知Media SDK媒体SDK已请求将Adobe Analytics Start调用(`pev2=ms_s`)发送到Adobe Analytics服务器。

1. **播放主内容至少不间断分钟**

   **内容播放**

   在内容播放过程中，Media SDK每隔十秒向Media Analytics服务器发送播放调用(心率)。

   有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **将应用程序或浏览器移至后台**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **将应用程序或浏览器引入前台**

   从后台返回时，应恢复内容播放。

1. **播放主要内容媒体至少不间断分钟**

   有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **关闭媒体播放器**

   关闭媒体播放器后，不会触发其他跟踪调用。

