---
seo-title: 质量参数
title: 质量参数
uuid: 0d9fa764-edef-4178-8650-90c9 a0852 a57
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# 质量参数{#quality-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列体验质量 (QoE/QoS) 数据，包括上下文数据值。

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

## 质量元数据 {#section_8467F9729DA04A888A2657712234D7C7}

### 平均比特率

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.qoe.bitrate </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 800-899 </li><li> **描述：**<br/>平均比特率(以kbps为单位)。此值是以 100 kbps 为间隔的预定义存储段。“平均比特率”计算为在播放会话期间发生的播放持续时间的所有相关比特率值的加权平均值。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>BitrateAvaagbit) </li> <li> **心跳：**<br/> (l：stream：比特率) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>Average Bitrate </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>BitrateAvaagbit) </li> <li> **数据馈送：**<br/>videoqoebitrateaverageevar </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>BitrateAvaagbit) </li> </ul> |



### 开始时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.qoe.timeToStart </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 30,000 </li><li> **描述：**<br/>如果您不通过QOSobject设置此值，则此值默认为零。您应以毫秒为单位设置此值。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **心跳：**<br/> (l：stream：startup_ time) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>开始时间 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **数据馈送：**<br/>videoqoetimetostartevar </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>timeToStart) </li> </ul> |



### FPS

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.qoe.framesPerSecond </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体开始、媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 24 </li><li> **描述：**<br/>流帧速率的当前值(以每秒帧为单位)。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> **心跳：**<br/> (l：stream：fps) </li> </ul> | <ul> <li> **可用：**<br/>否 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>不适用 </li> <li> **上下文数据：**<br/> </li> <li> **数据馈送：**<br/> </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 丢帧

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>droppedFrames </li> <li> **API 密钥：**<br/>media.qoe.droppedFrames </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 3 </li><li> **描述：**<br/>丢弃的帧的数量(整数)。此值计算为在播放会话期间所有丢帧的总和。此值取自最后一个值(l：stream：droved_ frame.)  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>droppedFrameCount) </li> <li> **心跳：**<br/> (l：stream：<br/>droved_ frames) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>丢帧 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>droppedFrameCount) </li> <li> **数据馈送：**<br/>videoqoedroppedframecountevar </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>droppedFrameCount) </li> </ul> |



### 缓冲事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 2 </li><li> **描述：**<br/>缓冲事件的数量。此量度计算为在播放会话期间出现不同缓冲状态的次数。此量度计算播放器从其他状态（例如，播放或暂停）进入缓冲状态的次数。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>bufferCount) </li> <li> **心跳：**<br/> (s：event：<br/>type= breffel) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>缓冲事件 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>bufferCount) </li> <li> **数据馈送：**<br/>videoqoebuffercountevar </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>bufferCount) </li> </ul> |



### 缓冲总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本:** </li> <li> **示例值：**<br/> 30 </li><li> **描述：**<br/>总是花在缓冲上的总时间(以秒为单位)。此值计算为在播放会话期间发生的所有缓冲事件持续时间的总和。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>bufferTime) </li> <li> **心跳：**<br/> (l：event：持续时间) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>缓冲总持续时间 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>bufferTime) </li> <li> **数据馈送：**<br/>videoqoebuffertimeevar </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>bufferTime) </li> </ul> |



### 比特率更改

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.qoe.bitrateChange </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 3 </li><li> **描述：**<br/>比特率更改的数量(整数)。此值计算为在播放会话期间发生的所有比特率更改事件的总和。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>BitrateChangeCount) </li> <li> **心跳：**<br/> (s：event：<br/>type= bitrate_ change) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>比特率更改 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>BitrateChangeCount) </li> <li> **数据馈送：**<br/>videoqoebitratechangecountevar </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>BitrateChangeCount) </li> </ul> |



### 错误/错误事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 1 </li><li> **描述：**<br/>发生错误的次数(整数)。此值计算为在播放会话期间发生的所有错误事件的总和。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>errorCount) </li> <li> **心跳：**<br/> (s：event：<br/>type= error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>errorCount) </li> <li> **数据馈送：**<br/>videoqoeerrorcountevar </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>errorCount) </li> </ul> |



