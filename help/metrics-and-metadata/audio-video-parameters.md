---
title: 音频和视频参数
description: null
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: ht
source-git-commit: ccd4209f6fad0547e9595674602ee978d86e10cd
workflow-type: ht
source-wordcount: '6103'
ht-degree: 100%

---


# 音频和视频参数{#audio-and-video-parameters}

>[!IMPORTANT]
>
>2019 年 2 月 7 日，Adobe Analytics for Video and Audio 发布了一项量度名称变更。“媒体启动”<i></i>现在将更名为“媒体开始”<i></i>。此名称变更是为了遵循量度和报表的行业标准，并使该量度可在报表中轻松识别。

>[!NOTE]
>
>从 2018 年 9 月 13 日起，一些维度、量度和报表的标签发生了更改，以便允许对视频和音频分析进行跨内容跟踪。已更改的标签包括：*视频初始化*&#x200B;改为&#x200B;*媒体初始化*、*视频长度*&#x200B;改为&#x200B;*内容时长*、*视频名称*&#x200B;改为&#x200B;*内容名称*。Reports and Analytics 中的视频报表均已更新为使用“媒体”名称而非“视频”。标签更改不会更改数据收集或历史数据。如果您在 Report Builder 中或任何其他可能受此更改影响的外部自动数据提取中使用这些标签，请注意这些更改。

本主题介绍 Adobe 通过解决方案变量收集的音频和视频内容数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或由 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示基本音频和视频跟踪是否需要该参数。
   * *类型* - 指定要设置的变量的类型：字符串或数字。
   * *发送条件* - 指示何时发送数据：*媒体开始*&#x200B;表示在媒体开始播放时发送分析调用；*广告开始*&#x200B;表示在广告等开始播放时发送分析调用；*关闭*&#x200B;调用表示在媒体会话或广告、章节等结束时直接从心率服务器向分析服务器发送经过汇编的分析调用。在网络数据包调用中无法使用关闭调用。
   * *最低 SDK 版本* - 指示您访问该参数所需的 SDK 版本。
   * *示例值* - 提供常用变量用法的示例。
* **网络参数：**&#x200B;显示传递到 Adobe Analytics 或心率服务器的值。此列显示网络调用中由 Adobe Media SDK 生成的参数的名称。
* **报告：**&#x200B;有关如何查看和分析音频和视频数据的信息。
   * *可用* - 指示在默认情况下数据在报表中可用（*是*），还是需要自定义设置（*自定义*）
   * *保留的变量* - 指示数据是作为保留变量中的事件、eVar、prop 还是分类而捕获的。
   * *过期* - 指示数据在每次点击后还是每次访问后过期。
   * *报表名称* - 变量的 Adobe Analytics 报表名称
   * *上下文数据* - 传递到报表服务器并用于处理规则的 Adobe Analytics 上下文数据的名称。
   * *数据源* - Clickstream 或实时流数据源中的变量的列名称
   * *Audience Manager* - Adobe Audience Manager 中的特征名称

>[!IMPORTANT]
>
>请勿更改下面列出的在“报表/保留的变量”下描述为“分类”的任何变量的分类名称。\
>在启用报表包进行媒体跟踪后，将定义媒体分类。Adobe 会不时添加新属性，如果添加了新属性，客户必须重新启用其报表包才能访问新的媒体属性。在更新过程中，Adobe 会通过检查变量名称来确定是否启用了分类。如果任何变量名称缺失，Adobe 会再次添加缺失的变量名称。

## 音频和视频核心数据 {#core-audio-and-video-data}

