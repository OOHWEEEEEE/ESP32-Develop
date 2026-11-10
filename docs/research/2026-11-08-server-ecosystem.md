# 小智服务端生态与通用服务端能力调研

调研日期：2026-11-08（Asia/Shanghai）。用于补充[能力池](../CAPABILITY_POOL.md)，与[屏幕、固件和摄像头调研](2026-11-08-esp32-projects.md)互相参照。

## 1. 本轮参考原则

用户明确：主要借鉴产品能力与底座能力；尺寸、板型和固件差异不作为排除理由，适配或迁移可以自主完成。本文按这一原则组织，兼容性仅保留为实现备注。

“参考能力”“复用源码”“采用整套框架”是三个独立选择。本轮扩大候选范围，没有选择服务端技术栈、部署方案或首期范围，也没有部署这些项目。

证据分为：作者／官方文档、关键代码采样、产品说明、我们的设计推导。文档列出功能不等于本次实测；规划项不计为已实现。第三方小智服务端不等于小智官方托管服务的源码；本次仍未确认官方云有完整公开实现。

## 2. 小智服务端和相关衍生项目

以下编号 XZ-01 至 XZ-10 是来源组；其中既有独立兼容实现，也有明确 fork、桥接器与配套服务，不把它们都称为同一仓库的直接分支。

