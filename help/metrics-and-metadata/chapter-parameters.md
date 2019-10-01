---
seo-title: 章节参数
title: 章节参数
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 4a14e2faae6401a3f885eb5e341c1344d7f1e94d

---


# 章节参数{#chapter-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列章节和/或区段数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或通过 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示该项是否为进行基本视频跟踪所必需的参数。
   * *类型* - 指定要设置的变量类型：字符串或数值。
   * *Sent With - Indicates when the data is sent: Media Start is the analytics call sent on media start, Ad Start is the analytics call sent on ad start, and so on; the Close calls are the compiled analytics calls sent directly from the heartbeat server to the analytics server at the end of the media session, or the end of the ad, chapter, etc.******* The close calls are not available in network packet calls.
   * *最小 SDK 版本* - 指示访问参数时所需的 SDK 版本。
   * *示例值* - 提供变量的常用值示例。
* **网络参数：**&#x200B;显示传递到 Adobe Analytics 或心率服务器的值。此列显示的是在由 Adobe Media SDK 生成的网络调用中看到的参数的名称。
* **报表：**&#x200B;关于如何查看和分析视频数据的信息。
   * *提供* - 指示是默认在报告中提供该数据（“是”**），还是需要自定义设置（“自定义”**）
   * *保留的变量* - 指示是否将数据作为保留变量中的事件、eVar、属性或分类进行捕获。
   * *报表名称* - Adobe Analytics 变量报表的名称
   * *上下文数据* - 传递到报表服务器并在处理规则中使用的 Adobe Analytics 上下文数据的名称。
   * *数据馈送* - Clickstream 或 Live Stream 数据馈送中存在的变量的列名称
   * *Audience Manager* - Adobe Audience Manager 中存在的特征名称

>[!IMPORTANT]
>
>Do not change the classification names for any variables listed below that are described under Reporting/Reserved Variable as "classification".\
>The media classifications are defined when a report suite is enabled for media tracking. From time to time, Adobe adds new properties, and, when this occurs, customers must re-enable their report suites to get access to the new media properties. During the update process Adobe determines whether the classifications are enabled by checking the names of the variables. If any of them is missing, Adobe adds the missing ones again.

## 章节元数据 {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### 章节名称

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.friendlyName </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> Sent with: Chapter Start, Chapter Close </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **Sample Value:**<br/> "The Big Bang Chapter 2 - Dating" </li><li> **Description:**<br/>The name of the chapter and/or segment.   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics: (a.media.chapter.<br/>friendlyName) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_name) </li> </ul> | <ul> <li> **可用：**<br/>默认创建...  </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节名称 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>friendlyName) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>friendlyName) </li> </ul> |

### 章节位置

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.index </li> <li> ****<br/> Required: SDK: No; API: Yes. </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> 示例值：2 </li><li> **说明：**<br/>章节在内容中的位置（索引、整数）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>position) </li> <li> ****<br/> 心跳：(l:stream:chapter_pos) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节位置 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>position) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>position) </li> </ul> |

### 章节偏移

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.offset </li> <li> ****<br/> 必需：SDK:不；API:是的。 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> Sent with: Chapter Close </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> Sample Value: 58 </li><li> **说明：**<br/>章节在内容中从开始时的偏移量（以秒为单位）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>偏移) </li> <li> ****<br/> 心跳：(l:stream:chapter_offset) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节偏移 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>偏移) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>偏移) </li> </ul> |

### 章节长度

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.chapter.length </li> <li> ****<br/> 必需：SDK:不；API:是的。 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> 示例值：486 </li><li> **说明：**<br/>章节的长度（以秒为单位）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>length) </li> <li> ****<br/> 心跳：(l:stream:chapter_length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节长度 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>length) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>length) </li> </ul> |

### 章节

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> </li><li> **Description:The auto-generated ID of the chapter.**<br/>   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>name) </li> <li> **Heartbeat:**<br/> (s:stream:chapter_id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>章节 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>name) </li> <li> **数据馈送：**<br/>videochapter </li> <li> ****<br/> Audience Manager: (c_contextdata.<br/>a.media.chapter。<br/>name) </li> </ul> |

## 章节量度 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### 章节开始

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>章节开始 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **Sample Value:**<br/> TRUE </li><li> **Description:**<br/>The number of chapter starts.  **重要信息：**&#x200B;如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>view) </li> <li> **Heartbeat:**<br/> (s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> ****<br/> 报告名称：第g章开始 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>view) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>view) </li> </ul> |

### 章节结束

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3</li> <li> ****<br/> 示例值：TRUE </li><li> **说明：**<br/>章节完成的次数。  **重要信息：**&#x200B;如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>complete) </li> <li> ****<br/> 心跳：(s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> ****<br/> 报告名称：章节完成g </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>complete) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>complete) </li> </ul> |

### 平均逗留时间

|   实施   | Network Parameters | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **Sample Value:**<br/> </li><li> **说明：**<br/>在章节中停留的时间。  在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>timePlayed) </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> ****<br/> 报告名称：第二章停留时间g </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>timePlayed) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>timePlayed) </li> </ul> |

## 相关API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - createChapterObjectWithName[](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - createChapterObject[](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