### 流类型 {#stream-type}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.streamType</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 2.2 <br/><br/>可从以下位置获取：[媒体收集 API 概述](/help/media-collection-api/mc-api-overview.md)或[下载 SDK - 版本 2.2](/help/sdk-implement/download-sdks.md)。  </li>  <li> **示例值：**<br/>&quot;video&quot;</li> <li> **描述：**<br/>标识流类型。有效值为“audio”、“video”和“all”。<br/><br/>[报表区段](/help/metrics-and-metadata/segments.md)：<br/><br/>媒体流类型：全部 -<br/>对所有媒体流数据进行分段；规则：存在内容 (ID)<br/><br/>媒体流类型：音频 -<br/>对所有音频流数据进行分段；规则：存在内容 (ID) 且媒体流类型 = audio<br/><br/>媒体流类型：“视频”-<br/>对所有视频流数据进行分段；规则：存在内容 (ID) 且媒体流类型 = audio<br/><br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.streamType)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.streamType)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>访问时</li> <li> **报表名称：**<br/>内容</li> <li> **上下文数据：**<br/>(a.media.streamType)</li> <li> **数据馈送：**<br/>videostreamtype</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.streamType)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 内容 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.id</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;4586695ABC&quot;</li> <li>**描述：**<br/>内容的内容 ID，可用于绑定到其他行业/CMS ID，等同于`s:asset:video_id.`的最后一个值</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.name)</li> <li> **心率：**<br/>(s:asset:video_id)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>访问时</li> <li> **报表名称：**<br/>内容</li> <li> **上下文数据：**<br/>(a.media.name)</li> <li> **数据馈送：**<br/>video</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.name)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### 内容时长（变量）

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.length</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>VOD：128；实时：86400；线性：1800。</li><li> **描述：**<br/>剪辑长度/运行时间 - 此值是所使用内容的最大长度（或时长），以秒为单位。它等同于“主要”类型事件中`l:asset:length`的最后一个值。<br/>如果未设置`l:asset:length`，那么会使用`l:asset:duration`的最后一个值。<br/>在报表中，“视频长度”是分类，而“内容时长（变量）”是 eVar。<br/> **重要信息：**&#x200B;此属性用于计算多个量度，例如进度跟踪量度和平均观看分钟数。如果未设置此值，或设置的值不大于零，那么这些量度将不可用。对于时长未知的实时媒体，此值默认为 86400。<br/>对于 1.5.1 以前的版本，此值为 `l:asset:duration`；对于 1.5.1 以后的版本，此值为 `l:asset:length.` <br/> **发行日期：2018 年 9 月 13 日** </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.length)</li> <li> **心率：**<br/>(l:asset:length)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>内容时长（变量）</li> <li> **上下文数据：**<br/>(a.media.length)</li> <li> **数据馈送：**<br/>videolength</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.length)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### 视频长度

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.length</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>VOD：128；实时：86400；线性：1800。</li> <li> **描述：**<br/>剪辑长度/运行时间 - 此值是所使用内容的最大长度（或时长），以秒为单位。它等同于“主要”类型事件中`l:asset:length`的最后一个值。如果未设置`l:asset:length`，那么会使用`l:asset:duration`的最后一个值。在报表中，“视频长度”是分类，而“内容时长（变量）”是 eVar。<br/> **重要信息：**&#x200B;此属性用于计算多个量度，例如进度跟踪量度和平均观看分钟数。如果未设置此值，或设置的值不大于零，那么这些量度将不可用。对于时长未知的实时媒体，此值默认为 86400。对于 1.5.1 以前的版本，此值为 `l:asset:duration`；对于 1.5.1 以后的版本，此值为 `l:asset:length.`<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.length)</li> <li> **心率：**<br/>(l:asset:length)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>分类</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>视频长度</li> <li> **上下文数据：**<br/>(a.media.length)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.length)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length, // <==
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### 内容类型

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.contentType</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>有限制的字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;vod&quot;</li> <li> **描述：**<br/>每种**流类型&#x200B;**的可用值：<br/> _音频：_“song”、“podcast”、“audiobook”、“radio”<br/> _视频：_“VoD”、“实时”、“线性”、“UGC”、“DVoD”<br/>客户可以为此参数提供自定义值。此值等同于 `s:stream:type.` 如果未设置，则等同于 `missing_content_type.` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.contentType)</li> <li> **心率：**<br/>(s:stream:type)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>内容类型</li> <li> **上下文数据：**<br/>(a.contentType)</li> <li> **数据馈送：**<br/>videocontenttype</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.contentType)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId,
                                            java.lang.Double length,
                                            java.lang.String streamType, // <==
                                            MediaHeartbeat.MediaType mediaType)
