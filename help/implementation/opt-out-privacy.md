---
title: 选择禁用和隐私设置
description: 了解如何处理选择启用、选择禁用和隐私。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/eF09wxu2mIUoFph5EdHz5y0XtcpXHHLINqSGLQEMoHU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 8b9e7582923a61bd2a43049a02ce36727a677e17
workflow-type: tm+mt
source-wordcount: 798
ht-degree: 3%

---

# 选择禁用和隐私设置

当用户选择退出跟踪时，流媒体库会立即停止所有数据收集活动。 对于该用户，不会发生会话开始调用、心率ping以及事件跟踪数据被发送到Adobe数据收集服务器。

## 选择禁用/选择启用

选择退出控件按设备或浏览器运行。 尊重用户同意是实施组织的责任。 有关Adobe隐私实践的概述，请参阅[Adobe隐私中心](https://www.adobe.com/cn/privacy.html)。

## 建议的实施类型

>[!BEGINTABS]

>[!TAB Web SDK]

Web SDK尊重使用`setConsent`命令设置的同意首选项。 当同意设置为`"out"`时，Web SDK将停止将所有事件（包括流媒体跟踪调用）转发到Edge Network。 会话之间的同意状态会保留在浏览器存储中。

在实施选择退出之前，请确保为您的Web SDK配置了流媒体组件。 有关详细信息，请参阅[设置Web SDK](../implementation/edge/web-sdk.md)。

使用Adobe 2.0同意标准将同意设置为选择退出：

```javascript
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: { val: "n" }
    }
  }]
});
```

同意值：

* `"y"`：已选择加入（允许数据收集）
* `"n"`：已选择退出（已禁止数据收集）
* `"p"`：待定（等待用户决定；在解析之前不收集任何数据）

要恢复跟踪，请再次调用`setConsent`，并将`"y"`作为`collect.val`值。

有关其他格式（包括IAB TCF 2.0），请参阅Web SDK文档中的[setConsent命令](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/commands/setconsent)。

>[!TAB iOS]

Adobe Experience Platform Mobile SDK尊重使用`MobileCore.setPrivacyStatus()`设置的隐私状态。 将状态设置为`.optedOut`会禁止在所有AEP扩展（包括流媒体）中进行所有数据收集。 状态会在应用程序会话之间保留。

```swift
MobileCore.setPrivacyStatus(.optedOut)
```

要恢复跟踪，请将隐私状态设置回`.optedIn`：

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

有关详细信息，请参阅AEP Mobile SDK文档中的[隐私和GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)。

>[!TAB Android]

Adobe Experience Platform Mobile SDK尊重使用`MobileCore.setPrivacyStatus()`设置的隐私状态。 将状态设置为`MobilePrivacyStatus.OPT_OUT`会禁止在所有AEP扩展（包括流媒体）中进行所有数据收集。 状态会在应用程序会话之间保留。

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT)
```

要恢复跟踪，请将隐私状态设置回`MobilePrivacyStatus.OPT_IN`：

```kotlin
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_IN)
```

有关详细信息，请参阅AEP Mobile SDK文档中的[隐私和GDPR](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/#setprivacystatus)。

>[!TAB Roku Edge]

Roku Edge SDK使用`setConsent()`和Adobe 2.0同意标准。 将`collect.val`设置为`"n"`会立即停止所有数据收集，包括流媒体事件。

同意值：

* `"y"`：已选择加入（允许数据收集）
* `"n"`：已选择退出（已禁止数据收集）
* `"p"`：待定（等待用户决定；在解析之前不收集任何数据）

```brightscript
currentDate = CreateObject("roDateTime")
timestampInISO8601 = currentDate.ToISOString("milliseconds")

collectConsentNo = {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "metadata": { "time": timestampInISO8601 },
      "collect": { "val": "n" }
    }
  }]
}

