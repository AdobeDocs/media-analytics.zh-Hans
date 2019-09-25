---
seo-title: 配置 Adobe Debug
title: 配置 Adobe Debug
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: tm+mt
source-git-commit: 5ff3566fae2c1df559341057fafdd289774e4b2f

---


# 配置 Adobe Debug{#configure-adobe-debug}

## 访问 Adobe Debug {#section_AF81E7AD331E41FFA371AB9DA924BFBB}

要访问 Adobe Debug，请执行以下操作：

1. Go to [Experience Cloud](https://www.marketing.adobe.com) and create a new Adobe Experience Cloud user.

   >[!TIP]
   >
   >此登录名与用于登录Adobe Analytics的用户名／密码不同。

1. 拥有 Experience Cloud 帐户后，请与 Adobe 代表联系以请求访问 Adobe Debug。
1. After access has been granted, go to [https://debug.adobe.com](https://debug.adobe.com) and use your Experience Cloud credentials to log in.

   ![](assets/adobe-debug-login.png)

   此工具支持的浏览器如下：
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 版本 9-11

推荐的浏览器是最新版本的 Chrome 和 Firefox。

## Debug Proxy {#section_8D3493B8426B46DEB9CD7E2ABD785D66}

下载并配置调试代理：

1. Download the Debug Proxy app at [App Downloads.](https://debug.adobe.com/#/downloads)

   支持的操作系统如下：
   * OS X 10.7 64 位或更高版本
   * Windows 7.1 64 位或更高版本
   ![](assets/debug-proxy-app.png)

1. Debug Proxy 服务器将在本地计算机的端口 33284 上运行，并且将被设置为系统代理。

   您可能需要根据操作系统和浏览器来调整浏览器设置。

## 在桌面或应用程序中下载并安装 SSL 证书 {#section_2F9547E301CB413299A67BD59AFBEE0D}

第一次运行 Adobe Debug 时，将生成唯一的 SSL 证书。如果您支持跨桌面和/或应用程序的 HTTPS 通信，则需要下载并安装 SSL 证书。

Download and install the SSL certificate:

1. After Adobe Debug has been installed and started, go to [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) and download the certification.
1. 导入证书

   **Mac OS**
   1. 双击根 CA 证书以在“钥匙串访问”中将其打开。
   1. 根 CA 证书会出现在登录中。
   1. 将根 CA 证书移动（拖动）到 System。
   1. 您必须将证书复制到系统中，以确保所有用户和本地系统进程都信任该证书。
   1. 打开根 CA 证书，展开“信任”，选择“始终信任”并保存更改。
   **Windows**
   1. 完成以下过程之一：

      * [将证书添加到本地计算机的“受信任的根证书颁发机构”存储区中](https://technet.microsoft.com/en-us/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. 对于Firefox，请完成[在Mozilla Firefox中安装根证书中的过程。](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)您
    
    可能需要退出并重新打开Firefox才能看到更改。
    
    **iOS devices**1. 
    Set your iOS device to use Adobe Debug as its HTTP proxy by clicking **[!UICONTROL Settings app]** **&gt;** **[!UICONTROL Wifi settings]**.
    
    1. 在Safari中，转到[调试]。](https://proxy.debug.adobe.com/ssl)
    
    Safari将提示您安装SSL证书。

## 为移动设备安装 SSL 证书 {#section_F2A3336F482C43E2ABEA742AD5CCACCA}

如果在 Adobe Debug 中缺少 HTTPS 调用，则必须在移动设备上安装适用于 Adobe Debug 的 SSL 证书。

### iOS

要在 iOS 设备上安装 SSL 证书，请执行以下操作：

1. On your laptop, turn on the Debug Proxy, and go to [Adobe Debug.](https://debug.adobe.com)
1. 在 iOS 设备上完成以下步骤：
   1. 将设备转换到飞行模式。
   1. 选择笔记本电脑所使用的相同 Wi-Fi 信号。
   1. 在笔记本电脑上，手动设置 Debug Proxy 应用程序中显示的 IP 和端口。
   1. 打开 Apple Safari 浏览器窗口。
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. 下载并安装 SSL 证书。

1. 在笔记本电脑上，启动 Adobe Debug 会话。
1. 在 iOS 设备上开始测试。

### Android

要在 Android 设备上安装 SSL 证书，请执行以下操作：

1. On your laptop turn on the Debug Proxy and go to [Adobe Debug.](https://debug.adobe.com)
1. 在 Android 设备上完成以下步骤：
   1. 将您的设备设置为飞行模式。
   1. 选择笔记本电脑所使用的相同 Wi-Fi 信号。
   1. 在笔记本电脑上，手动设置 Debug Proxy 应用程序中显示的 IP 和端口。
   1. 打开浏览器窗口。
   1. Go to [https://proxy.debug.adobe.com/ssl.](https://proxy.debug.adobe.com/ssl)
   1. 下载并安装 SSL 证书。

1. 在笔记本电脑上，启动 Adobe Debug 会话。
1. 在 Android 设备上开始测试。