```

### 媒体会话 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>从后端获取</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.8 </li> <li> **示例值：**<br/>1482236761294786918253</li> <li> **描述：**<br/>此值用于标识对于单次播放而言具有唯一性的内容流实例。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.vsid)</li> <li> **心率：**<br/>(s:event:sid)</li> </ul> | <ul> <li> **可用：**<br/>使用处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/>自定义</li> <li> **上下文数据：**<br/>(a.media.vsid)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.vsid)</li> </ul> |

### 媒体下载标志

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> `config.downloadedcontent` </li> <li> **API 密钥：**<br/>从后端获取</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>布尔值</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：**<br/>启动 Android 和 iOS 扩展版本 1.1.0 </li> <li> **示例值：**<br/>true</li> <li> **描述：**<br/>如果由于播放下载的内容媒体会话而生成了点击，则设置为 true。如果未播放下载的内容，则此参数不存在。<br/><br/>[Launch](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker-with-optional-configuration)</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.downloaded)</li> <li> **心率：**<br/>(s:meta:a.media.downloaded)</li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/>自定义</li> <li> **上下文数据：**<br/>(a.media.downloaded)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.downloaded)</li> </ul> |

### 内容播放器名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.playerName</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;Brightcove&quot;</li> <li> **描述：**<br/>播放器的名称。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.<br/>playerName)</li> <li> **心率：**<br/>(s:sp:player_name)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>内容播放器名称</li> <li> **上下文数据：**<br/>(a.media.playerName)</li> <li> **数据馈送：**<br/>videoplayername</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.playerName)</li> </ul> |

### 内容渠道

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.channel</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;Sports&quot;</li> <li> **描述：**<br/>分发站点/渠道或播放内容的位置。此处可接受任何字符串值。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.channel)</li> <li> **心率：**<br/>(s:sp:channel)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>内容渠道</li> <li> **上下文数据：**<br/>(a.media.channel)</li> <li> **数据馈送：**<br/>videochannel</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.channel)</li> </ul> |

### 内容区段

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **必需：**<br/>是</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;0-10&quot;</li> <li> **描述：**<br/>描述已查看的内容部分的间隔（以分钟为单位）。区段在播放会话期间计算为播放头的最小值和最大值。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>内容区段</li> <li> **上下文数据：**<br/>(a.media.segment)</li> <li> **数据馈送：**<br/>videosegment</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.segment)</li> </ul> |

### 内容名称（变量）

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.name</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>&quot;The Big Bang Theory&quot;</li> <li> **描述：**<br/>这是内容的“友好”（人类可读）名称，等同于`s:asset:name.`<br/>的最后一个值在报表中，视频名称是分类，内容名称（变量）是 eVAR。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.<br/>friendlyName)</li> <li> **心率：**<br/>(s:asset:name)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>内容名称（变量）</li> <li> **上下文数据：**<br/>(a.media.friendlyName)</li> <li> **数据馈送：**<br/>videoname</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.friendlyName)</li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType,
                                            MediaHeartbeat.MediaType mediaType)
```

### 视频名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.name</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>&quot;The Big Bang Theory&quot;</li> <li> **描述：**<br/>这是内容的“友好”（人类可读）名称，等同于`s:asset:name.`的最后一个值<br/>在报表中，视频名称是分类，内容名称（变量）是 eVAR。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.<br/>friendlyName)</li> <li> **心率：**<br/>(s:asset:name)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>分类</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>视频名称</li> <li> **上下文数据：**<br/>(a.media.friendlyName)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.friendlyName)</li> </ul> |

### 视频路径

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;4586695ABC&quot;</li> <li> **描述：**<br/>提供用于跟踪查看者在网站和/或应用程序中的路径的功能，以了解他们查看特定视频所采用的路径。任何整数和/或字母组合</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.name)</li> <li> **心率：**<br/>(s:asset:video_id)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>prop</li> <li> **报表名称：**<br/>视频路径</li> <li> **上下文数据：**<br/>(a.media.name)</li> <li> **数据馈送：**<br/>videopath</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.name)</li> </ul> |

### SDK 版本

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.sdkVersion</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;2.62.0_release&quot;</li> <li> **描述：**<br/>播放器使用的 SDK 版本。此参数可使用您的播放器支持的任何自定义值。<br/><br/>客户必须自行创建处理规则才能在报表中使用此值。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.<br/>sdkVersion)</li> <li> **心率：**<br/>(s:sp:sdk)</li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/>(a.media.sdkVersion)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.sdkVersion)</li> </ul> |

