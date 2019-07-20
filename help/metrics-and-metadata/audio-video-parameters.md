---
seo-title: 音频和视频参数
title: 音频和视频参数
uuid: fdacfb8b-db3 e-46fb-b ad ad-c3 a749555 b2 a
translation-type: tm+mt
source-git-commit: 6ce1ded12ff64962edb614f436e40f05b65dff34

---


# 音频和视频参数{#audio-and-video-parameters}

>[!IMPORTANT]
>
>在2019年月日，针对视频和音频的Adobe Analytics发布了指标名称更改。“媒体启动”<i></i>现在将更名为“媒体开始”<i></i>。此更改的目的是反映指标和报告中的行业标准，并使报表在报表中易于识别。

>[!NOTE]
>
>从2018年月13日开始，对某些维度、指标和报告的标签进行了更改，以允许对视频和音频分析进行跨内容跟踪。更改的标签包括：****“视频启动”已更改为“媒体启动”，****“视频长度”已更改为“内容时长”，****“视频名称”已更改为“内容名称”。而且，Reports &amp; Analytics 中的视频报表所使用的名称已全部从“视频”更新为“媒体”。这些标签更改并没有导致数据收集或历史数据发生变化。请记住这些更改，您有可能会在 Report Builder 或任何其他可能会受这些更改影响的外部自动化数据提取工具中使用这些标签。

本主题介绍 Adobe 通过解决方案变量收集的一系列音频和视频内容数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或通过 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示该项是否为进行基本音频和视频跟踪所必需的参数。
   * *类型* - 指定要设置的变量类型：字符串或数值。
   * *随附-* 指示数据何时发送： *媒体开始* 是在媒体开始时发送的分析调用， *广告开始* 是在广告开始时发送的分析调用，依此类推； *结束* 调用是在媒体会话结束时直接从心跳服务器发送到分析服务器的编译的分析调用，或者广告、章节等结尾处的分析调用。close调用在网络包调用中不可用。
   * *最小 SDK 版本* - 指示访问参数时所需的 SDK 版本。
   * *示例值* - 提供变量的常用值示例。
* **网络参数：**&#x200B;显示传递到 Adobe Analytics 或心率服务器的值。此列显示的是在由 Adobe Media SDK 生成的网络调用中看到的参数的名称。
* **报表：**&#x200B;有关如何查看并分析音频和视频数据的信息。
   * *提供* - 指示是默认在报告中提供该数据（“是”**），还是需要自定义设置（“自定义”**）
   * *保留的变量* - 指示是否将数据作为保留变量中的事件、eVar、属性或分类进行捕获。
   * *过期时间* - 指示数据是在每次点击后过期，还是在每次访问后过期
   * *报表名称* - Adobe Analytics 变量报表的名称
   * *上下文数据* - 传递到报表服务器并在处理规则中使用的 Adobe Analytics 上下文数据的名称。
   * *数据馈送* - Clickstream 或 Live Stream 数据馈送中存在的变量的列名称
   * *Audience Manager* - Adobe Audience Manager 中存在的特征名称

>[!IMPORTANT]
>
>请勿更改以下所列变量的分类名称，如“报告/保留变量”下所述的“分类”。\
>在启用了媒体跟踪的情况下，将定义媒体分类。Adobe时常会添加新属性，当发生这种情况时，客户必须重新启用报告套件才能访问新媒体属性。在更新过程中，Adobe通过检查变量的名称来确定是否启用了分类。如果其中任何一项缺失，Adobe将再次添加缺失的组件。

## 音频和视频核心数据 {#section_y55_y1m_n1b}

