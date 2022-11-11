---
title: 流媒体收集API请�求参数
description: “媒体收集API请求参数、请求密钥和描述的内容。”
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
exl-id: a70025ec-1418-46f1-b41f-433d09f024e1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 93%

---

# 请求参数{#request-parameters}

## Analytics 数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `analytics.trackingServer` | Y | 字符串 | `sessionStart` | Adobe Analytics 服务器的 URL |
| `analytics.reportSuite` | Y | 字符串 | `sessionStart` | 标识 Analytics 报表数据的 ID |
| `analytics.enableSSL` | N | 布尔 | `sessionStart` | 指示是否启用 SSL 的 true 或 false |
| `analytics.visitorId` | N | 字符串 | `sessionStart` | Adobe 访客 ID 是可在多个 Adobe 应用程序中使用的自定义 ID。心率 `visitorId` 等于 Analytics `VID.` |

## 访客数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | 字符串 | `sessionStart` | Experience Cloud 组织 ID，可在 Adobe Experience Cloud 生态系统中标识您的组织 |
| `visitor.marketingCloudUserId` | N | 字符串 | `sessionStart` | 这是 Experience Cloud 用户 ID (ECID)。在大多数情况下，这是您应当用来标识用户的 ID。心率 `marketingCloudUserId` 等于 Adobe Analytics 中的 `MID`。虽然从技术上讲不是必需的，但访问 Experience Cloud 系列应用程序时需要此参数。 |
| `visitor.aamLocationHint` | N | 整数 | `sessionStart` | 提供Adobe Audience Manager边缘数据 — 如果未输入值，则值为null。 |
| `appInstallationId` | N | 字符串 | `sessionStart` | appInstallationId 用于唯一标识应用程序和设备 |

## 内容数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `media.id` | Y | 字符串 | `sessionStart` | 内容的唯一标识符 |
| `media.name` | N | 字符串 | `sessionStart` | 人类可读的内容名称 |
| `media.length` | Y | 数字 | `sessionStart` | 内容长度（秒） |
| `media.contentType` | Y | 字符串 | `sessionStart` | 流的格式（可以是任何字符串，一些推荐值为“Live”、“VOD”或“Linear”） |
| `media.playerName` | Y | 字符串 | `sessionStart` | 负责呈现内容的播放器的名称 |
| `media.channel` | Y | 字符串 | `sessionStart` | 内容分发的渠道。分发渠道可以是移动应用程序名称或网站名称、属性名称 |
| `media.resume` | N | 布尔 | `sessionStart` | 指示用户是否正在恢复上一个会话（而不是启动新会话） |
| `media.sdkVersion` | N | 字符串 | `sessionStart` | 播放器使用的 SDK 版本 |

## 内容标准元数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `media.streamFormat` | N | 字符串 | `sessionStart` | 流格式，例如&quot;HD&quot; |
| `media.show` | N | 字符串 | `sessionStart` | 节目或系列节目的名称 |
| `media.season` | N | 字符串 | `sessionStart` | 节目或系列节目所属的季编号 |
| `media.episode` | N | 字符串 | `sessionStart` | 剧集的数量 |
| `media.assetId` | N | 字符串 | `sessionStart` | 视频资产内容的唯一标识符，例如电视剧剧集标识符、电影资产标识符或实时事件标识符。通常，这些 ID 是从元数据颁发机构（如 EIDR、TMS/Gracenote 或 Rovi）派生的。这些标识符也可以来自其他专有或内部系统。 |
| `media.genre` | N | 字符串 | `sessionStart` | 内容制作者定义的内容类型 |
| `media.firstAirDate` | N | 字符串 | `sessionStart` | 内容首次在电视上播出的日期 |
| `media.firstDigitalDate` | N | 字符串 | `sessionStart` | 内容首次在任何数字平台上播出的日期 |
| `media.rating` | N | 字符串 | `sessionStart` | 由电视节目家长指南定义的评级 |
| `media.originator` | N | 字符串 | `sessionStart` | 内容的创作者 |
| `media.network` | N | 字符串 | `sessionStart` | 网络/渠道名称 |
| `media.showType` | N | 字符串 | `sessionStart` | 内容的类型，以 0 到 3 之间的整数表示。 <ul> <li>0 - 整集 </li> <li>1 - 预览 </li> <li>2 - 剪辑 </li> <li>3 - 其它 </li> </ul> |
| `media.adLoad` | N | 字符串 | `sessionStart` | 加载的广告类型 |
| `media.pass.mvpd` | N | 字符串 | `sessionStart` | 由 Adobe 身份验证提供的 MVPD |
| `media.pass.auth` | N | 字符串 | `sessionStart` | 表示用户已获得 Adobe 身份验证授权（若要设置，则只能为 true） |
| `media.dayPart` | N | 字符串 | `sessionStart` | 一天中播放内容的时间 |
| `media.feed` | N | 字符串 | `sessionStart` | 信息源的类型，例如“West-HD” |

## 广告数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | 字符串 | `adBreakStart` | 广告时间的友好名称 |
| `media.ad.podIndex` | Y | 整数 | `adBreakStart` | 视频中广告面板的索引 |
| `media.ad.podSecond` | Y | 数字 | `adBreakStart` | 面板开始的时间（秒） |
| `media.ad.podPosition` | Y | 整数 | `adStart` | 广告时间内广告的索引（从 1 开始） |
| `media.ad.name` | N | 字符串 | `adStart` | 广告的友好名称 |
| `media.ad.id` | Y | 字符串 | `adStart` | 广告的名称 |
| `media.ad.length` | Y | 数字 | `adStart` | 视频广告的长度（以秒为单位） |
| `media.ad.playerName` | Y | 字符串 | `adStart` | 负责呈现广告的播放器的名称 |

