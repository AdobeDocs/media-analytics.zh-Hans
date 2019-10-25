---
seo-title: 质量参数
title: 质量参数
uuid: 0d9fa764-edef-4178-8650-90c9a0852a57
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# 质量参数{#quality-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列体验质量 (QoE/QoS) 数据，包括上下文数据值。

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

## 质量元数据 {#quality-metadata}

### 平均比特率

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [bitrate](./quality-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>media.qoe.bitrate </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：800-899 </li><li> **说明：**<br/>平均比特率（以kbps为单位）。 此值是以 100 kbps 为间隔的预定义存储段。“平均比特率”计算为在播放会话期间发生的播放持续时间的所有相关比特率值的加权平均值.  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateAverageBucket) </li> <li> ****<br/> 心跳：(l:stream:bitrate) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>Average Bitrate </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bitrateAverageBucket) </li> <li> **数据馈送：**<br/>videoqoebitrateaverageevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateAverageBucket) </li> </ul> |



### 开始时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.qoe.timeToStart </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：三万 </li><li> **说明：**<br/>如果不通过QoSObject设置此值，则此值默认为零。 您应以毫秒为单位设置此值。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> 心跳：(l:stream:startup_time) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>开始时间 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>timeToStart) </li> <li> **数据馈送：**<br/>videoqoetimetostartevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>timeToStart) </li> </ul> |



### FPS

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.qoe.framesPerSecond </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体开始，媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：24 </li><li> **描述：**<br/>流帧速率的当前值（以每秒帧数为单位）。  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> ****<br/> 心跳：(l:stream:fps) </li> </ul> | <ul> <li> **可用：**<br/>否 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>不适用 </li> <li> **上下文数据：**<br/> </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 丢帧

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>droppedFrames </li> <li> **API 密钥：**<br/>media.qoe.droppedFrames </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：3 </li><li> **说明：**<br/>丢帧的数量(Int)。 此值计算为在播放会话期间所有丢帧的总和。此值取自(l:stream:dropped_frames)的最后一个值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> 心跳：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>丢帧 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>droppedFrameCount) </li> <li> **数据馈送：**<br/>videoqoedroppedframecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>droppedFrameCount) </li> </ul> |



### 缓冲事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：2 </li><li> **说明：**<br/>缓冲区事件的数量。 此量度计算为在播放会话期间出现不同缓冲状态的次数。此量度计算播放器从其他状态（例如，播放或暂停）进入缓冲状态的次数。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> 心跳：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>缓冲事件 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bufferCount) </li> <li> **数据馈送：**<br/>videoqoebuffercountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferCount) </li> </ul> |



### 缓冲总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本:** </li> <li> ****<br/> 示例值：30 </li><li> **说明：**<br/>缓冲所用的总时间（以秒为单位）。 此值计算为在播放会话期间发生的所有缓冲事件持续时间的总和。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> 心跳：(l:event:duration) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>缓冲总持续时间 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bufferTime) </li> <li> **数据馈送：**<br/>videoqoebuffertimeevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferTime) </li> </ul> |



### 比特率更改

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/>media.qoe.bitrateChange </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：3 </li><li> **说明：**<br/>比特率更改的数量（整数）。 此值计算为在播放会话期间发生的所有比特率更改事件的总和。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> 心跳：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>比特率更改 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bitrateChangeCount) </li> <li> **数据馈送：**<br/>videoqoebitratechangecountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateChangeCount) </li> </ul> |



### 错误/错误事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：1 </li><li> **说明：**<br/>发生的错误数（整数）。 此值计算为在播放会话期间发生的所有错误事件的总和。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>errorCount) </li> <li> ****<br/> 心跳：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>errorCount) </li> <li> **数据馈送：**<br/>videoqoeerrorcountevar </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>errorCount) </li> </ul> |



### 播放器 SDK 错误 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> </li><li> **说明：**<br/>播放器SDK生成的唯一错误ID。 客户必须在实施时通过所提供的错误 API 来提供错误代码/ID。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> 心跳：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>playerSdkErrors) </li> <li> ****<br/> 数据馈送：videoqoeplayersdkerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>playerSdkErrors) </li> </ul> |



