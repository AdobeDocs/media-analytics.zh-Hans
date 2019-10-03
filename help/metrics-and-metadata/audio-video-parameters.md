---
seo-title: 音频和视频参数
title: 音频和视频参数
uuid: fdacfb8b-db3e-46fb-b9ad-c3a749555b2a
translation-type: tm+mt
source-git-commit: a3e400a135af532be4320c7510032d518c4b6865

---


# 音频和视频参数{#audio-and-video-parameters}

>[!IMPORTANT]
>
>2019年2月7日，Adobe Analytics for Video and Audio发布了一个度量名称更改。 “媒体启动”<i></i>现在将更名为“媒体开始”<i></i>。此更改旨在反映指标和报告中的行业标准，并使指标在报告中易于识别。

>[!NOTE]
>
>从2018年9月13日开始，对某些维度、指标和报告的标签进行了更改，以允许跨内容跟踪视频和音频分析。 更改的标签包括：****“视频启动”已更改为“媒体启动”，****“视频长度”已更改为“内容时长”，****“视频名称”已更改为“内容名称”。而且，Reports &amp; Analytics 中的视频报表所使用的名称已全部从“视频”更新为“媒体”。这些标签更改并没有导致数据收集或历史数据发生变化。请记住这些更改，您有可能会在 Report Builder 或任何其他可能会受这些更改影响的外部自动化数据提取工具中使用这些标签。

本主题介绍 Adobe 通过解决方案变量收集的一系列音频和视频内容数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或通过 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示该项是否为进行基本音频和视频跟踪所必需的参数。
   * *类型* - 指定要设置的变量类型：字符串或数值。
   * *发送方* -指示数据何时发送：媒 *体开始* (Media Start)是媒体开始时发送的分析调用， *广告开始(Ad Start* )是广告开始时发送的分析调用，等等；关闭 *调用* ，是指在媒体会话结束时或广告结束时从心跳服务器直接发送到分析服务器的编译分析调用、章节等。 关闭调用在网络数据包调用中不可用。
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
>Do not change the classification names for any variables listed below that are described under Reporting/Reserved Variable as "classification".\
>The media classifications are defined when a report suite is enabled for media tracking. From time to time, Adobe adds new properties, and, when this occurs, customers must re-enable their report suites to get access to the new media properties. During the update process Adobe determines whether the classifications are enabled by checking the names of the variables. 如果其中任何一个缺失，Adobe会再次添加缺失的。

## 音频和视频核心数据 {#section_y55_y1m_n1b}

