---
title: Adobe Audience Manager 支持什么？
description: 了解如何将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
source-git-commit: e781af84f23400aa7c899b686f0e9fee2c19d660
workflow-type: ht
source-wordcount: '409'
ht-degree: 100%

---

# Audience Manager 支持{#audience-manager-enablement}

Adobe Audience Manager (AAM) 是一种数据管理平台 (DMP)，可帮助您将受众数据资产整合在一起，从而轻松收集与网站访客相关的商业信息、创建可销售的区段，并向正确的受众提供有针对性的广告和内容。

使用 AAM，您不会受到数据销售商、交换或需求侧平台的束缚。此外，AAM 对传递给您合作伙伴的数据资产完全不可知。AAM 通过访问多个数据源，使数字发布者能够使用各种第三方数据和我们的专用数据协作。要了解有关 AAM 的更多信息，请参阅 AAM 文档 [Audience Manager 产品文档](https://docs-author.corp.adobe.com/content/help/zh-Hans/audience-manager/user-guide/aam-home.html)。

**VA 到 AAM 数据传输 -**&#x200B;对于视频内容和视频广告，使用解决方案（保留的）变量收集的量度和元数据可自动发送到 AAM。数据传输可跨所有平台使用，包括台式机、移动设备和 OTT。要启用此服务器端数据传输，您需要联系 Adobe 客户关怀团队以要求启用此源。

>[!IMPORTANT]
>
>为确保将数据顺利传输至 AAM，您应该使用最新版本的 Media SDK 库。

联合数据完全支持与 AAM 的数据共享。请与您的 Adobe 团队合作，确认联合数据设置。

## OTT/AAM 方法 {#ott-aam-methods}

您可以使用以下方法发送信号，并从 Audience Manager 中检索访客区段：

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   返回最近获取的访客资料。如果尚未提交信号，则返回空对象。

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   返回最近获取的访客资料。如果尚未提交信号，则返回空对象。

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   返回当前 DPUUID。

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   设置 DPID 和 DPUUID。如果设置了 DPID 和 DPUUID，则它们将随每个信号一起发送。

   ```js
   ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   向受众管理发送具有特征的信号。

   ```js
   ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   返回最近获取的访客资料。如果尚未提交信号，则返回空对象。

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   返回最近获取的访客资料。如果尚未提交信号，则返回空对象。

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   返回当前 DPUUID。

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   设置 DPID 和 DPUUID。如果设置了 DPID 和 DPUUID，则它们将随每个信号一起发送。

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   向受众管理发送具有特征的信号。

   ```js
   traitData = {}
   traitData["sampleTrait"] = "sampleValue"
   ADBMobile().audienceSubmitSignal(traitData)
   ```