### 流类型 {#stream-type}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.streamType </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK Version:** 2.2 <br/><br/>Available in [Media Collection API Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li>  <li> **示例值：**<br/>"video" </li> <li> **描述：**<br/> 标识流类型。有效值为“audio”、“video”和“all”。<br/><br/>[区段](../metrics-and-metadata/segments.md)： <br/><br/>streamType“All”-细分所有媒体流数据。 <br/> **规则：** 内容(ID)存在 <br/><br/>于streamType“音频”-区段所有音频流数据。<br/>**规则：** 内容(ID)存在并且Stream Type=音频 <br/><br/>StreamType“视频”-区段所有视频流数据。<br/>**规则：**&#x200B;存在内容 (ID)，且流类型为“video”<br/><br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. streamType) </li> <li> **心跳：**<br/> (s：meta：<br/>a media. mestreamType) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>内容 </li> <li> **上下文数据：**<br/> (a. media. streamType) </li> <li> **数据馈送：**<br/>videostreamtype </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.streamType) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.id </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"4586695ABC" </li> <li>**描述：**<br/> 内容ID(可用于绑定到其他行业/CMS ID，与上一个值相等) `s:asset:video_id` </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. name) </li> <li> **心跳：**<br/> (s：资产：video_ id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>内容 </li> <li> **上下文数据：**<br/> (a. media. name) </li> <li> **数据馈送：**<br/>video </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.name) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.length </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> VOD：128；实时：86400；线性：1800。 </li><li> **描述：**<br/> 剪辑长度/运行时-这是消耗内容的最大长度(或持续时间)(以秒为单位)。It equals the last value of `l:asset:length` from events of type Main. <br/>`l:asset:length` 如果未设置，则使用最后一个值 `l:asset:duration` 。<br/>在报告中，“视频长度”是分类，“内容长度”(变量)是eVar。 <br/> **重要信息：**&#x200B;此属性用于计算多个量度，例如进度跟踪量度和平均观看分钟数。如果未设置此值，或设置的值不大于零，那么这些量度将不可用。对于时长未知的实时媒体，此值默认为 86400。<br/>Pre version1.5.1，is `l:asset:duration`；1.5.1之后，这是 `l:asset:length.`<br/> **发行日期：2018 年 9 月 13 日** </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. length) </li> <li> **心跳：**<br/> (l：资产：length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容时长（变量） </li> <li> **上下文数据：**<br/> (a. media. length) </li> <li> **数据馈送：**<br/>videolength </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.length </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> VOD：128；实时：86400；线性：1800。 </li> <li> **描述：**<br/> 剪辑长度/运行时-这是消耗内容的最大长度(或持续时间)(以秒为单位)。它等同于“主要”类型事件中 l:asset:length 的最后一个值。如果未设置 l:asset:length，那么会使用 l:asset:duration 的最后一个值。In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **重要信息：**&#x200B;此属性用于计算多个量度，例如进度跟踪量度和平均观看分钟数。如果未设置此值，或设置的值不大于零，那么这些量度将不可用。对于时长未知的实时媒体，此值默认为 86400。Pre Version 1.5.1, this was l:asset:duration; after 1.5.1, this is l:asset:length.<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. length) </li> <li> **心跳：**<br/> (l：资产：length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>视频长度 </li> <li> **上下文数据：**<br/> (a. media. length) </li> <li> **数据馈送：**<br/>videoclassificationlength </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.contentType </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>有限制的字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"vod" </li> <li> **描述：**<br/>**每个流类型的可用值**： <br/> _音频：_ “歌曲”、“播客”、“audiobooks”、“adradio” <br/> _视频：_ “VOD”、“Live”、“Linear”、“UGC”、“DVOD” <br/> ，客户可以为此参数提供自定义值。This equals `s:stream:type.` If that is unset, this equals missing_content_type. </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. contentType) </li> <li> **心跳：**<br/> (s：stream：type) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容类型 </li> <li> **上下文数据：**<br/> (a. contentType) </li> <li> **数据馈送：**<br/>videocontenttype </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a<br/>. contentType) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>从后端获取 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.8 </li> <li> **示例值：**<br/>1482236761294786918253 </li> <li> **描述：**<br/> 它标识单个回放特有的内容流实例。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. vsid) </li> <li> **心跳：**<br/> (s：event：sid) </li> </ul> | <ul> <li> **可用：**<br/>使用处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> **上下文数据：**<br/> (a. media. vsid) </li> <li> **数据馈送：**<br/>vsid </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.vsid) </li> </ul> |