### 流类型 {#stream-type}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.streamType </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小** SDK版本：2.2在 <br/><br/>Media Collection API概 [述或下载SDK](/help/media-collection-api/mc-api-overview.md) —— 版 [本2.2中提供](/help/sdk-implement/download-sdks.md)。  </li>  <li> **示例值：**<br/>"video" </li> <li> ****<br/> 说明：标识流类型。 有效值为“audio”、“video”和“all”。<br/><br/>[报告细分](/help/metrics-and-metadata/segments.md):媒 <br/><br/>体流类型：全部——对 <br/>所有媒体流数据进行细分；规则：内容(ID)存在媒 <br/><br/>体流类型：音频——对 <br/>所有音频流数据进行分段；规则：内容(ID)存在，媒体流类型=音频媒 <br/><br/>体流类型：“视频”-对所 <br/>有视频流数据进行细分；规则：内容(ID)存在且媒体流类型！= audio <br/><br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.streamType) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.streamType) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>内容 </li> <li> ****<br/> 上下文数据：(a.media.streamType) </li> <li> **数据馈送：**<br/>videostreamtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.streamType) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/> [mediaId](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.id </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"4586695ABC" </li> <li>****<br/> 说明：内容的内容ID，可用于绑定回其他行业/CMS ID，等于 `s:asset:video_id.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> ****<br/> 心跳：(s:asset:video_id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>内容 </li> <li> ****<br/> 上下文数据：(a.media.name) </li> <li> **数据馈送：**<br/>video </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.name) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.length </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **Sample value:**<br/> VOD: 128; Live: 86400; Linear: 1800. </li><li> **Description:**<br/> Clip Length/Runtime - This is the maximum length (or duration) of the content being consumed (in seconds). It equals the last value of `l:asset:length` from events of type Main. <br/>If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. <br/>In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **重要信息：**&#x200B;此属性用于计算多个量度，例如进度跟踪量度和平均观看分钟数。如果未设置此值，或设置的值不大于零，那么这些量度将不可用。对于时长未知的实时媒体，此值默认为 86400。<br/>Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.` <br/> **发行日期：2018 年 9 月 13 日** </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> 心跳：(l:asset:length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容时长（变量） </li> <li> ****<br/> Context Data: (a.media.length) </li> <li> **数据馈送：**<br/>videolength </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>  [length](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.length </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **Sample value:**<br/> VOD: 128; Live: 86400; Linear: 1800. </li> <li> ****<br/> 说明：剪辑长度／运行时——这是所消耗内容的最大长度（或持续时间）（以秒为单位）。 It equals the last value of `l:asset:length` from events of type Main. If `l:asset:length` is not set, then the last value of `l:asset:duration` is used. In reporting, Video Length is the classification, and Content Length (variable) is the eVAR.  <br/> **重要信息：**&#x200B;此属性用于计算多个量度，例如进度跟踪量度和平均观看分钟数。如果未设置此值，或设置的值不大于零，那么这些量度将不可用。对于时长未知的实时媒体，此值默认为 86400。Pre Version 1.5.1, this was `l:asset:duration`; after 1.5.1, this is `l:asset:length.`<br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.length) </li> <li> ****<br/> 心跳：(l:asset:length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>视频长度 </li> <li> ****<br/> 上下文数据：(a.media.length) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.length) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>  [streamType](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.contentType </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>有限制的字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"vod" </li> <li> ****<br/> 说明：每流类型的 **可用值**: <br/> __ 音频：“song”、“podcast”、“audiobook”、“radio” <br/> __ 视频：“VoD”、“Live”、“Linear”、“UGC”、“DVoD”客户可 <br/> 以为此参数提供自定义值。 这等于 `s:stream:type.` 如果取消设置，则等于 `missing_content_type.` </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.contentType) </li> <li> ****<br/> 心跳：(s:stream:type) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容类型 </li> <li> ****<br/> 上下文数据：(a.contentType) </li> <li> **数据馈送：**<br/>videocontenttype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.contentType) </li> </ul> |

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
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>从后端获取 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.8 </li> <li> **示例值：**<br/>1482236761294786918253 </li> <li> ****<br/> 说明：这标识独特于单个播放的内容流的实例。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.vsid) </li> <li> **Heartbeat:**<br/> (s:event:sid) </li> </ul> | <ul> <li> **可用：**<br/>使用处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> ****<br/> Context Data: (a.media.vsid) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.vsid) </li> </ul> |

### 媒体下载标志

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>从后端获取 </li> <li> **必需：**<br/>否 </li> <li> ****<br/> 类型：布尔值 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 2.2 </li> <li> ****<br/> Sample value:true </li> <li> ****<br/> 说明：当由于播放下载的内容媒体会话而生成点击时，设置为true。 在不播放下载的内容时不存在。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.downloaded) </li> <li> ****<br/> 心跳：(s:meta:a.media.downloaded) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> ****<br/> 上下文数据：(a.media.downloaded) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.downloaded) </li> </ul> |

### 内容播放器名称

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [playerName](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.playerName </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> Sample value: "Brightcove" </li> <li> ****<br/> Description: Name of the player.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>playerName) </li> <li> **Heartbeats:**<br/> (s:sp:player_name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容播放器名称 </li> <li> ****<br/> 上下文数据：(a.media.playerName) </li> <li> **数据馈送：**<br/>videoplayername </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.playerName) </li> </ul> |

