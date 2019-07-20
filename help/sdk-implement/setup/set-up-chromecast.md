---
seo-title: 设置 Chromecast
title: 设置 Chromecast
uuid: d664e394-02a2-4985-bug-be1 bcc44 fb2 b
translation-type: tm+mt
source-git-commit: bb3a303edba724c8f444d612b3be9d7250eea363

---


# 设置 Chromecast{#set-up-chromecast}

## 常见问题解答

_我应该使用 Chromecast JavaScript SDK 还是标准 JavaScript SDK？_

正确的答案是“Chromecast”，原因如下：
* 标准 JS SDK 中的 AppMeasurement 和 VisitorAPI 库未经过认证，无法在 OTT 平台上运行。在 Chromecast JS SDK 中，视频心率库 (VHL)、Analytics 和 VisitorAPI 都内置于单个、统一且经过 Chromecast 认证的 SDK 中。
* Chromecast SDK 比标准 JS SDK 要简便得多。对于 OTT 平台所使用的较低端硬件来说，这一点非常关键。

## 先决条件

* **获得HeartBeats的有效配置参数**&#x200B;在设置媒体分析帐户之后，可以从Adobe代表获得这些参数。
* **在媒体播放器中提供以下功能：**
   * *可订阅播放器事件的 API -* Media SDK 要求您在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* - 此信息包括媒体名称和播放头位置等详细信息。

Adobe Mobile Services 提供了新的用户界面，以整合 Adobe Marketing Cloud 中针对移动设备应用程序的移动营销功能。最初，Mobile 服务无缝集成了 Adobe Analytics 和 Adobe Target 解决方案的应用程序分析和目标定位功能。Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

适用于 Experience Cloud 解决方案的 Chromecast SDK 2.x 让您能够测量使用 JavaScript 编写的 Chromecast 应用程序，通过受众管理收集并利用受众数据，以及通过视频心率测量视频参与。

## SDK 实施

1. 将[下载](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)的 Chromecast 库添加到您的项目中。

   1. `AdobeMobileLibrary-Chromecast-[version]` zip 文件包含以下软件组件：

      * `adbmobile-chromecast.min.js`：

         此库文件将包含在您的 Chromecast 应用程序源文件夹中。

      * `ADBMobileConfig` config

         这是为您的应用程序自定义的 SDK 配置文件。随 SDK 提供了一个 `ADBMobileConfig` 实施示例（在 `samples/` / 下）。请从 Adobe 代表处获取正确的设置。
   1. 将库文件添加到 `index.html` 文件中，并按照以下方式创建 `ADBMobileConfig` 全局变量（用于配置 Adobe Mobile for Heartbeats 的全局变量具有一个名为 `mediaHeartbeat` 的排他键）：

      ```js
      <script> 
          var ADBMobileConfig = { 
            "marketingCloud": { 
              "org": "972C898555E9F7BC7F000101@AdobeOrg" 
            }, 
            "target": { 
              "clientCode": "", 
              "timeout": 5 
            }, 
            "audienceManager": { 
              "server": "obumobile5.demdex.net" 
            }, 
            "analytics": { 
              "rsids": "mobile5vhl.sample.player", 
              "server": "obumobile5.sc.omtrdc.net", 
              "ssl": false, 
              "offlineEnabled": false, 
              "charset": "UTF-8", 
              "lifecycleTimeout": 300, 
              "privacyDefault": "optedin", 
              "batchLimit": 0, 
              "timezone": "MDT", 
              "timezoneOffset": -360, 
              "referrerTimeout": 0, 
              "poi": [] 
            }, 
            "mediaHeartbeat": { 
              "server": "obumobile5.hb.omtrdc.net", 
              "publisher": "972C898555E9F7BC7F000101@AdobeOrg", 
              "channel": "test-channel-chromecast", 
              "ssl": false, 
              "ovp": "chromecast-player", 
              "sdkVersion": "chromecast-sdk", 
              "playerName": "Chromecast" 
            } 
          }; 
        </script> 
      <script type="text/javascript" src="script/lib/adbmobile-chromecast.min.js"></script>
      ```

      >[!IMPORTANT]
      >
      >`mediaHeartbeat` 如果配置错误，媒体模块(VHL)输入错误状态，并将停止发送跟踪调用。

      mediaHeartbeat 键的 ADBMobile 配置参数：
   | 配置参数 | 描述     |
   | --- | --- |
   | `server` | 表示后端跟踪端点的 URL 的字符串。 |
   | `publisher` | 表示内容发布者唯一标识符的字符串。 |
   | `channel` | 表示内容分发渠道名称的字符串。 |
   | `ssl` | 布尔值，表示是否应使用 SSL 来跟踪调用。 |
   | `ovp` | 表示视频播放器提供程序名称的字符串。 |
   | `sdkversion` | 表示应用程序/SDK 当前版本的字符串。 |
   | `playerName` | 表示播放器名称的字符串。 |


1. 配置 Experience Cloud 访客 ID。

   Experience Cloud 访客 ID 服务可以跨多个 Experience Cloud 解决方案提供一个通用的访客 ID。访客 ID 服务是视频心率和其他 Marketing Cloud 集成所必需的。

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```js
   "marketingCloud": { 
       "org": YOUR-MCORG-ID" 
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   配置完成后，将生成一个 Experience Cloud 访客 ID，并将其包含在所有点击中。Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud 访客 ID 服务方法**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   | 方法 | 描述 |
   | --- | --- |
   | `getMarketingCloudID()` | Retrieves the Experience Cloud Visitor ID from the Visitor ID service.  <br/><br/>`ADBMobile.visitor.getMarketingCloudID();` |
   | `syncIdentifiers()` | 除了 Experience Cloud 访客 ID 之外，您还可以设置其他与每个访客关联的客户 ID。访客 API 接受同一访客具有多个客户 ID，并且使用客户类型标识符区分不同客户 ID 的适用范围。此方法对应于 JavaScript 库中的 `setCustomerIDs()`。For example: <br/><br/>`var identifiers = {};` <br/><br/>`identifiers["idType"] = "idValue";` <br/><br/>`ADBMobile.visitor.syncIdentifiers(identifiers);` |


<!--   **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->

