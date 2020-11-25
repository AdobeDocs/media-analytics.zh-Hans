---
title: 播放器状态参数
description: 本主题将介绍播放器状态跟踪参数。
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1cf631d7f3d5365a02be99af78655ac3b53fb3cb
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 99%

---


# 播放器状态参数{#player-state-parameters}

本主题将介绍 Adobe 通过解决方案变量收集的播放器状态数据列表。

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

## 播放器状态属性 {#player-state-properties}

播放器状态跟踪功能可以附加到音频或视频流。标准化的播放器状态跟踪量度可存储为解决方案变量。标准状态为：fullScreen、mute、closeCaption、pictureInPicture 和 inFocus。

### 全屏属性

#### 受全屏影响的流数量

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;受全屏影响的流数量。只有在播放会话期间出现至少一次全屏状态时，此量度才设置为 1。<br/> **重要信息**<br/> 如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.fullscreen.set<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;受全屏影响的流数量 </li> <li> **上下文数据**<br/> (a.media.states.fullscreen.set<br/> </li> <li> **数据源**<br/> videostatefullscreen </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.fullscreen.set </li> </ul> |

#### 全屏计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;显示全屏的次数。只有在播放会话期间出现至少一次全屏状态时，此量度才设置为 1。<br/> **重要信息**<br/>&#x200B;如果设置了此事件，则计数等于视频处于“全屏”状态的次数。如果不设置此事件，则不会发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.fullscreen.count<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;全屏计数 </li> <li> **上下文数据**<br/> a.media.states.fullscreen.count<br/> </li> <li> **数据源**<br/> videostatefullscreencount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.fullscreen.count </li> </ul> |



#### 全屏总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;显示全屏的时长。只有在播放会话期间出现至少一次全屏状态时，此量度才设置为 1。<br/> **重要信息**<br/>&#x200B;如果设置了此事件，则时长等于视频处于“全屏”状态的时长。如果不设置此事件，则不会发送任何值。  </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.fullscreen.time<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;全屏持续总时长 </li> <li> **上下文数据**<br/> a.media.states.fullscreen.time<br/> </li> <li> **数据源**<br/> videostatefullscreentime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.fullscreen.time </li> </ul> |


### 隐藏式字幕属性

#### 受隐藏式字幕影响的流数量

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;受隐藏式字幕影响的流数量。只有在播放会话期间出现至少一次隐藏式字幕状态时，此量度才设置为 1。<br/> **重要信息**<br/> 如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.closedcaptioning.set<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;受隐藏式字幕影响的流数量 </li> <li> **上下文数据**<br/> a.media.states.closedcaptioning.set<br/> </li> <li> **数据源**<br/> videostateclosedcaptioning </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.closedcaptioning.set </li> </ul> |


#### 隐藏式字幕计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;隐藏式字幕显示的次数。只有在播放会话期间出现至少一次隐藏式字幕状态时，此量度才设置为 1。<br/> **重要信息**<br/>&#x200B;如果设置了此事件，则计数等于视频处于“隐藏式字幕”状态的次数。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe**<br/> Analyticsa.media.states.closedcaptioning.count<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;隐藏式字幕计数 </li> <li> **上下文数据**<br/> a.media.states.closedcaptioning.count<br/> </li> <li> **数据源**<br/> videostateclosedcaptioningcount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.closedcaptioning.count </li> </ul> |


#### 隐藏式字幕总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;隐藏式字幕显示的时长。只有在播放会话期间出现至少一次全屏状态时，此量度才设置为 1。<br/> **重要信息**<br/>&#x200B;如果设置了此事件，则时长等于视频处于“隐藏式字幕”状态的时长。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.closedcaptioning.time<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;隐藏式字幕总持续时长 </li> <li> **上下文数据**<br/> a.media.states.closedcaptioning.time<br/> </li> <li> **数据源**<br/> videostateclosedcaptioningtime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.closedcaptioning.time </li> </ul> |


### 静音属性

#### 受静音影响的流数量

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;受静音影响的流数量。只有在播放会话期间出现至少一次静音状态时，此量度才设置为 1。<br/> **重要信息**<br/> 如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.mute.set<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;受静音影响的流数量 </li> <li> **上下文数据**<br/> a.media.states.mute.set<br/> </li> <li> **数据源**<br/> videostatemute </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.mute.set </li> </ul> |

#### 静音计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>“静音”显示的次数。只有在播放会话期间出现至少一次静音状态时，此量度才设置为 1。<br/> **重要信息**<br/>&#x200B;如果设置了此事件，则计数等于视频处于“静音”状态的次数。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.mute.count<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;静音计数 </li> <li> **上下文数据**<br/> a.media.states.mute.count<br/> </li> <li> **数据源**<br/> videostatemutecount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.mute.count </li> </ul> |

#### 静音总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>“静音”显示的时长。只有在播放会话期间出现至少一次静音状态时，此量度才设置为 1。<br/> **重要信息**<br/>&#x200B;如果设置了此事件，则时长等于视频处于“静音”状态的时长。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.mute.time<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;静音总持续时长 </li> <li> **上下文数据**<br/> a.media.states.mute.time<br/> </li> <li> **数据源**<br/> videostatemutetime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.mute.time </li> </ul> |


### 画中画属性


#### 受画中画影响的流数量

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;受画中画影响的流数量。只有在播放会话期间出现至少一次画中画状态时，此量度才设置为 1。<br/> **重要信息**<br/> 如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.pictureinpicture.set<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;受画中画影响的流数量 </li> <li> **上下文数据**<br/> a.media.states.pictureinpicture.set<br/> </li> <li> **数据源**<br/> videostatepictureinpicture </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.pictureinpicture.set </li> </ul> |


#### 画中画计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;显示画中画的次数。只有在播放会话期间出现至少一次画中画状态时，此量度才设置为 1。<br/> **重要信息**<br/>如果设置此事件，则计数等于视频处于“画中画”状态的次数。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.pictureinpicture.count<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;画中画计数 </li> <li> **上下文数据**<br/> a.media.states.pictureinpicture.count<br/> </li> <li> **数据源**<br/> videostatepictureinpicturecount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.pictureinpicture.count </li> </ul> |


#### 画中画总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;显示画中画的时长。只有在播放会话期间出现至少一次画中画状态时，此量度才设置为 1。<br/> **重要信息**<br/>如果设置了此事件，则时长等于视频处于“画中画”状态的时长。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.pictureinpicture.time<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;画中画总持续时长 </li> <li> **上下文数据**<br/> a.media.states.pictureinpicture.time<br/> </li> <li> **数据源**<br/> videostatepictureinpicturetime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.pictureinpicture.time </li> </ul> |


### 聚焦属性

#### 受聚焦影响的流数量

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;受聚焦影响的流数量。只有在播放会话期间出现至少一次聚焦状态时，此量度才设置为 1。<br/> **重要信息**<br/> 如果设置此事件，则唯一可能的值为 TRUE。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.infocus.set<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;受聚焦影响的流数量 </li> <li> **上下文数据**<br/> a.media.states.infocus.set<br/> </li> <li> **数据源**<br/> videostateinfocus </li> <li> **Audience Manager**<br/> c_contextdata.a.media.states.infocus.set </li> </ul> |


#### 聚焦计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;显示聚焦的次数。只有在播放会话期间出现至少一次聚焦状态时，此量度才设置为 1。<br/> **重要信息**<br/>&#x200B;如果设置了此事件，则计数等于视频处于“聚焦”状态的次数。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.infocus.count<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;聚焦计数 </li> <li> **上下文数据**<br/> a.media.states.infocus.count<br/> </li> <li> **数据源**<br/> videostateinfocuscount </li> <li> **Audience Manager**<br/> c_contextdata.media.states.infocus.count </li> </ul> |


#### 聚焦总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥**<br/>&#x200B;自动设置  </li> <li> **API 密钥**<br/>&#x200B;不适用 </li> <li> **必需**<br/>&#x200B;否 </li> <li> **类型**<br/>&#x200B;数值 </li> <li> **发送条件**<br/>&#x200B;媒体关闭 </li> <li> **最低 SDK 版本**<br/> 3.0</li> <li> **示例值**<br/> TRUE </li><li> **描述**<br/>&#x200B;显示聚焦的时长。只有在播放会话期间出现至少一次聚焦状态时，此量度才设置为 1。<br/> **重要信息**<br/>如果设置了此事件，则时长等于视频处于“聚焦”状态的时长。如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics**<br/> a.media.states.infocus.time<br/></li> <li> **心率**<br/>&#x200B;不适用 </li> </ul> | <ul> <li> **可用**<br/>&#x200B;是 </li> <li> **保留的变量**<br/> event </li> <li> **报表名称**<br/>&#x200B;聚焦总持续时长 </li> <li> **上下文数据**<br/> a.media.states.infocus.time<br/> </li> <li> **数据源**<br/> videostateinfocustime </li> <li> **Audience Manager**<br/> c_contextdata.media.states.infocus.time </li> </ul> |

## XDM 标识的属性列表

存储在 Analytics 中的数据可用于任何目的，并且可以使用 XDM 将播放器状态量度导入到 Adobe Experience Platform 中，用于 Customer Journey Analytics。

| 播放器状态属性 | 映射 |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## 相关 API {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