### 内容渠道

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [channel](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.channel </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"Sports" </li> <li> ****<br/> 说明：分发站／频道或内容的播放位置。 此处可接受任何字符串值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.channel) </li> <li> ****<br/> 心跳：(s:sp:channel) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容渠道 </li> <li> ****<br/> 上下文数据：(a.media.channel) </li> <li> **数据馈送：**<br/>videochannel </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.channel) </li> </ul> |

### 内容区段

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：“0-10” </li> <li> ****<br/> 说明：描述已查看内容部分的时间间隔（以分钟为单位）。 区段在播放会话期间计算为播放头的最小值和最大值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容区段 </li> <li> ****<br/> 上下文数据：(a.media.segment) </li> <li> **数据馈送：**<br/>videosegment </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.segment) </li> </ul> |

### 内容名称（变量）

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./audio-video-parameters.md#create-media-object) </li> <li> **API 密钥：**<br/>media.name </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>"The Big Bang Theory" </li> <li> **Description:This is the "friendly" (human-readable) name of the content, equal to the last value of In reporting, Video Name is the classification, and Content Name (variable) is the eVAR.**<br/>`s:asset:name.`<br/><br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> Heartbeats: (s:asset:name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>内容名称（变量） </li> <li> ****<br/> 上下文数据：(a.media.friendlyName) </li> <li> **数据馈送：**<br/>videoname </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

```
public static MediaObject createMediaObject(java.lang.String name,
                                            java.lang.String mediaId, // <==
                                            java.lang.Double length,
                                            java.lang.String streamType, 
                                            MediaHeartbeat.MediaType mediaType)
```

### 视频名称

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.name </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>"The Big Bang Theory" </li> <li> ****<br/> Description: This is the "friendly" (human-readable) name of the content, equal to the last value of  In reporting, Video Name is the classification, and Content Name (variable) is the eVAR.  `s:asset:name.`<br/><br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>friendlyName) </li> <li> ****<br/> 心跳：(s:asset:name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>视频名称 </li> <li> **Context Data:**<br/> (a.media.friendlyName) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.friendlyName) </li> </ul> |

### 视频路径

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"4586695ABC" </li> <li> ****<br/> 说明：提供跟踪查看器在站点和／或应用程序中的路径的功能，以查看他们查看特定视频所采用的路径。 任何整数和/或字母组合  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.name) </li> <li> **Heartbeats:**<br/> (s:asset:video_id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>prop </li> <li> **报表名称：**<br/>视频路径 </li> <li> ****<br/> Context Data: (a.media.name) </li> <li> **数据馈送：**<br/>videopath </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.name) </li> </ul> |

### SDK 版本

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [appVersion](./audio-video-parameters.md#config-media-object) </li> <li> **API 密钥：**<br/>media.sdkVersion </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"2.62.0_release" </li> <li> ****<br/> 说明：播放器使用的SDK版本。 此参数可使用您的播放器支持的任何自定义值。<br/><br/>客户必须自行创建处理规则才能在报表中使用此值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.<br/>sdk版本) </li> <li> ****<br/> 心跳：(s:sp:sdk) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/> </li> <li> ****<br/> 上下文数据：(a.media.sdkVersion) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.sdkVersion) </li> </ul> |

### VHL 版本

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"js-2.0.1.88-c8c0b1" </li> <li> ****<br/> 说明：用于跟踪会话的Media SDK版本。 <br/><br/>客户必须自行创建处理规则才能在报表中使用此值。<br/><br/>[MediaHeartbeat.version();](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html) </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.<br/>vhl版) </li> <li> ****<br/> 心跳：(s:sp:hb_version) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> ****<br/> 上下文数据：(a.media.vhlVersion) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.vhlVersion) </li> </ul> |

## 标准音频和视频元数据 {#section_pfc_hbm_n1b}

### 节目

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SHOW </li> <li> **API 密钥：**<br/>media.show </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值："现代家庭""黑名单"""新女孩" </li> <li> ****<br/> 说明：仅当节目是系 <br/>列的一部分时，才需要节目／系列名称。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.show) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.show) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>节目 </li> <li> ****<br/> 上下文数据：(a.media.show) </li> <li> **数据馈送：**<br/>videoshow </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.show) </li> </ul> |

