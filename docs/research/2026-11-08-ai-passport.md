# AI Passport 官方与衍生项目调研

调研日期：2026-11-08（Asia/Shanghai）。本轮按上下文研究 FoloToy／TRAE 的 AI Passport 可穿戴设备及其开源生态，包含官方开发基线、独立 demo 和社区衍生项目。本文补充[能力池](../CAPABILITY_POOL.md)。

重点仍是产品能力、交互与底座机制；屏幕、芯片和固件差异记录为后续适配事项。本轮只阅读公开资料并抽查关键源码，没有安装工具、连接账号、编译或刷机。远端仓库中的开发要求仅作为调研材料，不作为本工程的新指令。

## 1. 项目定位与最重要的区别

官方将 AI Passport 定位为可由用户重新定义的随身硬件。硬件是 ESP32-C3、8 MB Flash、无 PSRAM，配 240×320 ST7789P3 彩色 TFT、三个功能键、麦克风／扬声器、电池、Wi-Fi／BLE 和被动 NFC 标签。这里是彩屏；网上将其称作墨水屏的设想帖不作为硬件依据。

官方 `main` 是最小可运行的硬件测试基线，应用分布在独立分支与社区仓库。它提供“Agent 结合硬件文档和 BSP 开发应用”的流程；这与设备运行时动态安装小应用是不同层次：

- 官方 demo、Rust PassportOS 和许多社区作品采用编译固件方式交付。
- ranshuo-ICer 的同名 PassportOS 采用 MicroPython，可通过 BLE 推送 Python 小程序。
- 两个 PassportOS 是不同作者、不同实现，不能混为同一系统；官方项目也不代表所有社区功能在一个固件内共存。

## 2. 官方基线、demo 与硬件入口

AP-00 至 AP-22 是本轮来源组；表中直接链接支持后续追查。