## 广告标准元数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `media.ad.advertiser` | N | 字符串 | `adStart` | 广告中展现的产品所属的公司或品牌 |
| `media.ad.campaignId` | N | 字符串 | `adStart` | 广告营销活动的 ID |
| `media.ad.creativeId` | N | 字符串 | `adStart` | 广告创作的 ID |
| `media.ad.siteId` | N | 字符串 | `adStart` | 广告网站的 ID |
| `media.ad.creativeURL` | N | 字符串 | `adStart` | 广告创作的 URL |
| `media.ad.placementId` | N | 字符串 | `adStart` | 广告的版面 ID |

## 章节数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `media.chapter.index` | Y | 整数 | `chapterStart` | 标识章节在内容中的位置 |
| `media.chapter.offset` | Y | 数字 | `chapterStart` | 播放中章节开始的时间（秒） |
| `media.chapter.length` | Y | 数字 | `chapterStart` | 章节的长度（以秒为单位） |
| `media.chapter.friendlyName` | N | 字符串 | `chapterStart` | 章节的人类易记名称 |

## 质量数据

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `media.qoe.bitrate` | N | 整数 | 任何 | 平均比特率（以bps为单位）。 平均比特率计算为在播放会话期间发生的播放持续时间的所有相关比特率值的加权平均值。 |
| `media.qoe.droppedFrames` | N | 整数 | 任何 | 流中的丢帧数 |
| `media.qoe.framesPerSecond` | N | 整数 | 任何 | 每秒帧数 |
| `media.qoe.timeToStart` | N | 整数 | 任何 | 用户点击播放与内容加载和开始播放之间所经过的时间（以毫秒为单位） |

## 《加州消费者隐私法案》(CCPA) 参数  {#ccpa-params}

| 请求密钥 | 必需 | 请求类型键 | 设置... |  描述  |
| --- | :---: | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | 布尔 | `sessionStart` | 如果最终用户选择禁止在 Adobe Analytics 与其他 Experience Cloud 解决方案（如 Audience Manager）之间共享其数据，则设置为 true |
| `analytics.optOutShare` | N | 布尔 | `sessionStart` | 如果最终用户选择禁止联合其数据（例如，将其数据联合到其他 Adobe Analytics 客户端），则设置为 true。 |

## 其他详细信息 {#additional-details}

### visitor.marketingCloudUserId

在 `sessionStart` 调用中传递 Experience Cloud 用户 ID（也称为 `MID` 或 `MCID`），方法是使用以下键将其包含在 `params` 映射中：**visitor.marketingCloudUserId**。如果您已经与其他 Experience Cloud 产品集成并且已经获取了 MCID，那么这将是一项非常有用的功能。

>[!NOTE]
>
>Media Analytics (MA) 可与 Experience Cloud 系列应用程序（Adobe Analytics、Audience Manager、Target 等）集成。您需要 Experience Cloud ID 才能访问这些应用程序。_在大多数情况下，您应当使用 ECID 来标识用户。_

### appInstallationId

* **如果您&#x200B;*没有*传递 `appInstallationId` 值 -** MA 后端将不再生成 MCID，而是依赖 Adobe Analytics 来执行此操作。Adobe 的建议是发送 MCID（如果可用），或发送 `appInstallationId`（以及仍需强制使用的 `marketingCloudOrgId` 参数），以便媒体收集 API 生成 MCID 并在所有调用中发送 MCID。

* **如果您&#x200B;*确有*传递 `appInstallationId` 值 -**&#x200B;如果您传递 `appInstallationId` 值和（必需）`marketingCloudOrgId` 参数，则 MCID *可以*&#x200B;由 MA 后端生成。如果您自己确实传递了 `appInstallationId`，则必须在客户端保留其值。它必须为设备上的应用程序所特有的，并且只要不重新安装该应用程序，就必须持续保留该值。

>[!NOTE]
>
>`appInstallationId` 用于唯一标识应用程序&#x200B;*和设备*。对于每个设备上的每个应用程序来说，它必须是唯一的，也就是说，对于在不同的设备上使用相同应用程序、相同版本的两个用户，每个人必须发送一个不同的（唯一的）`appInstallationId`。

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The .
\<ul id="ul_iwc_fqt_pbb"\>
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li>
</ul> -->

### visitor.marketingCloudOrgId

除了在未提供 MCID 的情况下需要使用此参数生成 MCID 之外，此参数也用作发布者 ID 的值（具体依据执行[联合规则匹配](/help/use-cases/federated-analytics.md)的 Media Analytics）。

### Analytics 旧版用户 ID (aid) 和已声明的用户 ID (customerIDs)

* **analytics.aid：**

   此键的值必须是表示 Analytics 旧版用户 ID 的字符串
* **visitor.customerIDs：**

   此键的值必须是以下格式的对象：

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>>
   }
   ```

请注意，`visitor.customerIDs` 值可以包含所呈现格式的任意数量的对象。

### visitor.aamLocationHint

此参数指示当 Adobe Analytics 将客户数据发送至 Audience Manager 时，将会点击哪个 Adobe Audience Manager (AAM) Edge。如果未输入值，则值为null。 当最终用户倾向于在地理上相距较远的位置（例如，美国东部、美国西部、欧洲、亚洲）使用其设备时，这一点尤其重要。否则，用户数据将散布在多个 AAM 边缘中。

### media.resume

如果应用程序确定会话已关闭，稍后又恢复（例如用户离开视频但最终返回，并且播放器从停止的播放头处恢复视频），则可以在 **调用的参数分段内发送一个可选的布尔型** media.resume`sessionStart` 参数。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