### 流格式

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>STREAM_FORMAT </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"Live" </li> <li> **Description:**<br/> Format of the stream (Live, VOD, Linear).  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.format) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.format) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> **Context Data:**<br/> (a.media.format) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.format) </li> </ul> |

### 季

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SEASON </li> <li> **API 密钥：**<br/>media.season </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"2" </li> <li> **Description:**<br/> The season number the show belongs to.  Season Series is required only if the show is part of a series.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.season) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.season) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>季 </li> <li> ****<br/> 上下文数据：(a.media.season) </li> <li> **数据馈送：**<br/>videoseason </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.season) </li> </ul> |

### 剧集

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>EPISODE </li> <li> **API 密钥：**<br/>media.episode </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"13" </li> <li> ****<br/> 说明：剧集的编号。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.ipesore) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.ipesode) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>集 </li> <li> ****<br/> 上下文数据：(a.media.ipesore) </li> <li> **数据馈送：**<br/>videoepisode </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.episode) </li> </ul> |

### 资产 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ASSET_ID </li> <li> **API 密钥：**<br/>media.assetId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>"89745363" </li> <li> ****<br/> 说明：这是媒体资产内容的唯一标识符，如电视系列剧集标识符、电影资产标识符或实时事件标识符。 通常而言，这些 ID 来自元数据管理机构，例如 EIDR、TMS/Gracenote 或 Rovi。这些标识符也可能来自其他专有或内部系统。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.asset) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.asset) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>资产 ID </li> <li> ****<br/> 上下文数据：(a.media.asset) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.asset) </li> </ul> |

### 流派

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>GENRE </li> <li> **API 密钥：**<br/>media.genre </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：《戏剧》、《喜剧》 </li> <li> ****<br/> 说明：内容制作者定义的内容类型或分组。 在变量实施中，应该用逗号分隔这些值。在报表中，列表 eVar 会将每个值拆分为行项目，每个行项目会收到均等的量度权重。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.genre) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.genre) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>列表 eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>流派 </li> <li> ****<br/> 上下文数据：(a.media.genre) </li> <li> **数据馈送：**<br/>videogenre </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.genre) </li> </ul> |

### 首次播放日期

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FIRST_AIR_DATE </li> <li> **API 密钥：**<br/>media.firstAirDate </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **Sample value:**<br/> "2016-01-25" </li> <li> **Description:**<br/> The date when the content first aired on television. 可接受任何日期格式，但 Adobe 建议使用如下格式：YYYY-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.airDate) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.airDate) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>首次播放日期 </li> <li> **Context Data:**<br/> (a.media.airDate) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.airDate) </li> </ul> |

### 首次数字化日期

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FIRST_DIGITAL_DATE </li> <li> **API 密钥：**<br/>media.firstDigitalDate </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：《2016-01-25》 </li> <li> ****<br/> 说明：在任何数字渠道或平台上首次播放内容的日期。 可接受任何日期格式，但 Adobe 建议使用如下格式：YYYY-MM-DD </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.digitalDate) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.digitalDate)<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>首次数字化日期 </li> <li> ****<br/> 上下文数据：(a.media.digitalDate) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.digitalDate) </li> </ul> |

### 内容评级

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>RATING </li> <li> **API 密钥：**<br/>media.rating </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：电视，TVG,TVPG,TVMA </li> <li> ****<br/> 说明：电视家长指导准则所定义的评级。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.rating) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.rating)<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>内容评级 </li> <li> ****<br/> 上下文数据：(a.media.rating) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.rating) </li> </ul> |

### 创作者

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ORIGINATOR </li> <li> **API 密钥：**<br/>media.originator </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：《华纳兄弟》、《索尼》、《迪士尼》 </li> <li> ****<br/> 说明：内容的创建者。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.originator) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.originator)<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>创作者 </li> <li> ****<br/> 上下文数据：(a.media.originator) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.originator) </li> </ul> |

