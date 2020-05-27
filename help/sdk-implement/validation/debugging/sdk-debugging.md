---
title: SDK 调试
description: 本主题介绍 Media SDK 中提供的跟踪/日志记录功能。
uuid: a5972d87-c593-4b4f-a56f-dca6e25268e1
translation-type: ht
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a
workflow-type: ht
source-wordcount: '271'
ht-degree: 100%

---


# SDK 调试{#sdk-debugging}

您可以启用和禁用日志记录功能。Media SDK 会在整个媒体跟踪堆栈中提供广泛的跟踪/日志记录机制。您可以通过在配置对象中设置 `debugLogging` 标记，来启用或禁用日志记录功能。

## 有关调试日志记录的代码示例

### Android

```java
// Media Heartbeat initialization 
MediaHeartbeatConfig config = new MediaHeartbeatConfig(); 
config.debugLogging = true; 

// Use this space for setting other config values 
MediaHeartbeat _heartbeat = new MediaHeartbeat(this, config); 
```

### iOS

```
// Media Heartbeat Initialization 
ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
config.debugLogging = YES; 

// Use this space for setting other config values 
ADBMediaHeartbeat *_mediaHeartbeat =  
[[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### JavaScript

```js
// Media Heartbeat initialization 
var mediaConfig = new MediaHeartbeatConfig(); 
mediaConfig.debugLogging = true; 
this._mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement); 
```

### OTT（Chromecast、Roku）

ADBMobile 库通过 `setDebugLogging` 方法提供调试日志记录。对于所有生产应用程序，调试日志记录应设置为 `false`。

#### Roku

```
ADBMobile().setDebugLogging(true)
```

#### Chromecast

```
ADBMobile.config.setDebugLogging(true)
```

## 使用 Adobe Bloodhound 测试 Chromecast 应用程序

在应用程序开发期间，使用 Bloodhound 可以在本机上查看服务器调用，并可以选择将数据转发到 Adobe 收集服务器中。

<!--
For more information about Bloodhound, see the following guides:

* [Bloodhound 3.x for Mac](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=2ahUKEwiimfSUypDpAhVZHzQIHS6WDQIQFjABegQIChAD&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound%2F&usg=AOvVaw3t4s0gcvuWEpLIqBkhKdGH) 
* [Bloodhound 2.2 for Windows](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjil9aM87jRAhUExlQKHTYZCjoQFggoMAI&url=https%3A%2F%2Fmarketing.adobe.com%2Fresources%2Fhelp%2Fen_US%2Fmobile%2Fbloodhound_win_2x%2F&usg=AFQjCNEW-gZp1IdbifWFDgDNEaQcGlBobg&sig2=K0waTKxdMj_2kfNXdMI2yg)
-->

>[!IMPORTANT]
>
>从 2017 年 4 月 30 日起，Adobe Bloodhound 已废止。从 2017 年 5 月 1 日开始，将不再提供其他增强功能以及额外的工程部或 Adobe Expert Care 团队支持。

## 日志消息

日志消息采用以下格式：

```js
Format: [<timestamp>] [<level>] [<tag>] [<message>] 
Example: [16:10:29 GMT­0700 (PDT).245] [DEBUG] [plugin::player] Resolving qos.startupTime: 0
```

* **时间戳：**&#x200B;这是当前 CPU 时间（GMT 时区）
* **级别：**&#x200B;定义了 4 个消息级别：
   * 信息 - 通常来自应用程序的输入数据（验证播放器名称、视频 ID 等）
   * 调试 - 调试日志，开发人员使用它调试比较复杂的问题
   * 警告 - 指示潜在的集成/配置错误或心率 SDK 错误
   * 错误 - 指示重要的集成错误或心率 SDK 错误
* **标记：**&#x200B;发出日志消息的子组件的名称（通常是类名称）
* **消息：**&#x200B;实际跟踪消息

您可以使用 Media SDK 库输出的日志来验证实施。一种有效的方法是在日志中搜索字符串 `#track`。这会突出显示您的应用程序发出的所有 `track*()` 调用。

例如，在日志中过滤 `#track` 的结果如下所示：

```js
[16:10:29 GMT­0700 (PDT).222] [INFO] [plugin::player] #trackVideoLoad() 
[16:10:29 GMT­0700 (PDT).230] [INFO] [plugin::player] #trackSessionStart() 
[16:10:29 GMT­0700 (PDT).250] [INFO] [plugin::player] #trackPlay() 
[16:10:29 GMT­0700 (PDT).759] [INFO] [plugin::player] #trackChapterStart() 
[16:10:44 GMT­0700 (PDT).769] [INFO] [plugin::player] #trackAdStart() 
[16:10:59 GMT­0700 (PDT).752] [INFO] [plugin::player] #trackAdComplete() 
[16:10:59 GMT­0700 (PDT).770] [INFO] [plugin::player] #trackChapterStart() 
[16:11:29 GMT­0700 (PDT).734] [INFO] [plugin::player] #trackPause() 
[16:11:29 GMT­0700 (PDT).764] [INFO] [plugin::player] #trackComplete() 
[16:11:29 GMT­0700 (PDT).766] [INFO] [plugin::player] #trackVideoUnload()
```