### 内容播放器名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.playerName </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> “Brightcove” </li> <li> **描述：**<br/> 播放器的名称。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>playerName) </li> <li> **心跳：**<br/> (s：sp：player_ name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容播放器名称 </li> <li> **上下文数据：**<br/> (a. media. playerName) </li> <li> **数据馈送：**<br/>videoplayername </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.playerName) </li> </ul> |

### 内容渠道

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.channel </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"Sports" </li> <li> **描述：**<br/> 分发站/渠道或播放内容的位置。此处可接受任何字符串值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. channel) </li> <li> **心跳：**<br/> (s：sp：频道) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容渠道 </li> <li> **上下文数据：**<br/> (a. media. channel) </li> <li> **数据馈送：**<br/>videochannel </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.channel) </li> </ul> |

### 内容区段

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> “0-10” </li> <li> **描述：**<br/> 描述已查看内容部分的时间间隔(以分钟为单位)。区段在播放会话期间计算为播放头的最小值和最大值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容区段 </li> <li> **上下文数据：**<br/> (a. media. segment) </li> <li> **数据馈送：**<br/>videosegment </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.segment) </li> </ul> |

### 内容名称（变量）

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.name </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>"The Big Bang Theory" </li> <li> **描述：**<br/> 在报告中，视频名称是分类，内容名称(变量)是eVar。This is the "friendly" (human-readable) name of the content, equal to the last value of `s:asset:name.` <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>friendlyName) </li> <li> **心跳：**<br/> (s：资产：name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容名称（变量） </li> <li> **上下文数据：**<br/> (a media. mestrilyName) </li> <li> **数据馈送：**<br/>videoname </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.friendlyName) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.name </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>"The Big Bang Theory" </li> <li> **描述：**<br/> 这是内容的“友好”(人类可读)名称，等于 `s:asset:name.`<br/>“在报告中的最后一个值”，“视频名称”是分类，而内容名称(变量)是eVar。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>friendlyName) </li> <li> **心跳：**<br/> (s：资产：name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>视频名称 </li> <li> **上下文数据：**<br/> (a media. mestrilyName) </li> <li> **数据馈送：**<br/>videoclassificationname </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.friendlyName) </li> </ul> |

### 视频路径

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"4586695ABC" </li> <li> **描述：**<br/> 能够跨站点和/或App跟踪查看器路径，以查看他们查看特定视频所采用的路径。任何整数和/或字母组合  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. name) </li> <li> **心跳：**<br/> (s：资产：video_ id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>prop </li> <li> **报表名称：**<br/>视频路径 </li> <li> **上下文数据：**<br/> (a. media. name) </li> <li> **数据馈送：**<br/>videopath </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.name) </li> </ul> |

### SDK 版本

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.sdkVersion </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"2.62.0_release" </li> <li> **描述：**<br/> 播放器使用的SDK版本。此参数可使用您的播放器支持的任何自定义值。<br/><br/>客户必须自行创建处理规则才能在报表中使用此值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>SDKVersion) </li> <li> **心跳：**<br/> (s：sp：sdk) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. SDKVersion) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.sdkVersion) </li> </ul> |

### VHL 版本

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"js-2.0.1.88-c8c0b1" </li> <li> **描述：**<br/> 用于跟踪会话的心跳SDK版本。<br/><br/>客户必须自行创建处理规则才能在报表中使用此值。<br/><br/>[MediaHeartbat. version()；](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media.<br/>vHlVersion) </li> <li> **心跳：**<br/> (s：sp：hb_ version) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> **上下文数据：**<br/> (a. media. vHlVersion) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.vhlVersion) </li> </ul> |

## 标准音频和视频元数据 {#section_pfc_hbm_n1b}