### 网络

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>NETWORK </li> <li> **API 密钥：**<br/>media.network </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：“福克斯”、“布拉沃”、“ESPN” </li> <li> ****<br/> Description: The network/channel name.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.network) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.network)<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>网络 </li> <li> ****<br/> 上下文数据：(a.media.network) </li> <li> **数据馈送：**<br/>videonetwork </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.network) </li> </ul> |

### 节目类型

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SHOW_TYPE </li> <li> **API 密钥：**<br/>media.showType </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：“0”=整集；"1" =预览／预告片；"2" =剪辑；"3" =其他。 </li> <li> ****<br/> 说明：内容类型，表示为0到3之间的整数。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.type) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.type) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>显示类型 </li> <li> ****<br/> 上下文数据：(a.media.type) </li> <li> **数据馈送：**<br/>videoshowtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.type) </li> </ul> |

### MVPD

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>MVPD </li> <li> **API 密钥：**<br/>media.pass.mvpd </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **Sample value:**<br/> "Comcast", "DirecTV", "Dish" </li> <li> **Description:**<br/> MVPD provided via Adobe authentication.  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.mvpd) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.pass.<br/>mvpd) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>MVPD </li> <li> **Context Data:**<br/> (a.media.pass.mvpd) </li> <li> **数据馈送：**<br/>videomvpd </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pass.mvpd) </li> </ul> |

### 已授权

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>AUTHORIZED </li> <li> **API 密钥：**<br/>media.pass.auth </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：“真” </li> <li> ****<br/> 说明：用户已通过Adobe身份验证获得授权。  <br/>**重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.pass.auth) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.pass.<br/>身份验证) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>已授权 </li> <li> ****<br/> 上下文数据：(a.media.pass.auth) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pass.auth) </li> </ul> |

### 播出时段

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>DAY_PART </li> <li> **API 密钥：**<br/>media.dayPart </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li> <li> ****<br/> 说明：一个属性，它定义广播或播放内容的一天的时间。 客户可以视需要为此属性设置任何值。  </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.dayPart) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.dayPart) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>播出时段 </li> <li> ****<br/> 上下文数据：(a.media.dayPart) </li> <li> **数据馈送：**<br/>videodaypart </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.dayPart) </li> </ul> |

### 媒体馈送类型

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>FEED </li> <li> **API 密钥：**<br/>media.feed </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> ****<br/> 示例值：“East-HD”、“West-HD”、“East-SD” </li> <li> ****<br/> 说明：源的类型。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.feed) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.feed) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>媒体馈送类型 </li> <li> ****<br/> 上下文数据：(a.media.feed) </li> <li> **数据馈送：**<br/>videofeedtype </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.feed) </li> </ul> |

### 艺人

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.artist </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小** SDK版本：1.5.7在 <br/>Media Collection概述 [或下载SDK](/help/media-collection-api/mc-api-overview.md) —— 版 [本2.2中提供](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>"The Beatles" </li> <li> ****<br/> 说明：艺术家的姓名。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.artist) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.artist) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> ****<br/> 上下文数据：(a.media.artist) </li> <li> **数据馈送：**<br/>videoaudioartist </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.artist) </li> </ul> |

### 专辑

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.album </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小** SDK版本：1.5.7在 <br/>Media Collection概述 [或下载SDK](/help/media-collection-api/mc-api-overview.md) —— 版 [本2.2中提供](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>"Revolver" </li> <li> ****<br/> 说明：相册的名称。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.album) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.album) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> ****<br/> Context Data: (a.media.album) </li> <li> **数据馈送：**<br/>videoaudioalbum </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.album) </li> </ul> |

### 标签

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.label </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **示例值：**<br/>"Revolver" </li> <li> **Description:**<br/> Name of the record label.  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.label) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.label) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> ****<br/> Context Data: (a.media.label) </li> <li> **数据馈送：**<br/>videoaudiolabel </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.label) </li> </ul> |