### VHL 版本

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;js-2.0.1.88-c8c0b1&quot;</li> <li> **描述：**<br/>用于跟踪会话的 Media SDK 版本。<br/><br/>客户必须自行创建处理规则才能在报表中使用此值。<br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.<br/>vhlVersion)</li> <li> **心率：**<br/>(s:sp:hb_version)</li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/>自定义</li> <li> **上下文数据：**<br/>(a.media.vhlVersion)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.vhlVersion)</li> </ul> |

## 标准音频和视频元数据 {#standard-audio-and-video-metadata}

### 节目

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SHOW</li> <li> **API 密钥：**<br/>media.show</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;Modern Family&quot;、&quot;The Last Dance&quot;、&quot;New Girl&quot;</li> <li> **描述：**<br/>节目/系列名称<br/>只有在节目属于某个系列节目的组成部分时，才需要指定“节目名称”。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.show)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.show)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>节目</li> <li> **上下文数据：**<br/>(a.media.show)</li> <li> **数据馈送：**<br/>videoshow</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.show)</li> </ul> |

### 流格式

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>STREAM_FORMAT</li> <li> **API 密钥：**<br/>不适用</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;Live&quot;</li> <li> **描述：**<br/>流的格式（实时、VOD、线性）。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.format)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.format)</li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/>自定义</li> <li> **上下文数据：**<br/>(a.media.format)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.format)</li> </ul> |

### 季

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SEASON</li> <li> **API 密钥：**<br/>media.season</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;2&quot;</li> <li> **描述：**<br/>节目所属的季编号。只有在节目属于某个系列节目的组成部分时，才需要指定“季系列”。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.season)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.season)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>季</li> <li> **上下文数据：**<br/>(a.media.season)</li> <li> **数据馈送：**<br/>videoseason</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.season)</li> </ul> |

### 剧集

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>EPISODE</li> <li> **API 密钥：**<br/>media.episode</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;13&quot;</li> <li> **描述：**<br/>剧集的数量。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.episode)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.episode)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>集</li> <li> **上下文数据：**<br/>(a.media.episode)</li> <li> **数据馈送：**<br/>videoepisode</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.episode)</li> </ul> |

### 资产 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ASSET_ID</li> <li> **API 密钥：**<br/>media.assetId</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;89745363&quot;</li> <li> **描述：**<br/>此参数是媒体资产内容的唯一标识符，例如电视剧剧集标识符、电影资产标识符或直播赛事标识符。通常，这些 ID 是从元数据颁发机构（如 EIDR、TMS/Gracenote 或 Rovi）派生的。这些标识符也可以来自其他专有或内部系统。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.asset)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.asset)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>分类</li> <li> **报表名称：**<br/>资产 ID</li> <li> **上下文数据：**<br/>(a.media.asset)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.asset)</li> </ul> |

### 流派

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>GENRE</li> <li> **API 密钥：**<br/>media.genre</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;Drama&quot;、&quot;Comedy&quot;</li> <li> **描述：**<br/>由内容制作者定义的内容类型或分组。变量实施中的值应以逗号分隔。在报表中，列表 eVar 将每个值拆分为一个行项目，每个行项目具有相等的量度权重。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.genre)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.genre)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>列表 eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>流派</li> <li> **上下文数据：**<br/>(a.media.genre)</li> <li> **数据馈送：**<br/>videogenre</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.genre)</li> </ul> |

### 首次播放日期

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FIRST_AIR_DATE</li> <li> **API 密钥：**<br/>media.firstAirDate</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;2016-01-25&quot;</li> <li> **描述：**<br/>内容首次在电视上播出的日期。可接受任何日期格式，但 Adobe 建议使用如下格式：YYYY-MM-DD</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.airDate)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.airDate)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>分类</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>首次播放日期</li> <li> **上下文数据：**<br/>(a.media.airDate)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.airDate)</li> </ul> |

### 首次数字化日期

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FIRST_DIGITAL_DATE</li> <li> **API 密钥：**<br/>media.firstDigitalDate</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;2016-01-25&quot;</li> <li> **描述：**<br/>内容首次在任何数字渠道或平台上播出的日期。可接受任何日期格式，但 Adobe 建议使用如下格式：YYYY-MM-DD</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.digitalDate)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.digitalDate)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>分类</li> <li> **报表名称：**<br/>首次数字化日期</li> <li> **上下文数据：**<br/>(a.media.digitalDate)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.digitalDate)</li> </ul> |