### 节目

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SHOW </li> <li> **API 密钥：**<br/>media.show </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “现代家庭”“黑名单”“新爱人” </li> <li> **描述：**<br/> 仅当演示是系列的一部分时，才需要计划/系列名称 <br/>计划名称。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. show) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. show) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>节目 </li> <li> **上下文数据：**<br/> (a. media. show) </li> <li> **数据馈送：**<br/>videoshow </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.show) </li> </ul> |

### 流格式

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>STREAM_FORMAT </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"Live" </li> <li> **描述：**<br/> 流的格式(实时、VOD、线性)。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. format) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. format) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> **上下文数据：**<br/> (a. media. format) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.format) </li> </ul> |

### 季

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SEASON </li> <li> **API 密钥：**<br/>media.season </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"2" </li> <li> **描述：**<br/> 节目所属的季节编号。只有当节目属于系列内容时，才需要季节系列。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. dear) </li> <li> **心跳：**<br/> (s：meta：<br/>. media. dear) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>季 </li> <li> **上下文数据：**<br/> (a. media. dear) </li> <li> **数据馈送：**<br/>videoseason </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.season) </li> </ul> |

### 剧集

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>EPISODE </li> <li> **API 密钥：**<br/>media.episode </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"13" </li> <li> **描述：**<br/> 剧集的数量。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. play) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. playsite) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>集 </li> <li> **上下文数据：**<br/> (a. media. play) </li> <li> **数据馈送：**<br/>videoepisode </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.episode) </li> </ul> |

### 资产 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ASSET_ID </li> <li> **API 密钥：**<br/>media.assetId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"89745363" </li> <li> **描述：**<br/> 这是媒体资产内容的唯一标识符，如电视系列剧集标识符、电影资源标识符或实时事件标识符。通常而言，这些 ID 来自元数据管理机构，例如 EIDR、TMS/Gracenote 或 Rovi。这些标识符也可能来自其他专有或内部系统。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. asset) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. asset) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>资产 ID </li> <li> **上下文数据：**<br/> (a. media. asset) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.asset) </li> </ul> |

### 流派

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>GENRE </li> <li> **API 密钥：**<br/>media.genre </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “戏剧”、“喜剧” </li> <li> **描述：**<br/> 内容制作者定义的内容类型或分组。在变量实施中，应该用逗号分隔这些值。在报表中，列表 eVar 会将每个值拆分为行项目，每个行项目会收到均等的量度权重。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. genre) </li> <li> **心跳：**<br/> (s：meta：<br/>a media. genre) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>列表 eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>流派 </li> <li> **上下文数据：**<br/> (a. media. genre) </li> <li> **数据馈送：**<br/>videogenre </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.genre) </li> </ul> |

### 首次播放日期

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FIRST_AIR_DATE </li> <li> **API 密钥：**<br/>media.firstAirDate </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “2016-01-25” </li> <li> **描述：**<br/> 首次在电视上播放的内容的日期。可接受任何日期格式，但 Adobe 建议使用如下格式：YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. AIRDate) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. AIRDate) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>首次播放日期 </li> <li> **上下文数据：**<br/> (a. media. AIRDate) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.airDate) </li> </ul> |

### 首次数字化日期

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FIRST_DIGITAL_DATE </li> <li> **API 密钥：**<br/>media.firstDigitalDate </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “2016-01-25” </li> <li> **描述：**<br/> 首次在任何数字渠道或平台上播放内容时的日期。可接受任何日期格式，但 Adobe 建议使用如下格式：YYYY-MM-DD </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. digitalDate) </li> <li> **心跳：**<br/> (s：meta：<br/>a media. digitalDate) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>首次数字化日期 </li> <li> **上下文数据：**<br/> (a. media. digitalDate) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.digitalDate) </li> </ul> |

### 内容评级

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>RATING </li> <li> **API 密钥：**<br/>media.rating </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> TVY、TVG、TVPG、TVMA </li> <li> **描述：**<br/> 按电视家长准则定义的等级。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. ratings) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. ratings) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>内容评级 </li> <li> **上下文数据：**<br/> (a. media. ratings) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.rating) </li> </ul> |