### 播放器 SDK 错误 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>播放器SDK生成的唯一错误ID。客户必须在实施时通过所提供的错误 API 来提供错误代码/ID。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>playerSDKErrors) </li> <li> **心跳：**<br/> (s：event：<br/>type= error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>playerSDKErrors) </li> <li> **数据源：**<br/> videoqoplayersdkerrors </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>playerSDKErrors) </li> </ul> |



### 外部错误 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>来自任何外部源的唯一错误ID，例如CDN错误。客户必须在实施时通过所提供的错误 API 来提供错误代码/ID。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>ExternalErrors) </li> <li> **心跳：**<br/> (s：event：<br/>type= error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>ExternalErrors) </li> <li> **数据源：**<br/> videoqootnalalerrors </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>ExternalErrors) </li> </ul> |



### Media SDK 错误 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>回放期间由Media SDK生成的唯一错误ID。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>mediaSDKErrors) </li> <li> **心跳：**<br/> (s：event：<br/>type= error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>mediaSDKErrors) </li> <li> **数据馈送：**<br/>mediaqoeexternalerrors </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>mediaSDKErrors) </li> </ul> |




### 会话结束 {#session-end}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 2.1 </li> <li> **示例值：**<br/> end </li><li> **描述：**<br/>结束事件意味着SDK正在向后端发送一个close调用。收到此事件后，后端将关闭此视频的会话，然后执行进一步的处理。<br/>如果媒体已完成，则应在 `s:event:type=complete.` 查看 [内容完成后发送，](audio-video-parameters.md#content-complete) 以获取相关信息。 </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> **心跳：**<br/> (s：event：type= end) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>不适用 </li> <li> **上下文数据：**<br/> </li> <li> **数据馈送：**<br/> </li> <li> **Audience Manager：**<br/> </li> </ul> |



## 质量量度 {#section_8EB0C9CBC09340C8915E1D2707D0A9EE}

### 开始时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 30,000 </li><li> **描述：**<br/>如果您不通过QOSobject设置此值，则此值默认为零。您应以毫秒为单位设置此值。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **心跳：**<br/> (l：stream：startup_ time) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>开始时间 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>timeToStart) </li> <li> **数据馈送：**<br/>videoqoetimetostart </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>timeToStart) </li> </ul> |



### 缓冲事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 2 </li><li> **描述：**<br/>缓冲事件的数量(整数)。此量度计算为在播放会话期间发生缓冲事件的次数。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>bufferCount) </li> <li> **心跳：**<br/> (s：event：<br/>type= breffel) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>缓冲事件 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>bufferCount) </li> <li> **数据馈送：**<br/>videoqoebuffercount </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>bufferCount) </li> </ul> |



### 缓冲总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 15 </li><li> **描述：**<br/>缓冲的总时间(秒；整数)。此值计算为在播放会话期间发生的所有缓冲事件持续时间的总和。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>bufferTime) </li> <li> **心跳：**<br/> (l：event：持续时间) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>缓冲总持续时间 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>bufferTime) </li> <li> **数据馈送：**<br/>videoqoebuffertime </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>bufferTime) </li> </ul> |



### 比特率更改

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>事件 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> “3” </li><li> **描述：**<br/>比特率更改的数量。此值计算为在播放会话期间发生的所有比特率更改事件的总和。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>BitrateChangeCount) </li> <li> **心跳：**<br/> (s：event：<br/>type= bitrate_ change) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>比特率更改 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>BitrateChangeCount) </li> <li> **数据馈送：**<br/>videoqoebitratechangecount </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>BitrateChangeCount) </li> </ul> |



### 错误

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 1 </li><li> **描述：**<br/>发生的错误数(整数)。此值计算为在播放会话期间发生的所有错误事件的总和。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>errorCount) </li> <li> **心跳：**<br/> (s：event：<br/>type= error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>错误事件 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>errorCount) </li> <li> **数据馈送：**<br/>videoqoeerrorcount </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>errorCount) </li> </ul> |



### 丢帧

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 1 </li><li> **描述：**<br/>丢弃的帧的数量(整数)。此值计算为在播放会话期间所有丢帧的总和。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>droppedFrameCount) </li> <li> **心跳：**<br/> (l：stream：<br/>droved_ frames) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>丢帧 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>droppedFrameCount) </li> <li> **数据馈送：**<br/>videoqoedroppedframecount </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>droppedFrameCount) </li> </ul> |



