---
title: 控制事件的顺序
description: 控制事件的顺序
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 100%

---

# 控制事件的顺序{#controlling-the-order-of-events}

由于媒体收集 API 是 RESTful，并且视频跟踪是一种高度依赖于时间的操作，因此实施者可能会担心媒体收集 API 跟踪调用不会按顺序到达后端。后端“确实”**&#x200B;会尝试根据 `playerTime` 对象中提供的时间戳对事件进行排队和重新排序。但是，这种功能有一定的限制。当前，如果乱序执行的调用之间的延迟超过了一秒，则重新排序可能会失败。可能会在将来的更新中对这种“可接受的延迟时间”进行优化和/或配置。
