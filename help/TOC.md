---
audience: end-user
user-guide-title: 适用于流媒体的 Adobe Analytics
breadcrumb-title: Media Analytics 指南
user-guide-description: 实施适用于流媒体的 Adobe Analytics。包括 Media SDK 和 Media Collection API。
product: adobe analytics
sub-product: Media Analytics
translation-type: tm+mt
source-git-commit: 82923f4ad4d6fd2394fe83850edca3ffd6a913ea
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 100%

---


# 适用于流媒体的 Adobe Analytics {#using}

+ [在 Adobe Analytics 中测量流媒体](media-overview.md)
+ [支持的设备和平台](measurement-options/supported-devices.md)
+ 流媒体分析简介{#intro-to-ava}
   + [先决条件](intro-to-ava/prereqs.md)
   + 实施路径 {#implementation-paths}
      + [概述](intro-to-ava/implementation-paths/implementation-paths.md)
      + [客户端](intro-to-ava/implementation-paths/client-side-path.md)
      + 其他实施路径 {#other-paths}
         + 媒体模块里程碑跟踪 {#mm-milestone-tracking}
            + [里程碑概述](measurement-options/mm-milestone-tracking/milestone-overview.md)
            + [将里程碑迁移到 Media Analytics](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
            + [从里程碑迁移到自定义链接](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
         + Analytics 中的自定义链接 {#cl-in-aa}
            + [自定义链接实施指南](measurement-options/cl-in-aa/cl-impl-guide.md)
         + Primetime {#primetime}
            + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
         + [Audience Manager 启用](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [Media Analytics SDK 支持终止常见问题解答](sdk-implement/end-of-support-faqs.md)
   + [下载 SDK](sdk-implement/download-sdks.md)
   + 安装和配置 {#setup}
      + [概述](sdk-implement/setup/setup-overview.md)
      + [设置 Android](sdk-implement/setup/set-up-android.md)
      + [设置 iOS](sdk-implement/setup/set-up-ios.md)
      + 设置 JavaScript {#setup-javascript}
         + [设置 JavaScript 2.x](sdk-implement/setup/setup-javascript/set-up-js-2.md)
         + [设置 JavaScript 3.x](sdk-implement/setup/setup-javascript/set-up-js-3.md)
      + [设置 Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [设置 Roku](sdk-implement/setup/set-up-roku.md)
   + 跟踪流媒体播放{#track-av-playback}
      + [概述](sdk-implement/track-av-playback/track-core-overview.md)
      + 跟踪核心流媒体播放{#track-core}
         + [在 Android 中跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [在 iOS 中跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + 在 JavaScript 中跟踪核心播放 {#track-core-javascript}
            + [在 JavaScript 2.x 中跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js.md)
            + [在 JavaScript 3.x 中跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-javascript/track-core-js3.md)
         + [在 Chromecast 中跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [在 Roku 中跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + 跟踪缓冲 {#track-buffering}
         + [在 Android 中跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [在 iOS 中跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + 在 JavaScript 中跟踪缓冲 {#track-buffering-js}
            + [在 JavaScript 2.x 中跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js.md)
            + [在 JavaScript 3.x 中跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-js/track-buffering-js3.md)
         + [在 Chromecast 中跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [在 Roku 中跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + 跟踪搜寻 {#track-seeking}
         + [在 Android 中跟踪搜寻](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [在 iOS 中跟踪搜寻](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + 在 JavaScript 中跟踪搜寻 {#track-seeking-js}
            + [在 JavaScript 2.x 中跟踪搜寻](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js.md)
            + [在 JavaScript 3.x 中跟踪搜寻](sdk-implement/track-av-playback/track-seeking/track-seeking-js/track-seeking-js3.md)
         + [在 Chromecast 中跟踪搜寻](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [在 Roku 中跟踪搜寻](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + 实施标准元数据 {#impl-std-metadata}
         + [在 Android 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [在 iOS 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS 元数据键](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + 在 JavaScript 中实施标准元数据 {#impl-std-md-js}
            + [在 JavaScript 2.x 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js.md)
            + [在 JavaScript 3.x 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-md-js/impl-std-metadata-js3.md)
         + [在 Chromecast 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [标准元数据参数 - Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [在 Roku 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [标准元数据参数 - Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 跟踪广告 {#track-ads}
      + [概述](sdk-implement/track-ads/track-ads-overview.md)
      + [在 Android 中跟踪广告](sdk-implement/track-ads/track-ads-android.md)
      + [在 iOS 中跟踪广告](sdk-implement/track-ads/track-ads-ios.md)
      + 在 JavaScript 中跟踪广告 {#track-ads-js}
         + [在 JavaScript 2.x 中跟踪广告](sdk-implement/track-ads/track-ads-js/track-ads-js.md)
         + [在 JavaScript 3.x 中跟踪广告](sdk-implement/track-ads/track-ads-js/track-ads-js3.md)
      + [在 Chromecast 中跟踪广告](sdk-implement/track-ads/track-ads-chromecast.md)
      + [在 Roku 中跟踪广告](sdk-implement/track-ads/track-ads-roku.md)
      + 实施标准广告元数据 {#impl-std-ad-metadata}
         + [在 Android 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [在 iOS 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + 在 JavaScript 中实施标准广告元数据 {#impl-std-ad-md-js}
            + [在 JavaScript 2.x 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js.md)
            + [在 JavaScript 3.x 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-md-js/impl-std-ad-metadata-js3.md)
         + [在 Roku 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + 跟踪章节和区段 {#track-chapters}
      + [概述](sdk-implement/track-chapters/track-chapters-overview.md)
      + [在 Android 中跟踪章节和区段](sdk-implement/track-chapters/track-chapters-android.md)
      + [在 iOS 中跟踪章节和区段](sdk-implement/track-chapters/track-chapters-ios.md)
      + 在 JavaScript 中跟踪章节和区段 {#track-chapters-js}
         + [在 JavaScript 2.x 中跟踪章节和区段](sdk-implement/track-chapters/track-chapters-js/track-chapters-js.md)
         + [在 JavaScript 3.x 中跟踪章节和区段](sdk-implement/track-chapters/track-chapters-js/track-chapters-js3.md)
      + [在 Chromecast 中跟踪章节和区段](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [在 Roku 中跟踪章节和区段](sdk-implement/track-chapters/track-chapters-roku.md)
   + 跟踪体验质量 {#track-qos}
      + [概述](sdk-implement/track-qos/track-qos-overview.md)
      + [在 Android 中跟踪体验质量](sdk-implement/track-qos/track-qos-android.md)
      + [在 iOS 中跟踪体验质量](sdk-implement/track-qos/track-qos-ios.md)
      + 在 JavaScript 中跟踪体验质量 {#track-qos-js}
         + [在 JavaScript 2.x 中跟踪体验质量](sdk-implement/track-qos/track-qos-js/track-qos-js.md)
         + [在 JavaScript 3.x 中跟踪体验质量](sdk-implement/track-qos/track-qos-js/track-qos-js3.md)
      + [在 Chromecast 中跟踪体验质量](sdk-implement/track-qos/track-qos-chromecast.md)
      + [在 Roku 中跟踪体验质量](sdk-implement/track-qos/track-qos-roku.md)
   + 跟踪错误 {#track-errors}
      + [概述](sdk-implement/track-errors/track-errors-overview.md)
      + [在 Android 中跟踪错误](sdk-implement/track-errors/track-errors-android.md)
      + [在 iOS 中跟踪错误](sdk-implement/track-errors/track-errors-ios.md)
      + 在 JavaScript 中跟踪错误 {#track-errors-js}
         + [在 JavaScript 2.x 中跟踪错误](sdk-implement/track-errors/track-errors-js/track-errors-js.md)
         + [在 JavaScript 3.x 中跟踪错误](sdk-implement/track-errors/track-errors-js/track-errors-js3.md)
      + [在 Chromecast 中跟踪错误](sdk-implement/track-errors/track-errors-chromecast.md)
      + [在 Roku 中跟踪错误](sdk-implement/track-errors/track-errors-roku.md)
   + [选择禁用和隐私](sdk-implement/opt-out-privacy.md)
   + 跟踪方案 {#tracking-scenarios}
      + [不含广告的 VOD 播放](sdk-implement/tracking-scenarios/vod-no-intrs-details.md)
      + [包含前置广告的 VOD 播放](sdk-implement/tracking-scenarios/vod-preroll-ads.md)
      + [跳过广告的 VOD 播放](sdk-implement/tracking-scenarios/vod-skipped-ads.md)
      + [包含一个章节的 VOD 播放](sdk-implement/tracking-scenarios/vod-one-chapter.md)
      + [跳过一个章节的 VOD 播放](sdk-implement/tracking-scenarios/vod-skipped-chapter.md)
      + [在主内容中进行搜寻的 VOD 播放](sdk-implement/tracking-scenarios/vod-seeking.md)
      + [带有缓冲的 VOD 播放](sdk-implement/tracking-scenarios/vod-buffering.md)
      + [多个并行的 VOD 跟踪器](sdk-implement/tracking-scenarios/vod-multi-trackers.md)
      + [一个 VOD 跟踪器用于多个会话](sdk-implement/tracking-scenarios/vod-multi-track-one-session.md)
      + [实时主内容](sdk-implement/tracking-scenarios/live-main-content.md)
      + [具有连续跟踪的实时主内容](sdk-implement/tracking-scenarios/live-sequential.md)
   + 验证 {#validation}
      + [验证概述](sdk-implement/validation/validation-overview.md)
      + [测试 1：标准播放](sdk-implement/validation/test1-standard-playback.md)
      + [测试 2：媒体中断](sdk-implement/validation/test2-media-interrupt.md)
      + [测试调用详细信息](sdk-implement/validation/test-call-details.md)
      + [心率参数描述](sdk-implement/validation/heartbeat-params.md)
      + 调试 {#debugging}
         + [SDK 调试](sdk-implement/validation/debugging/sdk-debugging.md)
         + [配置 Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [创建新的调试报告](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [调试功能板和报表](sdk-implement/validation/debugging/debug-dash-repts.md)
   + OTT 应用程序中的 Analytics{#analytics-with-ott}
      + [跟踪应用程序状态](sdk-implement/analytics-with-ott/track-app-states.md)
      + [跟踪应用程序操作](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [设置用户 ID](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT 和 Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT 和 Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + 指南 {#cookbook}
      + [SDK 指南](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [处理应用程序在播放过程中出现的中断问题](sdk-implement/cookbook/app-interrupts.md)
      + [解决在广告之间出现 main:play 的问题](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [恢复不活动的会话](sdk-implement/cookbook/resuming-inactive.md)
      + [在 SceneGraph (Roku) 中跟踪](sdk-implement/cookbook/sdk-track-scenegraph.md)
   + 从 Media Analytics 1.x 迁移到 2.x {#va-1x-to-2x}
      + [迁移概述](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [代码对比：1.x 与 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [从 1.x API 转换到 VHL 2.x API](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
   + 从 Media Analytics SDK 迁移到 Launch{#sdk-to-launch}
      + [从 SDK 迁移到 Launch](sdk-implement/sdk-to-launch/sdk-to-launch-migration.md)
      + 从 SDK 迁移到 Launch 平台指南 {#sdk-to-launch-migration-platforms}
         + [Android](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-android.md)
         + [iOS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-ios.md)
         + [JS](sdk-implement/sdk-to-launch/sdk-to-launch-migration-platforms/sdk-to-launch-migration-js.md)
+ 媒体收集 API (RESTful) {#media-collection-api}
   + [概述](media-collection-api/mc-api-overview.md)
   + API 参考 {#mc-api-ref}
      + [会话请求](media-collection-api/mc-api-ref/mc-api-sessions-req.md)
      + [事件请求](media-collection-api/mc-api-ref/mc-api-events-req.md)
      + [请求参数](media-collection-api/mc-api-ref/mc-api-req-params.md)
      + [事件类型和描述](media-collection-api/mc-api-ref/mc-api-event-types.md)
      + [JSON 验证架构](media-collection-api/mc-api-ref/mc-api-json-validation.md)
   + 实施 API {#mc-api-impl}
      + [快速启动](media-collection-api/mc-api-impl/mc-api-quick-start.md)
      + [在播放器中设置 HTTP 请求类型](media-collection-api/mc-api-impl/mc-api-set-http-req.md)
      + [获取会话 ID](media-collection-api/mc-api-impl/mc-api-obtain-sid.md)
      + [实施事件请求](media-collection-api/mc-api-impl/mc-api-impl-events-req.md)
      + [验证事件请求](media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
      + [发送 Ping 事件](media-collection-api/mc-api-impl/mc-api-sed-pings.md)
      + [发送 QoE 数据](media-collection-api/mc-api-impl/mc-api-sending-qoe.md)
      + [自定义元数据支持](media-collection-api/mc-api-impl/mc-api-custom-meta.md)
      + [超时情况](media-collection-api/mc-api-impl/mc-api-timeout.md)
      + [控制事件的顺序](media-collection-api/mc-api-impl/mc-api-ctrl-order.md)
      + [会话响应缓慢时对事件进行排队](media-collection-api/mc-api-impl/mc-api-queuing.md)
   + 媒体跟踪时间轴 {#mc-api-timelines}
      + [时间轴 1 - 观看到内容的结尾](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [时间轴 2 - 用户放弃会话](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [时间轴 3 - 章节](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
+ 指南 {#media-analytics-cookbook}
   + [指南](media-analytics-cookbook/media-analytics-cookbook.md)
   + [媒体流归因](media-analytics-cookbook/media-dimensions.md)
+ 量度和元数据 {#metrics-and-metadata}
   + [流媒体参数](metrics-and-metadata/audio-video-parameters.md)
   + [广告参数](metrics-and-metadata/ad-parameters.md)
   + [章节参数](metrics-and-metadata/chapter-parameters.md)
   + [播放器状态参数](metrics-and-metadata/player-state-parameters.md)
   + [质量参数](metrics-and-metadata/quality-parameters.md)
   + [区段](metrics-and-metadata/segments.md)
   + [计算量度](metrics-and-metadata/calculated-metrics.md)
+ 报表和分析 {#media-reports}
   + [媒体报表启用](media-reports/media-reports-enable.md)
   + 媒体默认报表 {#media-default-reports}
      + [默认报表概述](media-reports/media-default-reports/default-reports-overview.md)
      + [媒体概览](media-reports/media-default-reports/media-reports-overview.md)
      + [媒体详细信息](media-reports/media-default-reports/media-reports-detail.md)
      + [“媒体时段”报表](media-reports/media-default-reports/media-reports-daypart.md)
      + [“媒体并行查看者”报表](media-reports/media-default-reports/media-concurrent-viewers.md)
   + 媒体工作区面板{#media-workspace-panels}
      + [“媒体并行查看者”面板](media-reports/media-workspace-panels/media-concurrent-viewers.md)
   + [媒体工作区模板](media-reports/media-workspace-templates.md)
   + [通过 API 获取并行查看者数据](media-reports/media-default-reports/get-concurrent-json20.md)
+ [跟踪下载的内容](media-collection-api/track-downloaded-content.md)
+ 播放器状态跟踪 {#player-state-tracking}
   + [概述](sdk-implement/player-state-tracking/player-state-overview.md)
   + [标准状态和自定义状态](sdk-implement/player-state-tracking/standard-and-custom-states.md)
   + [实施与报表](sdk-implement/player-state-tracking/implementation-and-reporting.md)
   + [播放器状态跟踪示例](sdk-implement/player-state-tracking/player-state-examples.md)
+ [Federated Analytics](federated-analytics.md)
<!-- + Player State Tracking {#player-state-tracking}
    + [Overview](sdk-implement/player-state-tracking/player-state-overview.md)
    + [Standard and custom states](sdk-implement/player-state-tracking/standard-and-custom-states.md)
    + [Implementation and reporting](sdk-implement/player-state-tracking/implementation-and-reporting.md)
    + [Player state tracking examples](sdk-implement/player-state-tracking/player-state-examples.md) -->
+ 其他资源 {#additional-resources}
   + [发行说明](additional-resources/doc-updates.md)
