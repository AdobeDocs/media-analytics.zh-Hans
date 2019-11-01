---
title: 文档更新
description: null
uuid: 1f3e48df-83b6-418c-8cf7-d7946481f79
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 资源{#resources}

## 发行说明{#release-notes}

* [发行说明](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## 文档更新{#documentation-updates}

### Last updated: October, 2019 {#October-2019-update}

大量编辑和格式更正。
说明书主题已扩展到Media SDK之外，包括有关“媒体跟踪之外的媒体维度”的新一般说明书主题。


### 上次更新时间：2019 年 3 月 7 日 {#March-2019-update}

* 此更新主要针对JavaScript和OTT平台上的2.2 Media SDK版本。
* JavaScript和OTT平台上的2.2 Media SDK版本为iOS和Android平台提供如下所述的支持（2018年11月1日更新）。

### 上次更新日期：2018 年 11 月 1 日 {#November-2018-update}

* 此更新主要适用于 Android 和 iOS 平台上的 2.2 Media SDK 版本。
* Android 和 iOS 上的 2.2 Media SDK 版本支持在这些平台上跟踪音频，并且还提供了一些内部改进。
* 由于添加了音频跟踪，而且当前在 Media SDK 和媒体收集 API 中同时提供了音频和视频跟踪功能，因此需要进行一次相对全面的命名更新：

   * 整体解决方案的名称为“Adobe Analytics for Audio and Video”
   * 以前在整个文档中使用的简写“Video Analytics”现在为“Media Analytics”
   * 在 SDK 中，对“视频心率库 (VHL)”的引用现在为“Media SDK”
   * 以前引用了“video”或“vhl”的文件名和 URL（例如，指向 API 引用的链接）现在使用“media”来代替这两者
   * 在代码中，元数据键的名称现在包含“MEDIA”而不是“VIDEO”
   * 等等...

* 除此之外，“Media SDK”部分也进行了一些额外的调整，其中包括标准元数据实施以及返回到其自身主题（在上一次文档更新中，已将这些主题纳入到“跟踪核心”**&#x200B;主题中）的引用。现在，这些主题已与“跟踪核心”**、“跟踪搜寻”**&#x200B;和“跟踪缓冲”**&#x200B;主题一起归入到“跟踪音频和视频播放”**&#x200B;中。

* Federated Analytics 表单已更新到版本 3.2，以反映与跟踪音频有关的新参数。

### 更新日期：2018 年 10 月 10 日 {#October-2018-update}

* 在“SDK 实施”区域中对文档结构进行了“重构”，具体操作是将单个（但大部分是相同的）平台实施指南合并到一个 SDK 实施部分，并在常见跟踪主题下的子部分中提供特定于平台的跟踪示例。
* 在向新文档系统的预期迁移过程中，对文件进行了重命名。消除了分别表示概念、引用和任务主题类型的所有DITA前缀(c_、r_、t_)。 将所有下划线（“_”）都替换为连字符（“-”）。此外，文件名现在更类似于主题的标题。
* 更新了常规的验证和认证主题。
* 新增了介绍性材料，包括测量选项的演示，以及对先决条件、实施路径和 Audience Manager 启用的更新。
* 更新了“量度和元数据”以及“报表和分析”部分，以反映增加的音频分析功能。