### 内容评级

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>RATING</li> <li> **API 密钥：**<br/>media.rating</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>TVY、TVG、TVPG、TVMA</li> <li> **描述：**<br/>由电视节目家长指南定义的评级。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.rating)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.rating)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>分类</li> <li> **报表名称：**<br/>内容评级</li> <li> **上下文数据：**<br/>(a.media.rating)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.rating)</li> </ul> |

### 创作者

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ORIGINATOR</li> <li> **API 密钥：**<br/>media.originator</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;Warner Brothers&quot;、&quot;Sony&quot;、&quot;Disney&quot;</li> <li> **描述：**<br/>内容的创作者。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.originator)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.originator)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>分类</li> <li> **报表名称：**<br/>创作者</li> <li> **上下文数据：**<br/>(a.media.originator)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.originator)</li> </ul> |

### 网络

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>NETWORK</li> <li> **API 密钥：**<br/>media.network</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;Fox&quot;、&quot;Bravo&quot;、&quot;ESPN&quot;</li> <li> **描述：**<br/>网络/渠道名称。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.network)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.network)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>网络</li> <li> **上下文数据：**<br/>(a.media.network)</li> <li> **数据馈送：**<br/>videonetwork</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.network)</li> </ul> |

### 节目类型

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SHOW_TYPE</li> <li> **API 密钥：**<br/>media.showType</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;0&quot; = 整集；&quot;1&quot; = 预览/预告片；&quot;2&quot; = 剪辑；&quot;3&quot; = 其他。</li> <li> **描述：**<br/>内容的类型，以 0 到 3 之间的整数表示。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.type)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.type)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>显示类型</li> <li> **上下文数据：**<br/>(a.media.type)</li> <li> **数据馈送：**<br/>videoshowtype</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.type)</li> </ul> |

### MVPD

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>MVPD</li> <li> **API 密钥：**<br/>media.pass.mvpd</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;Comcast&quot;、&quot;DirecTV&quot;、&quot;Dish&quot;</li> <li> **描述：**<br/>通过 Adobe 身份验证提供的 MVPD。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.pass.mvpd)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.pass.<br/>mvpd)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>MVPD</li> <li> **上下文数据：**<br/>(a.media.pass.mvpd)</li> <li> **数据馈送：**<br/>videomvpd</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.pass.mvpd)</li> </ul> |

### 已授权

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>AUTHORIZED</li> <li> **API 密钥：**<br/>media.pass.auth</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;TRUE&quot;</li> <li> **描述：**<br/>用户已通过 Adobe 身份验证获得授权。<br/>**重要信息：**如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.pass.auth)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.pass.<br/>auth)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>已授权</li> <li> **上下文数据：**<br/>(a.media.pass.auth)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.pass.auth)</li> </ul> |

### 播出时段

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>DAY_PART</li> <li> **API 密钥：**<br/>media.dayPart</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li> <li> **描述：**<br/>此属性定义内容在一天中的哪个时间广播或播放。客户可以视需要为此属性设置任何值。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.dayPart)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.dayPart)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>播出时段</li> <li> **上下文数据：**<br/>(a.media.dayPart)</li> <li> **数据馈送：**<br/>videodaypart</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.dayPart)</li> </ul> |

### 媒体馈送类型

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FEED</li> <li> **API 密钥：**<br/>media.feed</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&quot;East-HD&quot;、&quot;West-HD&quot;、&quot;East-SD&quot;</li> <li> **描述：**<br/>馈送类型。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.feed)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.feed)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/>媒体馈送类型</li> <li> **上下文数据：**<br/>(a.media.feed)</li> <li> **数据馈送：**<br/>videofeedtype</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.feed)</li> </ul> |

### 艺人

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.artist</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 <br/>可从以下位置获取：[媒体收集概述](/help/media-collection-api/mc-api-overview.md)或[下载 SDK - 版本 2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>&quot;The Beatles&quot;</li> <li> **描述：**<br/>艺人的姓名。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.artist)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.artist)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/>(a.media.artist)</li> <li> **数据馈送：**<br/>videoaudioartist</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.artist)</li> </ul> |

