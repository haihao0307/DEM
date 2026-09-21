# DEM 生产线执行规则

## 真实三维工作台硬门禁

本仓库及后续全部 DEM、Landscape、Ocean、Weather、Cloud 和地形相关 Mother，默认禁止调用图像生成或图像编辑工具。

除非用户在当前对话中明确要求“生成图片”“画一张图”“修改图片”或“给截图”，否则禁止生成概念图、效果图、预览图、参考图、海报、缩略图，也禁止用静态图片、视频、Canvas 假画面或占位页替代真实三维成果。

用户提出“做一版”“重新做”“继续做”“给我看”“按参考做”时，默认任务是修改真实生产源码，构建真实地形/海洋/气象三维场，并交付可交互的 Three.js、WebGPU 或 UE 工作台。

如果还没有可运行的三维版本，继续修改源码并明确尚未形成可验收成果；不得生成图片填补进度。只有截图而没有工作台，本轮自动判定失败。

浏览器截图只允许作为内部 QA 和回归证据。未经用户明确要求，不把 QA 截图当作创作成果发送。

每一份规划、任务卡、README、START_HERE、交接包、会议纪要和验收清单都必须包含：

- [ ] 没有用生成图片代替真实三维实现；
- [ ] 已实际修改生产源码；
- [ ] 用户看到的是可交互三维工作台；
- [ ] 画面来自实时三维运行时；
- [ ] 镜头、控制和用户要求的交互可以实际操作；
- [ ] 公网固定链接和真实浏览器已验证；
- [ ] 如果只有截图而没有工作台，本轮判定失败。


## 用户最终交付格式：单体 HTML 双击直开（2026-09-21 永久规则）

凡是交给用户直接打开、查看、测试、验收的网页、三维工作台或演示，**最终交付本体必须是一个独立的 `.html` 文件**。用户只需双击即可运行；不得要求解压、配置路径、运行 npm/Vite/Python/local server、另外放 assets 目录或再打开第二个工具。

所有运行必需的 JavaScript、Three.js/runtime、shader、CSS、图片、数据、模型、音频和 decoder 必须在构建时封装进该 HTML（inline / data URI / base64 / typed array / compressed payload + inline decoder / Blob URL 均可）。核心运行不得依赖 CDN、远程图片/GLB/JSON、GitHub raw、localhost 或首次 service-worker 预缓存。

发布前必须真实执行 `file://` / 本地双击测试：首帧成功、关键交互可用、console 0 error、无缺失资源、无 CORS 核心失败、无需服务器、核心功能所需网络请求为 0。内部开发仍可多文件；用户交付必须 build 成一个 standalone HTML。

单文件规则不允许降低三维、物理、材质、数据或视觉质量；禁止用截图/视频/简化展示壳代替真实工作台。在线固定网址可以作为附加镜像，但不能替代 standalone HTML，也不能成为其运行前提。

若本仓库旧规则写“只交公开网址/必须服务器”，与本条冲突时以用户 2026-09-21 最新单体 HTML 指令为准。跨 Mother 完整规范见 `haihao0307/guilin-dem-pipeline@5791e1edef55b75888e783d5d355cc2cdfe277ba:knowledge/SINGLE_FILE_DOUBLE_CLICK_HTML_DELIVERY_GATE.md`。