### 创作者

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ORIGINATOR </li> <li> **API 密钥：**<br/>media.originator </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “Warner Brothers”、“Sony”、“Disney” </li> <li> **描述：**<br/> 内容的创建者。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. oricator) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. oricator) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>创作者 </li> <li> **上下文数据：**<br/> (a. media. oricator) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.originator) </li> </ul> |

### 网络

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>NETWORK </li> <li> **API 密钥：**<br/>media.network </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “Fox”、“Bravo”、“ESPN” </li> <li> **描述：**<br/> 网络/频道名称。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. network) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. network) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>网络 </li> <li> **上下文数据：**<br/> (a. media. network) </li> <li> **数据馈送：**<br/>videonetwork </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.network) </li> </ul> |

### 节目类型

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SHOW_TYPE </li> <li> **API 密钥：**<br/>media.showType </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “0”=完整集；“1”=预览/预告片；“2”= Clip；“3”=其他。 </li> <li> **描述：**<br/> 内容类型，表示为与到3之间的整数。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. type) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. type) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>显示类型 </li> <li> **上下文数据：**<br/> (a. media. type) </li> <li> **数据馈送：**<br/>videoshowtype </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.type) </li> </ul> |

### MVPD

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>MVPD </li> <li> **API 密钥：**<br/>media.pass.mvpd </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “Comcast”、“DirectTV”、“Dh” </li> <li> **描述：**<br/> 通过Adobe身份验证提供的MVPD。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a media. pass. mvd) </li> <li> **心跳：**<br/> (s：meta：<br/>a media. pass.<br/>mvpd) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>MVPD </li> <li> **上下文数据：**<br/> (a media. pass. mvd) </li> <li> **数据馈送：**<br/>videomvpd </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.pass.mvpd) </li> </ul> |

### 已授权

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>AUTHORIZED </li> <li> **API 密钥：**<br/>media.pass.auth </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “TRUE” </li> <li> **描述：**<br/> 用户已通过AdobePass获得授权。<br/>**重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a media. pass. pass) </li> <li> **心跳：**<br/> (s：meta：<br/>a media. pass.<br/>身份验证) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>已授权 </li> <li> **上下文数据：**<br/> (a media. pass. pass) </li> <li> **数据馈送：**<br/>videoauthorized </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.pass.auth) </li> </ul> |

### 播出时段

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>DAY_PART </li> <li> **API 密钥：**<br/>media.dayPart </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li> <li> **描述：**<br/> 定义广播或播放内容之日的时间的属性。客户可以视需要为此属性设置任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a media. media. DayPart) </li> <li> **心跳：**<br/> (s：meta：<br/>a media. media. DayPart) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>播出时段 </li> <li> **上下文数据：**<br/> (a media. media. DayPart) </li> <li> **数据馈送：**<br/>videodaypart </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.dayPart) </li> </ul> |

### 媒体馈送类型

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FEED </li> <li> **API 密钥：**<br/>media.feed </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> “East-HD”、“West-HD”、“East-SD” </li> <li> **描述：**<br/> 源类型。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. feed) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. feed) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>媒体馈送类型 </li> <li> **上下文数据：**<br/> (a. media. feed) </li> <li> **数据馈送：**<br/>videofeedtype </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.feed) </li> </ul> |

### 艺人

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.artist </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **示例值：**<br/>"The Beatles" </li> <li> **描述：**<br/> 艺术家的姓名。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. artist) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. artist) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. artist) </li> <li> **数据馈送：**<br/>videoaudioartist </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.artist) </li> </ul> |

### 专辑

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.album </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **示例值：**<br/>"Revolver" </li> <li> **描述：**<br/> 相册的名称。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. album) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. album) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. album) </li> <li> **数据馈送：**<br/>videoaudioalbum </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.album) </li> </ul> |

### 标签

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.label </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **示例值：**<br/>"Revolver" </li> <li> **描述：**<br/> 记录标签的名称。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. label) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. label) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. label) </li> <li> **数据馈送：**<br/>videoaudiolabel </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.label) </li> </ul> |