### 专辑

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.album</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 <br/>可从以下位置获取：[媒体收集概述](/help/media-collection-api/mc-api-overview.md)或[下载 SDK - 版本 2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>&quot;Revolver&quot;</li> <li> **描述：**<br/>专辑的名称。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.album)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.album)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/>(a.media.album)</li> <li> **数据馈送：**<br/>videoaudioalbum</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.album)</li> </ul> |

### 标签

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.label</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 <br/>可从以下位置获取：[媒体收集概述](/help/media-collection-api/mc-api-overview.md)或[下载 SDK - 版本 2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>&quot;Revolver&quot;</li> <li> **描述：**<br/>记录标签的名称。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.label)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.label)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/>(a.media.label)</li> <li> **数据馈送：**<br/>videoaudiolabel</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.label)</li> </ul> |

### 作者

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.author</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 <br/>可从以下位置获取：[媒体收集概述](/help/media-collection-api/mc-api-overview.md)或[下载 SDK - 版本 2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>&quot;John Kennedy Toole&quot;</li> <li> **描述：**<br/>（有声读物）作者的姓名。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.author)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.author)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/>(a.media.author)</li> <li> **数据馈送：**<br/>videoaudioauthor</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.author)</li> </ul> |

### 电台/电视台

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.station</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 <br/>可从以下位置获取：[媒体收集概述](/help/media-collection-api/mc-api-overview.md)或[下载 SDK - 版本 2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>&quot;NPR&quot;</li> <li> **描述：**<br/>广播电台的名称/ID。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.station)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.station)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/>(a.media.station)</li> <li> **数据馈送：**<br/>videoaudiostation</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.station)</li> </ul> |

### 发布者

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.publisher</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始、媒体关闭</li> <li> **最低 SDK 版本：** 1.5.7 <br/>可从以下位置获取：[媒体收集概述](/help/media-collection-api/mc-api-overview.md)或[下载 SDK - 版本 2.2](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>&quot;Random Bauhaus&quot;</li> <li> **描述：**<br/>音频内容发布者的名称。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.publisher)</li> <li> **心率：**<br/>(s:meta:<br/>a.media.publisher)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>点击时</li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/>(a.media.publisher)</li> <li> **数据馈送：**<br/>videoaudiopublisher</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.publisher)</li> </ul> |

## 音频和视频量度 {#audio-and-video-metrics}

### 媒体开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体开始</li> <li> **最低 SDK 版本：**&#x200B;任何版本</li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>媒体的载入事件。（当查看者单击_播放&#x200B;_按钮时，会发生此事件。）即使存在前置广告、缓冲和错误等，也会将此计为视频载入事件。<br/>**重要信息：**如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.view)</li> <li> **心率：**<br/>(s:event:<br/>type=start)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>媒体开始</li> <li> **上下文数据：**<br/>(a.media.view)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.view)</li> </ul> |

### 内容开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>第一帧媒体内容已观看。如果用户在广告播放或缓冲等过程中放弃观看，则不会计为“内容开始”事件。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>内容开始</li> <li> **上下文数据：**<br/>(a.media.play)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.play)</li> </ul> |

### 内容结束 {#content-complete}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>已观看至结束的流。这不一定意味着用户观看或收听了整个流；他们可以跳到前面。此参数仅意味着用户百分百到达流结尾。<br/>另请参阅[会话结束](quality-parameters.md#session-end)<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>(s:event:<br/>type=complete)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>内容结束</li> <li> **上下文数据：**<br/>(a.media.complete)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.complete)</li> </ul> |

### 内容逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>105</li> <li> **描述：**<br/>计算主内容中所有“播放”类型事件的事件总时长（以秒为单位）。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>内容逗留时间</li> <li> **上下文数据：**<br/>(a.media.timePlayed)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.timePlayed)</li> </ul> |

### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>120</li> <li> **描述：**<br/>计算主要内容和广告内容中所有“播放”类型事件的事件总时长（以秒为单位）。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>媒体逗留时间</li> <li> **上下文数据：**<br/>(a.media.totalTimePlayed)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.totalTimePlayed)</li> </ul> |

### 不重复播放时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>94</li> <li> **描述：**<br/>会话期间不重复播放的内容区段的时间值（以秒为单位）。不包含向回搜寻观看的情况（查看者多次观看同一内容区段）所播放的时间。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>自定义</li> <li> **上下文数据：**<br/>(a.media.uniqueTimePlayed)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.uniqueTimePlayed)</li> </ul> |

