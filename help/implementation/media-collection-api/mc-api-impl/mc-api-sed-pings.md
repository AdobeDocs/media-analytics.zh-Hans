---
title: 发送 Ping 事件
description: Ping事件是流媒体收集加载项的心率。 了解如何针对主要内容或广告跟踪发送定时 Ping。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 240fa48bdc738425e04cd29c27625c7dd612ff18
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 50%

---

# 发送 Ping 事件{#sending-ping-events}

**您必须每10秒触发一次Ping事件，从播放10秒之后开始，而不考虑已发送的其他API事件。 这同时适用于主内容和广告跟踪。**

Ping事件是流媒体收集加载项的“心率”。 Ping 调用所需的唯一参数是 `eventType: ping` 以及 `playerTime` 对象（播放头位置和时间戳）。

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