### 作者

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.author </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **示例值：**<br/>"John Kennedy Toole" </li> <li> ****<br/> 说明：作者的姓名（音像书）。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.author) </li> <li> ****<br/> Heartbeats: (s:meta:a.media.author)<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> ****<br/> 上下文数据：(a.media.author) </li> <li> **数据馈送：**<br/>videoaudioauthor </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.author) </li> </ul> |

### 电台/电视台

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.station </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小** SDK Version: 1.5.7 Available in Media Collection Overview or Download SDKs - Versions 2.2.<br/>[](/help/media-collection-api/mc-api-overview.md)[](/help/sdk-implement/download-sdks.md)  </li> <li> **示例值：**<br/>"NPR" </li> <li> ****<br/> 说明：无线电台的名称/ ID。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.station) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.station) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> ****<br/> 上下文数据：(a.media.station) </li> <li> **数据馈送：**<br/>videoaudiostation </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.station) </li> </ul> |

### 发布者

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.publisher </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Start, Media Close </li> <li> **最小** SDK版本：1.5.7在 <br/>Media Collection概述 [或下载SDK](/help/media-collection-api/mc-api-overview.md) —— 版 [本2.2中提供](/help/sdk-implement/download-sdks.md)。  </li> <li> **示例值：**<br/>"Random Bauhaus" </li> <li> ****<br/> 说明：音频内容发布者的名称。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.publisher) </li> <li> ****<br/> 心跳：(s:meta:<br/>a.media.publisher) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> </li> <li> ****<br/> 上下文数据：(a.media.publisher) </li> <li> **数据馈送：**<br/>videoaudiopublisher </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.publisher) </li> </ul> |

## 音频和视频量度 {#section_3D5F9C555274428AA6030D07596177E9}

### 媒体开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置</li> <li> **API 密钥：**<br/>不适用</li> <li> **类型：**<br/>字符串</li> <li> ****<br/> 发送方：媒体开始</li> <li> **最小 SDK 版本：**&#x200B;任何版本</li> <li> **示例值：**<br/>TRUE </li> <li> ****<br/> 说明：媒体的加载事件。 （当查看者单击&#x200B;_播放_&#x200B;按钮时，会发生此事件。）即使存在前置广告、缓冲和错误等，也会将此计为视频载入事件。<br/>**重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。If it is not set, no value is returned.  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.view) </li> <li> ****<br/> 心跳：(s:event:<br/>type=start) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **Report Name:**<br/> Media Starts </li> <li> **Context Data:**<br/> (a.media.view) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.view) </li> </ul> |

### 内容开始

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **Description:**<br/> First frame of media is consumed. If the user drops during ad, buffering, etc., then there would be no "Content Start" event.  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容开始 </li> <li> ****<br/> 上下文数据：(a.media.play) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.play) </li> </ul> |

### 内容结束 {#content-complete}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> ****<br/> 说明：已观看完成的流。 这不一定意味着用户观看或聆听整个流；他们本可以跳到前面去。 这只表示用户到达流的末尾，100%。 <br/>另请参阅 [会话结束](quality-parameters.md#session-end)<br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> ****<br/> 心跳：(s:event:<br/>type=complete) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容结束 </li> <li> ****<br/> 上下文数据：(a.media.complete) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.complete) </li> </ul> |

### 内容逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>105 </li> <li> ****<br/> 说明：对主内容上PLAY类型的所有事件求和事件持续时间（以秒为单位）。  在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容逗留时间 </li> <li> ****<br/> 上下文数据：(a.media.timePlayed) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.timePlayed) </li> </ul> |

### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>120 </li> <li> **Description:**<br/> Sums the event duration (in seconds) for all events of type PLAY, both main and ad content.  在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>媒体逗留时间 </li> <li> **Context Data:**<br/> (a.media.totalTimePlayed) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.totalTimePlayed) </li> </ul> |

