---
title: Adobe Audience Manager 支持什么？
description: 了解如何将应用程序操作链接到媒体跟踪数据，而无需其他的处理规则和自定义变量。
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# Audience Manager 启用{#audience-manager-enablement}

Adobe Audience Manager (AAM) 是一种数据管理平台 (DMP)，可帮助您将受众数据资产整合在一起，从而轻松收集与网站访客相关的商业信息、创建可销售的区段，并向正确的受众提供有针对性的广告和内容。

使用 AAM，您不会受到数据销售商、交换或需求侧平台的束缚。 此外，AAM 对传递给您合作伙伴的数据资产完全不可知。 AAM 通过访问多个数据源，使数字发布者能够使用各种第三方数据。 要了解有关 AAM 的更多信息，请参阅 AAM 文档 [Audience Manager 产品文档](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=zh-Hans)。

**VA 到 AAM 数据传输 —**&#x200B;对于视频内容和视频广告，使用解决方案（保留的）变量收集的量度和元数据可自动发送到 AAM。 数据传输可跨所有平台使用，包括台式机、移动设备和 OTT。 要启用此服务器端数据传输，您需要联系 Adobe 客户关怀团队以要求启用此源。

>[!IMPORTANT]
>
>为确保将数据顺利传输至 AAM，您应该使用最新版本的 Media SDK 库。

联合数据完全支持与 AAM 的数据共享。 请与您的 Adobe 团队合作，确认联合数据设置。

## OTT/AAM 方法 {#ott-aam-methods}

您可以使用以下方法发送信号，并从 Audience Manager 中检索访客区段：

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

  返回最近获取的访客轮廓。 如果尚未提交信号，则返回空对象。

  ```js
  ADBMobile.audienceManager.getVisitorProfile();
  ```

* `getDpid() -`

  返回最近获取的访客轮廓。 如果尚未提交信号，则返回空对象。

  ```js
  ADBMobile.audienceManager.getDpid();
  ```

* `getDpuuid() -`

  返回当前 DPUUID。

  ```js
  ADBMobile.audienceManager.getDpuuid();
  ```

* `setDpidAndDpuuid() -`

  设置 DPID 和 DPUUID。 如果设置了 DPID 和 DPUUID，则它们将随每个信号一起发送。

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

  返回最近获取的访客轮廓。 如果尚未提交信号，则返回空对象。

  ```js
  ADBMobile().audienceVisitorProfile()
  ```

* `audienceDpid -`

  返回最近获取的访客轮廓。 如果尚未提交信号，则返回空对象。

  ```js
  ADBMobile().audienceDpid()
  ```

* `audienceDpuuid -`

  返回当前 DPUUID。

  ```js
  ADBMobile().audienceDpuuid()
  ```

* `audienceSetDpidAndDpuuid -`

  设置 DPID 和 DPUUID。 如果设置了 DPID 和 DPUUID，则它们将随每个信号一起发送。

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
