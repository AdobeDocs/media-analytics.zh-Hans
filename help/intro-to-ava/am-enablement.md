---
seo-title: Audience Manager 启用
title: Audience Manager 启用
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: tm+mt
source-git-commit: 8ae15f1e14731a97d212ab66816a777b4dcc897e

---


# Audience Manager 启用{#audience-manager-enablement}

Adobe Audience Manager (AAM) 是一个数据管理平台 (DMP)，它可以帮助您汇总受众数据资产，从而您可以出于商业目的轻松收集与网站访客有关的信息，创建可投向市场的区段，以及向合适的受众提供有针对性的广告和内容。

使用 AAM，您可以不必依赖于数据销售商、交易所或需求方平台。此外，就合作伙伴的数据资产而言，AAM 与其完全没有任何关系。通过访问多个数据源，AAM 可让数字出版商能够使用各种各样的第三方数据和我们的私有数据协作。要了解有关AAM的更多信息，请参阅AAM文档 [Audience manager产品文档。](https://docs-author.corp.adobe.com/content/help/en/audience-manager/user-guide/aam-home.html)

**VA 到 AAM 的数据传输** - 对于视频内容和视频广告，使用解决方案（保留）变量收集的量度和元数据可以自动发送到 AAM。数据传输可在所有平台中进行，包括桌面、移动设备和 OTT。要启用此服务器端数据传输，您需要联系 Adobe 客户关怀团队，并要求启用此数据源。

>[!IMPORTANT]
>
>为确保顺利地将数据传输到AAM，您应使用最新版Media SDK库。

联合数据完全支持对 AAM 的数据共享。请与您的 Adobe 团队合作，以确认联合数据设置。

## OTT/AAM 方法 {#section_yqq_5br_v2b}

您可以使用以下方法发送信号，并从 Audience Manager 中检索访客区段：

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   返回最近获取的访客资料。若尚未提交信号，则返回空对象。

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   返回最近获取的访客资料。若尚未提交信号，则返回空对象。

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   返回当前 DPUUID。

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   设置 DPID 和 DPUUID。如果设置了 DPID 和 DPUUID，它们将与每个信号一起发送。

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   向受众管理发送具有特征的信号。

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   返回最近获取的访客资料。若尚未提交信号，则返回空对象。

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   返回最近获取的访客资料。若尚未提交信号，则返回空对象。

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   返回当前 DPUUID。

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   设置 DPID 和 DPUUID。如果设置了 DPID 和 DPUUID，它们将与每个信号一起发送。

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   向受众管理发送具有特征的信号。

   ```js
   ADBMobile().audienceSubmitSignal()
   ```

