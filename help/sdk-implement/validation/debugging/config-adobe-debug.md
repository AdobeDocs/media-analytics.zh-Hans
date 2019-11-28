---
title: 配置 Adobe Debug
description: 本主题介绍如何配置 Adobe Debug，以便用于对 Media SDK 实施进行故障诊断。
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 配置 Adobe Debug{#configure-adobe-debug}

## 访问 Adobe Debug {#accessing-adobe-debug}

要访问 Adobe Debug，请执行以下操作：

1. 转到 [Experience Cloud](https://www.marketing.adobe.com) 并创建新的 Adobe Experience Cloud 用户。

   >[!TIP]
   >
   >此登录不是您用来登录到 Adobe Analytics 的相同用户名/密码。

1. 拥有 Experience Cloud 帐户后，请与 Adobe 代表联系以请求访问 Adobe Debug。
1. 获得访问权限后，请转到 [https://debug.adobe.com](https://debug.adobe.com) 并使用 Experience Cloud 凭据登录。

   ![](assets/adobe-debug-login.png)

   此工具支持的浏览器如下：
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 版本 9-11

推荐的浏览器是最新版本的 Chrome 和 Firefox。

## Debug Proxy {#debug-proxy}

要下载并配置 Debug Proxy，请执行以下操作：

1. 在[应用程序下载](https://debug.adobe.com/#/downloads)页面下载 Debug Proxy 应用程序。

   支持的操作系统如下：
   * OS X 10.7 64 位或更高版本
   * Windows 7.1 64 位或更高版本
   ![](assets/debug-proxy-app.png)

1. Debug Proxy 服务器将在本地计算机的端口 33284 上运行，并且将被设置为系统代理。

   您可能需要根据操作系统和浏览器来调整浏览器设置。

## 在桌面或应用程序中下载并安装 SSL 证书 {#download-and-install-sSL-desktop}

第一次运行 Adobe Debug 时，将生成唯一的 SSL 证书。如果您支持跨桌面和/或应用程序的 HTTPS 通信，则需要下载并安装 SSL 证书。

要下载并安装 SSL 证书，请执行以下操作：

1. 安装并启动 Adobe Debug 后，转到 [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl) 并下载证书。
1. 导入证书

   **Mac OS**
   1. 双击根 CA 证书以在“钥匙串访问”中将其打开。
   1. 根 CA 证书会出现在登录中。
   1. 将根 CA 证书移动（拖动）到 System。
   1. 您必须将证书复制到系统中，以确保所有用户和本地系统进程都信任该证书。
   1. 打开根 CA 证书，展开“信任”，选择“始终信任”并保存更改。
   **Windows**
   1. 完成以下过程之一：

      * [将证书添加到本地计算机的“受信任的根证书颁发机构”存储区中](https://technet.microsoft.com/zh-cn/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. 对于 Firefox，请完成 [在 Mozilla Firefox 中安装根证书中的步骤。](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox) 
    
    您可能需要退出 Firefox 后重新将其打开才能看到所做的更改。
    
    **iOS 设备**
    1. 通过单击 **[!UICONTROL 设置应用程序]** **&gt;** **[!UICONTROL Wifi 设置]**，将 iOS 设备设置为使用 Adobe Debug 作为其 HTTP 代理。
    
    1. 在 Safari 中，转到 [Debug。](https://proxy.debug.adobe.com/ssl)
    
    Safari 将提示您安装 SSL 证书。

## 为移动设备安装 SSL 证书 {#install-sSL-for-mobile-device}

如果在 Adobe Debug 中缺少 HTTPS 调用，则必须在移动设备上安装适用于 Adobe Debug 的 SSL 证书。

### iOS

要在 iOS 设备上安装 SSL 证书，请执行以下操作：

1. 在笔记本电脑上，打开 Debug Proxy，然后转到 [Adobe Debug](https://debug.adobe.com)。
1. 在 iOS 设备上完成以下步骤：
   1. 将设备转换到飞行模式。
   1. 选择笔记本电脑所使用的相同 Wi-Fi 信号。
   1. 在笔记本电脑上，手动设置 Debug Proxy 应用程序中显示的 IP 和端口。
   1. 打开 Apple Safari 浏览器窗口。
   1. 转到 [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)。
   1. 下载并安装 SSL 证书。

1. 在笔记本电脑上，启动 Adobe Debug 会话。
1. 在 iOS 设备上开始测试。

### Android

要在 Android 设备上安装 SSL 证书，请执行以下操作：

1. 在笔记本电脑上，打开 Debug Proxy，然后转到 [Adobe Debug](https://debug.adobe.com)。
1. 在 Android 设备上完成以下步骤：
   1. 将您的设备设置为飞行模式。
   1. 选择笔记本电脑所使用的相同 Wi-Fi 信号。
   1. 在笔记本电脑上，手动设置 Debug Proxy 应用程序中显示的 IP 和端口。
   1. 打开浏览器窗口。
   1. 转到 [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)。
   1. 下载并安装 SSL 证书。

1. 在笔记本电脑上，启动 Adobe Debug 会话。
1. 在 Android 设备上开始测试。

