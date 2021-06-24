---
title: 发送 Ping 事件
description: Ping事件是流媒体分析的心率。 了解如何为主内容或广告跟踪发送定时Ping。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 79%

---

# 发送 Ping 事件{#sending-ping-events}

**对于主内容，您必须每 10 秒触发一次 Ping 事件，从播放 10 秒之后开始，而不考虑已发送的其他 API 事件。对于广告跟踪，必须每 1 秒触发一次 Ping 事件。**

Ping 事件实际上就是 Media Analytics 的“心率”。Ping 调用所需的唯一参数是 `eventType: ping` 以及 `playerTime` 对象（播放头位置和时间戳）。

以下代码片段显示了一种为主内容实施定时 Ping 机制的方法（10 秒间隔）：

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