### 外部错误 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> </li><li> **说明：**<br/>来自任何外部源的唯一错误ID，如CDN错误。 客户必须在实施时通过所提供的错误 API 来提供错误代码/ID。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> 心跳：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>externalErrors) </li> <li> ****<br/> 数据馈送：videoqoeexternererrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>externalErrors) </li> </ul> |



### Media SDK 错误 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> </li><li> **说明：**<br/>回放过程中Media SDK生成的唯一错误ID。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>mediaSdkErrors) </li> <li> ****<br/> 心跳：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>错误 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>mediaSdkErrors) </li> <li> **数据馈送：**<br/>mediaqoeexternalerrors </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>mediaSdkErrors) </li> </ul> |




### 会话结束 {#session-end}

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/> </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 2.1 </li> <li> ****<br/> 示例值：end </li><li> **说明：**<br/>结束事件表示SDK正在向后端发送关闭调用。 收到此事件后，后端将关闭此视频的会话，然后执行进一步的处理。<br/>如果媒体已完成到100%，则应在查看内容完成后发送此 `s:event:type=complete.` 消息 [以了解相关信息](audio-video-parameters.md#content-complete) 。 </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>不适用 </li> <li> ****<br/> 心跳：(s:event:type=end) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>不适用 </li> <li> **上下文数据：**<br/> </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> </li> </ul> |



## 质量量度 {#quality-metrics}

### 开始时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：三万 </li><li> **说明：**<br/>如果不通过QoSObject设置此值，则此值默认为零。 您应以毫秒为单位设置此值。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>timeToStart) </li> <li> ****<br/> 心跳：(l:stream:startup_time) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>开始时间 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>timeToStart) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>timeToStart) </li> </ul> |



### 缓冲事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [startupTime](./quality-parameters.md#related_apis_section) </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：2 </li><li> **说明：**<br/>缓冲区事件数（整数）。 此量度计算为在播放会话期间发生缓冲事件的次数。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferCount) </li> <li> ****<br/> 心跳：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>缓冲事件 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bufferCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferCount) </li> </ul> |



### 缓冲总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：15 </li><li> **说明：**<br/>缓冲的总时间(秒；integer)。 此值计算为在播放会话期间发生的所有缓冲事件持续时间的总和。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bufferTime) </li> <li> ****<br/> 心跳：(l:event:duration) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>缓冲总持续时间 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bufferTime) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bufferTime) </li> </ul> |



### 比特率更改

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>事件 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：“3” </li><li> **说明：**<br/>比特率更改的数量。 此值计算为在播放会话期间发生的所有比特率更改事件的总和。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChangeCount) </li> <li> ****<br/> 心跳：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>比特率更改 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bitrateChangeCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateChangeCount) </li> </ul> |



### 错误

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：1 </li><li> **说明：**<br/>发生的错误数（整数）。 此值计算为在播放会话期间发生的所有错误事件的总和。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>errorCount) </li> <li> ****<br/> 心跳：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>错误事件 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>errorCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>errorCount) </li> </ul> |



### 丢帧

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：1 </li><li> **说明：**<br/>丢帧的数量（整数）。 此值计算为在播放会话期间所有丢帧的总和。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrameCount) </li> <li> ****<br/> 心跳：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>丢帧 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>droppedFrameCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>droppedFrameCount) </li> </ul> |



### 开始前丢帧

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：TRUE </li><li> **说明：**<br/>用户在视频开始前退出视频的次数。 只有在没有任何内容呈现的情况下（不论是否有广告），此量度才设置为 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>dropBeforeStart) </li> <li> ****<br/> 心跳：(s:event:<br/>type=aa_start) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>开始前丢帧 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>dropBeforeStart) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>dropBeforeStart) </li> </ul> |



>[!IMPORTANT]
>如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。