| 来源 | 项目及直接资料 | 发现的产品能力 | 值得借鉴的底座与证据范围 |
| --- | --- | --- | --- |
| XZ-01 | [xinnan-tech/xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server)、[单模块部署](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/main/docs/Deployment.md) | 语音／视觉问答、声纹、知识检索、插件控制、设备管理 | 多协议接入与可替换服务接口；有单独运行语音 Server 的路线，也有完整管理平台。不能把 MySQL／Redis／管理后台一律视为语音接入的强制前提；具体扩展仍有独立依赖 |
| XZ-02 | [hackers365/xiaozhi-esp32-server-golang](https://github.com/hackers365/xiaozhi-esp32-server-golang)、[OpenClaw 接入](https://github.com/hackers365/xiaozhi-esp32-server-golang/blob/main/doc/openclaw_integration.md)、[知识库](https://github.com/hackers365/xiaozhi-esp32-server-golang/blob/main/doc/knowledge_base.md) | 流式问答、声纹与音色、外部 Agent 模式、文档同步与召回测试、MCP 市场、主动音频下发 | 传输层与业务分离；文档异步处理；按设备／智能体调试工具；声音资源流式读取。文档及通知模块代码已采样；README 的“主动式 AI”仍在规划，不能由下发能力推定完整自主任务系统 |
| XZ-03 | [joey-zhou/xiaozhi-esp32-server-java](https://github.com/joey-zhou/xiaozhi-esp32-server-java)、[更新记录](https://github.com/joey-zhou/xiaozhi-esp32-server-java/blob/main/CHANGELOG.md) | 作者列出角色／声音、实时打断、家庭成员记忆、就近单设备应答、知识库、记忆图谱、主动消息、设备自检 | 对话服务与管理后台分开；身份、角色、设备、会话分别建模；运行监测。README 明示部分功能未开源，以上是产品能力参考，未逐项证明全部包含在公开版，不以“企业级”宣传替代验证 |
| XZ-04 | [findstr/xiaozhi-esp32-server-mini](https://github.com/findstr/xiaozhi-esp32-server-mini) | 轻量语音服务、会话历史摘要、用户画像、首次输入选择 Agent、网页调试 | 大模型使用 API，降低本机部署负担；区分当前上下文、历史摘要和画像。README 将联网检索、简易 Workflow、知识库和 HA 列为未完成／TODO；内存数字是作者环境记录，不是本次测试 |
| XZ-05 | [sdjdd/dashachun](https://github.com/sdjdd/dashachun) | 小智协议兼容的 Rust 服务端，语音流水线、OTA 配置、设备激活／绑定和账号 | 参考将协议入口、账号与语音处理分离的最小服务边界；作者说明仍在开发、接口可能变化。仅核对 README 与目录，不推定已具备完整工具、知识或主动任务能力 |
| XZ-06 | [hougeai/xiaozhiPro](https://github.com/hougeai/xiaozhiPro) | OpenClaw／Hermes 双向桥接、定向投递／广播、HA、浏览器摄像头视觉、提醒、个人音频库、树索引知识检索 | 外部 Agent 与设备语音可分层；慢任务异步返回，消息与目标设备分离。依据产品文档和更新日志，公开仓库以说明及固件发布入口为主，未确认完整服务端源码可复用；2026-07-30 更新已将音乐调整为用户上传，旧版公网搜索描述不作当前承诺 |
| XZ-07 | [shenjingnan/xiaozhi-client](https://github.com/shenjingnan/xiaozhi-client) | 多个小智接入点共用工具配置，网页配置与状态查看，连接本地／远程 MCP | 工具聚合、可见性开关、接入适配器与后台桥接。名字里的 client 是 MCP 桥接客户端，不是替代整套 ASR／LLM／TTS 的语音服务端 |
| XZ-08 | [xinnan-tech/mcp-endpoint-server](https://github.com/xinnan-tech/mcp-endpoint-server)、[ziruny 衍生版](https://github.com/ziruny/xiaozhi-mcp-endpoint-server) | 一个智能体使用多个 MCP 服务；衍生版加入远程 SSE／Streamable HTTP 服务 | 工具注册、聚合、名称路由、连接清理和健康状态；不同传输方式可经适配统一暴露。接入点解决连接和转发，记忆、任务、权限语义仍由上层实现 |
| XZ-09 | [Verdure MCP Platform](https://github.com/maker-community/verdure-mcp-for-xiaozhi) | 将工具绑定到小智、涂鸦等不同助手；独立连接配置与网页管理 | 多助手适配、连接恢复、工具绑定、用户隔离；多租户平台可参考数据关系，不默认照搬完整 Keycloak／平台部署 |
| XZ-10 | [sheacoding/mcp-reminder](https://github.com/sheacoding/mcp-reminder)、[V2 说明](https://github.com/sheacoding/mcp-reminder/blob/main/V2_TEST_GUIDE.md) | 自然语言闹钟、待办、完成状态和到期查询，JSON 持久化 | 小型领域工具和资源接口可参考。V2 指南与实现实际依赖客户端读取触发检查，不能据 README 标题认定已具备独立计时、离线投递或到点自动播报 |

### 2.1 XZ-01 中额外值得保留的服务端能力

这些功能分布在不同扩展文档中，不只是一套“接模型聊天”的服务：

- **上下文源**：构建提示词时获取外部 HTTP 数据，让助手在开始交互时获得待办或设备状态；查询后是否刷新要另行处理。[来源](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/main/docs/context-provider-integration.md)
- **联网检索**：对话中调用搜索插件，可替换搜索服务；网页正文读取、引用呈现和写入知识库是后续组合场景。[来源](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/main/docs/web-search-integration.md)
- **设备间呼叫**：通讯录、双方授权、远程唤醒和语音通道联动；文档有特定设备、AEC 和 MQTT 网关前提，这些记为适配事项，不排除产品能力。[来源](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/main/docs/device-call-guide.md)
- **多种记忆机制**：支持短期摘要、Mem0、PowerMem 等选项。它们展示了不同实现路线，不改变用户已确认的“Agent 自主管理记忆”；系统自动抽取事实并非既定需求。[来源](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/main/docs/powermem-integration.md)

### 2.2 两处关键代码采样

**Go 通知资源**：采样时仓库 main 为 `531930f9249e49d28bc8dfad020fa3260eab3591`。[通知服务](https://github.com/hackers365/xiaozhi-esp32-server-golang/blob/531930f9249e49d28bc8dfad020fa3260eab3591/internal/app/server/notify/service.go)维护有时效的通知配置，提供 Redis 与进程内降级缓存；[音频地址与 TTS 解析](https://github.com/hackers365/xiaozhi-esp32-server-golang/blob/531930f9249e49d28bc8dfad020fa3260eab3591/internal/app/server/notify_helper.go)为设备拉取音频解析可访问地址及声音服务。值得借鉴“短期媒体资源”和“长期任务／收件箱”分别维护，前者不能代替后者。本次没有验证跨重启投递、设备唤醒和播放确认的完整链路。

**提醒 V2**：采样时 main 为 `5686788f466681f23e4b632c86a3fd521a3da1d9`。[server_v2.py](https://github.com/sheacoding/mcp-reminder/blob/5686788f466681f23e4b632c86a3fd521a3da1d9/src/mcp_reminder/server_v2.py)在读取 `reminder://pending` 时计算到期项和新增数量；对应指南明确无后台检查任务。因此只能确认为提醒 CRUD、资源读取与新增项跟踪参考，主动调度和通知消费仍需上层完成。

## 3. 小智之外的通用服务端参考

以下项目作为能力和机制参考，不是推荐全部安装。SV-01 至 SV-13 与 XZ 来源编号共用能力池索引。

| 来源 | 项目与直接资料 | 已查到的机制 | 可转化为我们的候选能力 |
| --- | --- | --- | --- |
| SV-01 | [Pipecat 语音轮次](https://docs.pipecat.ai/pipecat/learn/speech-input)、[打断机制](https://docs.pipecat.ai/pipecat/fundamentals/interruptions) | 结合 VAD、转写和语句完整性判断轮次；打断时清理在途生成／合成及未播音频，维护已播内容 | 少抢话、少误打断；区分“模型生成了什么”“屏幕展示了什么”“用户实际听到了什么”。端侧仍需实现对应播放／取消语义 |
| SV-02 | [LangGraph 持久化](https://docs.langchain.com/oss/python/langgraph/persistence)、[暂停恢复](https://docs.langchain.com/oss/python/langgraph/interrupts) | 会话状态 checkpoint 与跨会话 store 分开；执行可等待外部输入后恢复 | 长任务中途补充信息、点选方案再继续、故障后恢复；持久存储和副作用重复处理需要应用设计，框架本身不免除这些工作 |
| SV-03 | [OpenClaw Automation](https://docs.openclaw.ai/automation)、[任务调度入口](https://docs.openclaw.ai/automation/cron-jobs) | 持久定时任务、条件／外部触发、执行上下文、投递目标、安静时段与运行历史 | 定时简报、持续关注某主题、有变化才报告；任务触发、Agent 执行和通知分别管理。当前文档已将旧 heartbeat 监测归入普通任务，不把过时教程中的所有机制当作现行设计 |
| SV-04 | [Hermes Agent](https://github.com/NousResearch/hermes-agent)、[定时任务](https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/cron.md) | Agent 整理记忆、历史会话检索、经验转技能；多入口、委派和定时投递；任务可携带前次结果 | 自主记忆、可复用个人工作流程、跨次监测去重、复杂任务分工。定时任务上下文与交互会话分开，不应默认可共享全部记忆和权限 |
| SV-05 | [RAGFlow](https://github.com/infiniflow/ragflow) | 多格式解析、分块／重排、来源引用、多步检索；当前文档还列出生成 Wiki、树、时间线、思维导图等知识产物 | 文件／网页进入知识收件箱；可追溯回答和多种整理结果。生成 Wiki 产物不等于已支持对用户 Obsidian 目录做增量合并和人工编辑冲突处理 |
| SV-06 | [n8n Wait](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/) | 等待时间、外部回调或表单；等待时将执行数据交给数据库，满足条件后继续 | 对接外部服务、Webhook 触发流程，以及“等用户确认后继续”；可学机制或使用工作流服务，不要求首期引入可视化编排平台 |
| SV-07 | [Temporal 执行与恢复](https://docs.temporal.io/workflow-execution) | 用事件历史恢复长时间运行的工作流，区分工作流、外部活动和消息 | 提交后持续执行、服务重启后恢复、等待外部结果；适合研究可靠任务语义，不代表个人项目必须部署完整 Temporal |
| SV-08 | [Home Assistant 语音流水线](https://contributors.home-assistant.io/core/internals/assist-pipelines/)、[Wyoming](https://www.home-assistant.io/integrations/wyoming/) | 唤醒、转写、意图和合成的分段接口；局域网其他主机可承担 Whisper／Piper 等服务 | 本地／云端混合语音、家庭设备状态和事件源；使用本地语音服务不自动等于整个 Agent 已完全离线 |
| SV-09 | [LiteLLM Router](https://docs.litellm.ai/docs/routing) | 多服务路由、超时、重试、冷却、故障切换和额度相关路由 | 不同任务使用不同模型，服务故障时降级，前台语音与后台整理分配不同预算；实际质量和成本需用自己的场景测量 |
| SV-10 | [Langfuse 观测](https://langfuse.com/docs/observability/overview)、[评测分数](https://langfuse.com/docs/evaluation/scores/overview) | 关联提示词、模型、工具、检索、耗时与用量；人工／程序／模型评测、数据集实验 | 定位慢在哪一段，比较模型／提示词调整前后的表现；自建轻量日志和场景样例也可先承接这些需求 |
| SV-11 | [ntfy 消息与动作](https://docs.ntfy.sh/publish/)、[订阅](https://docs.ntfy.sh/subscribe/api/) | HTTP 发布、主题订阅、缓存、优先级、附件和动作按钮 | 墨水屏、手机、网页分别接收结果；点选后回到原任务。消息服务接收成功不能等同设备已展示、用户已阅读或动作已完成 |
| SV-12 | [IBM ContextForge](https://github.com/IBM/mcp-context-forge) | 工具目录与代理，MCP／REST 等服务聚合，按需组合虚拟工具集，鉴权、限流与调用观测 | 统一工具登记、按任务暴露工具、为现有业务 API 增加适配层；可以只借鉴目录与适配机制，不默认部署企业网关 |
| SV-13 | [SQLite Online Backup API](https://www.sqlite.org/backup.html) | 对正在使用的数据库进行一致快照，支持增量拷贝；另有 VACUUM INTO 等路线 | 提醒服务端数据需可备份、可恢复。全系统还需覆盖媒体、知识文件、配置与索引；这是我们的设计推导，本文不据此决定采用 SQLite |
| SV-14 | [Quacksat 唤醒选择](https://github.com/andreagenovese/quacksat/blob/c3c54b0c4faae9a8360178a604c129057868e92b/bridge/bridge.py#L57) | 参考桥接器在短窗口收集唤醒分数，保留最高分设备，并通知其他设备停止聆听 | 可借鉴候选上报和落选反馈。检测置信度能否稳定选中更近的设备，需要在目标麦克风、增益与环境下验证 |

## 4. 新增或补强的产品能力

以下情境是由调研提出的候选，不是用户已确认需求。已存在的功能优先补充来源，避免换个名称重复计数。

| 能力池 ID | 用户能得到的结果 | 主要启发 |
| --- | --- | --- |
| U-02、U-05 | 停顿思考时少被抢话；打断后不继续播放旧回答 | SV-01、XZ-01／02／03 |
| U-04 | 角色、声音、说话人身份分别设置；可选个性音色 | XZ-01／02／03，身份关联仍需设计 |
| U-08 | 多台终端同时听到唤醒，只由合适的一台回答 | XZ-03 为产品说明。可参考 SV-08 的重复触发拦截和 SV-14 的候选打分。 [Home Assistant 源码](https://github.com/home-assistant/core/blob/6a811d3359c7b2076dc9e1cf900843a129c044af/homeassistant/components/assist_pipeline/run.py#L309) |
| K-09 | 把文件或网页交给助手，异步整理后可查询、可入库 | XZ-02／06、SV-05 |
| K-10 | 同一批材料可生成主题页、时间线、导图等不同结果 | SV-05；Obsidian 整理由我们连接 |
| K-11 | 看到材料是否处理成功，查看来源片段，重试失败材料 | XZ-02、SV-05 |
| K-12 | 联网找资料、阅读网页并保留引用 | XZ-01 的检索插件及 SV-04；检索与入库分别触发 |
| T-04、S-02 | 长任务先受理，后续查看进度；需要补充时显示选择并继续 | LOCAL-07、XZ-06、SV-02／06／07；完整墨水屏卡片链路是组合设计 |
| T-09 | 在同一聊天入口把任务交给外部 Agent，之后接收结果 | XZ-02／06；不要求另建独立记录入口 |
| T-10 | 将反复进行的操作保存为可复用的个人工作流程 | SV-04／06；普通模板、技能和确定性流程可以分别选 |
| T-11 | 持续关注指定主题或状态，发生值得关注的变化时报告 | SV-03／04；执行依据、静默条件和终止条件需明确 |
| T-12 | 呼叫另一台设备、语音对讲；留言和广播可另行扩展 | XZ-01 有呼叫文档、XZ-06 列出广播；留言是设计推导 |
| T-13 | 复杂任务分给不同执行者，最终汇总成一个结果 | SV-04；单 Agent 也能先完成简单场景，不默认引入多 Agent |
| T-14 | 外部事件触发指定流程，而不必先开口聊天 | XZ-01、SV-03／06／08；动作和通知边界待讨论 |
| V-10、F-04 | 使用浏览器／外部摄像头，以及个人音频库 | XZ-06、CAM-08；摄像头源和播放源分别适配 |

## 5. 底座方面的收获

已有 B-01 至 B-18 保留，新增 B-19 至 B-28；新增是为了让后续选择有明确讨论对象，不表示它们都应成为首期组件。

| 主题 | 需要回答的问题 | 对应能力池 |
| --- | --- | --- |
| 上下文 | 哪些信息每次交互前加载，哪些由工具按需查；何时过期、失败如何继续 | B-19，参考 XZ-01 |
| Agent 与技能 | 谁处理当前请求，转交时带哪些上下文，记忆归谁管理，技能如何选择与更新 | B-20，参考 XZ-02／06、SV-04 |
| 可靠执行 | 对话结束后任务是否继续；等待输入、取消、重启恢复和重复副作用如何处理 | B-08、B-21，参考 SV-02／06／07 |
| 模型与成本 | 语音快答、知识整理、视觉等任务如何选模型；超时、限额和服务失败如何降级 | B-03、B-22，参考 XZ-01／02、SV-09 |
| 工具目录 | 工具如何发现、命名、绑定目标并按需暴露；不同协议如何适配 | B-04、B-23，参考 XZ-07／08／09、SV-12 |
| 投递 | 哪台终端显示，何时播报，离线是否保留，收到／展示／阅读／执行怎样区分 | B-10、B-11，参考 XZ-02／06、SV-11 |
| 身份 | 设备、使用者、角色、Agent 各自是什么；个人／共享知识与记忆怎样对应 | B-15、B-24，参考 XZ-03／09 |
| 实时语音 | 用户说完了吗，旧回答取消了吗，历史里哪些内容用户实际听过 | B-25，参考 SV-01 |
| 效果回归 | 调整模型和提示词后，记录是否丢失、知识是否误合并、工具是否误调用、等待是否变长 | B-16、B-26，参考 SV-10，具体验收例子由我们制定 |
| 外部执行 | 本机、另一台电脑或外部 Agent 执行任务时，文件、凭据、工作目录与取消如何传递 | B-27，参考 XZ-06、SV-04 |
| 数据恢复 | 哪些是原始事实、哪些是索引或派生产物；换服务器、误改或重建后怎样恢复 | B-28，参考 SV-13，完整恢复方案由我们设计 |

### 5.1 与三个已确认重点的联系

- **语音问答**：优先讨论会话、语音轮次、服务接口、工具和上下文；是否全离线、是否全双工仍是独立选择。
- **记录想法**：保存原始输入、给出明确受理状态、让整理任务与连接分离；等待确认、离线录音和原音保留深度待选。
- **整理知识**：Obsidian 仍是用户知识库目的地。文档解析、索引、检索、Agent 记忆和自动合并笔记分别建模；RAG 平台可以作辅助层，不因采用检索而替换目的地。

上述是待讨论的依赖关系，不是首期架构决议。完成这些最小语义可以使用简单模块；选择框架之前先确定实际场景与验收结果。

## 6. 本轮未作出的决定

没有决定复用 Python／Go／Java 服务端中的任何一套，也没有决定引入 OpenClaw、Hermes、LangGraph、n8n、Temporal、RAGFlow、LiteLLM 或企业 MCP 网关。所有新增产品项保持“待选择”。

硬件尺寸和固件适配不用于提前剔除有价值能力；“是否保留”“能力做到多深”“代码如何迁移”“部署多少组件”留到后续逐项讨论。