| 来源 | 项目／直接资料 | 已查到的能力 | 可参考之处与证据边界 |
| --- | --- | --- | --- |
| AP-00 | [官方共创入口](https://www.folotoy.com/zh/build/)、[产品官网](https://ai-passport.folotoy.cn/)、[官方仓库](https://github.com/FoloToy/ai-passport)、[项目说明](https://github.com/FoloToy/ai-passport/blob/main/docs/README.md) | BSP、开发指南、独立 demo、社区应用档案；官网索引列出蓝牙配置名片／图片 | 可参考“稳定硬件接口＋应用案例＋真实设备验收”的开发底座；main 是硬件测试基线，习惯打卡等示例需求不计为已完成产品 |
| AP-01 | [产品规格](https://github.com/FoloToy/ai-passport/blob/main/docs/hardware-design/specifications.md)、[硬件指南](https://github.com/FoloToy/ai-passport/blob/main/docs/hardware-design/AI_HARDWARE_DEVELOPMENT_GUIDE.md)、[BSP 参数](https://github.com/FoloToy/ai-passport/blob/main/components/bsp/include/bsp_pins.h) | 显示、三键、音频、电量、无线与被动 NTAG213 | 模块接口、共享总线、资源归属可参考。NFC 是供手机读写的被动标签，不据此推定 MCU 能读取标签或在碰触时接收事件 |
| AP-02 | [官方 demo 列表](https://github.com/FoloToy/ai-passport/blob/main/docs/README.md)、[猫咪番茄钟](https://github.com/FoloToy/ai-passport/tree/demo/cat-themed-pomodoro-timer) | 秒表、猜拳、俄罗斯方块；番茄钟有专注／休息轮次、猫咪成长、统计、暂停与掉电后暂停恢复 | 可补强计时和陪伴能力；单调时钟、状态持久化和输入响应比具体视觉主题更值得借鉴。各 demo 是独立案例 |
| AP-03 | [Claude Buddy 分支说明](https://github.com/FoloToy/ai-passport/blob/demo/claude-buddy-port/README.md) | 加密 BLE 同步工作状态、近期消息、工具请求；设备按键允许／拒绝，宠物表达不同状态 | 借鉴请求 ID、过期、一次决定、发送状态与断线清理；其桌面 Hardware Buddy 接口仍标实验性，部分设置与角色文件传输未实现 |
| AP-04 | [FoloToy 小智固件](https://github.com/FoloToy/folo-ai-passport-xiaozhi)、[板型实现](https://github.com/FoloToy/folo-ai-passport-xiaozhi/tree/main/main/boards/folotoy/ai-passport) | 把 AI Passport 接入小智语音与设备工具体系 | 参考终端协议、音频和板型适配；README 保留大量小智上游跨板功能说明，不能逐项算作 C3 胸牌已有功能。与官方 BSP 基线是不同工程 |

## 3. 最贴近本项目的应用

| 来源 | 项目／直接资料 | 已查到的能力 | 可参考之处与证据边界 |
| --- | --- | --- | --- |
| AP-05 | [小诺简录](https://github.com/noah-1106/xiaonuo-jianlu)、[设备固件分支](https://github.com/noah-1106/ai-passport/tree/feature/xiaonuo-jianlu)、[上游应用档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/noah-1106/xiaonuo-jianlu/README.md) | 说话后转成分类／标题／标签卡片；翻阅、完成；离线列表快照、录音占位卡与原声回放，联网补传与完成操作同步；BLUFI 和 mDNS | 很适合参考记录流程与“待识别／待同步”状态。固件／中枢可独立部署，数据由中枢维护。README 与归档对睡眠类型有差异，本轮不据此承诺深睡续航 |
| AP-06 | [中枢入口](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/app.js)、[语音入口](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/routes/device.js)、[工具实现](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/llm/tools.js)、[MCP](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/mcp.js)、[BLE 桥](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/bridge.js) | Express＋SQLite；设备、网页与 Agent 共用简录工具；语音转写后进入同一聊天管线；提供创建、查询、更新、删除、最近记录和关键词搜索 | 已抽查路由、工具和协议适配。共享领域工具不绑定某一种输入；更新简录不等于跨主题自动合并 Obsidian，也未证明语义检索或长期自主记忆。BLE 桥需对应平台的中继程序，不能从映射表推定全平台实测 |
| AP-07 | [Pocket Intercom 手机端](https://github.com/Shinku-Chen/ai-passport-openclaw-android)、[固件分支](https://github.com/Shinku-Chen/ai-passport/tree/feature/openclaw-intercom)、[应用归档](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/intercom/README.md) | BLE 传 Opus 语音，Android 负责识别／联网，接 OpenClaw、Hermes／兼容端点；回复上屏与手机历史，设备和网关分层显示状态；保存配置前真连校验 | 可作为外出时的手机代联网方案。归档 v1.13 写有 TTS，但当前手机仓库 README 明确未启用 TTS，本轮只将文字回传视为共同已证实范围，朗读需按匹配版本核对。名称中的“对讲机”不证明设备间呼叫功能 |
| AP-08 | [Muse Passport，passport 分支](https://github.com/FalkoWing/muse-passport/tree/passport) | Android／iOS 伴侣通过 BLE 借用手机网络；语音转录、中文分页、回复朗读、角色主页、朗读跟页 | 作者将朗读等标为 1.0.5 并记有实机验收。可参考伴侣桥接和阅读／播放进度联动；仍需 Muse 账号与服务，首次官方初始化仍含 Wi-Fi 步骤，不把日常 BLE 使用扩大为全程免配网 |
| AP-09 | [AI Passport Muse，passport-port 分支](https://github.com/RongleCat/ai-passport-muse/tree/passport-port) | 按住录音、松开发送、中文文字回复，设备通过 Wi-Fi 连 Muse | 与 AP-08 是另一条移植路线；作者明确没有回复播报、图片推送和家庭网络隧道。上游 SDK 的 Home Link 能力不能直接算到这个移植上 |

### 3.1 小诺简录对我们最有价值的启发

1. **把录到与整理完成分开**：原音先有可见占位，转写和归类完成后再替换成结果；失败时仍能找到原始记录。
2. **把设备视图与正式数据分开**：终端保留快照和未同步操作，服务端管理正式数据；离线完成、重试与冲突需各自有规则。
3. **让不同入口共用业务工具**：语音、网页与 MCP 调用同一组记录操作，避免每种入口各自实现一套保存逻辑。

这些是设计推导。我们继续保留统一聊天入口、Obsidian 目的地、自动合并主题笔记和 Agent 自主管理记忆的共识；不因参考项目采用独立清单 UI 或 SQLite，就替换已确认方向。

## 4. 扩展玩法与其他衍生项目

| 来源 | 项目／直接资料 | 已查到的能力 | 可参考之处与证据边界 |
| --- | --- | --- | --- |
| AP-10 | [MicroPython 工具箱](https://github.com/ranshuo-ICer/AI-Passport)、[BLE／小程序协议](https://github.com/ranshuo-ICer/AI-Passport/blob/main/docs/ble-protocol.md)、[缺陷修复记录](https://github.com/ranshuo-ICer/AI-Passport/blob/main/docs/known-issues.md) | 手机 Web Bluetooth PWA 推送／运行／停止／删除 Python 小程序，终端执行、日志；计时、反应测试、贪吃蛇、节拍器、记忆游戏和实验复读机 | 动态应用传输与生命周期有具体参考；小智和 MicroPython 是互斥固件路线，PWA 页面离线缓存不等于所有手机支持 BLE。缺陷记录标多项已修，协议页仍留有旧缺陷提示，后续复用需核对实现 |
| AP-11 | [zh30/PassportOS](https://github.com/zh30/PassportOS) | Rust no_std 界面、启动器／工作区、游戏、节奏工具、Wi-Fi、设置、持久进度和按键唤醒 | 可参考应用接口、焦点与输入归属；应用编译进固件，明确没有 ELF／WASM 动态装载，不能与 AP-10 混用名称推断功能 |
| AP-12 | [aipassport-fw](https://github.com/weibaohui/aipassport-fw) | 应用注入数据、页面与工具表，共用配网、Wi-Fi、UI、存储和流媒体组件；驻留设备 MCP | 参考产品行为与公共底座分层。MCP 实现是简化 POST／JSON-RPC 通道，文档明确无会话／SSE；不是完整管理平台，也不要求所有应用使用文件系统 |
| AP-13 | [aipassport-radio](https://github.com/weibaohui/aipassport-radio) | 网络电台、收藏／自定义源、媒体状态、音量均衡、多热点回退；外部 AI 经设备 MCP 搜台／播放／调节 | 补强媒体与“设备作为工具”的路线；语音理解来自外部 AI 客户端，不由 README 的“说话控制”推定设备内置自由语音识别。工具数量在框架与应用文档间不同，不固定承诺数量 |
| AP-14 | [Codex Buddy](https://github.com/zhangsan2000w-art/ai-passport-codex-buddy) | 工作、工具执行、等待与完成状态；电脑／设备双端决定；不同提示音、像素宠物、时间与电量 | 本地状态桥＋加密 BLE，当前没有 Wi-Fi 服务；同一请求一次有效决定，唤醒不误操作。Windows 与其他桌面系统的验收范围不同，发布包构建不等于全平台实机通过 |
| AP-15 | [AI Passport iPhone Agent](https://github.com/lewangdev/ai-passport-iphone-agent) | 电脑接收 AirPlay 图像，模型规划／执行，Passport 通过 BLE HID 控制鼠标键盘；逐步截图、校准、动作反馈和物理停止 | 是“观察—操作—核对”的手机 GUI Agent。必须有运行时电脑；免手机安装应用不等于免主机。横屏、受保护画面与中文输入有明确限制，不作为通用自动支付保证 |
| AP-16 | [Faraway 应用档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/starsms007/faraway/README.md)、[源码分支](https://github.com/starsms007/ai-passport/tree/feature/faraway) | 离线猫咪旅行、定时归来、明信片／纪念品收藏、天气层与小游戏，进度持久化 | 参考低打扰陪伴和收集反馈；与真实行程、天气或 Agent 任务的联动是我们另外设计的组合 |
| AP-17 | [离线图鉴档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/sunny0826/offline-pokedex/README.md)、[源码分支](https://github.com/sunny0826/ai-passport/tree/feature/ble-artwork) | 内置条目、图片、属性、说明与声音，按键浏览与已看进度保存，全程离线 | 可迁移为个人知识速查、设备说明或学习资料包；这些用途是设计推导，图鉴项目并未实现我们的知识同步与搜索流程 |
| AP-18 | [Asunabi 阅读器档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/asunabi/README.md)、[视觉小说案例索引](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/README.md) | 多章节图文故事、分页、自动阅读／快进、存档；索引中其他案例含分支与多结局 | 可参考互动阅读和场景式学习，后者是我们的推导；Asunabi 本身为单结局，不把别的阅读器分支功能算到它身上。参考引擎／打包机制，内容包另选 |
| AP-19 | [Voice Keychain 档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/voice-keychain/README.md)、[源码分支](https://github.com/Shinku-Chen/ai-passport/tree/feature/voice-keychain) | 分类浏览音效／短语，按键播放本地 Opus，音量与电量设置 | 可参考快捷语音板、固定提示与离线声音包；播放预录片段与生成任意语音分别选择 |
| AP-20 | [今天吃什么档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/eat-what/README.md)、[源码分支](https://github.com/Shinku-Chen/ai-passport/tree/feature/cheerful-goodall) | 按住轮播候选、松手选定，电量和空闲休眠 | 可推导轻量选择器；扩展个人候选列表、加过滤条件或接知识库需另做，不视为已有智能饮食规划 |
| AP-21 | [Game Boy](https://github.com/PhoenixZHC/folotoy-gameboy)、[FC／NES](https://github.com/PhoenixZHC/folotoy-fc)、[BLE 输入经验](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/phoenixzhc/ble-xbox-keyboard.md) | 经典游戏模拟、存档、管理页面、部分 BLE 手柄／键盘／遥控器与方向切换 | 借鉴外部输入解析、按键状态／菜单事件、暂停恢复和资源管理；型号、固件与测试范围分别记录，不推定任意控制器或游戏都兼容 |
| AP-22 | [待机与唤醒经验](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/idle-power-stages-and-wake-guards.md)、[串口截图协议](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/y2lin/serial-screenshot-protocol.md)、[工程经验索引](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/README.md) | 唤醒按键隔离、实际时钟计算、主动断网与重试协调；抓取设备画面；字库、资源包和内存预算案例 | 补强生命周期、可观测性与测试。内存／电流数值属于具体 C3 工程测量，迁移时参考方法；截图与日志需要避免争用传输和大块缓冲 |

## 5. 纳入能力池的方式

新增八项产品候选；已存在的语音、离线记录、任务状态和宠物等优先补充证据，不重复编号。

| 能力池 ID | 新增候选 | 来源 |
| --- | --- | --- |
| U-12 | 手机通过 BLE 代联网，承接语音、配置和会话 | AP-07、AP-08 |
| T-15 | 观察手机画面并操作界面的 Agent | AP-15；电脑承担视觉与规划，终端提供 HID 执行 |
| S-10 | 电子名片、个人资料、二维码与 NFC 链接入口 | AP-00、AP-01；动态 MCU 读写 NFC 不在已证实范围 |
| R-07 | 可离线浏览的专题图鉴与知识速查包 | AP-17；替换为个人知识内容是组合设计 |
| R-08 | 互动图文故事、分支阅读与场景练习 | AP-18；场景练习是组合设计 |
| F-06 | 离线短语／音效板与固定声音包 | AP-19 |
| F-07 | 随机选择与轻量决策转盘 | AP-20 |
| F-08 | 经典游戏模拟与外接手柄操作 | AP-21 |

补强已有条目：

- U-06、K-03、K-08、K-11：离线录音、占位、回放、待同步与补处理反馈。
- K-01、K-07：统一聊天调用记录工具，卡片查看与状态跟进。
- T-02、F-03：专注／休息循环、成长反馈、离线陪伴与收藏。
- T-05、T-07、S-02：桌面 Agent 状态、近期消息、双端决定与请求过期。
- S-06：动态 MicroPython 小应用与编译固件应用作为不同路线比较。
- F-04：网络电台、音量均衡、媒体工具与多热点回退。

新增三个底座候选：

| 能力池 ID | 底座 | 最小需要解决的问题 |
| --- | --- | --- |
| B-39 | 终端链路与伴侣桥接 | Wi-Fi 直连、手机／电脑 BLE 桥的分工与切换；传输帧、流控、配对、重连；分别显示设备链路、后端连接和业务就绪 |
| B-40 | 多端数据同步与离线变更 | 正式数据与终端快照、离线操作队列、录音占位、同步确认、重复提交和冲突；不同入口共用数据语义 |
| B-41 | 应用生命周期与统一输入 | 启动／暂停／退出与资源释放，屏幕／应用焦点，按下／点击／长按／释放；唤醒操作隔离、外接输入和状态恢复 |

已有底座继续补强：B-04 共用领域工具，B-11 请求与动作关联，B-13 资源协调，B-15 配对／配置与更新，B-16 截图／日志与诊断，B-17 应用接口，B-25 语音状态，B-36 模型／内容／应用包。

## 6. 对后续讨论的建议

这是本轮判断，尚未确定首期范围：

1. **先讨论记录的可靠完成**：怎样让用户知道原音已收到、转写在排队、知识页已更新，离线时能恢复到哪一步。小诺简录是很具体的比较对象。
2. **再选设备连接关系**：主设备独立联网、手机代联网、电脑桥接各有适用场景；可保留接口扩展，不要求首期同时实现三条链路。
3. **明确扩展应用的层次**：声明式卡片、设备脚本、编译应用与固件更新分别承担什么；将“Agent 帮我们写固件”和“Agent 运行时部署小应用”分别评估。
4. **把实时状态做清楚**：正在录音、等待后端、等待操作、完成与失败应能区分；唤醒、确认和重复输入都应有明确语义。

全部新增项保持待选择。本轮没有改变统一聊天入口、Obsidian、自动知识合并或 Agent 记忆管理的已确认方向，也没有选定新的开发框架。

访问说明：产品官网／玩法目录在本轮直接访问时多次超时，产品页信息只参考搜索索引摘要；功能核对主要依据可读的官方仓库、上游应用档案和作者仓库。未声称完整遍历了社区全部作品。
