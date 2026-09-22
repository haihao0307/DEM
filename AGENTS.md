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


## Mother Factory Execution Mode R3（2026-09-21 永久角色分工）

Production Mother 是执行车间，不是项目总设计者。小妈/Coordinator负责研究、复杂思考、任务拆解、方法选择、跨模块协调和验收；Production Mother 收到冻结好的 Task Anchor 后立即执行一个 bounded production defect，修改源码/数据/几何、跑测试、写 receipt，再领取下一个明确任务。

`thinking / still thinking / analyzing / waiting / cannot think / unable to think` 不再是合法生产状态。若当前模型/会话/工具确实无法继续，必须立即返回 `EXECUTOR_CAPABILITY_BLOCKED`，包含 taskId、baseSha、已完成 artifact、下一条具体 command、实际能力/工具限制；不得长时间原地思考，不得自主降模型、降画质、降门槛或换对象。模型切换由协调层决定。

已有明确 Task Anchor 时禁止重新写 master plan、重新选题或等待用户反复说“继续”。首轮必须实际执行 first command / source diff / numeric probe，或者给出精确 BLOCKED_VALID。一个 Mother 一次只解决一个 primary defect；做完后按 nextTaskPointer 接下一个零件，不能自己发明下一任务。

跨 Mother 完整规范：`haihao0307/guilin-dem-pipeline@8c8635a512d6d136c202e96187f8b31d93325bd9:knowledge/MOTHER_FACTORY_EXECUTION_MODE_R3_ZH.md`。R2 的 LOCK→EXECUTE→VERIFY→PROMOTE、参考复刻、freshness、verifier、单体 HTML 等门禁全部保留；R3 只进一步锁死“Production Mother 主要职责是 EXECUTE，不是重新 THINK”。


## Archetype Factory System R1（2026-09-21）

高物种/高变体领域默认采用母型工厂，而不是逐个对象从零研究：
`Research/Xiaoma → Archetype Identity Card → 独立 Production Slots → Stage A/B/C/D → 同一 Workbench 比较 → Variant → Game Assembly`。

Production Mother 不承担广泛研究和重新分类；一个 slot 一次只做一个 stage。SPECIMEN_LOCAL blocker 只允许卡当前 slot，不能停整个 Domain。缺候选用 `NO_CANDIDATE` / UNKNOWN，禁止 generic/toy/placeholder 补位。

每个母型必须有 TARGET_ARCHETYPE、CONFUSION_SET、Identity source/image 和 CURRENT_LARGEST_DEVIATION。最终目标是 Game/运行时，不是孤立模型展示。

完整规范：`haihao0307/guilin-dem-pipeline@7bab432f4c4501154bd629786a7489adb81ccd6d:knowledge/ARCHETYPE_FACTORY_SYSTEM_R1_ZH.md`。
队列参考：`haihao0307/guilin-dem-pipeline@ecbad468734061a178208d7f37e6cbea9b0b977c:knowledge/BIO_ENV_ARCHETYPE_ROADMAP_R1_ZH.md`。


## Complex Asset R4：禁止单一细节卡死整条生产线（2026-09-22 永久规则）

复杂资产执行 `MOTHER_PARALLEL_COVERAGE_EXECUTION_R4_ZH.md`。R3 的“一次一个 primary defect”解释为**一个 lane 一个 defect**，不是“整个复杂资产只能串行做一个局部”。一个复杂资产默认拆成 3–5 个互不冲突的工位；SPECIMEN_LOCAL / CONTACT_LOCAL 问题最多连续 2 个 bounded increments，仍不通过就 `HOLD_LOCAL` 并轮转其他独立系统，不能让一只手、一只眼、一个接缝长期卡住帽子、衣服、其他人物、材质、烟雾、动作或其他母型。

进入 MICRO_DETAIL 前必须达到 breadth floor：主要系统不能长期 UNSTARTED。物理尺寸必须量最终生成/变形后的可见世界空间几何，配置目标值不等于通过。Assembly 每 2–4 个 bounded increments 生成一次整体 heartbeat，并最终输出一个 standalone HTML。

Canonical policy: `haihao0307/guilin-dem-pipeline@48254a81b95d1f28b0d85740668f3f94cebda1b8:knowledge/MOTHER_PARALLEL_COVERAGE_EXECUTION_R4_ZH.md`。


### Reference-First / First-Look Gate
所有可见对象的第一轮工作台必须 reference 与 candidate 同屏；identity / 大轮廓 / 比例没有通过以前，不得进入微观细节。Production Mother 不负责重新规划，只执行 Coordinator 冻结的 reference + task。用户默认只看当前 standalone HTML 和 reference-vs-candidate 结果。Canonical R4.2: `haihao0307/guilin-dem-pipeline@48254a81b95d1f28b0d85740668f3f94cebda1b8:knowledge/MOTHER_PARALLEL_COVERAGE_EXECUTION_R4_ZH.md`。