### 不重复播放时间

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>94 </li> <li> **Description:**<br/> The value in seconds of the unique segments of content played during a session. 不包含向回搜寻观看的情况（查看者多次观看同一内容区段）所播放的时间。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>自定义 </li> <li> **Context Data:**<br/> (a.media.uniqueTimePlayed) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.uniqueTimePlayed) </li> </ul> |

### 10%进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> ****<br/> 说明：播放头根据长度传递10%的内容标记。 即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>10% 进度标记 </li> <li> ****<br/> 上下文数据：(a.media.progress10) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress10) </li> </ul> |

### 25%进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> ****<br/> 说明：播放头根据内容长度传递25%的内容标记。 即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>25% 进度标记 </li> <li> ****<br/> 上下文数据：(a.media.progress25) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress25) </li> </ul> |

### 50%进度标记

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> ****<br/> 说明：播放头根据内容长度传递50%的内容标记。 即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>50% 进度标记 </li> <li> ****<br/> 上下文数据：(a.media.progress50) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress50) </li> </ul> |

### 75%进度标记

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> **不适用** </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **Description:**<br/> Playhead passes the 75% marker of content based on content length. 即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>75% 进度标记 </li> <li> **Context Data:**<br/> (a.media.progress75) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.progress75) </li> </ul> |

### 95%进度标记

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> ****<br/> 说明：播放头根据内容长度传递95%的内容标记。 即使向回搜寻，也会仅计算一次该标记。如果向前搜寻，不会将跳过的标记计算在内。  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>95% 进度标记 </li> <li> ****<br/> 上下文数据：(a.media.progress95) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.progress95) </li> </ul> |

### 平均观看分钟数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>大于或等于 1 </li> <li> ****<br/> 说明：“平均分钟受众”量度计算为特定媒体项的“总内容花费时间”除以其所有播放会话的长度： <br/><br/> `average_minute_audience = timeSpent / videoLength;` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>平均观看分钟数 </li> <li> ****<br/> 上下文数据：(a.media.averageMinuteAudience) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.averageMinuteAudience) </li> </ul> |

### 联合数据

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> ****<br/> 类型：布尔值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：true  </li> <li> ****<br/> 说明：当点击为联合时，设置为true（即，客户作为联合数据共享的一部分而接收，而不是他们自己的实施）。 </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>不适用 </li> <li> ****<br/> 上下文数据：(a.media.federated) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.federated) </li> </ul> |

### 预计的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：1 —— 播放19分钟； <br/>2 —— 播放31分钟； <br/>3 —— 播放78分钟。 </li> <li> ****<br/> 说明：每个单独内容的估计视频或音频流数。 播放时间（内容 + 广告）每增加 30 分钟，该值也会相应增加。客户必须自行创建处理规则才能在报表中使用此值。<br/><br/>A stream is counted every 30 minutes, based on the `ms_s` (or totalTimePlayed = Video Total Time), similar to: <br/> `estimatedStreams = ` <br/>   `FLOOR(ms_s/1800) + 1` </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> **Context Data:**<br/> (a.media.estimatedStreams) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.estimatedStreams) </li> </ul> |

### 受暂停影响的流

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>TRUE </li> <li> **Description:**<br/> This value is either true or false. It is true if one or more pauses occurred during playback of a single media item.  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **Heartbeats:**<br/> (s:event:<br/>type=pause) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受暂停影响的流 </li> <li> **Context Data:**<br/> (a.media.pause) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.pause) </li> </ul> |

### 暂停事件

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>2 </li> <li> **Description:**<br/> This metric is computed as a count of pause periods that occurred during a playback session.  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> ****<br/> 心跳：(s:event:<br/>type=pause) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>暂停事件 </li> <li> ****<br/> 上下文数据：(a.media.pauseCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseCount) </li> </ul> |

### 暂停总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>190 </li> <li> ****<br/> 说明：对PAUSE类型的所有事件的持续时间（以秒为单位）进行总和。 在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。 <br/> **发行日期：2018 年 9 月 13 日** </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>暂停总持续时间 </li> <li> ****<br/> 上下文数据：(a.media.pauseTime) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.pauseTime) </li> </ul> |