m.aepSdk.setConsent(collectConsentNo)
```

要恢复跟踪，请将`collect.val`设置为`"y"`并再次调用`setConsent()`。

您还可以使用带有`ADB_CONSTANTS.CONFIGURATION.CONSENT_DEFAULT`密钥的`updateConfiguration()`在SDK初始化时设置默认同意值。 有关详细信息，请参阅[Roku Edge SDK文档](https://github.com/adobe/aepsdk-roku)。

>[!TAB Media Edge API]

Media Edge API是一种服务器端实施。 没有任何SDK层会自动强制同意 — 您的应用程序必须先检查用户同意状态，然后才能进行任何API调用并禁止选择退出用户的请求。

对于完全选择退出，对于已选择退出的用户，请勿在`/va/v2/sessions`端点（或任何后续事件端点）执行POST操作：

```javascript
// Check consent status before initiating a media session
if (userHasOptedOut) {
  // Do not call the Media Edge API
  return;
}

// Only call the API for users who have not opted out
fetch("https://edge.adobedc.net/va/v2/sessions", {
  method: "POST",
  body: JSON.stringify(sessionStartPayload)
});
```

有关详细信息，请参阅[Media Edge API引用](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/)。

>[!ENDTABS]

## 旧版实施类型（仅限Analytics）

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Media SDK JS 3.x库将遵循Adobe访客API(Identity Service)选择退出状态。 当用户选择退出使用访客API时，Media SDK会自动隐藏所有跟踪调用。

```javascript
var visitor = Visitor.getInstance("YOUR_ORG_ID@AdobeOrg");
visitor.setOptOut(true);
```

将`YOUR_ORG_ID@AdobeOrg`替换为Adobe Admin Console中的组织ID。

要恢复跟踪，请将`false`传递给`setOptOut()`。

有关详细信息，请参阅[Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)。

>[!TAB Chromecast]

Chromecast Media SDK 3.x尊重使用`ADBMobile.config.setPrivacyStatus()`设置的隐私状态。 将状态设置为`PRIVACY_STATUS_OPT_OUT`会禁止所有数据收集。

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT);
```

要恢复跟踪，请将状态重新设置为opted in ：

```javascript
ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN);
```

您还可以在初始化`ADBMobileConfig`对象的SDK时设置默认隐私状态：

```javascript
var ADBMobileConfig = {
  "analytics": {
    "privacyDefault": "optedout"
  }
};
```

>[!TAB Roku 2.x]

Roku 2.x SDK尊重使用`setPrivacyStatus`设置的隐私状态。 将状态设置为`PRIVACY_STATUS_OPT_OUT`会禁止所有数据收集。

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_OUT)
```

要恢复跟踪，请将状态重新设置为opted in ：

```brightscript
adb = ADBMobile()
adb.setPrivacyStatus(adb.PRIVACY_STATUS_OPT_IN)
```

您还可以在`ADBMobileConfig.json`文件中的SDK初始化时设置默认隐私状态：

```json
"analytics": {
  "privacyDefault": "optedout"
}
```

>[!TAB 媒体收集API]

媒体收集API是服务器端实施。 应用程序必须先检查用户同意状态，然后才能进行API调用并禁止选择退出的用户请求。

对于完全选择退出，请勿对已选择退出的用户的会话端点执行POST操作。

对于CCPA下的部分选择退出，请在`sessionStart`请求的`params`对象中包含选择退出标记：

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "analytics.optOutServerSideForwarding": true,
    "analytics.optOutShare": true
  }
}
```

* `analytics.optOutServerSideForwarding`：设置为`true`可选择在Adobe Analytics与其他Experience Cloud解决方案（如Audience Manager）之间共享数据。
* `analytics.optOutShare`：设置为`true`可选择不与其他Adobe Analytics客户端共享联合数据。

有关可用参数的完整列表，请参阅[媒体收集API请求参数引用](../implementation/media-collection-api/mc-api-ref/mc-api-req-params.md)。

>[!ENDTABS]
