---
seo-title: 章节参数
title: 章节参数
uuid: 2b9247-a694-46e9-98e1-424c08 c27 c
translation-type: tm+mt
source-git-commit: f7ffb9a88f1cf3ffefba0ae5508a857fa3de8432

---


# 章节参数{#chapter-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列章节和/或区段数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或通过 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示该项是否为进行基本视频跟踪所必需的参数。
   * *类型* - 指定要设置的变量类型：字符串或数值。
   * *随附-* 指示数据何时发送： *媒体开始* 是在媒体开始时发送的分析调用， *广告开始* 是在广告开始时发送的分析调用，依此类推； *结束* 调用是在媒体会话结束时直接从心跳服务器发送到分析服务器的编译的分析调用，或者广告、章节等结尾处的分析调用。close调用在网络包调用中不可用。
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
>请勿更改以下所列变量的分类名称，如“报告/保留变量”下所述的“分类”。\
>在启用了媒体跟踪的情况下，将定义媒体分类。Adobe时常会添加新属性，当发生这种情况时，客户必须重新启用报告套件才能访问新媒体属性。在更新过程中，Adobe通过检查变量的名称来确定是否启用了分类。如果其中任何一项缺失，Adobe将再次添加缺失的组件。

## 章节元数据 {#section_534D3A6BFEB24D1884F80AD6A50BF13C}

### 章节名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.friendlyName </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 章节开始，章节关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> “大爆炸第章-日期” </li><li> **描述：**<br/>章节和/或区段的名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>friendlyName) </li> <li> **心跳：**<br/> (s：stream：fenter_ name) </li> </ul> | <ul> <li> **可用：**<br/>默认创建...  </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节名称 </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>friendlyName) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>friendlyName) </li> </ul> |

### 章节位置

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.index </li> <li> **必需：**<br/> SDK：不；API：是的。 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 章节关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> 2 </li><li> **描述：**<br/>内容内章节的位置(索引、整数)。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>position) </li> <li> **心跳：**<br/> (l：stream：panel_ pos) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节位置 </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>position) </li> <li> **数据馈送：**<br/> </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>position) </li> </ul> |

### 章节偏移

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.chapter.offset </li> <li> **必需：**<br/> SDK：不；API：是的。 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 章节关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> 58 </li><li> **描述：**<br/>从一开始，内容内的一章的偏移量(以秒为单位)。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>offset) </li> <li> **心跳：**<br/> (l：stream：fenter_ offset) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节偏移 </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>offset) </li> <li> **数据馈送：**<br/> </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>offset) </li> </ul> |

### 章节长度

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.chapter.length </li> <li> **必需：**<br/> SDK：不；API：是的。 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 章节关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> 486 </li><li> **描述：**<br/>章节的长度，以秒为单位。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>length) </li> <li> **心跳：**<br/> (l：stream：folition_ length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>章节长度 </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>length) </li> <li> **数据馈送：**<br/> </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>length) </li> </ul> |

### 章节

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 章节关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>章节的自动生成的ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>name) </li> <li> **心跳：**<br/> (s：stream：fenter_ id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>章节 </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>name) </li> <li> **数据馈送：**<br/>videochapter </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>name) </li> </ul> |

## 章节量度 {#section_1C47D6FB1DF343C39CE7A8F724406F33}

### 章节开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>章节开始 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>章节的开始次数。重要信息：如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>view) </li> <li> **心跳：**<br/> (s：event：<br/>type= chapter_ start) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报告名称：**<br/> 章节开始g </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>view) </li> <li> **数据馈送：**<br/>videochapterstart </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>view) </li> </ul> |

### 章节结束

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 章节关闭 </li> <li> **最小 SDK 版本：** 1.3</li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>章节的完成次数。重要信息：如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>complete) </li> <li> **心跳：**<br/> (s：event：<br/>type= farcher_ complete) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报告名称：**<br/> 章节完成g </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>complete) </li> <li> **数据馈送：**<br/>videochaptercomplete </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>complete) </li> </ul> |

### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置  </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 章节关闭 </li> <li> **最小 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>本章所花的时间。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. psa.<br/>时间播放) </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报告名称：**<br/> 章节逗留时间g </li> <li> **上下文数据：**<br/> (a. media. psa.<br/>时间播放) </li> <li> **数据馈送：**<br/>videochaptertime </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. media. appa.<br/>时间播放) </li> </ul> |

## Related APIs {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* Javascript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
