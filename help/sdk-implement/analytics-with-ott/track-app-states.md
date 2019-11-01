---
title: 跟踪应用程序状态
description: '应用程序状态是应用程序中的不同屏幕或视图，当显示该状态时，将导致trackState调用。 '
uuid: 2f98fb43-c362-4a9b-8732-fa7e963da729
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 跟踪应用程序状态{#track-app-states}

状态是指您的应用程序中的不同屏幕或视图。每次在应用程序中显示新状态时，您都应该发送呼 `trackState` 叫。 例如，当用户从主页导航到视频详细信息屏幕时，发送调 `trackState` 用。 状态通常使用路径报表来查看，以便您能够查看用户在应用程序中导航的方式以及最常查看的状态。

## trackState调用

通常，每次应 `trackState` 用程序加载新屏幕时，您都会调用它。

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. 在其他Analytics界面中，“查看状态”报告为“页面名称”;“状态视图”报告为“页面视图”。

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
>上下文数据值必须映射到Adobe Mobile services中的自定义变量。