### 10% 进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>根据内容时长，播放头经过内容的 10% 进度标记。即使向后搜索，标记也只会计数一次。如果向前搜索，则不计数跳过的标记。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>10% 进度标记</li> <li> **上下文数据：**<br/>(a.media.progress10)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.progress10)</li> </ul> |

### 25% 进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>根据内容时长，播放头经过内容的 25% 进度标记。即使向后搜索，标记也只会计数一次。如果向前搜索，则不计数跳过的标记。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>25% 进度标记</li> <li> **上下文数据：**<br/>(a.media.progress25)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.progress25)</li> </ul> |

### 50% 进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>根据内容时长，播放头经过内容的 50% 进度标记。即使向后搜索，标记也只会计数一次。如果向前搜索，则不计数跳过的标记。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>50% 进度标记</li> <li> **上下文数据：**<br/>(a.media.progress50)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.progress50)</li> </ul> |

### 75% 进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/> **不适用** </li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>根据内容时长，播放头经过内容的 75% 进度标记。即使向后搜索，标记也只会计数一次。如果向前搜索，则不计数跳过的标记。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>75% 进度标记</li> <li> **上下文数据：**<br/>(a.media.progress75)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.progress75)</li> </ul> |

### 95% 进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>根据内容时长，播放头经过内容的 95% 进度标记。即使向后搜索，标记也只会计数一次。如果向前搜索，则不计数跳过的标记。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>95% 进度标记</li> <li> **上下文数据：**<br/>(a.media.progress95)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.progress95)</li> </ul> |

### 平均观看分钟数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>大于或等于 1</li> <li> **描述：**<br/>“平均观看分钟数”量度的计算方式为一个特定媒体项目的内容逗留总时间除以该媒体项目所有播放会话的时长：<br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>平均观看分钟数</li> <li> **上下文数据：**<br/>(a.media.averageMinuteAudience)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.averageMinuteAudience)</li> </ul> |

### 自上次调用以后经过的秒数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>600</li> <li> **说明：**<br/>如果流在关闭时带有完整事件或结束事件，则自上次调用量度开始的秒数为 0；如果由于超时而关闭，则通常为 600。此量度没有解决方案变量和自动处理规则，因此您必须创建自定义处理规则才能进行保存。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/>不适用</li> <li> **上下文数据：**<br/>(a.media.secondsSinceLastCall)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.secondsSinceLastCall)</li> </ul> |

### 联合数据

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>布尔值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>true</li> <li> **描述：**<br/>如果点击已联合（即，客户作为联合数据共享的一部分接收，而不是他们自己的实施），则设置为 true。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/>不适用</li> <li> **上下文数据：**<br/>(a.media.federated)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.federated)</li> </ul> |

### 预计的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>1 - 播放 19 分钟；<br/>2 - 播放 31 分钟；<br/>3 - 播放 78 分钟。</li> <li> **描述：**<br/>每个内容的预计视频流或音频流数量。播放时间（内容 + 广告）每增加 30 分钟，该值也会相应增加。客户必须自行创建处理规则才能在报表中使用此值。<br/><br/>会将每 30 分钟计为一个流，此计算基于`ms_s`（或 totalTimePlayed = Video Total Time），类似于：<br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则</li> <li> **保留的变量：**<br/>不适用</li> <li> **报表名称：**<br/>自定义</li> <li> **上下文数据：**<br/>(a.media.estimatedStreams)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.estimatedStreams)</li> </ul> |

### 受暂停影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>此值为 true 或 false。如果在播放单个媒体项目期间发生了一次或多次暂停，则值为 true。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>(s:event:<br/>type=pause)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>受暂停影响的流</li> <li> **上下文数据：**<br/>(a.media.pause)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.pause)</li> </ul> |

### 暂停事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>2</li> <li> **描述：**<br/>此量度计算为在播放会话期间发生暂停时段的次数。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>(s:event:<br/>type=pause)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>暂停事件</li> <li> **上下文数据：**<br/>(a.media.pauseCount)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.pauseCount)</li> </ul> |

### 暂停总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>数值</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>190</li> <li> **描述：**<br/>计算所有“暂停”类型事件的时长总和（以秒为单位）。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>暂停总持续时间</li> <li> **上下文数据：**<br/>(a.media.pauseTime)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.pauseTime)</li> </ul> |