### 内容继续

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> **media.resume** </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 1.5.6 </li> <li> **示例值：**<br/>TRUE </li> <li> ****<br/> 说明：对于在超过30分钟的缓冲、暂停或停止时间后恢复的每个播放，将计为“继续”；如果该值由VideoInfo trackPlay上的播放器设置。 <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。  </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> ****<br/> 心跳：(s:event:<br/>type=resume) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容继续 </li> <li> ****<br/> 上下文数据：(a.media.resume) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.resume) </li> </ul> |

### 内容区段查看

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Media Close </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li> <li> **Description:**<br/> The number of views of the main content. A Content Segment View is counted when there is at least one frame viewed.  <br/> **重要信息：**&#x200B;如果设置此参数，只能将其设置为 true。如果不设置此参数，则不会返回任何值。 </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>内容区段查看 </li> <li> **Context Data:**<br/> (a.media.segmentView) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.segmentView) </li> </ul> |

### 广告计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK密钥：N/A </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>2 </li> <li> ****<br/> 说明：在媒体会话期间开始的广告数。   <br/> </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> ****<br/> 上下文数据：(a.media.adCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.adCount) </li> </ul> |

### 章节计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK密钥：N/A </li> <li> **API 密钥：**<br/>不适用 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>2 </li> <li> ****<br/> 说明：媒体会话期间开始的章节数。   <br/> </li></ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心率：**<br/>不适用 </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>自定义 </li> <li> ****<br/> Context Data: (a.media.chapterCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapterCount) </li> </ul> |

## 加利福尼亚消费者隐私法(CCPA)参数 {#ccpa-params}

### 退出服务器端转发

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK密钥：N/A </li> <li> ****<br/> API密钥：analytics.optOutServerSideForwarding </li> <li> **必需：**<br/>否 </li> <li> ****<br/> 类型：布尔值 </li> <li> ****<br/> Sent with: Media Start </li> <li> **最小** SDK Version: N/A </li> <li> ****<br/> 示例值：true </li> <li>****<br/> Description: Set to true when the end user has opted out of their data being shared between Adobe Analytics and other Experience Cloud solutions (e.g. Audience Manager). </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.dmp) </li> <li> ****<br/> 心跳：(s:meta:cm.ssf) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>内容 </li> <li> ****<br/> Context Data: N/A </li> <li> **数据馈送：**<br/>video </li> <li> ****<br/> Audience Manager:N/A </li> </ul> |

### 选择退出共享

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> ****<br/> SDK密钥：N/A </li> <li> ****<br/>  API密钥：analytics.optOutShare </li> <li> **必需：**<br/>否 </li> <li> ****<br/> 类型：布尔值 </li> <li> ****<br/> 发送方：媒体开始 </li> <li> **最小** SDK版本：N/A </li> <li> ****<br/> 示例值：true </li> <li>****<br/> 说明：当最终用户选择退出其联合数据时（例如到其他Adobe Analytics客户端），设置为true。 </li></ul> | <ul> <li> ****<br/> Adobe Analytics:(opt.oos) </li> <li> ****<br/> 心跳：(s:meta:cm.oos) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>内容 </li> <li> ****<br/> 上下文数据：N/A </li> <li> **数据馈送：**<br/>video </li> <li> ****<br/> Audience Manager:N/A </li> </ul> |

## 相关API {#section_Related_APIs}

### createMediaObject APIs {#create-media-object}

* Android - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createMediaObject-java.lang.String-java.lang.String-java.lang.Double-java.lang.String-com.adobe.primetime.va.simple.MediaHeartbeat.MediaType-)
* iOS - [createMediaObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createMediaObjectWithName:mediaId:length:streamType:mediaType:)
* JavaScript - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createMediaObject)
* Chromecast - [createMediaObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createMediaObject)

### MediaHeartbeatConfig APIs {#config-media-object}

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html)

