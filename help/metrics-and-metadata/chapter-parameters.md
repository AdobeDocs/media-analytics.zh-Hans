---
seo-title: 章节参数
title: 章节参数
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# 章节参数{#chapter-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列章节和/或区段数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或通过 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示该项是否为进行基本视频跟踪所必需的参数。
   * *类型* - 指定要设置的变量类型：字符串或数值。
   * *发送方* -指示数据何时发送：媒 *体开始* (Media Start)是媒体开始时发送的分析调用， *广告开始(Ad Start* )是广告开始时发送的分析调用，等等；关闭 *调用* ，是指在媒体会话结束时或广告结束时从心跳服务器直接发送到分析服务器的编译分析调用、章节等。 关闭调用在网络数据包调用中不可用。
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
>请勿更改以下列出的任何变量的分类名称，这些变量在报告／保留变量下描述为“分类”。\
>在启用报表包进行媒体跟踪时，将定义媒体分类。 Adobe会不时添加新属性，一旦出现这种情况，客户必须重新启用其报表包才能访问新的媒体属性。 在更新过程中，Adobe通过检查变量名称来确定是否启用了分类。 如果其中任何一个缺失，Adobe会再次添加缺失的。

## 章节元数据 {#chapter-metadata}

### 章节名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.friendlyName </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：第一章开始、章结束 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> 示例值：《大爆炸2》 </li><li> **说明：**<br/>章节和／或区段的名称。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>friendlyName) </li> <li> ****<br/> 心跳：(s:stream:chapter_name) </li> </ul> | <ul> <li> **可用：**<br/>默认创建...  </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节名称 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>friendlyName) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>friendlyName) </li> </ul> |

### 章节位置

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.index </li> <li> ****<br/> 必需：SDK:不；API:是的。 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> 示例值：2 </li><li> **说明：**<br/>章节在内容中的位置（索引、整数）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>position) </li> <li> ****<br/> 心跳：(l:stream:chapter_pos) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节位置 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>position) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>position) </li> </ul> |

### 章节偏移

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.offset </li> <li> ****<br/> 必需：SDK:不；API:是的。 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> 示例值：58 </li><li> **说明：**<br/>章节在内容中从开始时的偏移量（以秒为单位）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>偏移) </li> <li> ****<br/> 心跳：(l:stream:chapter_offset) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节偏移 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>偏移) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>偏移) </li> </ul> |

### 章节长度

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.chapter.length </li> <li> ****<br/> 必需：SDK:不；API:是的。 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> 示例值：486 </li><li> **说明：**<br/>章节的长度（以秒为单位）。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>length) </li> <li> ****<br/> 心跳：(l:stream:chapter_length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节长度 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>length) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>length) </li> </ul> |

### 章节

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> </li><li> **说明：**<br/>章节的自动生成的ID。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>name) </li> <li> ****<br/> 心跳：(s:stream:chapter_id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>章节 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>name) </li> <li> **数据馈送：**<br/>videochapter </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>name) </li> </ul> |

## 章节量度 {#chapter-Metrics}

### 章节开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>章节开始 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> ****<br/> 示例值：TRUE </li><li> **说明：**<br/>开始章节的数量。  **重要信息：**&#x200B;如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>view) </li> <li> ****<br/> 心跳：(s:event:<br/>type=chapter_start) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> ****<br/> 报告名称：第g章开始 </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>view) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>view) </li> </ul> |

### 章节结束

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3</li> <li> ****<br/> 示例值：TRUE </li><li> **说明：**<br/>章节完成的次数。  **重要信息：**&#x200B;如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>complete) </li> <li> ****<br/> 心跳：(s:event:<br/>type=chapter_complete) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> ****<br/> 报告名称：章节完成g </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>complete) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>complete) </li> </ul> |

### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：章关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> </li><li> **说明：**<br/>在章节中停留的时间。  在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**   </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.chapter.<br/>timePlayed) </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> ****<br/> 报告名称：第二章停留时间g </li> <li> ****<br/> 上下文数据：(a.media.chapter.<br/>timePlayed) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.chapter。<br/>timePlayed) </li> </ul> |

## 相关API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
