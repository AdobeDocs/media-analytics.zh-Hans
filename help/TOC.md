---
product: Media Analytics
audience: 最终用户
user-guide-title: Adobe Analytics for Audio和Video
translation-type: tm+mt
source-git-commit: 1f9fe870b906246c3959eead2d23301f9a64f99c

---


# Adobe Analytics for Audio and Video {#using}

+ [在Adobe Analytics中测量音频和视频](media-overview.md)
+ Measurement Options {#measurement-options}
   + Media Module Milestone Tracking {#mm-milestone-tracking}
      + [里程碑概述](measurement-options/mm-milestone-tracking/milestone-overview.md)
      + [将里程碑迁移到媒体分析](measurement-options/mm-milestone-tracking/migrate-ms-to-va.md)
      + [从里程碑迁移到自定义链接](measurement-options/mm-milestone-tracking/migrate-ms-to-cl.md)
   + Analytics 中的自定义链接 {#cl-in-aa}
      + [自定义链接实施指南](measurement-options/cl-in-aa/cl-impl-guide.md)
+ 音频和视频分析简介 {#intro-to-ava}
   + [先决条件](intro-to-ava/prereqs.md)
   + 实施路径 {#implementation-paths}
      + [概述](intro-to-ava/implementation-paths/implementation-paths.md)
      + [客户端](intro-to-ava/implementation-paths/client-side-path.md)
      + [Adobe Experience Platform Launch](intro-to-ava/implementation-paths/launch-path.md)
      + [Primetime](intro-to-ava/implementation-paths/primetime-path.md)
   + [Audience Manager 启用](intro-to-ava/am-enablement.md)
+ Media Analytics SDK {#sdk-implement}
   + [下载 SDK](sdk-implement/download-sdks.md)
   + 安装和配置 {#setup}
      + [概述](sdk-implement/setup/setup-overview.md)
      + [设置 Android](sdk-implement/setup/set-up-android.md)
      + [设置 iOS](sdk-implement/setup/set-up-ios.md)
      + [设置 JavaScript](sdk-implement/setup/set-up-js.md)
      + [设置 Chromecast](sdk-implement/setup/set-up-chromecast.md)
      + [设置 Roku](sdk-implement/setup/set-up-roku.md)
   + 跟踪音频和视频播放 {#track-av-playback}
      + [概述](sdk-implement/track-av-playback/track-core-overview.md)
      + Track Core Audio and Video Playback {#track-core}
         + [在Android上跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-android.md)
         + [在iOS上跟踪核心播放](sdk-implement/track-av-playback/track-core/track-core-ios.md)
         + [在JavaScript上跟踪核心回放](sdk-implement/track-av-playback/track-core/track-core-js.md)
         + [在Chromecast上跟踪核心回放](sdk-implement/track-av-playback/track-core/track-core-chromecast.md)
         + [在Roku上跟踪核心回放](sdk-implement/track-av-playback/track-core/track-core-roku.md)
      + Track Buffering {#track-buffering}
         + [在Android上跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-android.md)
         + [在iOS上跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-ios.md)
         + [在JavaScript上跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-js.md)
         + [Chromecast上的跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-chromecast.md)
         + [在Roku上跟踪缓冲](sdk-implement/track-av-playback/track-buffering/track-buffering-roku.md)
      + Track Seeking {#track-seeking}
         + [在Android上跟踪搜索](sdk-implement/track-av-playback/track-seeking/track-seeking-android.md)
         + [在iOS上跟踪搜索](sdk-implement/track-av-playback/track-seeking/track-seeking-ios.md)
         + [在JavaScript上跟踪搜索](sdk-implement/track-av-playback/track-seeking/track-seeking-js.md)
         + [Chromecast上的跟踪搜索](sdk-implement/track-av-playback/track-seeking/track-seeking-chromecast.md)
         + [在Roku上搜索音轨](sdk-implement/track-av-playback/track-seeking/track-seeking-roku.md)
      + 实施标准元数据{#impl-std-metadata}
         + [在 Android 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-android.md)
         + [在 iOS 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-ios.md)
         + [iOS元数据密钥](sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
         + [在 JavaScript 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-js.md)
         + [在 Chromecast 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-chromecast.md)
         + [标准元数据参数- Chromecast](sdk-implement/track-av-playback/impl-std-metadata/chromecast-metadata.md)
         + [在 Roku 中实施标准元数据](sdk-implement/track-av-playback/impl-std-metadata/impl-std-metadata-roku.md)
         + [标准元数据参数- Roku](sdk-implement/track-av-playback/impl-std-metadata/roku-metadata.md)
   + 跟踪广告 {#track-ads}
      + [概述](sdk-implement/track-ads/track-ads-overview.md)
      + [在Android上跟踪广告](sdk-implement/track-ads/track-ads-android.md)
      + [在iOS上跟踪广告](sdk-implement/track-ads/track-ads-ios.md)
      + [在JavaScript上跟踪广告](sdk-implement/track-ads/track-ads-js.md)
      + [在Chromecast上跟踪广告](sdk-implement/track-ads/track-ads-chromecast.md)
      + [在Roku上跟踪广告](sdk-implement/track-ads/track-ads-roku.md)
      + 实施标准广告元数据 {#impl-std-ad-metadata}
         + [在 Android 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
         + [在 iOS 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
         + [在 JavaScript 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-js.md)
         + [在 Roku 中实施标准广告元数据](sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   + 跟踪章节和区段 {#track-chapters}
      + [概述](sdk-implement/track-chapters/track-chapters-overview.md)
      + [在Android上跟踪章节和细分](sdk-implement/track-chapters/track-chapters-android.md)
      + [在iOS上跟踪章节和细分](sdk-implement/track-chapters/track-chapters-ios.md)
      + [在JavaScript上跟踪章节和细分](sdk-implement/track-chapters/track-chapters-js.md)
      + [在Chromecast上跟踪章节和细分](sdk-implement/track-chapters/track-chapters-chromecast.md)
      + [在Roku上跟踪章节和细分](sdk-implement/track-chapters/track-chapters-roku.md)
   + 跟踪体验质量 {#track-qos}
      + [概述](sdk-implement/track-qos/track-qos-overview.md)
      + [在Android上跟踪体验质量](sdk-implement/track-qos/track-qos-android.md)
      + [在iOS上跟踪体验质量](sdk-implement/track-qos/track-qos-ios.md)
      + [在JavaScript上跟踪体验质量](sdk-implement/track-qos/track-qos-js.md)
      + [Chromecast的体验跟踪质量](sdk-implement/track-qos/track-qos-chromecast.md)
      + [跟踪Roku上的体验质量](sdk-implement/track-qos/track-qos-roku.md)
   + Track Errors {#track-errors}
      + [概述](sdk-implement/track-errors/track-errors-overview.md)
      + [在Android上跟踪错误](sdk-implement/track-errors/track-errors-android.md)
      + [在iOS上跟踪错误](sdk-implement/track-errors/track-errors-ios.md)
      + [在JavaScript上跟踪错误](sdk-implement/track-errors/track-errors-js.md)
      + [Chromecast上的跟踪错误](sdk-implement/track-errors/track-errors-chromecast.md)
      + [Roku上的跟踪错误](sdk-implement/track-errors/track-errors-roku.md)
   + [选择退出和隐私](sdk-implement/opt-out-privacy.md)
   + Tracking Scenarios {#tracking-scenarios}
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
      + [测试2:媒体中断](sdk-implement/validation/test2-media-interrupt.md)
      + [测试呼叫详细信息](sdk-implement/validation/test-call-details.md)
      + [心率参数描述](sdk-implement/validation/heartbeat-params.md)
      + 调试 {#debugging}
         + [SDK调试](sdk-implement/validation/debugging/sdk-debugging.md)
         + [配置 Adobe Debug](sdk-implement/validation/debugging/config-adobe-debug.md)
         + [创建新的调试报告](sdk-implement/validation/debugging/create-new-debug-report.md)
         + [调试功能板和报表](sdk-implement/validation/debugging/debug-dash-repts.md)
   + Analytics in OTT Apps {#analytics-with-ott}
      + [跟踪应用程序状态](sdk-implement/analytics-with-ott/track-app-states.md)
      + [跟踪应用程序操作](sdk-implement/analytics-with-ott/track-app-actions.md)
      + [设置用户ID](sdk-implement/analytics-with-ott/set-user-ids.md)
      + [OTT 和 Audience Manager](sdk-implement/analytics-with-ott/ott-am.md)
      + [OTT 和 Experience Cloud](sdk-implement/analytics-with-ott/ott-experience-cloud.md)
   + 操作指南 {#cookbook}
      + [SDK说明书](sdk-implement/cookbook/sdk-cookbook-overview.md)
      + [处理应用程序在播放过程中出现的中断问题](sdk-implement/cookbook/app-interrupts.md)
      + [解决在广告之间出现 main:play 的问题](sdk-implement/cookbook/fix-ad-play-ad.md)
      + [恢复非活动会话](sdk-implement/cookbook/resuming-inactive.md)
      + [在 SceneGraph (Roku) 中跟踪](sdk-implement/cookbook/sdk-track-scenegraph.md)
      + [SDK和启动差异](sdk-implement/cookbook/sdk-vs-launch-qoe.md)
   + Media Analytics 1.x to 2.x Migration {#va-1x-to-2x}
      + [迁移概述](sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
      + [代码对比：1.x 与 2.x](sdk-implement/va-1x-to-2x/code-comparison-1x-2x.md)
      + [从 1.x API 转换到 VHL 2.x API](sdk-implement/va-1x-to-2x/1x-2x-api-change.md)
+ Media Collection API(RESTful) {#media-collection-api}
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
   + Media Tracking Timelines {#mc-api-timelines}
      + [时间轴 1 - 观看到内容的结尾](media-collection-api/mc-api-timelines/mc-api-timeline-1.md)
      + [时间轴 2 - 用户放弃会话](media-collection-api/mc-api-timelines/mc-api-timeline-2.md)
      + [时间轴 3 - 章节](media-collection-api/mc-api-timelines/mc-api-timeline-3.md)
   + [跟踪下载的内容](media-collection-api/track-downloaded-content.md)
+ 操作指南 {#media-analytics-cookbook}
   + [说明书概述](media-analytics-cookbook/cookbook-overview.md)
   + [媒体跟踪之外的媒体维度](media-analytics-cookbook/media-dimensions.md)
+ 量度和元数据 {#metrics-and-metadata}
   + [音频和视频参数](metrics-and-metadata/audio-video-parameters.md)
   + [广告参数](metrics-and-metadata/ad-parameters.md)
   + [章节参数](metrics-and-metadata/chapter-parameters.md)
   + [质量参数](metrics-and-metadata/quality-parameters.md)
   + [区段](metrics-and-metadata/segments.md)
   + [计算量度](metrics-and-metadata/calculated-metrics.md)
+ Reporting and Analysis {#media-reports}
   + [启用媒体报告](media-reports/media-reports-enable.md)
   + Media Default Reports {#media-default-reports}
      + [默认报告概述](media-reports/media-default-reports/default-reports-overview.md)
      + [媒体概览](media-reports/media-default-reports/media-reports-overview.md)
      + [媒体详细信息](media-reports/media-default-reports/media-reports-detail.md)
      + [媒体时段](media-reports/media-default-reports/media-reports-daypart.md)
      + [媒体并行查看者](media-reports/media-default-reports/media-concurrent-viewers.md)
      + [获取并行查看者 JSON 报表数据](media-reports/media-default-reports/get-concurrent-json.md)
   + [媒体工作区模板](media-reports/media-workspace-templates.md)
+ [Federated Analytics](federated-analytics.md)
+ 其他资源 {#additional-resources}
   + [资源](additional-resources/doc-updates.md)