### 作者

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.author </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **示例值：**<br/>"John Kennedy Toole" </li> <li> **描述：**<br/> 作者姓名(在一个相册中)。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. author) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. author) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. author) </li> <li> **数据馈送：**<br/>videoaudioauthor </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.author) </li> </ul> |

### 电台/电视台

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.station </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **示例值：**<br/>"NPR" </li> <li> **描述：**<br/> 无线电台的名称/ID。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. station) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. station) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. station) </li> <li> **数据馈送：**<br/>videoaudiostation </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.station) </li> </ul> |

### 发布者

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.publisher </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK Version:** 1.5.7 <br/>Available in [Media Collection Overview](../media-collection-api/mc-api-overview.md) or [Download SDKs - Versions 2.2](../sdk-implement/download-sdks.md).  </li> <li> **示例值：**<br/>"Random Bauhaus" </li> <li> **描述：**<br/> 音频内容publisher的名称。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. publisher sher) </li> <li> **心跳：**<br/> (s：meta：<br/>a. media. publisher sher) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. publisher sher) </li> <li> **数据馈送：**<br/>videoaudiopublisher </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.publisher) </li> </ul> |

## 音频和视频量度 {#section_3D5F9C555274428AA6030D07596177E9}

### 媒体开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> **发送随：**<br/> 媒体开始</li> <li> **最小 SDK 版本：**&#x200B;任何版本</li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 媒体的加载事件。（当查看者单击&#x200B;_播放_&#x200B;按钮时，会发生此事件。）即使存在前置广告、缓冲和错误等，也会将此计为视频载入事件。<br/>**重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。If it is not set, no value is returned.  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. view) </li> <li> **心跳：**<br/> (s：event：<br/>type= start) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报告名称：**<br/> 媒体开始 </li> <li> **上下文数据：**<br/> (a. media. view) </li> <li> **数据馈送：**<br/>videostart </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.view) </li> </ul> |

### 内容开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 将消耗第一帧媒体。If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容开始 </li> <li> **上下文数据：**<br/> (a. media. play) </li> <li> **数据馈送：**<br/>videoplay </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.play) </li> </ul> |

### 内容结束 {#content-complete}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 已观看完成的流。这并不一定意味着用户观看或监听整个流；他们可能已抢占先机。这仅表示用户到达流的末尾，100%。<br/>另请参阅 [会话结束](quality-parameters.md#session-end)<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心跳：**<br/> (s：event：<br/>type= complete) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容结束 </li> <li> **上下文数据：**<br/> (a. media. complete) </li> <li> **数据馈送：**<br/>videocomplete </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.complete) </li> </ul> |

### 内容逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>105 </li> <li> **描述：**<br/> 为主内容上类型为PLAY的所有事件求和事件持续时间(以秒为单位)。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容逗留时间 </li> <li> **上下文数据：**<br/> (a. media. TimePlayed) </li> <li> **数据馈送：**<br/>videotime </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.timePlayed) </li> </ul> |

### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>120 </li> <li> **描述：**<br/> 为“播放”类型的所有事件(主和广告内容)求和事件持续时间(以秒为单位)。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>媒体逗留时间 </li> <li> **上下文数据：**<br/> (a. media. totalTimePlayed) </li> <li> **数据馈送：**<br/>videototaltime </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.totalTimePlayed) </li> </ul> |

### 不重复播放时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>94 </li> <li> **描述：**<br/> 会话期间播放的唯一内容区段的秒值。不包含向回搜寻观看的情况（查看者多次观看同一内容区段）所播放的时间。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>自定义 </li> <li> **上下文数据：**<br/> (a. media. uniqueTimeed) </li> <li> **数据馈送：**<br/>videouniquetimeplayed </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. uniqueTimePlayed) </li> </ul> |

### 十个进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 播放头根据长度传递内容的10%标记。即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>10% 进度标记 </li> <li> **上下文数据：**<br/> (a. media. progress10) </li> <li> **数据馈送：**<br/>videoprogress10 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.progress10) </li> </ul> |

