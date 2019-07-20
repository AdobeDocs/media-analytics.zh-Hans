---
seo-title: 跟踪应用程序状态
title: 跟踪应用程序状态
uuid: 2f98fb43-c362-4a9 b-8732-fa7 e963 da729
translation-type: tm+mt
source-git-commit: 9cdf69e30fa727aeb974213769a7ab61fb05b756

---


# 跟踪应用程序状态{#track-app-states}

状态是指您的应用程序中的不同屏幕或视图。Each time a new state is displayed in your application, you should send a `trackState` call. For example, when a user navigates from the home page to the video details screen, send a `trackState` call. 状态通常使用路径报表来查看，以便您能够查看用户在应用程序中导航的方式以及最常查看的状态。

## trackState调用

You typically call `trackState` each time the app loads a new screen.

### Roku

```js
ADBMobile().trackState("State Name", {})
```

### Chromecast

```js
ADBMobile.analytics.trackState("State Name",{});
```

The state name is reported in the "View State" variable in Adobe Mobile services, and a view is recorded for each `trackState` call. 在其他Analytics界面中，“查看状态”报告为“页面名称”；“状态视图”报告为“页面查看”。

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
>在Adobe Mobile服务中，上下文数据值必须映射到自定义变量。