### 内容继续

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/> **media.resume** </li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>每次在超过 30 分钟的缓冲、暂停或停止时段后继续播放，即计为继续一次，或者此值由播放器在 VideoInfo trackPlay 中进行设置。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>(s:event:<br/>type=resume)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>内容继续</li> <li> **上下文数据：**<br/>(a.media.resume)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.resume)</li> </ul> |

### 内容区段查看

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送条件：**<br/>媒体关闭</li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE</li> <li> **描述：**<br/>主内容的查看次数。在查看了至少一个帧时，即计为内容区段查看一次。<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。 </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用</li> <li> **心率：**<br/>不适用</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>event</li> <li> **报表名称：**<br/>内容区段查看</li> <li> **上下文数据：**<br/>(a.media.segmentView)</li> <li> **数据馈送：**<br/>不适用</li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.segmentView)</li> </ul> |

<!--
### Ad Count

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of ads started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.adCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.adCount) </li> </ul> |

### Chapter Count

| &nbsp;&nbsp;Implementation&nbsp;&nbsp; | Network&nbsp;Parameters | Reporting |
| --- | --- | --- |
| <ul> <li> **SDK Key:**<br/> N/A </li> <li> **API Key:**<br/> N/A </li> <li> **Type:**<br/> number </li> <li> **Sent with:**<br/> Media Close </li> <li> **Min. SDK Version:** Any </li> <li> **Sample value:**<br/> 2 </li> <li> **Description:**<br/> The number of chapters started during the media session.   <br/> </li></ul> | <ul> <li> **Adobe Analytics:**<br/> N/A </li> <li> **Heartbeats:**<br/> N/A </li> </ul> | <ul> <li> **Available:**<br/> Use custom processing rule </li> <li> **Reserved Variable:**<br/> N/A </li> <li> **Report Name:**<br/> Custom </li> <li> **Context Data:**<br/> (a.media.chapterCount) </li> <li> **Data Feed:**<br/> N/A </li> <li> **Audience Manager:**<br/> (c_contextdata.<br/>a.media.chapterCount) </li> </ul> |
-->

## 《加州消费者隐私法案》(CCPA) 参数 {#ccpa-params}

### 选择禁用服务器端转发

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>不适用</li> <li> **API 密钥：**<br/>analytics.optOutServerSideForwarding</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>布尔值</li> <li> **发送条件：**<br/>媒体开始</li> <li> **最低 SDK 版本：**&#x200B;不适用 </li> <li> **示例值：**<br/>true</li> <li>**描述：**<br/>如果最终用户选择禁止在 Adobe Analytics 与其他 Experience Cloud 解决方案（如 Audience Manager）之间共享其数据，则设置为 true。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(opt.dmp)</li> <li> **心率：**<br/>(s:meta:cm.ssf)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>访问时</li> <li> **报表名称：**<br/>内容</li> <li> **上下文数据：**<br/>不适用</li> <li> **数据馈送：**<br/>video</li> <li> **Audience Manager：**<br/>不适用</li> </ul> |

### 选择禁用共享

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>不适用</li> <li> **API 密钥：**<br/>analytics.optOutShare</li> <li> **必需：**<br/>否</li> <li> **类型：**<br/>布尔值</li> <li> **发送条件：**<br/>媒体开始</li> <li> **最低 SDK 版本：**&#x200B;不适用 </li> <li> **示例值：**<br/>true</li> <li>**描述：**<br/>如果最终用户选择禁止联合其数据（例如，将其数据联合到其他 Adobe Analytics 客户端），则设置为 true。</li></ul> | <ul> <li> **Adobe Analytics：**<br/>(opt.oos)</li> <li> **心率：**<br/>(s:meta:cm.oos)</li> </ul> | <ul> <li> **可用：**<br/>是</li> <li> **保留的变量：**<br/>eVar</li> <li> **过期时间：**<br/>访问时</li> <li> **报表名称：**<br/>内容</li> <li> **上下文数据：**<br/>不适用</li> <li> **数据馈送：**<br/>video</li> <li> **Audience Manager：**<br/>不适用</li> </ul> |

## 相关 API {#section_Related_APIs}

### createMediaObject API {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig API {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)
