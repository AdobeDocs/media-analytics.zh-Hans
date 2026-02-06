---
title: 跟踪应用程序状态
description: 应用程序状态是指您的应用程序中的不同屏幕或视图。了解如何使用 trackState 调用跟踪应用程序中的应用程序状态。
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
exl-id: bb1e0eee-7c59-40b4-9359-a7441b9686b8
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 100%

---

# 跟踪应用程序状态{#track-app-states}

状态是指您的应用程序中的不同屏幕或视图。每次在应用程序中显示新状态时，都应发送 `trackState` 调用。例如，当用户从主页导航到视频详细信息屏幕时，应发送 `trackState` 调用。状态通常使用路径报表来查看，以便您能够查看用户在应用程序中导航的方式以及最常查看的状态。

## trackState 调用

每当应用程序加载新屏幕时，通常会调用 `trackState`。

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

在 Adobe Mobile Services 中，状态名称将在“视图状态”变量中进行报告，并且每个 `trackState` 调用均会记录一个视图。在其他 Analytics 界面中，“视图状态”将被报告为“页面名称”，“状态查看次数”将被报告为“页面查看次数”。

## 发送上下文数据

除了“状态名称”之外，您还可以通过每个跟踪状态调用发送其他上下文数据。

### Roku

```js
dictionary = { } 
dictionary["myapp.login.LoginStatus"] = "logged in"  
ADBMobile().trackState("Home Screen", dictionary)
```

### Chromecast

```js
var dictionary = { }; 
dictionary["myapp.login.LoginStatus"] = "logged in"; 
ADBMobile.analytics.trackState("Home Screen", dictionary); 
```

>[!NOTE]
>
>上下文数据值必须映射到 Adobe Mobile Services 中的自定义变量。
