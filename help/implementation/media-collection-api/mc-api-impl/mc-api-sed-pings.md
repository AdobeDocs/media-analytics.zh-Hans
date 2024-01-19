---
title: 发送 Ping 事件
description: Ping 事件是流媒体分析的心跳。 了解如何针对主要内容或广告跟踪发送定时 Ping。
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e84864164adf056f47f24d65f0400c89d53d1630
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 70%

---

# 发送 Ping 事件{#sending-ping-events}

**您必须每10秒触发一次Ping事件，从播放10秒之后开始，而不考虑已发送的其他API事件。 这同时适用于主内容和广告跟踪。**

Ping 事件实际上就是媒体分析的“心跳”。Ping 调用所需的唯一参数是 `eventType: ping` 以及 `playerTime` 对象（播放头位置和时间戳）。

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
