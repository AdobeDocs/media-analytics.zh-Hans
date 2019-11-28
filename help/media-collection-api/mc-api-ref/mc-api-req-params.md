---
title: 请求参数
description: null
uuid: f83e9ef1-803d-4152-a6c7-acaa325036b9
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 请求参数{#request-parameters}

## Analytics 数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | Adobe Analytics 服务器的 URL |
| `analytics.reportSuite` | Y | `sessionStart` | 标识 Analytics 报表数据的 ID |
| `analytics.enableSSL` | N | `sessionStart` | 指示是否启用 SSL 的 true 或 false |
| `analytics.visitorId` | N | `sessionStart` | Adobe 访客 ID 是可在多个 Adobe 应用程序中使用的自定义 ID。心率 `visitorId` 等于 Analytics `VID.` |

## 访客数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | Experience Cloud 组织 ID，可在 Adobe Experience Cloud 生态系统中标识您的组织 |
| `visitor.marketingCloudUserId` | N | `sessionStart` | 这是 Experience Cloud 用户 ID (ECID)。在大多数情况下，这是您应当用来标识用户的 ID。心率 `marketingCloudUserId` 等于 Adobe Analytics 中的 `MID`。虽然从技术上讲不是必需的，但访问 Experience Cloud 系列应用程序时需要此参数。 |
| `visitor.aamLocationHint` | N | `sessionStart` | 提供 Adobe Audience Manager Edge 数据 |
| `appInstallationId` | N | `sessionStart` | appInstallationId 用于唯一标识应用程序和设备 |

## 内容数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `media.id` | Y | `sessionStart` | 内容的唯一标识符 |
| `media.name` | N | `sessionStart` | 人类可读的内容名称 |
| `media.length` | Y | `sessionStart` | 内容长度（秒） |
| `media.contentType` | Y | `sessionStart` | 流的格式（可以是任何字符串，一些推荐值为“Live”、“VOD”或“Linear”） |
| `media.playerName` | Y | `sessionStart` | 负责呈现内容的播放器的名称 |
| `media.channel` | Y | `sessionStart` | 内容的分发渠道。这可以是一个移动应用程序名称或一个网站名称、属性名称 |
| `media.resume` | N | `sessionStart` | 指示用户是否正在恢复上一个会话（而不是启动新会话） |
| `media.sdkVersion` | N | `sessionStart` | 播放器使用的 SDK 版本 |

## 内容标准元数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `media.show` | N | `sessionStart` | 节目或系列节目的名称 |
| `media.season` | N | `sessionStart` | 节目或系列节目所属的季编号 |
| `media.episode` | N | `sessionStart` | 剧集的数量 |
| `media.assetId` | N | `sessionStart` | 视频资产内容的唯一标识符，例如电视剧剧集标识符、电影资产标识符或直播赛事标识符。通常而言，这些 ID 来自元数据管理机构，例如 EIDR、TMS/Gracenote 或 Rovi。这些标识符也可能来自其他专有或内部系统。 |
| `media.genre` | N | `sessionStart` | 内容制作者定义的内容类型 |
| `media.firstAirDate` | N | `sessionStart` | 内容首次在电视上播出的日期 |
| `media.firstDigitalDate` | N | `sessionStart` | 内容首次在任何数字平台上播出的日期 |
| `media.rating` | N | `sessionStart` | 由电视节目家长指南定义的评级 |
| `media.originator` | N | `sessionStart` | 内容的创作者 |
| `media.network` | N | `sessionStart` | 网络/渠道名称 |
| `media.showType` | N | `sessionStart` | 内容的类型，以 0 到 3 之间的整数表示： <ul> <li>0 - 完整剧集 </li> <li>1 - 预告片 </li> <li>2 - 剪辑 </li> <li>3 - 其他 </li> </ul> |
| `media.adLoad` | N | `sessionStart` | 加载的广告类型 |
| `media.pass.mvpd` | N | `sessionStart` | 由 Adobe 身份验证提供的 MVPD |
| `media.pass.auth` | N | `sessionStart` | 表示用户已获得 Adobe 身份验证授权（若要设置，则只能为 true） |
| `media.dayPart` | N | `sessionStart` | 一天中播放内容的时间 |
| `media.feed` | N | `sessionStart` | 信息源的类型，例如“West-HD” |

## 广告数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `media.ad.podFriendlyName` | N | `adBreakStart` | 广告时间的友好名称 |
| `media.ad.podIndex` | Y | `adBreakStart` | 视频中广告面板的索引 |
| `media.ad.podSecond` | Y | `adBreakStart` | 面板开始的时间（秒） |
| `media.ad.podPosition` | Y | `adStart` | 广告时间内广告的索引（从 1 开始） |
| `media.ad.name` | N | `adStart` | 广告的友好名称 |
| `media.ad.id` | Y | `adStart` | 广告的名称 |
| `media.ad.length` | Y | `adStart` | 视频广告的长度（以秒为单位） |
| `media.ad.playerName` | Y | `adStart` | 负责呈现广告的播放器的名称 |

## 广告标准元数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `media.ad.advertiser` | N | `adStart` | 广告中展现的产品所属的公司或品牌 |
| `media.ad.campaignId` | N | `adStart` | 广告营销活动的 ID |
| `media.ad.creativeId` | N | `adStart` | 广告创作的 ID |
| `media.ad.siteId` | N | `adStart` | 广告网站的 ID |
| `media.ad.creativeURL` | N | `adStart` | 广告创作的 URL |
| `media.ad.placementId` | N | `adStart` | 广告的版面 ID |

## 章节数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `media.chapter.index` | Y | `chapterStart` | 标识章节在内容中的位置 |
| `media.chapter.offset` | Y | `chapterStart` | 播放中章节开始的时间（秒） |
| `media.chapter.length` | Y | `chapterStart` | 章节的长度（以秒为单位） |
| `media.chapter.friendlyName` | N | `chapterStart` | 章节的人类易记名称 |

## 质量数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `media.qoe.bitrate` | N | “任一” | 流的比特率 |
| `media.qoe.droppedFrames` | N | “任一” | 流中丢帧的数量 |
| `media.qoe.framesPerSecond` | N | “任一” | 每秒帧数 |
| `media.qoe.timeToStart` | N | “任一” | 用户点击播放和内容加载并开始播放之间所经过的时间（以毫秒为单位） |

## 《加州消费者隐私法案》(CCPA) 参数 {#ccpa-params}

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `analytics.optOutServerSideForwarding` | N | `sessionStart` | 如果最终用户选择禁止在 Adobe Analytics 与其他 Experience Cloud 解决方案（如 Audience Manager）之间共享其数据，则设置为 true |
| `analytics.optOutShare` | N | `sessionStart` | 如果最终用户选择禁止联合其数据（例如，将其数据联合到其他 Adobe Analytics 客户端），则设置为 true。 |

## 其他详细信息 {#additional-details}

### visitor.marketingCloudUserId

在 `sessionStart` 调用中传递 Experience Cloud 用户 ID（也称为 `MID` 或 `MCID`），方法是使用以下键将其包含在 `params` 映射中：**visitor.marketingCloudUserId**。如果您已经与其他 Experience Cloud 产品集成并且已经获取了 MCID，那么这将是一项非常有用的功能。

>[!NOTE]
>
>Media Analytics (MA) 可与 Experience Cloud 系列应用程序（Adobe Analytics、Audience Manager、Target 等）集成。您需要 Experience Cloud ID 才能访问这些应用程序。_在大多数情况下，您应当使用 ECID 来标识用户。_

### appInstallationId

* **如果您&#x200B;*没有*传递`appInstallationId`值 -** MA 后端将不再生成 MCID，而是依赖 Adobe Analytics 来执行此操作。Adobe 的建议是发送 MCID（如果可用），或发送 `appInstallationId`（以及仍需强制使用的 `marketingCloudOrgId` 参数），以便媒体收集 API 生成 MCID 并在所有调用中发送 MCID。

* **如果您&#x200B;*确有*传递`appInstallationId`值 -**&#x200B;如果您传递 `appInstallationId` 值和（必需）`marketingCloudOrgId` 参数，则 MCID *可以*&#x200B;由 MA 后端生成。如果您自己确实传递了 `appInstallationId`，则必须在客户端保留其值。它必须为设备上的应用程序所特有的，并且只要不重新安装该应用程序，就必须持续保留该值。

>[!NOTE]
>
>`appInstallationId` 用于唯一标识应用程序&#x200B;*和设备*。对于每个设备上的每个应用程序来说，它必须是唯一的，也就是说，对于在不同的设备上使用相同应用程序、相同版本的两个用户，每个人必须发送一个不同的（唯一的）`appInstallationId`。

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

除了在未提供 MCID 的情况下需要使用此参数生成 MCID 之外，此参数也用作发布者 ID 的值（具体依据执行[联合规则匹配](/help/federated-analytics.md)的 Media Analytics）。

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

此参数指示当 Adobe Analytics 将客户数据发送至 Audience Manager 时，将会点击哪个 Adobe Audience Manager (AAM) Edge。如果您未传递此参数，则 Adobe 会将其硬编码为 1。当最终用户倾向于在地理位置相距遥远的地方（例如，美国东部、美国西部、欧洲、亚洲）使用其设备时，这一点尤为重要。否则，用户数据将分布在多个 AAM Edge 中。

### media.resume

如果应用程序确定会话已关闭，稍后又恢复（例如用户离开视频但最终返回，并且播放器从停止的播放头处恢复视频），则可以在 **调用的参数分段内发送一个可选的布尔型** media.resume`sessionStart` 参数。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