### 受缓冲影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：TRUE </li><li> **描述：**<br/>受缓冲影响的流数。 只有在播放会话期间发生至少一次缓冲事件时，此量度才设置为 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>buffer) </li> <li> ****<br/> 心跳：(s:event:<br/>type=buffer) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受缓冲影响的流 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>buffer) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>buffer) </li> </ul> |



>[!IMPORTANT]
>如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。

### 受比特率更改影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：TRUE </li><li> **描述：**<br/>发生比特率更改的流数。 只有在播放会话期间发生至少一次比特率更改事件时，此量度才设置为 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateChange) </li> <li> ****<br/> 心跳：(s:event:<br/>type=bitrate_change) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> ****<br/> 报告名称：受比特率更改影响的流 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bitrateChange) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateChange) </li> </ul> |



>[!IMPORTANT]
>如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。

### 平均比特率

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：3200 </li><li> **说明：**<br/>平均比特率（以kbps、整数为单位）。 此量度计算为在播放会话期间发生的播放持续时间的所有相关比特率值的加权平均值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>bitrateAverage) </li> <li> ****<br/> 心跳：(l:stream:bitrate) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>Average Bitrate </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>bitrateAverage) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>bitrateAverage) </li> </ul> |



### 受错误影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：TRUE </li><li> **说明：**<br/>发生错误事件的流数(即，在播放会话期间调用，并生成 `trackError``type=error` 了心跳调用)。 </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>error) </li> <li> ****<br/> 心跳：(s:event:<br/>type=error) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受错误影响的流 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>error) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>error) </li> </ul> |



>[!IMPORTANT]
>如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。

### 受丢帧影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> ****<br/> 示例值：TRUE </li><li> **说明：**<br/>丢帧的流数。 只有在播放会话期间至少丢失了一个帧时，此量度才设置为 1。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>droppedFrames) </li> <li> ****<br/> 心跳：(l:stream:<br/>dropped_frames) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>受丢帧影响的流 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>droppedFrames) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>droppedFrames) </li> </ul> |



>[!IMPORTANT]
>如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。

### 受停滞影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 1.5 及更高版本 </li> <li> ****<br/> 示例值：TRUE </li><li> **说明：**<br/>发生停滞事件的流数。 只有在播放期间发生至少一次停滞事件时，此量度才设置为 1。客户必须自行创建处理规则才能在报表中使用此值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stall) </li> <li> ****<br/> 心跳：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/> </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>stall) </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>stall) </li> </ul> |



>[!IMPORTANT]
>如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。

### 停滞事件

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 1.5 及更高版本 </li> <li> ****<br/> 示例值：“3” </li><li> **说明：**<br/>在播放会话期间播放被停止的次数。 客户必须自行创建处理规则才能在报表中使用此值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stallCount) </li> <li> ****<br/> 心跳：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/> </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>stallCount) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>stallCount) </li> </ul> |



### 停滞总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>数值 </li> <li> ****<br/> 发送方：媒体关闭 </li> <li> **最小 SDK 版本：** 1.5 及更高版本 </li> <li> ****<br/> 示例值：12 </li><li> **说明：**<br/>总时间(秒；整数)播放在播放会话期间被停止。 客户必须自行创建处理规则才能在报表中使用此值。  </li> </ul> | <ul> <li> ****<br/> Adobe Analytics:(a.media.qoe.<br/>stallTime) </li> <li> ****<br/> 心跳：(s:event:<br/>type=stall) </li> </ul> | <ul> <li> **可用：**<br/>使用自定义处理规则 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/> </li> <li> ****<br/> 上下文数据：(a.media.qoe.<br/>stallTime) </li> <li> **数据馈送：**<br/>不适用 </li> <li> ****<br/> Audience Manager:(c_contextdata.<br/>a.media.qoe。<br/>stallTime) </li> </ul> |



## 相关API {#related_apis_section}

* Android - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createQoSObject-java.lang.Long-java.lang.Double-java.lang.Double-java.lang.Long-)
* iOS - [createQoSObjectWithBitrate](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)
* Javascript - [createQoSObject ](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createQoSObject)

