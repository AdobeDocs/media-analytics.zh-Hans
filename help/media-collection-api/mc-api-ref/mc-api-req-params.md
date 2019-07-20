---
seo-title: 请求参数
title: 请求参数
uuid: f83e9ef1-803d-4152d6c7-acca325036 b9
translation-type: tm+mt
source-git-commit: 4c5fe469d5ef858e1caa65a25cc23d2a84637144

---


# 请求参数{#request-parameters}

## Analytics 数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `analytics.trackingServer` | Y | `sessionStart` | Adobe Analytics 服务器的 URL |
| `analytics.reportSuite` | Y | `sessionStart` | 标识 Analytics 报表数据的 ID |
| `analytics.enableSSL` | N | `sessionStart` | 指示是否启用 SSL 的 true 或 false |
| `analytics.visitorId` | N | `sessionStart` | Adobe访问者ID是可跨多个Adobe应用程序使用的自定义ID。The Heartbeat `visitorId` equals the Analytics `VID.` |

## 访客数据

| 请求密钥 | 必需 | 设置位置... |  描述  |
| --- | :---: | :---: | --- |
| `visitor.marketingCloudOrgId` | Y | `sessionStart` | Experience Cloud 组织 ID，可在 Adobe Experience Cloud 生态系统中标识您的组织 |
| `visitor.marketingCloudUserId` | N | `sessionStart` | 这是Experience Cloud用户ID(ECID)。在大多数情况下，这是用于识别用户的ID。The Heartbeat `marketingCloudUserId` equals the `MID` in Adobe Analytics. 尽管不是技术要求，但此参数对于访问Experience Cloud系列应用程序是必需的。 |
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
| `media.resume` | N | `sessionStart` | 指示用户是否正在恢复上一会话(与开始新会话相反) |
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
| `media.ad.placementId` | N | `adStart` | 广告的展示位置 ID |

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

## 其他详细信息 {#section_ryt_ccy_lcb}

### visitor.marketingCloudUserId

Pass the Experience Cloud User ID (also known as the `MID` or `MCID`) on the `sessionStart` call by including it inside the `params` map using the following key: **visitor.marketingCloudUserId**. 如果您已经与其他 Experience Cloud 产品集成并且已经获取了 MCID，那么这将是一项非常有用的功能。

>[!NOTE]
>
>Media Analytics(MA)与Experience Cloud系列应用程序(Adobe Analytics、Audience Manager、Target等)集成。您需要 Experience Cloud ID 才能访问这些应用程序。_EID是在大多数情况下用于识别用户的内容。_

### appInstallationId

* **如果您&#x200B;**没有传递`appInstallationId`值-** MA后端将不再生成一个MCID，而是依赖Adobe Analytics来执行此操作。Adobe 的建议是发送 MCID（如果可用），或发送 `appInstallationId`（以及仍需强制使用的 `marketingCloudOrgId` 参数），以便媒体收集 API 生成 MCID 并在所有调用中发送 MCID。

* **如果&#x200B;*您确实*传递`appInstallationId`值-***如果* 您传递值 `appInstallationId` 和(必需) `marketingCloudOrgId` 参数，则MA可由MA后端生成MCID。如果您自己确实传递了 `appInstallationId`，则必须在客户端保留其值。它必须为设备上的应用程序所特有的，并且只要不重新安装该应用程序，就必须持续保留该值。

>[!NOTE]
>
>The `appInstallationId` uniquely identifies the app *and the device*. 对于每个设备上的每个应用程序来说，它必须是唯一的，也就是说，对于在不同的设备上使用相同应用程序、相同版本的两个用户，每个人必须发送一个不同的（唯一的）`appInstallationId`。

<!-- Initially, there were no browser-based customers. In future this will be part of a two-bullet list, one bullet for Native Apps, the other for Browser apps. The . 
\<ul id="ul_iwc_fqt_pbb"\> 
 \<li\>For Browser Apps, this should be a first-party cookie that is persistent for as long as the user stays in the same browser. If clients have multiple websites, they need to have different cookies for each site.</li> 
</ul> -->

### visitor.marketingCloudOrgId

In addition to being necessary for MCID generation when that is not provided, this parameter is also used as the value for the publisher ID (based on which Media Analytics performs [federation rule matching.](../../federated-analytics.md))

### Analytics旧版用户ID(帮助)和声明用户ID(自定义ID)

* **analytics. Assistance：**

   此键的值必须是表示Analytics旧版用户ID的字符串
* **reciptor. customerID：**

   此键的值必须是以下格式的对象：

   ```js
   "<<insert your ID name here>>": {  
     "id": " <<insert your id here>>",  
      "authState": <<insert one of 0, 1, 2>> 
   }
   ```

请注意，`visitor.customerIDs` 值可以包含所呈现格式的任意数量的对象。

### visitor.aamLocationHint

此参数指示Adobe Analytics将客户数据发送到Audience Manager时将点击哪些Adobe Audience Manager(AAM) Edge。如果您未传递此参数，则 Adobe 会将其硬编码为 1。当最终用户倾向于在地理位置相距遥远的地方（例如，美国东部、美国西部、欧洲、亚洲）使用其设备时，这一点尤为重要。否则，用户数据将分布在多个 AAM Edge 中。

### media.resume

如果应用程序确定会话已关闭，稍后又恢复（例如用户离开视频但最终返回，并且播放器从停止的播放头处恢复视频），则可以在 **调用的参数分段内发送一个可选的布尔型** media.resume`sessionStart` 参数。

<!--
| `media.uniqueTimePlayed` | N | Close | The value in seconds of the unique segments of content played during a session. Excludes time played on seek back scenarios in which a viewer is watching the same segment of the content multiple times.  |
-->
