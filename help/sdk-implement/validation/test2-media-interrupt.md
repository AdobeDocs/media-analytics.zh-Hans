---
seo-title: Test 2媒体中断
title: Test 2媒体中断
uuid: eeccd534-63fd-4dd3-b096-0431bc9a11ff
translation-type: tm+mt
source-git-commit: 5822e634c51cb53a60400623d115c6d862dad44f

---


# 测试2:媒体中断{#test-media-interruption}

此测试用例可验证移动中断行为。 它是您的认证请求中的必需元素。

## 认证申请表

**请单击此处下载认证申请表：==&gt;认证**&#x200B;申 [请表。](cert_req_form.docx)

## 测试过程

您必须按照以下顺序完成并记录这些任务：

1. **启动媒体播放器**

   当媒体播放器启动时，将按以下顺序发送以下调用：

   1. Adobe Analytics(AppMeasurement)开始
   1. 媒体分析（心率）开始
   1. Media Analytics（心率）Adobe Analytics start呼叫请求
   上述前两次调用包含其他元数据和变量。 有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上述第三个调用告知Media Analytics服务器，Media SDK请求将Adobe Analytics开始调用(`pev2=ms_s`)发送到Adobe Analytics服务器。

1. **播放主内容至少5分钟不间断**

   **内容播放**

   在内容播放期间，Media SDK每十秒向Media Analytics服务器发送播放调用（心跳）。

   有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

   Also see your platform's [Track Ads](/help/sdk-implement/track-ads/track-ads-overview.md) instructions for additonal information about these Ad calls.

1. **将应用程序或浏览器移至后台**

   While the app runs in the background, only `main:pause` calls should be sent to the Media Analytics server, starting with VHL version 1.6.6 and later.

1. **将应用程序或浏览器重新置于前台**

   从后台返回时，应恢复内容播放。

1. **Play main content media for at least 5 minutes uninterrupted**

   有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **关闭媒体播放器**

   No additional tracking calls should fire after the media player is closed.