### 开始前丢帧

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>用户在开始之前退出视频的次数。只有在没有任何内容呈现的情况下（不论是否有广告），此量度才设置为 1。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>DropBeforeStart) </li> <li> **心跳：**<br/> (s：event：<br/>type= aa_ start) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>开始前丢帧 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>DropBeforeStart) </li> <li> **数据馈送：**<br/>videoqoedropbeforestart </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>DropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>如果设置此事件，则唯一可能的值为TRUE。如果不设置此事件，则不会发送任何值。

### 受缓冲影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>缓冲影响的流数。只有在播放会话期间发生至少一次缓冲事件时，此量度才设置为 1。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>buffer) </li> <li> **心跳：**<br/> (s：event：<br/>type= breffel) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受缓冲影响的流 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>buffer) </li> <li> **数据馈送：**<br/>videoqoebuffer </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>如果设置此事件，则唯一可能的值为TRUE。如果不设置此事件，则不会发送任何值。

### 受比特率更改影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>发生比特率更改的流数。只有在播放会话期间发生至少一次比特率更改事件时，此量度才设置为 1。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>BitrateChange) </li> <li> **心跳：**<br/> (s：event：<br/>type= bitrate_ change) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受缓冲更改影响的流 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>BitrateChange) </li> <li> **数据馈送：**<br/>videoqoebitratechange </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>BitrateChange) </li> </ul> |



>[!IMPORTANT]
>如果设置此事件，则唯一可能的值为TRUE。如果不设置此事件，则不会发送任何值。

### 平均比特率

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 3200 </li><li> **描述：**<br/>平均比特率(以kbps为单位，整数)。此量度计算为在播放会话期间发生的播放持续时间的所有相关比特率值的加权平均值。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>Bitrate平均) </li> <li> **心跳：**<br/> (l：stream：比特率) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>Average Bitrate </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>Bitrate平均) </li> <li> **数据馈送：**<br/>videoqoebitrateaverage </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>Bitrate平均) </li> </ul> |



### 受错误影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>发生比特率更改的流数。只有在播放会话期间发生至少一次比特率更改事件时，此量度才设置为 1。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>error) </li> <li> **心跳：**<br/> (s：event：<br/>type= error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受错误影响的流 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>error) </li> <li> **数据馈送：**<br/>videoqoeerror </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>error) </li> </ul> |



>[!IMPORTANT]
>如果设置此事件，则唯一可能的值为TRUE。如果不设置此事件，则不会发送任何值。

### 受丢帧影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>丢弃帧的流数。只有在播放会话期间至少丢失了一个帧时，此量度才设置为 1。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **心跳：**<br/> (l：stream：<br/>droved_ frames) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受丢帧影响的流 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>droppedFrames) </li> <li> **数据馈送：**<br/>videoqoedroppedframes </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>如果设置此事件，则唯一可能的值为TRUE。如果不设置此事件，则不会发送任何值。

### 受停滞影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5 及更高版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>发生started事件的流数。只有在播放期间发生至少一次停滞事件时，此量度才设置为 1。客户必须自行创建处理规则才能在报表中使用此值。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>stall) </li> <li> **心跳：**<br/> (s：event：<br/>type= stall) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/> </li> <li> **数据馈送：**<br/>不适用 </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>stall) </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>stall) </li> </ul> |



>[!IMPORTANT]
>如果设置此事件，则唯一可能的值为TRUE。如果不设置此事件，则不会发送任何值。

### 停滞事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5 及更高版本 </li> <li> **示例值：**<br/> “3” </li><li> **描述：**<br/>回放会话期间回放的次数。客户必须自行创建处理规则才能在报表中使用此值。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>stallCount) </li> <li> **心跳：**<br/> (s：event：<br/>type= stall) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>stallCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>stallCount) </li> </ul> |



### 停滞总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送随：**<br/> 媒体关闭 </li> <li> **最小 SDK 版本：** 1.5 及更高版本 </li> <li> **示例值：**<br/> 12 </li><li> **描述：**<br/>总时间(秒；整数)回放会话期间暂停播放。客户必须自行创建处理规则才能在报表中使用此值。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a. media. qoe.<br/>stallTime) </li> <li> **心跳：**<br/> (s：event：<br/>type= stall) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/> </li> <li> **上下文数据：**<br/> (a. media. qoe.<br/>stallTime) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a media. qoe。<br/>stallTime) </li> </ul> |



## Related APIs {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