### 25%的进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 播放头根据内容长度传递25%的内容标记。即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>25% 进度标记 </li> <li> **上下文数据：**<br/> (a. media. progress25) </li> <li> **数据馈送：**<br/>videoprogress25 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.progress25) </li> </ul> |

### 50%进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 播放头根据内容长度传递50%的内容标记。即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>50% 进度标记 </li> <li> **上下文数据：**<br/> (a. media. progress50) </li> <li> **数据馈送：**<br/>videoprogress50 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.progress50) </li> </ul> |

### 75%进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> **不适用** </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 播放头根据内容长度传递75%的内容标记。即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>75% 进度标记 </li> <li> **上下文数据：**<br/> (a media. progress75) </li> <li> **数据馈送：**<br/>videoprogress75 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.progress75) </li> </ul> |

### 95%的进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 播放头根据内容长度传递95%的内容标记。即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>95% 进度标记 </li> <li> **上下文数据：**<br/> (a. media. progress95) </li> <li> **数据馈送：**<br/>videoprogress95 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.progress95) </li> </ul> |

### 平均观看分钟数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>大于或等于 1 </li> <li> **描述：**<br/> 平均分钟受众指标计算为特定媒体项目的总内容花费时间，除以其所有回放会话的长度除以其长度： <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>平均观看分钟数 </li> <li> **上下文数据：**<br/> (a. media. avaigminuteAudience) </li> <li> **数据馈送：**<br/>videoaverageminuteaudience </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.averageMinuteAudience) </li> </ul> |

### 预计的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> -播放19分钟； <br/>-播放31分钟； <br/>-播放78分钟。 </li> <li> **描述：**<br/> 每个单独内容估计的视频或音频流数。播放时间（内容 + 广告）每增加 30 分钟，该值也会相应增加。客户必须自行创建处理规则才能在报表中使用此值。<br/><br/>根据( `ms_s` 或totalTimeSted= Video总时间)，每30分钟计算一次流，类似于： <br/> `estimatedStreams = ` <br/> `&nbsp;&nbsp;FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> **上下文数据：**<br/> (a media. meessessatedStreams) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. meessessatedStreams) </li> </ul> |

### 受暂停影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 此值为true或false。It is true if one or more pauses occurred during playback of a single media item.  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心跳：**<br/> (s：event：<br/>type= pause) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受暂停影响的流 </li> <li> **上下文数据：**<br/> (a. media. pause) </li> <li> **数据馈送：**<br/>videopause </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.pause) </li> </ul> |

### 暂停事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>2 </li> <li> **描述：**<br/> 此量度计算为播放会话期间发生的暂停时段计数。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心跳：**<br/> (s：event：<br/>type= pause) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>暂停事件 </li> <li> **上下文数据：**<br/> (a. media. pauseCount) </li> <li> **数据馈送：**<br/>videopausecount </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.pauseCount) </li> </ul> |

### 暂停总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>190 </li> <li> **描述：**<br/> 汇总Pause类型的所有事件的持续时间(以秒为单位)。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>暂停总持续时间 </li> <li> **上下文数据：**<br/> (a. media. pauseTime) </li> <li> **数据馈送：**<br/>videopausetime </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.pauseTime) </li> </ul> |

### 内容继续

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> **media.resume** </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 对于在缓冲区、暂停或停顿时间超过30分钟(如果此值由VideoInfo TrackPlay上的播放器设置)之后恢复的每个播放计数计数。 <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心跳：**<br/> (s：event：<br/>type= resume) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容继续 </li> <li> **上下文数据：**<br/> (a. media. resume) </li> <li> **数据馈送：**<br/>videoresume </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.resume) </li> </ul> |

### 内容区段查看

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **描述：**<br/> 主要内容的查看次数。A Content Segment View is counted when there is at least one frame viewed.  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。 </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容区段查看 </li> <li> **上下文数据：**<br/> (a. media. SegmentView) </li> <li> **数据馈送：**<br/>videosegmentviews </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.segmentView) </li> </ul> |

## Related APIs {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

