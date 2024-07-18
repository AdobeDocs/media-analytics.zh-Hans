---
title: 章节参数
description: "了解用于实施、网络和报告的章节参数。"
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
exl-id: 73da3e52-9498-478e-bfd7-8ff6c8e6bfc5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 917c87d759a43f124dfb3e3ac7f6a441c65fde94
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 96%

---

# 章节参数{#chapter-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列章节和/或区段数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或由 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示基本视频跟踪是否需要该参数。
   * *类型* - 指定要设置的变量的类型：字符串或数字。
   * *发送条件* - 指示何时发送数据：*媒体开始*&#x200B;表示在媒体开始播放时发送分析调用；*广告开始*&#x200B;表示在广告等开始播放时发送分析调用；*关闭*&#x200B;调用表示在媒体会话或广告、章节等结束时直接从心率服务器向分析服务器发送经过汇编的分析调用。在网络数据包调用中无法使用关闭调用。
   * *最低 SDK 版本* - 指示您访问该参数所需的 SDK 版本。
   * *示例值* - 提供常用变量用法的示例。
* **网络参数：**&#x200B;显示传递到 Adobe Analytics 或心率服务器的值。此列显示网络调用中由 Adobe Media SDK 生成的参数的名称。
* **报告：**&#x200B;有关如何查看和分析视频数据的信息。
   * *可用* - 指示在默认情况下数据在报表中可用（*是*），还是需要自定义设置（*自定义*）
   * *保留的变量* - 指示数据是作为保留变量中的事件、eVar、prop 还是分类而捕获的。
   * *报表名称* - 变量的 Adobe Analytics 报表名称
   * *上下文数据* - 传递到报表服务器并用于处理规则的 Adobe Analytics 上下文数据的名称。
   * *数据源* - Clickstream 或实时流数据源中的变量的列名称
   * *Audience Manager* - Adobe Audience Manager 中的特征名称

>[!IMPORTANT]
>
>请勿更改下面列出的在“报表/保留的变量”下描述为“分类”的任何变量的分类名称。\
>在启用报表包进行媒体跟踪后，将定义媒体分类。Adobe 会不时添加新属性，如果添加了新属性，客户必须重新启用其报表包才能访问新的媒体属性。在更新过程中，Adobe 会通过检查变量名称来确定是否启用了分类。如果任何变量名称缺失，Adobe 会再次添加缺失的变量名称。

## 章节元数据 {#chapter-metadata}

### 章节名称

|   实施   | 网络参数 | 报表 |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [name](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/> media.chapter.friendlyName </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;章节开始、章节关闭 </li> <li> **最低 SDK 版本：** 1.3 </li> <li> **示例值：**<br/>&quot;The Big Bang Chapter 2 - Dating&quot; </li><li> **描述：**<br/>&#x200B;章节和/或区段的名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>friendlyName) </li> <li> **心率：**<br/> (<code>s:stream:chapter_name</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;默认创建...  </li> <li> **保留的变量：**<br/>&#x200B;分类 </li> <li> **报表名称：**<br/>&#x200B;章节名称 </li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>friendlyName) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>friendlyName) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.dc:title </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.chapterDetails.friendlyName </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.friendlyName </li> </ul> |

### 章节位置

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [position](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/> media.chapter.index </li> <li> **必需：**<br/> SDK：否；API：是。 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/>&#x200B;章节关闭 </li> <li> **最低 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> 2 </li><li> **描述：**<br/>&#x200B;章节在内容中的位置（索引、整数）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>position) </li> <li> **心率：**<br/> (<code>l:stream:chapter_pos</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/>&#x200B;分类 </li> <li> **报表名称：**<br/>&#x200B;章节位置 </li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>position) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>position) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.index </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.chapterDetails.index </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.index </li> </ul> |

### 章节偏移

|   实施   | 网络参数 | 报表 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [startTime](./chapter-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/> media.chapter.offset </li> <li> **必需：**<br/> SDK：否；API：是。 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/>&#x200B;章节关闭 </li> <li> **最低 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> 58 </li><li> **描述：**<br/>&#x200B;章节在内容中与开始的偏移（以秒为单位）。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>offset) </li> <li> **心率：**<br/> (<code>l:stream:chapter_offset</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/>&#x200B;分类 </li> <li> **报表名称：**<br/>&#x200B;章节偏移 </li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>offset) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>offset) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetViewDetails.offset </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.chapterDetails.offset </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.offset </li> </ul> |

### 章节长度

|   实施   | 网络参数 | 报表 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/> media.chapter.length </li> <li> **必需：**<br/> SDK：否；API：是。 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/>&#x200B;章节关闭 </li> <li> **最低 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> 486 </li><li> **描述：**<br/>&#x200B;章节的长度，以秒为单位。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>length) </li> <li> **心率：**<br/> (<code>l:stream:chapter_length</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/>&#x200B;分类 </li> <li> **报表名称：**<br/>&#x200B;章节长度 </li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>length) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>length) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.xmpDM:duration </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.chapterDetails.length </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.length </li> </ul> |

### 章节

|   实施   | 网络参数 | 报表 |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置 </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;章节关闭 </li> <li> **最低 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>&#x200B;自动生成的章节 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>name) </li> <li> **心率：**<br/> (<code>s:stream:chapter_id</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;章节 </li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>name) </li> <li> **数据馈送：**<br/> videochapter </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>name) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.mediaChapter.<br/>chapterAssetReference.@id </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.ID </li> </ul> |

## 章节量度 {#chapter-Metrics}

### 章节开始

|   实施   | 网络参数 | 报表 |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置  </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;章节开始 </li> <li> **最低 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>&#x200B;章节开始的次数。**重要信息：**&#x200B;如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>view) </li> <li> **心率：**<br/> (<code>s:event:</code><br/>type=chapter_start) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> event </li> <li> **报表名称：**<br/>&#x200B;章节开始</li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>view) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>view) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.chapterCount.<br/>value > 0 => &quot;TRUE&quot; </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.isStarted </li> </ul> |

### 章节结束

|   实施   | 网络参数 | 报表 |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置  </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;章节关闭 </li> <li> **最低 SDK 版本：** 1.3</li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>&#x200B;章节结束的次数。**重要信息：**&#x200B;如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>complete) </li> <li> **心率：**<br/> (<code>s:event:</code><br/>type=chapter_complete) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> event </li> <li> **报表名称：**<br/>&#x200B;章节结束</li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>complete) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>complete) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.mediaChapter.<br/>completes.value </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.isCompleted </li> </ul> |

### 章节逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置  </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/>&#x200B;章节关闭 </li> <li> **最低 SDK 版本：** 1.3 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>&#x200B;章节花费的时间。该值将以时间格式(<code>HH:MM:SS)显示</code>Analysis Workspace )以及Reports &amp; Analytics中的“禁止页面加载闪烁”。 而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.chapter.<br/>timePlayed) </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> event </li> <li> **报表名称：**<br/>&#x200B;章节逗留时间</li> <li> **上下文数据：**<br/>(a.media.chapter.<br/>timePlayed) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.chapter.<br/>timePlayed) </li> <li> **XDM 字段路径：**<br/> media.mediaTimed.mediaChapter.<br/>timePlayed.value </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.chapterDetails.timePlayed </li> </ul> |

## 相关 API {#related_apis_section}

* Android - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createChapterObject-java.lang.String-java.lang.Long-java.lang.Double-java.lang.Double-)
* iOS - [createChapterObjectWithName](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createChapterObjectWithName:position:length:startTime:)
* JavaScript - [createChapterObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createChapterObject)
