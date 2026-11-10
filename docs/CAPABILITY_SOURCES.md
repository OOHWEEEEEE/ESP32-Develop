# 能力与来源项目索引

本索引根据现有能力池和调研报告整理，覆盖产品能力与底座候选。各项的首期决定沿用能力池，具体设计仍待讨论。

“来源项目”列指向相关来源组，部分来源组包含多个项目或技术资料。每组具体提供了什么、存在什么限制，以后面的来源说明及其链接为准。能力池中由多个来源组合推导的场景，不能视为某个项目已经实现完整功能。底座行中出现的 U、K 等编号指向本项目的能力条目。

当前整理基于已有调研资料，项目状态和当前版本未在本次整理中重新核验。

## 各项能力对应的来源

点击来源组可查看项目链接、原调研摘录和适配边界。

### 语音与多方式输入

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| U-01 | 按住说话进行语音问答 | 首期做 | [LOCAL-02 助手说明／会话实现](#local-02)、[LOCAL-11 端点配置／配置下发／协议](#local-11)、[PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[HA-03 BigBobbas S3 Box 3 Custom](#ha-03)、[RF-01 本地会话与状态／音频队列／音频接口等](#rf-01) |
| U-02 | 连续对话、免按键唤醒和实时打断 | 连续对话首期复用验证；唤醒／自动打断后续做 | [PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[PR-02 社区小智服务端](#pr-02)、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[SV-01 Pipecat 语音轮次／打断机制](#sv-01)、[HA-01 Home Assistant Voice PE／固件／Assist Satellite](#ha-01)、[S31-03 TinyML Demo](#s31-03)、[S31-15 ESP-Mosaico BSP](#s31-15)、[RF-01 本地会话与状态／音频队列／音频接口等](#rf-01)、[RF-05 监听模式／收音与 abort／Silero VAD等](#rf-05)、[RF-08 ESP-SR 官方支持表／官方组件版本／本地依赖条件等](#rf-08) |
| U-03 | 语音配合触屏选择、修改和确认 | 选择／确认首期最小版；中文短文本首期验证；完整编辑后续 | [LOCAL-03 A2UI／初始化](#local-03)、[LOCAL-12 网络页键盘／键盘接口／构建配置](#local-12)、[PR-04 Sticky／openHASP／FreeTouchDeck](#pr-04)、[HA-03 BigBobbas S3 Box 3 Custom](#ha-03)、[HA-04 openHASP／HA 配套集成／集成说明](#ha-04)、[RF-03 LVGL 9.5 拼音说明／官方示例／本地依赖版本等](#rf-03)、[RF-09 A2UI 接口／按钮事件／助手初始化](#rf-09) |
| U-04 | 个性化角色、声音和不同说话人 | 默认角色／音色／简单预设切换首期最小版；复刻／声纹后续 | [PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[PR-02 社区小智服务端](#pr-02)、[XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01)、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[XZ-03 joey-zhou/xiaozhi-esp32-server-java／更新记录](#xz-03)、[RF-06 真实角色切换工具／配置](#rf-06)、[RF-07 Edge provider／FunASR provider／Sherpa ASR provider等](#rf-07)、[RF-10 复刻 TTS 接口／声纹适配／声纹部署说明等](#rf-10) |
| U-05 | 回复可阅读、可朗读，播报可中止 | 本机朗读／既有耳机首期；跟页首期复用验证；其它输出后续 | [LOCAL-02 助手说明／会话实现](#local-02)、[PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[SV-01 Pipecat 语音轮次／打断机制](#sv-01)、[HA-01 Home Assistant Voice PE／固件／Assist Satellite](#ha-01)、[HA-03 BigBobbas S3 Box 3 Custom](#ha-03)、[S31-15 ESP-Mosaico BSP](#s31-15)、[AP-08 Muse Passport，passport 分支](#ap-08)、[RF-01 本地会话与状态／音频队列／音频接口等](#rf-01)、[RF-02 Muse 播放／缓冲／阅读跟随等](#rf-02)、[RF-04 厂商模式说明／蓝牙界面与连接／AT 模式切换等](#rf-04) |
| U-06 | 离线录音、联网后补处理 | 首期复用验证 | [LOCAL-06 文件传输说明／产品说明](#local-06)、[LOCAL-07 WorkBuddy](#local-07)、[PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05)、[WS-03 Rustmix Wave](#ws-03)、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05)、[AP-06 中枢入口／语音入口／工具实现等](#ap-06) |
| U-07 | 电脑／手机文字输入与多终端接续 | 后续做 | [AP-06 中枢入口／语音入口／工具实现等](#ap-06)、[AP-07 Pocket Intercom 手机端／固件分支／应用归档](#ap-07)、[XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01) |
| U-08 | 多台终端就近应答、避免同时回答 | 后续做 | [XZ-03 joey-zhou/xiaozhi-esp32-server-java／更新记录](#xz-03)、[SV-08 Home Assistant 语音流水线／Wyoming](#sv-08)、[SV-14 Quacksat 唤醒选择](#sv-14) |
| U-09 | USB 连接电脑接收按键、录放或作为语音终端 | F5 语音快捷键首期暂定；USB 录放和有线对话终端后续做 | [LOCAL-02 助手说明／会话实现](#local-02)、[LOCAL-06 文件传输说明／产品说明](#local-06)、[S31-07 官方 USB 方案／esp-usb／esp-iot-solution](#s31-07)、[S31-08 uext_screen／作者说明](#s31-08) |
| U-10 | 侧边滑条、背部触摸与接近／触摸唤醒 | 后续做 | [LOCAL-10 电源策略／共享电源](#local-10)、[S31-12 官方触摸与接近感知方案／滑条组件 0.3.0／S31 触摸驱动](#s31-12)、[S31-13 S31 低功耗核文档](#s31-13) |
| U-11 | 手机蓝牙免提通话与屏幕通话控制 | 后续做 | [S31-04 官方音频方案／esp_bt_audio](#s31-04)、[RF-04 厂商模式说明／蓝牙界面与连接／AT 模式切换等](#rf-04)、[LOCAL-10 电源策略／共享电源](#local-10) |
| U-12 | 手机通过 BLE 代联网的随身语音终端 | 后续做 | [AP-07 Pocket Intercom 手机端／固件分支／应用归档](#ap-07)、[AP-08 Muse Passport，passport 分支](#ap-08)、[LOCAL-02 助手说明／会话实现](#local-02) |

### 记录、知识和记忆

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| K-01 | 对话中直接记录、讨论后整理保存 | 首期核心，筛选后细化 | [PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05)、[PR-09 Obsidian Local REST API／MCPVault](#pr-09)、[PR-10 Knowledge Inbox／Audio Inbox／LLM Wiki 原始说明](#pr-10)、[WS-01 ALXV FolloUp，folloup-waveshare 分支](#ws-01)、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05)、[AP-06 中枢入口／语音入口／工具实现等](#ap-06) |
| K-02 | 定时归纳、更新已有主题笔记 | 首期核心，筛选后细化 | [PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05)、[PR-09 Obsidian Local REST API／MCPVault](#pr-09)、[PR-10 Knowledge Inbox／Audio Inbox／LLM Wiki 原始说明](#pr-10)、[WS-02 Chroninkle](#ws-02)、[SV-03 OpenClaw Automation／任务调度入口](#sv-03) |
| K-03 | 原始记录、整理产物、来源与修改历史关联 | 暂缓选择，筛选后集中讨论 | [LOCAL-02 助手说明／会话实现](#local-02)、[PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05)、[PR-10 Knowledge Inbox／Audio Inbox／LLM Wiki 原始说明](#pr-10)、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05) |
| K-04 | 查找旧想法、基于知识库回答 | 首期做，筛选后细化 | [PR-09 Obsidian Local REST API／MCPVault](#pr-09)、[PR-10 Knowledge Inbox／Audio Inbox／LLM Wiki 原始说明](#pr-10)、[AP-06 中枢入口／语音入口／工具实现等](#ap-06)、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[SV-05 RAGFlow](#sv-05) |
| K-05 | Agent 自主维护记忆 | 首期做，筛选后细化 | [PR-11 Letta／OpenClaw／Mem0](#pr-11)、[SV-04 Hermes Agent／定时任务](#sv-04) |
| K-06 | 按项目／主题生成回顾、周报或阶段摘要 | 首期做，筛选后细化 | [WS-02 Chroninkle](#ws-02)、[PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05) |
| K-07 | 想法复盘、标记跟进、搁置与完成 | 首期做，筛选后细化 | [WS-01 ALXV FolloUp，folloup-waveshare 分支](#ws-01)、[WS-02 Chroninkle](#ws-02)、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05)、[AP-06 中枢入口／语音入口／工具实现等](#ap-06) |
| K-08 | 录音标记、暂停继续、原音回放和校正 | 首期做，筛选后细化 | [WS-03 Rustmix Wave](#ws-03)、[PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05)、[S31-09 Harness ESP32S31](#s31-09)、[S31-10 S31 Playground／视频留言项目状态](#s31-10)、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05) |
| K-09 | 文件、图片和网页进入知识收件箱 | 首期做，筛选后细化 | [XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[SV-05 RAGFlow](#sv-05) |
| K-10 | 从材料生成主题页、时间线、导图等知识产物 | 首期做，筛选后细化 | [SV-05 RAGFlow](#sv-05) |
| K-11 | 查看材料处理状态、来源片段并重试 | 首期做，筛选后细化 | [XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[SV-05 RAGFlow](#sv-05)、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05) |
| K-12 | 联网搜索、网页阅读和来源追溯 | 后续做 | [XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01)、[SV-04 Hermes Agent／定时任务](#sv-04) |

### 任务、主动服务与外部控制

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| T-01 | 语音待办、日期安排和提醒 | 首期做，筛选后细化 | [LOCAL-05 首页应用／待机页](#local-05)、[PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05)、[PR-07 Hearth／EInk-Push](#pr-07) |
| T-02 | 闹钟、倒计时、番茄钟、重复和稍后提醒 | 首期做，筛选后细化 | [LOCAL-10 电源策略／共享电源](#local-10)、[WS-03 Rustmix Wave](#ws-03)、[PR-06 unidex／Pala Nekogotchi](#pr-06)、[AP-02 官方 demo 列表／猫咪番茄钟](#ap-02) |
| T-03 | 每日简报、晚间回顾与定时汇总 | 首期做，筛选后细化 | [PR-05 Pala Note 作者页／Forrest Note／Glane Notes](#pr-05)、[PR-03 InkHub／TRMNL](#pr-03)、[HA-07 pavlojs e-Paper Dashboard](#ha-07)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| T-04 | 后台任务继续执行、查看进度和结果 | 首期做，筛选后细化 | [LOCAL-07 WorkBuddy](#local-07)、[PR-12 Watcher／StackChan／AInk等](#pr-12)、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[SV-02 LangGraph 持久化／暂停恢复](#sv-02)、[SV-07 Temporal 执行与恢复](#sv-07) |
| T-05 | 语音遥控电脑／Coding Agent | 后续做 | [LOCAL-07 WorkBuddy](#local-07)、[PR-08 vibecoding-plus／Claude 状态桥／Codex 看板](#pr-08)、[AP-03 Claude Buddy 分支说明](#ap-03)、[AP-14 Codex Buddy](#ap-14) |
| T-06 | Home Assistant、设备和外部服务控制 | 后续做 | [PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[PR-04 Sticky／openHASP／FreeTouchDeck](#pr-04)、[PR-12 Watcher／StackChan／AInk等](#pr-12)、[CAM-08 ESPHome Camera](#cam-08)、[HA-00 ESPHome Native API／LVGL／Voice Assistant](#ha-00)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22)、[S31-14 ESP-Mosaico Matter／Zigbee SDK 更新记录](#s31-14) |
| T-07 | AI 额度、任务状态、日历和服务状态看板 | 首期做，筛选后细化 | [WS-05 QuotaFrame／设备能力表](#ws-05)、[PR-08 vibecoding-plus／Claude 状态桥／Codex 看板](#pr-08)、[PR-03 InkHub／TRMNL](#pr-03)、[AP-03 Claude Buddy 分支说明](#ap-03)、[AP-14 Codex Buddy](#ap-14) |
| T-08 | 共享购物、家庭便签、一周菜单与分工 | 后续做 | [PR-07 Hearth／EInk-Push](#pr-07) |
| T-09 | 同一聊天入口切换／委托外部 Agent | 后续做 | [XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[XZ-06 hougeai/xiaozhiPro](#xz-06) |
| T-10 | 保存和复用个人工作流程 | 首期做，筛选后细化 | [SV-04 Hermes Agent／定时任务](#sv-04)、[SV-06 n8n Wait](#sv-06) |
| T-11 | 持续关注主题或状态，有变化才报告 | 后续做 | [SV-03 OpenClaw Automation／任务调度入口](#sv-03)、[SV-04 Hermes Agent／定时任务](#sv-04) |
| T-12 | 设备间呼叫、对讲、留言和广播 | 后续做 | [XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01)、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[S31-09 Harness ESP32S31](#s31-09)、[S31-10 S31 Playground／视频留言项目状态](#s31-10) |
| T-13 | 复杂任务拆分、委派与汇总 | 后续做 | [SV-04 Hermes Agent／定时任务](#sv-04) |
| T-14 | 外部事件触发指定工作流程 | 首期做，筛选后细化 | [XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01)、[SV-03 OpenClaw Automation／任务调度入口](#sv-03)、[SV-06 n8n Wait](#sv-06)、[SV-08 Home Assistant 语音流水线／Wyoming](#sv-08)、[HA-12 Everything Presence Lite／产品文档](#ha-12)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| T-15 | 观察手机画面并操作界面的 Agent | 后续做 | [AP-15 AI Passport iPhone Agent](#ap-15) |

### 屏幕交互与内容呈现

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| S-01 | 富文本、公式、图片和结构化卡片回复 | 首期做，筛选后细化 | [LOCAL-03 A2UI／初始化](#local-03) |
| S-02 | 可操作的结果卡片 | 首期做，筛选后细化 | [LOCAL-03 A2UI／初始化](#local-03)、[PR-04 Sticky／openHASP／FreeTouchDeck](#pr-04)、[AP-03 Claude Buddy 分支说明](#ap-03)、[AP-14 Codex Buddy](#ap-14) |
| S-03 | 多来源显示调度、临时占屏和常驻回退 | 首期做，筛选后细化 | [PR-03 InkHub／TRMNL](#pr-03)、[HA-06 Weatherman Dashboard](#ha-06) |
| S-04 | 待机／关机保留待办、项目焦点和结果摘要 | 首期做，筛选后细化 | [LOCAL-05 首页应用／待机页](#local-05)、[WS-02 Chroninkle](#ws-02)、[HA-07 pavlojs e-Paper Dashboard](#ha-07) |
| S-05 | 相册、壁纸、图表与图像内容推送 | 首期做，筛选后细化 | [LOCAL-05 首页应用／待机页](#local-05)、[LOCAL-06 文件传输说明／产品说明](#local-06)、[PR-03 InkHub／TRMNL](#pr-03) |
| S-06 | Agent 动态部署设备小应用 | 首期做，筛选后细化 | [WS-07 OnlyClaws ESP／构建配置](#ws-07)、[WS-03 Rustmix Wave](#ws-03)、[PR-06 unidex／Pala Nekogotchi](#pr-06)、[PR-12 Watcher／StackChan／AInk等](#pr-12)、[S31-11 ESP-Claw／Skills Lab](#s31-11)、[AP-10 MicroPython 工具箱／BLE／小程序协议／缺陷修复记录](#ap-10) |
| S-07 | 桌面预览、界面模拟和布局调试 | 首期做，筛选后细化 | [WS-06 CrossMux／微雪目标记录](#ws-06)、[PR-07 Hearth／EInk-Push](#pr-07)、[HA-10 OMOTE 社区固件](#ha-10)、[HA-18 firsttris Energy Dashboard](#ha-18) |
| S-08 | USB 桌面副屏、文档或选定窗口镜像 | 后续做 | [S31-07 官方 USB 方案／esp-usb／esp-iot-solution](#s31-07)、[S31-08 uext_screen／作者说明](#s31-08) |
| S-09 | 主辅屏与多设备协同显示、互动 | 后续做 | [S31-18 官方 HMI 方案](#s31-18)、[S31-15 ESP-Mosaico BSP](#s31-15) |
| S-10 | 电子名片、个人资料、二维码与 NFC 链接入口 | 首期做，筛选后细化 | [AP-00 官方共创入口／产品官网／官方仓库等](#ap-00)、[AP-01 产品规格／硬件指南／BSP 参数](#ap-01) |

### 阅读、写作与学习

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| R-01 | 本地 EPUB／TXT／电子书和图像阅读 | 首期保留 | [LOCAL-04 阅读代码／书签数据](#local-04) |
| R-02 | 当前页提问、语音批注、摘录进知识库 | 后续做 | [LOCAL-04 阅读代码／书签数据](#local-04)、[WS-06 CrossMux／微雪目标记录](#ws-06) |
| R-03 | 词典、单词／知识卡复习、朗读与拼写练习 | 后续做 | [WS-03 Rustmix Wave](#ws-03)、[WS-06 CrossMux／微雪目标记录](#ws-06)、[PR-07 Hearth／EInk-Push](#pr-07) |
| R-04 | 外接键盘 Markdown 写作／修改笔记 | 首期做，筛选后细化 | [WS-04 Draftling／硬件表](#ws-04)、[S31-07 官方 USB 方案／esp-usb／esp-iot-solution](#s31-07) |
| R-05 | 网页／OPDS／WebDAV／Calibre 内容传输 | 首期做，筛选后细化 | [LOCAL-06 文件传输说明／产品说明](#local-06)、[WS-06 CrossMux／微雪目标记录](#ws-06)、[S31-07 官方 USB 方案／esp-usb／esp-iot-solution](#s31-07) |
| R-06 | 遥控翻页、重力旋转与阅读统计 | 后续做 | [LOCAL-04 阅读代码／书签数据](#local-04)、[WS-03 Rustmix Wave](#ws-03)、[WS-05 QuotaFrame／设备能力表](#ws-05)、[WS-06 CrossMux／微雪目标记录](#ws-06) |
| R-07 | 离线专题图鉴与知识速查包 | 首期做，筛选后细化 | [AP-17 离线图鉴档案／源码分支](#ap-17) |
| R-08 | 互动图文故事、分支阅读与场景练习 | 后续做 | [AP-18 Asunabi 阅读器档案／视觉小说案例索引](#ap-18) |

### 摄像头与视觉

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| V-01 | 拍一张照片并语音提问 | 首期做，筛选后细化 | [LOCAL-08 DVP 采集／相机适配／MCP](#local-08)、[PR-01 小智官方固件／协议／MCP 示例](#pr-01) |
| V-02 | 图片加口述说明，形成视觉笔记 | 首期做，筛选后细化 | [LOCAL-09 助手拍照](#local-09)、K-01、K-02 |
| V-03 | 纸面／票据／屏幕 OCR、摘要和翻译 | 后续做 | [CAM-07 PP-OCRv6 官方组件](#cam-07)、[LOCAL-08 DVP 采集／相机适配／MCP](#local-08)、[SV-05 RAGFlow](#sv-05) |
| V-04 | 二维码读入链接、设备或物品标识 | 后续做 | [CAM-04 ESP32QRCodeReader](#cam-04)、[CAM-06 ESP-VISION S31 指南／支持表](#cam-06)、[S31-02 S31 视觉工作坊／ESP-VISION 支持表](#s31-02) |
| V-05 | 特定对象、人脸或人员出现事件 | 首期做，筛选后细化 | [CAM-03 ESP-WHO／官方入门例程](#cam-03)、[CAM-05 ESP-DL](#cam-05)、[S31-01 官方边缘视觉方案](#s31-01)、[S31-02 S31 视觉工作坊／ESP-VISION 支持表](#s31-02)、[S31-03 TinyML Demo](#s31-03) |
| V-06 | 周期抽帧、带目标的场景观察 | 首期做，筛选后细化 | [LOCAL-08 DVP 采集／相机适配／MCP](#local-08)、[PR-12 Watcher／StackChan／AInk等](#pr-12) |
| V-07 | 画面变化／运动触发抓拍和通知 | 后续做 | [CAM-01 ESP32-CAM_MJPEG2SD](#cam-01)、[PR-12 Watcher／StackChan／AInk等](#pr-12) |
| V-08 | 浏览器／NAS 查看实时相机流 | 后续做 | [CAM-02 esp32cam-rtsp](#cam-02)、[CAM-01 ESP32-CAM_MJPEG2SD](#cam-01) |
| V-09 | SD 录像、事件片段、延时摄影与回放 | 首期做，筛选后细化 | [CAM-01 ESP32-CAM_MJPEG2SD](#cam-01)、[S31-10 S31 Playground／视频留言项目状态](#s31-10) |
| V-10 | 多相机／外部视觉源接入 Agent | 后续做 | [CAM-02 esp32cam-rtsp](#cam-02)、[CAM-08 ESPHome Camera](#cam-08)、[PR-12 Watcher／StackChan／AInk等](#pr-12)、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[S31-07 官方 USB 方案／esp-usb／esp-iot-solution](#s31-07) |
| V-11 | 端侧小模型、颜色／几何／标记识别 | 首期做，筛选后细化 | [CAM-05 ESP-DL](#cam-05)、[CAM-06 ESP-VISION S31 指南／支持表](#cam-06)、[S31-01 官方边缘视觉方案](#s31-01)、[S31-02 S31 视觉工作坊／ESP-VISION 支持表](#s31-02)、[S31-03 TinyML Demo](#s31-03) |
| V-12 | 手势翻页或控制卡片 | 后续做 | [WS-05 QuotaFrame／设备能力表](#ws-05)、[CAM-05 ESP-DL](#cam-05)、[CAM-06 ESP-VISION S31 指南／支持表](#cam-06)、[S31-01 官方边缘视觉方案](#s31-01)、[S31-02 S31 视觉工作坊／ESP-VISION 支持表](#s31-02) |
| V-13 | 姿态关键点、手部区域事件与动作交互 | 后续做 | [S31-01 官方边缘视觉方案](#s31-01)、[S31-02 S31 视觉工作坊／ESP-VISION 支持表](#s31-02) |

### 传感器、媒体与陪伴

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| F-01 | 倾斜、摇动等体感操作或小游戏 | 首期做，筛选后细化 | [LOCAL-01 板型定义／产品说明](#local-01)、[WS-03 Rustmix Wave](#ws-03)、[S31-15 ESP-Mosaico BSP](#s31-15) |
| F-02 | 天气与环境信息、传感器事件 | 首期做，筛选后细化 | [LOCAL-01 板型定义／产品说明](#local-01)、[WS-05 QuotaFrame／设备能力表](#ws-05)、[PR-03 InkHub／TRMNL](#pr-03)、[XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01)、[HA-12 Everything Presence Lite／产品文档](#ha-12)、[HA-16 AirGradient 固件／HA 集成](#ha-16)、[S31-15 ESP-Mosaico BSP](#s31-15) |
| F-03 | 宠物、陪伴表情、状态动画和轻量游戏 | 首期做，筛选后细化 | [PR-06 unidex／Pala Nekogotchi](#pr-06)、[PR-07 Hearth／EInk-Push](#pr-07)、[PR-12 Watcher／StackChan／AInk等](#pr-12)、[S31-15 ESP-Mosaico BSP](#s31-15)、[S31-18 官方 HMI 方案](#s31-18)、[AP-02 官方 demo 列表／猫咪番茄钟](#ap-02)、[AP-03 Claude Buddy 分支说明](#ap-03)、[AP-11 zh30/PassportOS](#ap-11)、[AP-14 Codex Buddy](#ap-14)、[AP-16 Faraway 应用档案／源码分支](#ap-16) |
| F-04 | 音乐／播客／个人音频库和媒体控制 | 首期做，筛选后细化 | [LOCAL-01 板型定义／产品说明](#local-01)、[PR-12 Watcher／StackChan／AInk等](#pr-12)、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[HA-02 Satellite1-ESPHome](#ha-02)、[HA-03 BigBobbas S3 Box 3 Custom](#ha-03)、[HA-19 Squeezelite-ESP32／HA Squeezebox 集成](#ha-19)、[S31-04 官方音频方案／esp_bt_audio](#s31-04)、[S31-05 ESP32-S31 A2DP Codecs](#s31-05)、[S31-09 Harness ESP32S31](#s31-09)、[AP-13 aipassport-radio](#ap-13) |
| F-05 | LE Audio／Auracast 共享收听与广播 | 首期做，筛选后细化 | [S31-04 官方音频方案／esp_bt_audio](#s31-04)、[S31-06 Auracast Transmitter](#s31-06) |
| F-06 | 离线短语／音效板与固定声音包 | 后续做 | [AP-19 Voice Keychain 档案／源码分支](#ap-19) |
| F-07 | 随机选择与轻量决策转盘 | 后续做 | [AP-20 今天吃什么档案／源码分支](#ap-20) |
| F-08 | 经典游戏模拟与外接手柄操作 | 后续做 | [AP-21 Game Boy／FC／NES／BLE 输入经验](#ap-21) |

### 家庭场景与 Home Assistant

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| H-01 | 按房间查看和控制家庭设备 | 后续做 | [HA-03 BigBobbas S3 Box 3 Custom](#ha-03)、[HA-04 openHASP／HA 配套集成／集成说明](#ha-04)、[HA-05 NSPanel HA Blueprint](#ha-05) |
| H-02 | 一键／一句话执行家庭场景 | 后续做 | [HA-05 NSPanel HA Blueprint](#ha-05)、[HA-10 OMOTE 社区固件](#ha-10)、[HA-21 Tasmota／ESP32 功能／Rules等](#ha-21)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| H-03 | 房间／区域有人检测 | 后续做 | [HA-02 Satellite1-ESPHome](#ha-02)、[HA-12 Everything Presence Lite／产品文档](#ha-12) |
| H-04 | 通过已绑定设备推测所在房间 | 后续做 | [HA-11 ESPresense／官方说明](#ha-11) |
| H-05 | 旋钮、实体键与遥控器快速操作 | 后续做 | [HA-08 Skons/M5Dial／Jasionf Smart Home Button](#ha-08)、[HA-09 SeedLabs SmartKnob 固件／HA 集成](#ha-09)、[HA-10 OMOTE 社区固件](#ha-10) |
| H-06 | 旧电器的红外／射频接入 | 后续做 | [HA-10 OMOTE 社区固件](#ha-10)、[HA-14 OpenMQTTGateway／HA 集成](#ha-14) |
| H-07 | 扩展蓝牙覆盖与远端设备采集 | 后续做 | [HA-13 ESPHome Bluetooth Proxies／代理组件](#ha-13)、[HA-14 OpenMQTTGateway／HA 集成](#ha-14) |
| H-08 | 环境趋势、通风提醒与舒适度联动 | 后续做 | [HA-12 Everything Presence Lite／产品文档](#ha-12)、[HA-16 AirGradient 固件／HA 集成](#ha-16) |
| H-09 | 家庭用电、光伏、储能与费用看板 | 后续做 | [HA-17 CircuitSetup ESP32 Energy Meter](#ha-17)、[HA-18 firsttris Energy Dashboard](#ha-18) |
| H-10 | 断网时保留指定本地控制 | 后续做 | [HA-05 NSPanel HA Blueprint](#ha-05)、[HA-21 Tasmota／ESP32 功能／Rules等](#ha-21) |
| H-11 | NFC 实物卡触发场景、媒体或对象定位 | 后续做 | [HA-20 ESP32 Tag Reader／按需扫描的 S3 衍生示例](#ha-20) |
| H-12 | 灯光效果表达任务和家庭状态 | 后续做 | [HA-15 WLED／HA 集成](#ha-15) |
| H-13 | 家庭历史查询与事件回顾 | 后续做 | [HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| H-14 | Matter／Thread／Zigbee 接入、中枢与桥接 | 后续做 | [S31-14 ESP-Mosaico Matter／Zigbee SDK 更新记录](#s31-14) |
| H-15 | ESP-NOW 等本地链路的多设备协作 | 后续做 | [S31-15 ESP-Mosaico BSP](#s31-15) |

### 底座候选

| 编号 | 能力 | 当前范围 | 来源项目和相关能力 |
| --- | --- | --- | --- |
| B-01 | 统一内部事件 | 候选，待讨论 | U-01、U-03、U-07、V-10 |
| B-02 | 会话与历史 | 候选，待讨论 | [LOCAL-02 助手说明／会话实现](#local-02)、[PR-01 小智官方固件／协议／MCP 示例](#pr-01) |
| B-03 | 音频与模型服务接口 | 候选，待讨论 | [PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[PR-02 社区小智服务端](#pr-02)、[XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01)、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[SV-08 Home Assistant 语音流水线／Wyoming](#sv-08)、[RF-07 Edge provider／FunASR provider／Sherpa ASR provider等](#rf-07) |
| B-04 | 工具登记与执行 | 候选，待讨论 | [PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[PR-02 社区小智服务端](#pr-02)、[PR-09 Obsidian Local REST API／MCPVault](#pr-09)、[AP-06 中枢入口／语音入口／工具实现等](#ap-06)、[AP-12 aipassport-fw](#ap-12) |
| B-05 | Agent 记忆管理 | 候选，待讨论 | K-05、[PR-11 Letta／OpenClaw／Mem0](#pr-11) |
| B-06 | 知识写入与版本 | 候选，待讨论 | K-01、K-02、K-03、[PR-10 Knowledge Inbox／Audio Inbox／LLM Wiki 原始说明](#pr-10) |
| B-07 | 检索与引用 | 候选，待讨论 | K-04、K-09、K-11、K-12、[SV-05 RAGFlow](#sv-05)、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02) |
| B-08 | 持久任务 | 候选，待讨论 | T-04、[LOCAL-07 WorkBuddy](#local-07)、[PR-10 Knowledge Inbox／Audio Inbox／LLM Wiki 原始说明](#pr-10) |
| B-09 | 时间与事件触发 | 候选，待讨论 | K-02、T-01、T-02、T-03、T-11、T-14、[SV-03 OpenClaw Automation／任务调度入口](#sv-03)、[SV-06 n8n Wait](#sv-06)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| B-10 | 通知与结果投递 | 候选，待讨论 | U-06、T-04、[LOCAL-10 电源策略／共享电源](#local-10)、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[SV-11 ntfy 消息与动作／订阅](#sv-11) |
| B-11 | 卡片与动作回传 | 候选，待讨论 | S-01、S-02、[LOCAL-03 A2UI／初始化](#local-03)、[PR-04 Sticky／openHASP／FreeTouchDeck](#pr-04)、[HA-04 openHASP／HA 配套集成／集成说明](#ha-04)、[HA-08 Skons/M5Dial／Jasionf Smart Home Button](#ha-08)、[AP-03 Claude Buddy 分支说明](#ap-03)、[AP-14 Codex Buddy](#ap-14) |
| B-12 | 显示调度 | 候选，待讨论 | S-03、S-04、[PR-03 InkHub／TRMNL](#pr-03)、[HA-06 Weatherman Dashboard](#ha-06)、[HA-07 pavlojs e-Paper Dashboard](#ha-07) |
| B-13 | 设备资源协调 | 候选，待讨论 | [LOCAL-06 文件传输说明／产品说明](#local-06)、[LOCAL-08 DVP 采集／相机适配／MCP](#local-08)、[LOCAL-10 电源策略／共享电源](#local-10)、[S31-09 Harness ESP32S31](#s31-09)、[S31-15 ESP-Mosaico BSP](#s31-15)、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05)、[AP-22 待机与唤醒经验／串口截图协议／工程经验索引](#ap-22) |
| B-14 | 文件与媒体资产 | 候选，待讨论 | R-05、V-02、S-05 |
| B-15 | 配置、身份和更新 | 候选，待讨论 | [LOCAL-11 端点配置／配置下发／协议](#local-11)、[PR-01 小智官方固件／协议／MCP 示例](#pr-01)、[PR-02 社区小智服务端](#pr-02)、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[XZ-03 joey-zhou/xiaozhi-esp32-server-java／更新记录](#xz-03)、[HA-00 ESPHome Native API／LVGL／Voice Assistant](#ha-00)、[HA-13 ESPHome Bluetooth Proxies／代理组件](#ha-13)、[S31-09 Harness ESP32S31](#s31-09)、[AP-07 Pocket Intercom 手机端／固件分支／应用归档](#ap-07)、[AP-08 Muse Passport，passport 分支](#ap-08)、[AP-14 Codex Buddy](#ap-14) |
| B-16 | 运行观测与验证 | 候选，待讨论 | [PR-02 社区小智服务端](#pr-02)、[WS-03 Rustmix Wave](#ws-03)、S-07、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[SV-10 Langfuse 观测／评测分数](#sv-10)、[AP-22 待机与唤醒经验／串口截图协议／工程经验索引](#ap-22) |
| B-17 | 可扩展模块与协议版本 | 候选，待讨论 | [WS-07 OnlyClaws ESP／构建配置](#ws-07)、[WS-06 CrossMux／微雪目标记录](#ws-06)、[PR-06 unidex／Pala Nekogotchi](#pr-06)、[S31-11 ESP-Claw／Skills Lab](#s31-11)、[AP-10 MicroPython 工具箱／BLE／小程序协议／缺陷修复记录](#ap-10)、[AP-11 zh30/PassportOS](#ap-11)、[AP-12 aipassport-fw](#ap-12) |
| B-18 | 图像源与视觉处理 | 候选，待讨论 | [LOCAL-08 DVP 采集／相机适配／MCP](#local-08)、[CAM-01 ESP32-CAM_MJPEG2SD](#cam-01)、[CAM-06 ESP-VISION S31 指南／支持表](#cam-06)、V-10 |
| B-19 | 动态上下文与状态快照 | 候选，待讨论 | [XZ-01 xinnan-tech/xiaozhi-esp32-server／单模块部署](#xz-01)、T-03、T-14、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| B-20 | Agent 路由与技能 | 候选，待讨论 | T-09、T-10、[XZ-02 hackers365/xiaozhi-esp32-server-golang／OpenClaw 接入／知识库](#xz-02)、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[SV-04 Hermes Agent／定时任务](#sv-04) |
| B-21 | 多步骤流程与暂停恢复 | 候选，待讨论 | T-04、S-02、[SV-02 LangGraph 持久化／暂停恢复](#sv-02)、[SV-06 n8n Wait](#sv-06)、[SV-07 Temporal 执行与恢复](#sv-07) |
| B-22 | 模型路由、预算和降级 | 候选，待讨论 | B-03、[SV-09 LiteLLM Router](#sv-09)、T-03、K-02 |
| B-23 | 工具目录、可见性与协议桥接 | 候选，待讨论 | B-04、[XZ-07 shenjingnan/xiaozhi-client](#xz-07)、[XZ-08 xinnan-tech/mcp-endpoint-server／ziruny 衍生版](#xz-08)、[XZ-09 Verdure MCP Platform](#xz-09)、[SV-12 IBM ContextForge](#sv-12)、[HA-14 OpenMQTTGateway／HA 集成](#ha-14)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| B-24 | 使用者、角色与数据域 | 候选，待讨论 | U-04、T-08、[XZ-03 joey-zhou/xiaozhi-esp32-server-java／更新记录](#xz-03)、[XZ-09 Verdure MCP Platform](#xz-09)、[HA-11 ESPresense／官方说明](#ha-11) |
| B-25 | 语音轮次与取消协调 | 候选，待讨论 | U-01、U-02、U-05、[SV-01 Pipecat 语音轮次／打断机制](#sv-01)、[AP-07 Pocket Intercom 手机端／固件分支／应用归档](#ap-07)、[AP-08 Muse Passport，passport 分支](#ap-08) |
| B-26 | 场景样例、效果评测与版本回归 | 候选，待讨论 | [SV-10 Langfuse 观测／评测分数](#sv-10)、K-02、B-16 |
| B-27 | 本地与外部执行环境 | 候选，待讨论 | T-05、T-09、T-13、[XZ-06 hougeai/xiaozhiPro](#xz-06)、[SV-04 Hermes Agent／定时任务](#sv-04) |
| B-28 | 数据导出、备份与恢复 | 候选，待讨论 | K-03、B-14、[SV-13 SQLite Online Backup API](#sv-13) |
| B-29 | 家庭实体、空间与连接器 | 候选，待讨论 | H-01、H-02、[HA-00 ESPHome Native API／LVGL／Voice Assistant](#ha-00)、[HA-04 openHASP／HA 配套集成／集成说明](#ha-04)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22) |
| B-30 | 状态订阅与控制回报 | 候选，待讨论 | [HA-08 Skons/M5Dial／Jasionf Smart Home Button](#ha-08)、[HA-22 HA WebSocket API／MQTT／MCP Server](#ha-22)、B-11、B-19 |
| B-31 | 传感器与历史数据语义 | 候选，待讨论 | [HA-11 ESPresense／官方说明](#ha-11)、[HA-12 Everything Presence Lite／产品文档](#ha-12)、[HA-16 AirGradient 固件／HA 集成](#ha-16)、[HA-17 CircuitSetup ESP32 Energy Meter](#ha-17)、[HA-18 firsttris Energy Dashboard](#ha-18) |
| B-32 | 本地规则与控制优先级 | 候选，待讨论 | H-10、[HA-05 NSPanel HA Blueprint](#ha-05)、[HA-21 Tasmota／ESP32 功能／Rules等](#ha-21) |
| B-33 | 音频输出路由与抢占 | 候选，待讨论 | U-05、F-04、[HA-01 Home Assistant Voice PE／固件／Assist Satellite](#ha-01)、[HA-02 Satellite1-ESPHome](#ha-02)、[HA-03 BigBobbas S3 Box 3 Custom](#ha-03)、[HA-19 Squeezelite-ESP32／HA Squeezebox 集成](#ha-19)、[S31-04 官方音频方案／esp_bt_audio](#s31-04)、[S31-09 Harness ESP32S31](#s31-09) |
| B-34 | USB 角色与设备类 | 候选，待讨论 | U-09、S-08、R-04、R-05、V-10、[S31-07 官方 USB 方案／esp-usb／esp-iot-solution](#s31-07)、[S31-08 uext_screen／作者说明](#s31-08) |
| B-35 | 图像与音频硬件处理管线 | 候选，待讨论 | [S31-00 芯片数据手册／量产公告／软件状态入口](#s31-00)、[S31-04 官方音频方案／esp_bt_audio](#s31-04)、[S31-07 官方 USB 方案／esp-usb／esp-iot-solution](#s31-07)、[S31-18 官方 HMI 方案](#s31-18) |
| B-36 | 端侧模型与应用包 | 候选，待讨论 | S-06、V-11、[S31-01 官方边缘视觉方案](#s31-01)、[S31-03 TinyML Demo](#s31-03)、[S31-11 ESP-Claw／Skills Lab](#s31-11)、[S31-16 78/nuttx-esp32s31](#s31-16)、[AP-10 MicroPython 工具箱／BLE／小程序协议／缺陷修复记录](#ap-10)、[AP-17 离线图鉴档案／源码分支](#ap-17)、[AP-18 Asunabi 阅读器档案／视觉小说案例索引](#ap-18)、[AP-22 待机与唤醒经验／串口截图协议／工程经验索引](#ap-22) |
| B-37 | 低功耗后台与唤醒 | 候选，待讨论 | U-10、[S31-12 官方触摸与接近感知方案／滑条组件 0.3.0／S31 触摸驱动](#s31-12)、[S31-13 S31 低功耗核文档](#s31-13) |
| B-38 | 外设能力目录与设备拓扑 | 候选，待讨论 | S-09、H-15、[S31-15 ESP-Mosaico BSP](#s31-15) |
| B-39 | 终端链路与伴侣桥接 | 候选，待讨论 | U-12、[AP-06 中枢入口／语音入口／工具实现等](#ap-06)、[AP-07 Pocket Intercom 手机端／固件分支／应用归档](#ap-07)、[AP-08 Muse Passport，passport 分支](#ap-08)、[AP-10 MicroPython 工具箱／BLE／小程序协议／缺陷修复记录](#ap-10) |
| B-40 | 多端数据同步与离线变更 | 候选，待讨论 | U-06、K-03、K-07、K-11、[AP-05 小诺简录／设备固件分支／上游应用档案](#ap-05)、[AP-06 中枢入口／语音入口／工具实现等](#ap-06) |
| B-41 | 应用生命周期与统一输入 | 候选，待讨论 | [AP-02 官方 demo 列表／猫咪番茄钟](#ap-02)、[AP-10 MicroPython 工具箱／BLE／小程序协议／缺陷修复记录](#ap-10)、[AP-11 zh30/PassportOS](#ap-11)、[AP-12 aipassport-fw](#ap-12)、[AP-21 Game Boy／FC／NES／BLE 输入经验](#ap-21)、[AP-22 待机与唤醒经验／串口截图协议／工程经验索引](#ap-22) |

#### 通过产品能力关联的来源

B-01 和 B-14 在能力池中通过产品能力编号关联资料。以下项目沿该关系展开，可用于继续查找参考。它们对对应底座的具体支持仍需逐项核对。

**B-01 统一内部事件**

- U-01 关联本产品助手、配置与协议、小智官方固件、Home Assistant S3 Box 3 Custom 和本地会话复核。 [LOCAL-02](#local-02) · [LOCAL-11](#local-11) · [PR-01](#pr-01) · [HA-03](#ha-03) · [RF-01](#rf-01)
- U-03 关联本产品 A2UI 与触屏键盘、Sticky、openHASP、FreeTouchDeck、S3 Box 3 Custom 和输入复核。 [LOCAL-03](#local-03) · [LOCAL-12](#local-12) · [PR-04](#pr-04) · [HA-03](#ha-03) · [HA-04](#ha-04) · [RF-03](#rf-03) · [RF-09](#rf-09)
- U-07 关联小诺简录中枢、Pocket Intercom 和小智社区服务端。 [AP-06](#ap-06) · [AP-07](#ap-07) · [XZ-01](#xz-01)
- V-10 关联 esp32cam-rtsp、ESPHome Camera、Watcher 等项目、小智 Pro 和 ESP32-S31 USB 方案。 [CAM-02](#cam-02) · [CAM-08](#cam-08) · [PR-12](#pr-12) · [XZ-06](#xz-06) · [S31-07](#s31-07)

**B-14 文件与媒体资产**

- R-05 关联本产品文件传输、CrossMux 和 ESP32-S31 USB 方案。 [LOCAL-06](#local-06) · [WS-06](#ws-06) · [S31-07](#s31-07)
- V-02 关联本产品助手拍照，以及 K-01、K-02 的记录与知识整理来源。 [LOCAL-09](#local-09) · [K-01 和 K-02](#记录知识和记忆)
- S-05 关联本产品首页与文件传输、InkHub 和 TRMNL。 [LOCAL-05](#local-05) · [LOCAL-06](#local-06) · [PR-03](#pr-03)

## 来源项目与资料说明

下列说明保留原报告对参考能力及适配条件的描述。来源编号中的项目资料可能包含官方文档、具体代码、作者说明及方法参考。

### 本产品源码

#### LOCAL-01

[板型定义](E:/ESP32-SERVICE/main/boards/metalio-e-ink4-plus/config.h)、[产品说明](E:/ESP32-SERVICE/README_zn.md)

并行墨水屏、触摸与按键、冷暖前光、SD、音频、RTC、三轴加速度计、摄像头等已有定义。 是源码板型基线；实物版本、外设装配和表现仍需实机确认

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-02

[助手说明](E:/ESP32-SERVICE/main/display/screen/assistant_screen/README.md)、[会话实现](E:/ESP32-SERVICE/main/application.cc)

PTT、小智模式、识别和回复显示、会话分页及临时历史。 切换页面或待机会影响会话；SD 聊天历史开机清空，不可充当服务端长期记忆

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-03

[A2UI](E:/ESP32-SERVICE/main/display/a2ui/README.md)、[初始化](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_fonts.cc)

富文本、公式、图片、卡片及按钮渲染；助手初始化将 on_action 置空。 渲染按钮与把操作送回服务端是两项工作，完整交互闭环尚需接通

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-04

[阅读代码](E:/ESP32-SERVICE/main/reader/)、[书签数据](E:/ESP32-SERVICE/main/reader/book_bookmarks.h)

电子书、EPUB、TXT、书签、阅读进度、字体和排版；文档说明图像书及自动方向。 当前页内容／书签尚需显式暴露给 Agent，不能直接视为已支持阅读问答

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-05

[首页应用](E:/ESP32-SERVICE/main/display/screen/home_screen/home_screen.cc)、[待机页](E:/ESP32-SERVICE/main/display/screen/standby_screen/)

清单、最近阅读、天气和待办待机摘要、壁纸、多个首页主题。 云端业务端点当前为空；本地界面存在不等于自建服务端已有同步能力

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-06

[文件传输说明](E:/ESP32-SERVICE/docs/ap-file-transfer.md)、[产品说明](E:/ESP32-SERVICE/README_zn.md)

AP／局域网文件管理、USB MSC、云端文件接收、字体和书籍导入。 文件访问与 SD 挂载需协调；USB 接管 SD 时不能假设其他应用仍可同时操作文件

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-07

[WorkBuddy](E:/ESP32-SERVICE/main/workbuddy/README.md)

扫码绑定、语音提交、按受理编号读取回复、同步文字历史、待机暂停。 依赖其服务端／账号体系。可参考任务编号和结果快照机制，不等于现成的通用电脑 Agent 桥

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-08

[DVP 采集](E:/ESP32-SERVICE/main/boards/common/camera/dvp_camera.cc)、[相机适配](E:/ESP32-SERVICE/main/boards/common/camera/dvp_camera_adapter.cc)、[MCP](E:/ESP32-SERVICE/main/mcp_server.cc)

GC2145 以 640×480 RGB565 采集，硬件编码 JPEG；MCP 拍照后用 HTTP 上传图片与问题。 视觉服务由 MCP 初始化中的 vision.url 配置；该路径尚无本地识图模型

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-09

[助手拍照](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_boot_photo.cc)

双击 BOOT 的拍照入口、原图上传尝试、灰度图插入会话；上传失败仍可继续本地插图。 上传业务使用 api::VisionUploadUrl，与 MCP 拍照解释地址独立；不是持久影像笔记的完整实现

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-10

[电源策略](E:/ESP32-SERVICE/main/boards/common/power_policy/README.md)、[共享电源](E:/ESP32-SERVICE/main/boards/metalio-e-ink4-plus/display/epd_board_metalio_eink4_plus.c)

业务声明电源需求、待机收尾、网络暂停、浅睡眠切片、恢复和关机。 不能套用其他 S3 项目的深睡代码；主动通知和远程任务必须处理设备离线／待机

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-11

[端点配置](E:/ESP32-SERVICE/main/cloudzao_endpoints.c)、[配置下发](E:/ESP32-SERVICE/main/ota.cc)、[协议](E:/ESP32-SERVICE/main/protocols/websocket_protocol.cc)

开源端点为空；对话配置可下发 URL、Token、协议版本；音频和控制消息已有协议。 自建服务端仍需实现配置、会话、鉴权及业务接口。固件升级检查和对话配置请求独立

[原调研记录](research/2026-11-08-esp32-projects.md)

#### LOCAL-12

[网络页键盘](E:/ESP32-SERVICE/main/display/screen/network_screen/network_keyboard.cc)、[键盘接口](E:/ESP32-SERVICE/main/display/screen/network_screen/network_keyboard.h)、[构建配置](E:/ESP32-SERVICE/sdkconfig)

已有用于 Wi-Fi 密码的自定义触屏键盘：大小写、两页数字／符号、空格、末尾退格、长按清空和确认；有墨水屏按键反馈、末尾静态光标。 当前是密码页专用缓冲与回调，最长 64 字节；中文拼音输入未启用，未见该输入框的自由光标／选区编辑。可抽取键盘布局和刷新逻辑，完整中文笔记编辑仍需输入法与文本编辑适配

[原调研记录](research/2026-11-08-esp32-projects.md)

### 微雪与相关屏幕项目

#### WS-01

[ALXV FolloUp，folloup-waveshare 分支](https://github.com/alxv2016/folloup-sticky/tree/folloup-waveshare)

录音后转写、摘要，将想法／待办／笔记分类，重要项目置为便签。 目标板明确；AI 使用 Gemini 云端，材料保存在 SD。原仓库 main 面向另一块 Sticky，必须看指定分支

[原调研记录](research/2026-11-08-esp32-projects.md)

#### WS-02

[Chroninkle](https://github.com/mach1na/chroninkle)

主题关联、按主题回顾、按需摘要、待办锁屏和 TXT 阅读。 基于 FolloUp 的微雪路线；主题汇总不等于 Obsidian 跨笔记自动归并

[原调研记录](research/2026-11-08-esp32-projects.md)

#### WS-03

[Rustmix Wave](https://github.com/aimindseye/rustmix-wave)

阅读、录音暂停／继续和回放、词典、日历、RTC 闹钟、体感小游戏。 文档提供应用状态表。Wear OS 翻页遥控使用单独 BLE 构建，该构建关闭 Wi-Fi；不能把两种构建能力简单相加

[原调研记录](research/2026-11-08-esp32-projects.md)

#### WS-04

[Draftling](https://github.com/clackups/draftling)、[硬件表](https://github.com/clackups/draftling/blob/main/HARDWARE.md)

BLE 键盘输入、Markdown 编辑，减少干扰的写作界面。 明确列出微雪 3.97 板；移植到 Plus 需验证通用 BLE HID 主机支持，外置蓝牙音频通路不能代替键盘通路

[原调研记录](research/2026-11-08-esp32-projects.md)

#### WS-05

[QuotaFrame](https://github.com/eMUQI/QuotaFrame)、[设备能力表](https://github.com/eMUQI/QuotaFrame/blob/main/docs/devices.md)

桌面 Bridge 通过 BLE 推送 AI 用量、重置倒计时，微雪目标可保存趋势、显示温湿度和时钟。 设备表逐型号列出能力。实验性摄像头手势属于另一个 ESP-Mosaico 目标，不能算到微雪 3.97 上

[原调研记录](research/2026-11-08-esp32-projects.md)

#### WS-06

[CrossMux](https://github.com/0x1abin/crossmux)、[微雪目标记录](https://github.com/0x1abin/crossmux/blob/main/docs/engineering/waveshare-epaper-397.md)

中文阅读、摘录、词典、阅读统计、书籍传输；项目还提供插件和轻量应用。 微雪处于 Nightly／实验目标。作者记录过启动、阅读和休眠等实机检查，也明确列出待验项；全项目功能不保证逐项覆盖该板

[原调研记录](research/2026-11-08-esp32-projects.md)

#### WS-07

[OnlyClaws ESP](https://github.com/shinjiyu/onlyclaws-esp)、[构建配置](https://github.com/shinjiyu/onlyclaws-esp/blob/main/rlcd/platformio.ini)

Agent 下发 Lua 应用，设备绘制、发声、读传感器、回传事件；服务端控制平面可自建。 已查到 esp32-s3-epaper-397 配置；这个目标为节省 TLS 堆内存关闭 BLE。部分宣传画来自模拟器，不能作为该板实机证明

[原调研记录](research/2026-11-08-esp32-projects.md)

### 摄像头与视觉项目

#### CAM-01

[ESP32-CAM_MJPEG2SD](https://github.com/s60sc/ESP32-CAM_MJPEG2SD)

运动触发录制、连续／延时录像、SD AVI、回放、RTSP、通知、HA、浏览器对讲。 摄像头产品功能参考，面向特定 ESP32／S3 与传感器。ML 部分是用户模型接口，不是内置通用识物；Plus 需重新评估采集、编码和资源争用

[原调研记录](research/2026-11-08-esp32-projects.md)

#### CAM-02

[esp32cam-rtsp](https://github.com/rzeldent/esp32cam-rtsp)

RTSP Motion-JPEG、HTTP 视频流、静态抓拍；兼容板可提供音频。 借鉴将画面交给浏览器／NAS，再由服务端抽帧。其 MJPEG 不等于 H.264，也不代表墨水屏能流畅显示视频

[原调研记录](research/2026-11-08-esp32-projects.md)

#### CAM-03

[ESP-WHO](https://github.com/espressif/esp-who)、[官方入门例程](https://developer.espressif.com/blog/2026/05/esp-who-get-started/)

人脸检测和识别、行人检测、二维码，以及图形界面结合。 官方可读示例；所查支持板为 S3／P4 等，未列出 Metalio Plus。适合作为识别事件和界面联动参考

[原调研记录](research/2026-11-08-esp32-projects.md)

#### CAM-04

[ESP32QRCodeReader](https://github.com/alvarowolfx/ESP32QRCodeReader)

使用 Quirc 读取二维码并输出内容；示例以 OV2640 和 PSRAM 板为基础。 可推导扫码录入链接／物品标识，不依赖通用大模型。需将我们的图像缓冲适配给解码器，不能直接复制其相机驱动

[原调研记录](research/2026-11-08-esp32-projects.md)

#### CAM-05

[ESP-DL](https://github.com/espressif/esp-dl)

量化小模型推理、模型转换和部署，可用于特定目标检测／分类。 是部署工具链和模型基础，不是现成个人视觉助理。训练数据、模型大小、目标芯片和延迟均待评估

[原调研记录](research/2026-11-08-esp32-projects.md)

#### CAM-06

[ESP-VISION S31 指南](https://docs.espressif.com/projects/esp-vision/en/latest/esp32s31/index.html)、[支持表](https://docs.espressif.com/projects/esp-vision/en/latest/esp32s31/target-support/index.html)

Python 视觉开发框架，S31 参考板具有图像处理、二维码、AprilTag、模型推理等入口。 S31 有参考路线，但支持表未列 Metalio Plus；它是另一套固件／运行时路线，不能将其包视为现有 C++ 固件中的即插即用功能

[原调研记录](research/2026-11-08-esp32-projects.md)

#### CAM-07

[PP-OCRv6 官方组件](https://components.espressif.com/components/espressif/pp_ocr_v6/versions/0.1.1/readme?language=en)

中文、英文等文字识别，检测与识别两阶段。 所查组件 v0.1.1 的支持表只有 ESP32-P4。OCR 可加入能力池，Plus 端侧运行未获验证；服务器 OCR／视觉模型是另一条候选路线

[原调研记录](research/2026-11-08-esp32-projects.md)

#### CAM-08

[ESPHome Camera](https://esphome.io/components/esp32_camera/)

摄像头作为 Home Assistant 可接入的图像实体。 借鉴外置相机接入智能家居与 Agent 的方法；不作为 Metalio 固件直接兼容证明

[原调研记录](research/2026-11-08-esp32-projects.md)

### 先前调研项目

#### PR-01

[小智官方固件](https://github.com/78/xiaozhi-esp32)、[协议](https://github.com/78/xiaozhi-esp32/blob/main/docs/websocket_zh.md)、[MCP 示例](https://github.com/78/mcp-calculator)

语音会话、双向工具能力、按需视觉；官方托管云与开源固件分开

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-02

[社区小智服务端](https://github.com/xinnan-tech/xiaozhi-esp32-server)

可替换语音／模型／记忆／工具、测试工具、轻量部署；不是官方云源码

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-03

[InkHub](https://github.com/strincake/InkHub)、[TRMNL](https://github.com/usetrmnl/trmnl-firmware)

显示调度、常驻回退、定时看板；硬件适配独立

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-04

[Sticky](https://github.com/cagataycali/sticky-the-reterminal)、[openHASP](https://www.openhasp.com/0.7.0/)、[FreeTouchDeck](https://github.com/DustinWatts/FreeTouchDeck)

可操作卡片、动作回传、控制面板与快捷操作

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-05

[Pala Note 作者页](https://ko-fi.com/s/674a1a82e0)、[Forrest Note](https://github.com/Forrest404/forrest-notes)、[Glane Notes](https://github.com/qinwenshi/GlaneNotes)

快速记录、离线保留、摘要、任务、简报。Pala 2.0 依据作者说明；Forrest 明确不将同名笔记直接合并

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-06

[unidex](https://github.com/Forrest404/unidex)、[Pala Nekogotchi](https://github.com/defcon1702/pala-nekogotchi)

提醒、日历、插件、游戏和宠物；Nekogotchi 作者注明尚未实机验证

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-07

[Hearth](https://github.com/shantanugoel/hearth)、[EInk-Push](https://github.com/moyubyte/EInk-Push)

家庭清单、菜单、提醒、间隔复习、语音练习、轻量应用

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-08

[vibecoding-plus](https://github.com/MaydayV/vibecoding-plus)、[Claude 状态桥](https://github.com/BarryBarrywu/claude-eink-bridge)、[Codex 看板](https://github.com/BarryBarrywu/codex-zectrix-dashboard)

电脑任务、方案选择、任务状态和用量；部分客户端仅 macOS

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-09

[Obsidian Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api)、[MCPVault](https://github.com/bitbonsai/mcpvault)

笔记读写／搜索的插件和直接文件两条接入路线

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-10

[Knowledge Inbox](https://github.com/HortenseJ/knowledge-inbox)、[Audio Inbox](https://github.com/andsea007/obsidian-audio-inbox)、[LLM Wiki 原始说明](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)

原始材料、持久任务、整理产物、知识维护；LLM Wiki 是方法参考

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-11

[Letta](https://docs.letta.com/concepts/memfs)、[OpenClaw](https://docs.openclaw.ai/concepts/memory-architecture)、[Mem0](https://docs.mem0.ai/core-concepts/memory-operations/add)

Agent 自主记忆、后台整理、系统提取记忆的不同机制

[原调研记录](research/2026-11-08-esp32-projects.md)

#### PR-12

[Watcher](https://wiki.seeedstudio.com/getting_started_with_watcher_task/)、[StackChan](https://github.com/m5stack/StackChan)、[AInk](https://github.com/BatsIhor/UkieLab-AInk)、[小智 Pro](https://github.com/hougeai/xiaozhiPro)

事件任务、陪伴反馈、自描述屏幕、外部 Agent 接入；额外硬件和第三方能力不算官方标配

[原调研记录](research/2026-11-08-esp32-projects.md)

### 小智服务端项目

#### XZ-01

[xinnan-tech/xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server)、[单模块部署](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/main/docs/Deployment.md)

语音／视觉问答、声纹、知识检索、插件控制、设备管理。 多协议接入与可替换服务接口；有单独运行语音 Server 的路线，也有完整管理平台。不能把 MySQL／Redis／管理后台一律视为语音接入的强制前提；具体扩展仍有独立依赖

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### XZ-02

[hackers365/xiaozhi-esp32-server-golang](https://github.com/hackers365/xiaozhi-esp32-server-golang)、[OpenClaw 接入](https://github.com/hackers365/xiaozhi-esp32-server-golang/blob/main/doc/openclaw_integration.md)、[知识库](https://github.com/hackers365/xiaozhi-esp32-server-golang/blob/main/doc/knowledge_base.md)

流式问答、声纹与音色、外部 Agent 模式、文档同步与召回测试、MCP 市场、主动音频下发。 传输层与业务分离；文档异步处理；按设备／智能体调试工具；声音资源流式读取。文档及通知模块代码已采样；README 的“主动式 AI”仍在规划，不能由下发能力推定完整自主任务系统

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### XZ-03

[joey-zhou/xiaozhi-esp32-server-java](https://github.com/joey-zhou/xiaozhi-esp32-server-java)、[更新记录](https://github.com/joey-zhou/xiaozhi-esp32-server-java/blob/main/CHANGELOG.md)

作者列出角色／声音、实时打断、家庭成员记忆、就近单设备应答、知识库、记忆图谱、主动消息、设备自检。 对话服务与管理后台分开；身份、角色、设备、会话分别建模；运行监测。README 明示部分功能未开源，以上是产品能力参考，未逐项证明全部包含在公开版，不以“企业级”宣传替代验证

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### XZ-06

[hougeai/xiaozhiPro](https://github.com/hougeai/xiaozhiPro)

OpenClaw／Hermes 双向桥接、定向投递／广播、HA、浏览器摄像头视觉、提醒、个人音频库、树索引知识检索。 外部 Agent 与设备语音可分层；慢任务异步返回，消息与目标设备分离。依据产品文档和更新日志，公开仓库以说明及固件发布入口为主，未确认完整服务端源码可复用；2026-07-30 更新已将音乐调整为用户上传，旧版公网搜索描述不作当前承诺

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### XZ-07

[shenjingnan/xiaozhi-client](https://github.com/shenjingnan/xiaozhi-client)

多个小智接入点共用工具配置，网页配置与状态查看，连接本地／远程 MCP。 工具聚合、可见性开关、接入适配器与后台桥接。名字里的 client 是 MCP 桥接客户端，不是替代整套 ASR／LLM／TTS 的语音服务端

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### XZ-08

[xinnan-tech/mcp-endpoint-server](https://github.com/xinnan-tech/mcp-endpoint-server)、[ziruny 衍生版](https://github.com/ziruny/xiaozhi-mcp-endpoint-server)

一个智能体使用多个 MCP 服务；衍生版加入远程 SSE／Streamable HTTP 服务。 工具注册、聚合、名称路由、连接清理和健康状态；不同传输方式可经适配统一暴露。接入点解决连接和转发，记忆、任务、权限语义仍由上层实现

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### XZ-09

[Verdure MCP Platform](https://github.com/maker-community/verdure-mcp-for-xiaozhi)

将工具绑定到小智、涂鸦等不同助手；独立连接配置与网页管理。 多助手适配、连接恢复、工具绑定、用户隔离；多租户平台可参考数据关系，不默认照搬完整 Keycloak／平台部署

[原调研记录](research/2026-11-08-server-ecosystem.md)

### 其他服务端项目

#### SV-01

[Pipecat 语音轮次](https://docs.pipecat.ai/pipecat/learn/speech-input)、[打断机制](https://docs.pipecat.ai/pipecat/fundamentals/interruptions)

结合 VAD、转写和语句完整性判断轮次；打断时清理在途生成／合成及未播音频，维护已播内容。 少抢话、少误打断；区分“模型生成了什么”“屏幕展示了什么”“用户实际听到了什么”。端侧仍需实现对应播放／取消语义

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-02

[LangGraph 持久化](https://docs.langchain.com/oss/python/langgraph/persistence)、[暂停恢复](https://docs.langchain.com/oss/python/langgraph/interrupts)

会话状态 checkpoint 与跨会话 store 分开；执行可等待外部输入后恢复。 长任务中途补充信息、点选方案再继续、故障后恢复；持久存储和副作用重复处理需要应用设计，框架本身不免除这些工作

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-03

[OpenClaw Automation](https://docs.openclaw.ai/automation)、[任务调度入口](https://docs.openclaw.ai/automation/cron-jobs)

持久定时任务、条件／外部触发、执行上下文、投递目标、安静时段与运行历史。 定时简报、持续关注某主题、有变化才报告；任务触发、Agent 执行和通知分别管理。当前文档已将旧 heartbeat 监测归入普通任务，不把过时教程中的所有机制当作现行设计

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-04

[Hermes Agent](https://github.com/NousResearch/hermes-agent)、[定时任务](https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/features/cron.md)

Agent 整理记忆、历史会话检索、经验转技能；多入口、委派和定时投递；任务可携带前次结果。 自主记忆、可复用个人工作流程、跨次监测去重、复杂任务分工。定时任务上下文与交互会话分开，不应默认可共享全部记忆和权限

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-05

[RAGFlow](https://github.com/infiniflow/ragflow)

多格式解析、分块／重排、来源引用、多步检索；当前文档还列出生成 Wiki、树、时间线、思维导图等知识产物。 文件／网页进入知识收件箱；可追溯回答和多种整理结果。生成 Wiki 产物不等于已支持对用户 Obsidian 目录做增量合并和人工编辑冲突处理

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-06

[n8n Wait](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/)

等待时间、外部回调或表单；等待时将执行数据交给数据库，满足条件后继续。 对接外部服务、Webhook 触发流程，以及“等用户确认后继续”；可学机制或使用工作流服务，不要求首期引入可视化编排平台

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-07

[Temporal 执行与恢复](https://docs.temporal.io/workflow-execution)

用事件历史恢复长时间运行的工作流，区分工作流、外部活动和消息。 提交后持续执行、服务重启后恢复、等待外部结果；适合研究可靠任务语义，不代表个人项目必须部署完整 Temporal

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-08

[Home Assistant 语音流水线](https://contributors.home-assistant.io/core/internals/assist-pipelines/)、[Wyoming](https://www.home-assistant.io/integrations/wyoming/)

唤醒、转写、意图和合成的分段接口；局域网其他主机可承担 Whisper／Piper 等服务。 本地／云端混合语音、家庭设备状态和事件源；使用本地语音服务不自动等于整个 Agent 已完全离线

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-09

[LiteLLM Router](https://docs.litellm.ai/docs/routing)

多服务路由、超时、重试、冷却、故障切换和额度相关路由。 不同任务使用不同模型，服务故障时降级，前台语音与后台整理分配不同预算；实际质量和成本需用自己的场景测量

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-10

[Langfuse 观测](https://langfuse.com/docs/observability/overview)、[评测分数](https://langfuse.com/docs/evaluation/scores/overview)

关联提示词、模型、工具、检索、耗时与用量；人工／程序／模型评测、数据集实验。 定位慢在哪一段，比较模型／提示词调整前后的表现；自建轻量日志和场景样例也可先承接这些需求

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-11

[ntfy 消息与动作](https://docs.ntfy.sh/publish/)、[订阅](https://docs.ntfy.sh/subscribe/api/)

HTTP 发布、主题订阅、缓存、优先级、附件和动作按钮。 墨水屏、手机、网页分别接收结果；点选后回到原任务。消息服务接收成功不能等同设备已展示、用户已阅读或动作已完成

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-12

[IBM ContextForge](https://github.com/IBM/mcp-context-forge)

工具目录与代理，MCP／REST 等服务聚合，按需组合虚拟工具集，鉴权、限流与调用观测。 统一工具登记、按任务暴露工具、为现有业务 API 增加适配层；可以只借鉴目录与适配机制，不默认部署企业网关

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-13

[SQLite Online Backup API](https://www.sqlite.org/backup.html)

对正在使用的数据库进行一致快照，支持增量拷贝；另有 VACUUM INTO 等路线。 提醒服务端数据需可备份、可恢复。全系统还需覆盖媒体、知识文件、配置与索引；这是我们的设计推导，本文不据此决定采用 SQLite

[原调研记录](research/2026-11-08-server-ecosystem.md)

#### SV-14

[Quacksat 唤醒选择](https://github.com/andreagenovese/quacksat/blob/c3c54b0c4faae9a8360178a604c129057868e92b/bridge/bridge.py#L57)

参考桥接器在短窗口收集唤醒分数，保留最高分设备，并通知其他设备停止聆听。 可借鉴候选上报和落选反馈。检测置信度能否稳定选中更近的设备，需要在目标麦克风、增益与环境下验证

[原调研记录](research/2026-11-08-server-ecosystem.md)

### Home Assistant 与 ESP32 项目

#### HA-00

[ESPHome Native API](https://esphome.io/components/api/)、[LVGL](https://esphome.io/components/lvgl/)、[Voice Assistant](https://esphome.io/components/voice_assistant/)

将传感器、控制、界面和语音接到 HA；设备也可调用 HA 动作并处理响应。 声明式配置、组件分层、状态输入与动作输出、错误响应、可配置实体绑定；ESPHome 是可参考的实现体系，不意味着替换现有固件

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-01

[Home Assistant Voice PE](https://www.home-assistant.io/voice-pe/)、[固件](https://github.com/esphome/home-assistant-voice-pe)、[Assist Satellite](https://www.home-assistant.io/integrations/assist_satellite/)

唤醒、语音交互、计时器、播报、物理静音和状态反馈；ESP32-S3 配合独立音频处理芯片。 将听取、处理、回应和错误分别反馈；媒体与播报分开管理。语音识别／推理可由本地服务器或云端承担，不是 ESP32 独立完成通用问答

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-02

[Satellite1-ESPHome](https://github.com/FutureProofHomes/Satellite1-ESPHome)

语音助手、TTS 公告、音乐、温湿度／光照、可选存在雷达、按钮与灯环。 “语音＋环境感知＋结果播报”的复合节点；附加 HAT／传感器扩展能力。参考模块组合，不要求将全部硬件集成到主墨水屏

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-03

[BigBobbas S3 Box 3 Custom](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome)

触屏控制 HA 实体、传感器、计时器、Alarmo、PTT／唤醒、媒体控制、将声音转给外部 HA 播放器。 语音与触屏共存；声音输出可独立路由；前台页面、屏保和传感器数据分层。作者将配置定位为可定制模板，Alarmo 也不是所有 HA 警报集成的通用实现

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-04

[openHASP](https://github.com/HASwitchPlate/openHASP)、[HA 配套集成](https://github.com/HASwitchPlate/openHASP-custom-component)、[集成说明](https://www.openhasp.com/0.7.0/integrations/home-assistant/howto/)

自定义屏幕控件、页面、属性更新；触摸事件调用 HA 动作。 JSON 界面对象与实体状态绑定，通过 MQTT 连接。很适合参考“设备只画控件并回传动作，服务端解释业务”的分工；已有 PR-04 本轮补充 HA 侧证据

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-05

[NSPanel HA Blueprint](https://github.com/Blackymas/NSPanel_HA_Blueprint)

按实体生成按钮，灯光、窗帘、恒温、天气、物理按键；可选本地回退。 通过 Blueprint 配置实体和界面，减少逐页修改代码；常用操作直接完成，长按进入详细设置。部分本地控制只适用于面板实际连接的继电器

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-06

[Weatherman Dashboard](https://github.com/Madelena/esphome-weatherman-dashboard)

门口天气／出行信息；有数据变化且有人活动时刷新；更新时间与刷新计数可见。 信息随摆放场景组织；把数据变化、人在附近、显示更新三者结合，而非收到每个传感器值都刷新墨水屏。已抽查配置

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-07

[pavlojs e-Paper Dashboard](https://github.com/pavlojs/esphome-epaper-dashboard)

天气、多日预报、日历聚合、传感器、车辆和任务计数；定时联网后休眠。 启动等待连接及数据、设等待上限、显示快照再休眠；电池与更新时间可见。续航数字为作者记录，本轮不作为用户设备指标；已抽查配置

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-08

[Skons/M5Dial](https://github.com/Skons/M5Dial)、[Jasionf Smart Home Button](https://github.com/Jasionf/smart-home-button)

用旋钮／触屏切页和调节音量、温度、亮度；后者还有天气、音乐封面与进度等页面。 同一个旋钮区分导航与调值；延迟合并连续调节；等待 HA 状态回报时显示待确认。Skons 明确为 PoC，已抽查其配置；后者部分风速／摆风控件仍需绑定实际动作

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-09

[SeedLabs SmartKnob 固件](https://github.com/SeedLabs-it/smartknob-firmware)、[HA 集成](https://github.com/SeedLabs-it/smartknob-home-assistant-integration)

带显示、按压和触觉反馈的 ESP32-S3 旋钮；HA 配置界面与 MQTT 连接。 让不同控制范围拥有不同手感；把应用与实体绑定放到配置端。SeedLabs 与 Scott 原版不是同一固件／集成；某些发布功能标为 beta 或未验证，不视为全部成熟

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-10

[OMOTE 社区固件](https://github.com/OMOTE-Community/OMOTE-Firmware)

红外电视／功放、BLE 媒体控制、MQTT 智能家居、红外码学习、LVGL 模拟器。 多种控制通道共用遥控界面；实体键与屏幕动作统一；可先在桌面预览。当前示例需要自行配置／编译，网页图形配置是待办，不计为已有

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-11

[ESPresense](https://github.com/ESPresense/ESPresense)、[官方说明](https://espresense.com/)

ESP32 检测可跟踪 BLE 设备，向 MQTT／HA 提供房间定位；也有 Companion 定位路线。 通过已绑定手机／手表等设备推测所在房间；距离滤波、节点覆盖与数据过期需要处理。它定位设备，不直接识别人；不能与声纹身份视为同一信号

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-12

[Everything Presence Lite](https://github.com/EverythingSmartHome/everything-presence-lite)、[产品文档](https://docs.everythingsmart.io/s/products/doc/everything-presence-lite-epl-ZVnBzYzuX2)

毫米波存在与光照、配置区域、目标位置等 HA 实体。 房间里是否有活动、哪个区域有目标，可驱动灯光和屏幕；雷达不等于身份识别。官方文档注明不提供运动方向判断；高频目标数据和长期记录可以分别取舍

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-13

[ESPHome Bluetooth Proxies](https://github.com/esphome/bluetooth-proxies)、[代理组件](https://esphome.io/components/bluetooth_proxy/)

将远处蓝牙广播和支持的 GATT 连接通过 ESP32 提供给 HA。 分布式采集节点，扩展蓝牙覆盖；广播采集、主动连接和设备解码是不同能力。是 BLE 代理，不是任意蓝牙音频或键盘协议的通用透明代理

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-14

[OpenMQTTGateway](https://github.com/1technophile/OpenMQTTGateway)、[HA 集成](https://docs.openmqttgateway.com/integrate/home_assistant.html)

BLE、红外、射频等通道转为 MQTT；采集温湿度、信标、秤、植物传感器等支持设备。 把旧电器和异构传感器转为统一实体／事件；协议解码、采集和业务动作分开。可用外部节点承接，不要求主屏承担射频网关

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-15

[WLED](https://github.com/wled-dev/WLED)、[HA 集成](https://www.home-assistant.io/integrations/wled/)

灯带分区、颜色、预设、播放列表、声音响应和多节点同步。 用外部灯光表达任务或家庭状态；业务只选择预设，设备负责效果。是成熟灯控产品的参考，不把灯光效果运行时并入墨水屏 UI

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-16

[AirGradient 固件](https://github.com/Open-Air-Foundation/firmware-one-openair)、[HA 集成](https://www.home-assistant.io/integrations/airgradient/)

ESP32-C3 等空气监测设备，按型号提供 CO2、颗粒物、温湿度、VOC／NOx 等；本地接口与配置。 环境指标、校准与显示反馈；通风建议和联动为我们可组合的场景，不能把某型号传感器全集套到所有设备

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-17

[CircuitSetup ESP32 Energy Meter](https://github.com/CircuitSetup/Expandable-6-Channel-ESP32-Energy-Meter)

多通道功率与电能监测，通过 ESPHome 接入 HA。 把家庭总量、分路和太阳能数据提供给看板／Agent；数据单位、校准、方向与累计量分开。调研仅涉及能力和数据接口，不涉及用户家庭配电施工

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-18

[firsttris Energy Dashboard](https://github.com/firsttris/esphome-energy-dashboard)

ESP32 屏幕显示光伏、电网、储能和家庭能量流，日累计、成本及趋势。 即时功率与累计电能分开；缺失传感器有降级、离线有标志。宣传截图／GIF 明示由桌面预览和示例值生成，不视为全部实机效果证明；墨水屏可借鉴静态概览

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-19

[Squeezelite-ESP32](https://github.com/sle118/squeezelite-esp32)、[HA Squeezebox 集成](https://www.home-assistant.io/integrations/squeezebox/)

ESP32 网络播放器、多房间同步、屏幕／旋钮控制，另有 AirPlay／蓝牙等模式。 回复、公告和媒体可送到指定房间播放。此 HA 集成通过 LMS／Lyrion 音乐服务器控制播放器，不能把它写成无需媒体服务的通用直连方案

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-20

[ESP32 Tag Reader](https://github.com/Seth-Scott/tagreader-esp32)、[按需扫描的 S3 衍生示例](https://github.com/FizykPSX/ha-rfid-esp32-s3-reader)

NFC 标签触发 HA，灯光／蜂鸣反馈；后者通过按键开启短暂扫描窗口。 实物卡可触发场景、选择媒体或定位对象；读取标签与执行流程分开。首个项目已采样配置，保留旧版配置迁移备注；不因此新增独立笔记入口

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-21

[Tasmota](https://github.com/arendst/Tasmota)、[ESP32 功能](https://tasmota.github.io/docs/ESP32/)、[Rules](https://tasmota.github.io/docs/Rules/)、[HA 接入](https://tasmota.github.io/docs/Home-Assistant/)

本地设备控制、传感器、定时／规则、MQTT、ESP32 上的 Berry 和 LVGL。 将简单、确定的控制放在本地规则中；HA／Agent 承担跨设备协调与解释。规则、脚本和大模型自主行动分别评估；并非所有设备操作都需要经过 LLM

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

#### HA-22

[HA WebSocket API](https://contributors.home-assistant.io/core/internals/websocket-api/)、[MQTT](https://www.home-assistant.io/integrations/mqtt/)、[MCP Server](https://www.home-assistant.io/integrations/mcp_server/)

状态查询／事件订阅／动作调用；MQTT 发现与在线状态；外部 Agent 可以通过 MCP 使用 HA 工具。 不必为每种家居品牌单独建立 Agent 工具。接口、目标实体和工具范围按最终场景选择；HA 也可作为既有自动化与历史数据的来源

[原调研记录](research/2026-11-08-home-assistant-esp32.md)

### ESP32-S31 项目

#### S31-00

[芯片数据手册](https://documentation.espressif.com/esp32-s31_datasheet_en.html)、[量产公告](https://www.espressif.com/en/news/ESP32_S31_Mass_Production)、[软件状态入口](https://developer.espressif.com/hardware/esp32s31/)

双核 RISC-V、低功耗核；Wi-Fi 6、经典／低功耗蓝牙、802.15.4；USB HS、JPEG、PPA 等。 提供应用可能性；量产与 SDK 功能成熟度是不同事实，具体以组件／示例版本核对，不把全部特性当成现有产品开关

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-01

[官方边缘视觉方案](https://esp32-s31.espressif.com/en/official-projects/6)

人脸跟踪、人体关键点、目标检测、静态手势；支持 ESP-DL 模型部署。 有演示与模型耗时参考；动作计数等属于在关键点基础上的进一步应用，不视为完整现成产品

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-02

[S31 视觉工作坊](https://developer.espressif.com/workshops/introduction-to-esp32-s31-with-vision/)、[ESP-VISION 支持表](https://docs.espressif.com/projects/esp-vision/en/latest/esp32s31/target-support/index.html)

本地手部检测／区域进入事件，ESP-IDF 人脸检测；图像处理、二维码、AprilTag 与小模型。 MicroPython 视觉和原生 ESP-IDF 是不同路线；可借鉴输入、事件和工具接口。该框架的 H.264／RTSP 模块当前按 P4 编译条件提供，不由视频容器名称推定 S31 有硬件 H.264

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-03

[TinyML Demo](https://github.com/ozanoner/tinyml-demo-esp32s31)

唤醒后识别固定短语，拍照、YOLO 检测、框与类别列表，保留结果直到清除。 “本地短指令＋拍照＋本地结果”的完整小流程；并非离线自由语音问答，文档明确只有指定短语触发拍照

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-04

[官方音频方案](https://esp32-s31.espressif.com/en/official-projects/5)、[esp_bt_audio](https://components.espressif.com/components/espressif/esp_bt_audio/versions/0.8.2/readme)

A2DP 音乐、AVRCP 控制／媒体信息、HFP 双向免提、LE Audio 单播／广播及同步；硬件采样率转换。 可组成屏幕音箱、电话外设、共享播报；音频角色、连接状态、媒体与通话事件由统一接口交给应用。演示指标不直接作为用户设备验收值

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-05

[ESP32-S31 A2DP Codecs](https://github.com/WillyBilly06/ESP32-S31-A2DP-Codecs)

多种蓝牙音频解码、I2S 输出、切换时分配／释放资源、断流清缓冲。 音乐接收与媒体服务模块化；依赖修改后的 IDF，不能把其编解码全集视为标准 SDK 默认能力。源码复用时另核对各编解码库许可

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-06

[Auracast Transmitter](https://github.com/malarisch/esp32s31-auracast-transmitter)

将外部 I2S 音频转成 LE Audio 广播，运行期配置、多广播流与时钟漂移补偿。 共享听书、讲解或公告可参考；项目的 AES67 输入由外部 FPGA 等提供，不是 S31 自身完成整条网络专业音频链

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-07

[官方 USB 方案](https://esp32-s31.espressif.com/en/official-projects/3)、[esp-usb](https://github.com/espressif/esp-usb)、[esp-iot-solution](https://github.com/espressif/esp-iot-solution)

Device 模式组合音频／CDC／HID／显示；Host 模式接 UVC、UAC、键鼠与复合外设，亦展示多相机。 USB 角色与设备类是可选组合，需要明确数据流和资源归属；当前文件传输可向更完整电脑外设演进

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-08

[uext_screen](https://github.com/xkk6663/uext_screen)、[作者说明](https://esp32-s31.espressif.com/en/community/343)

USB Windows 扩展屏、HID 触摸、UAC 麦克风／扬声器，主机 JPEG 传图与设备解码。 可推导静态文档／窗口镜像、桌面控制终端；显示使用配套 Windows IDD 驱动，不是所有电脑即插即用显示器。帧率为作者 LCD 项目记录

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-09

[Harness ESP32S31](https://github.com/xkk6663/Harness_ESP32S31)

蓝牙音箱、PC 歌词副屏、SD 录音／回放、局域网对讲、MJPEG AVI 播放、A/B OTA、主固件与 USB 副屏固件切换。 特别值得借鉴音频命令队列、界面不直接操作音频、资源互斥与升级回滚。文档还区分主线与人脸打卡／AI 等支线，不把宣传中的全部功能视为同一固件同时运行

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-10

[S31 Playground](https://github.com/MarioCruz/esp32-s31-playground)、[视频留言项目状态](https://github.com/MarioCruz/esp32-s31-playground/blob/main/wedding-recorder/SPEC.md)

作者记录已完成按键驱动 WAV 录音、720p MJPEG＋PCM 封装与 SD 写入验证。 音视频留言、独立原音保留、存储写入与采集解耦可参考。触屏派对留言机、联网图库和分享在规格中是后续计划，不计为已完成

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-11

[ESP-Claw](https://github.com/espressif/esp-claw)、[Skills Lab](https://github.com/espressif/esp-claw-skills-lab)

通过对话定义设备行为、动态 Lua、事件触发、结构化记忆、MCP 双向接口；小应用与 Agent 技能有不同包格式。 已有 S31 目标；可参考可扩展设备运行时、工具和应用目录。设备执行 Agent 循环不代表 LLM 本地运行，README 明确模型接口／自定义端点；是否采用框架仍待选

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-12

[官方触摸与接近感知方案](https://esp32-s31.espressif.com/en/official-projects/2)、[滑条组件 0.3.0](https://components.espressif.com/components/espressif/touch_slider_sensor/versions/0.3.0/readme)、[S31 触摸驱动](https://docs.espressif.com/projects/esp-idf/en/v6.1/esp32s31/api-reference/peripherals/cap_touch_sens.html)

电容按键、滑条、轮盘、接近感应和触摸唤醒。滑条组件已列 S31，标为实验用途。 已有位置与滑动事件实现。侧边／背部电极和接近感应需按目标硬件校准。Metalio 正面 FT6336U 可另用其 GPIO 中断研究浅睡唤醒

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-13

[S31 低功耗核文档](https://docs.espressif.com/projects/esp-idf/en/v6.1/esp32s31/api-reference/system/ulp-lp-core.html)

主核睡眠时，低功耗核执行 GPIO／传感器读取等简单任务。 参考“后台观察—满足条件—唤醒处理”的分工；可访问资源受电源域和外设支持限制，不能据此推定睡眠中仍运行完整网络 Agent

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-14

[ESP-Mosaico Matter](https://github.com/esp-mosaico/esp-mosaico-matter)、[Zigbee SDK 更新记录](https://github.com/espressif/esp-zigbee-sdk/blob/main/RELEASE_NOTES.md)

Matter 中枢／桥、扫码配网、屏幕与网页控制、自动化、MCP／Agent 接入；Zigbee SDK 有 S31 preview 记录。 中枢控制已配网设备，桥则向外部控制器暴露本地设备，角色不同。当前 Mosaico Thread 边界路由示例使用 Thread-RCP 配件，不推定 S31 内置射频已在此固件承担全部角色

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-15

[ESP-Mosaico BSP](https://github.com/esp-mosaico/esp-mosaico-bsp)

统一外设 API、模块发现／占用、相机与图库、短语命令／中文 TTS、ESP-NOW 聊天、多屏 Pong、磁吸拓扑。 借鉴模块能力目录、生命周期和多设备事件；还可扩展测距／热成像等外部模块。部分示例使用独立固件；固定指令／预设 TTS 不等于完整离线自由问答

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-16

[78/nuttx-esp32s31](https://github.com/78/nuttx-esp32s31)

NuttX 多核、用户态 ELF、虚拟内存、文件系统应用装载、Wi-Fi／TLS 等，附作者硬件回归记录。 可长期参考可更新应用与进程隔离；项目明确不是现成应用平台、SDK、云或产品 UI，不默认迁入本项目

[原调研记录](research/2026-11-08-esp32-s31.md)

#### S31-18

[官方 HMI 方案](https://esp32-s31.espressif.com/en/official-projects/4)

JPEG、PPA 缩放／旋转／混合、双屏独立内容、图层合成、相册与表情。 主屏与小副屏、静态预览和图像处理均可参考；LCD 动画帧率不作为墨水屏指标。该文章仍预告后续工具包，不把全部演示视为已发布组件

[原调研记录](research/2026-11-08-esp32-s31.md)

### AI Passport 项目

#### AP-00

[官方共创入口](https://www.folotoy.com/zh/build/)、[产品官网](https://ai-passport.folotoy.cn/)、[官方仓库](https://github.com/FoloToy/ai-passport)、[项目说明](https://github.com/FoloToy/ai-passport/blob/main/docs/README.md)

BSP、开发指南、独立 demo、社区应用档案；官网索引列出蓝牙配置名片／图片。 可参考“稳定硬件接口＋应用案例＋真实设备验收”的开发底座；main 是硬件测试基线，习惯打卡等示例需求不计为已完成产品

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-01

[产品规格](https://github.com/FoloToy/ai-passport/blob/main/docs/hardware-design/specifications.md)、[硬件指南](https://github.com/FoloToy/ai-passport/blob/main/docs/hardware-design/AI_HARDWARE_DEVELOPMENT_GUIDE.md)、[BSP 参数](https://github.com/FoloToy/ai-passport/blob/main/components/bsp/include/bsp_pins.h)

显示、三键、音频、电量、无线与被动 NTAG213。 模块接口、共享总线、资源归属可参考。NFC 是供手机读写的被动标签，不据此推定 MCU 能读取标签或在碰触时接收事件

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-02

[官方 demo 列表](https://github.com/FoloToy/ai-passport/blob/main/docs/README.md)、[猫咪番茄钟](https://github.com/FoloToy/ai-passport/tree/demo/cat-themed-pomodoro-timer)

秒表、猜拳、俄罗斯方块；番茄钟有专注／休息轮次、猫咪成长、统计、暂停与掉电后暂停恢复。 可补强计时和陪伴能力；单调时钟、状态持久化和输入响应比具体视觉主题更值得借鉴。各 demo 是独立案例

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-03

[Claude Buddy 分支说明](https://github.com/FoloToy/ai-passport/blob/demo/claude-buddy-port/README.md)

加密 BLE 同步工作状态、近期消息、工具请求；设备按键允许／拒绝，宠物表达不同状态。 借鉴请求 ID、过期、一次决定、发送状态与断线清理；其桌面 Hardware Buddy 接口仍标实验性，部分设置与角色文件传输未实现

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-05

[小诺简录](https://github.com/noah-1106/xiaonuo-jianlu)、[设备固件分支](https://github.com/noah-1106/ai-passport/tree/feature/xiaonuo-jianlu)、[上游应用档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/noah-1106/xiaonuo-jianlu/README.md)

说话后转成分类／标题／标签卡片；翻阅、完成；离线列表快照、录音占位卡与原声回放，联网补传与完成操作同步；BLUFI 和 mDNS。 很适合参考记录流程与“待识别／待同步”状态。固件／中枢可独立部署，数据由中枢维护。README 与归档对睡眠类型有差异，本轮不据此承诺深睡续航

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-06

[中枢入口](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/app.js)、[语音入口](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/routes/device.js)、[工具实现](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/llm/tools.js)、[MCP](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/mcp.js)、[BLE 桥](https://github.com/noah-1106/xiaonuo-jianlu/blob/main/hub/src/bridge.js)

Express＋SQLite；设备、网页与 Agent 共用简录工具；语音转写后进入同一聊天管线；提供创建、查询、更新、删除、最近记录和关键词搜索。 已抽查路由、工具和协议适配。共享领域工具不绑定某一种输入；更新简录不等于跨主题自动合并 Obsidian，也未证明语义检索或长期自主记忆。BLE 桥需对应平台的中继程序，不能从映射表推定全平台实测

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-07

[Pocket Intercom 手机端](https://github.com/Shinku-Chen/ai-passport-openclaw-android)、[固件分支](https://github.com/Shinku-Chen/ai-passport/tree/feature/openclaw-intercom)、[应用归档](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/intercom/README.md)

BLE 传 Opus 语音，Android 负责识别／联网，接 OpenClaw、Hermes／兼容端点；回复上屏与手机历史，设备和网关分层显示状态；保存配置前真连校验。 可作为外出时的手机代联网方案。归档 v1.13 写有 TTS，但当前手机仓库 README 明确未启用 TTS，本轮只将文字回传视为共同已证实范围，朗读需按匹配版本核对。名称中的“对讲机”不证明设备间呼叫功能

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-08

[Muse Passport，passport 分支](https://github.com/FalkoWing/muse-passport/tree/passport)

Android／iOS 伴侣通过 BLE 借用手机网络；语音转录、中文分页、回复朗读、角色主页、朗读跟页。 作者将朗读等标为 1.0.5 并记有实机验收。可参考伴侣桥接和阅读／播放进度联动；仍需 Muse 账号与服务，首次官方初始化仍含 Wi-Fi 步骤，不把日常 BLE 使用扩大为全程免配网

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-10

[MicroPython 工具箱](https://github.com/ranshuo-ICer/AI-Passport)、[BLE／小程序协议](https://github.com/ranshuo-ICer/AI-Passport/blob/main/docs/ble-protocol.md)、[缺陷修复记录](https://github.com/ranshuo-ICer/AI-Passport/blob/main/docs/known-issues.md)

手机 Web Bluetooth PWA 推送／运行／停止／删除 Python 小程序，终端执行、日志；计时、反应测试、贪吃蛇、节拍器、记忆游戏和实验复读机。 动态应用传输与生命周期有具体参考；小智和 MicroPython 是互斥固件路线，PWA 页面离线缓存不等于所有手机支持 BLE。缺陷记录标多项已修，协议页仍留有旧缺陷提示，后续复用需核对实现

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-11

[zh30/PassportOS](https://github.com/zh30/PassportOS)

Rust no_std 界面、启动器／工作区、游戏、节奏工具、Wi-Fi、设置、持久进度和按键唤醒。 可参考应用接口、焦点与输入归属；应用编译进固件，明确没有 ELF／WASM 动态装载，不能与 AP-10 混用名称推断功能

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-12

[aipassport-fw](https://github.com/weibaohui/aipassport-fw)

应用注入数据、页面与工具表，共用配网、Wi-Fi、UI、存储和流媒体组件；驻留设备 MCP。 参考产品行为与公共底座分层。MCP 实现是简化 POST／JSON-RPC 通道，文档明确无会话／SSE；不是完整管理平台，也不要求所有应用使用文件系统

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-13

[aipassport-radio](https://github.com/weibaohui/aipassport-radio)

网络电台、收藏／自定义源、媒体状态、音量均衡、多热点回退；外部 AI 经设备 MCP 搜台／播放／调节。 补强媒体与“设备作为工具”的路线；语音理解来自外部 AI 客户端，不由 README 的“说话控制”推定设备内置自由语音识别。工具数量在框架与应用文档间不同，不固定承诺数量

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-14

[Codex Buddy](https://github.com/zhangsan2000w-art/ai-passport-codex-buddy)

工作、工具执行、等待与完成状态；电脑／设备双端决定；不同提示音、像素宠物、时间与电量。 本地状态桥＋加密 BLE，当前没有 Wi-Fi 服务；同一请求一次有效决定，唤醒不误操作。Windows 与其他桌面系统的验收范围不同，发布包构建不等于全平台实机通过

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-15

[AI Passport iPhone Agent](https://github.com/lewangdev/ai-passport-iphone-agent)

电脑接收 AirPlay 图像，模型规划／执行，Passport 通过 BLE HID 控制鼠标键盘；逐步截图、校准、动作反馈和物理停止。 是“观察—操作—核对”的手机 GUI Agent。必须有运行时电脑；免手机安装应用不等于免主机。横屏、受保护画面与中文输入有明确限制，不作为通用自动支付保证

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-16

[Faraway 应用档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/starsms007/faraway/README.md)、[源码分支](https://github.com/starsms007/ai-passport/tree/feature/faraway)

离线猫咪旅行、定时归来、明信片／纪念品收藏、天气层与小游戏，进度持久化。 参考低打扰陪伴和收集反馈；与真实行程、天气或 Agent 任务的联动是我们另外设计的组合

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-17

[离线图鉴档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/sunny0826/offline-pokedex/README.md)、[源码分支](https://github.com/sunny0826/ai-passport/tree/feature/ble-artwork)

内置条目、图片、属性、说明与声音，按键浏览与已看进度保存，全程离线。 可迁移为个人知识速查、设备说明或学习资料包；这些用途是设计推导，图鉴项目并未实现我们的知识同步与搜索流程

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-18

[Asunabi 阅读器档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/asunabi/README.md)、[视觉小说案例索引](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/README.md)

多章节图文故事、分页、自动阅读／快进、存档；索引中其他案例含分支与多结局。 可参考互动阅读和场景式学习，后者是我们的推导；Asunabi 本身为单结局，不把别的阅读器分支功能算到它身上。参考引擎／打包机制，内容包另选

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-19

[Voice Keychain 档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/voice-keychain/README.md)、[源码分支](https://github.com/Shinku-Chen/ai-passport/tree/feature/voice-keychain)

分类浏览音效／短语，按键播放本地 Opus，音量与电量设置。 可参考快捷语音板、固定提示与离线声音包；播放预录片段与生成任意语音分别选择

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-20

[今天吃什么档案](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/eat-what/README.md)、[源码分支](https://github.com/Shinku-Chen/ai-passport/tree/feature/cheerful-goodall)

按住轮播候选、松手选定，电量和空闲休眠。 可推导轻量选择器；扩展个人候选列表、加过滤条件或接知识库需另做，不视为已有智能饮食规划

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-21

[Game Boy](https://github.com/PhoenixZHC/folotoy-gameboy)、[FC／NES](https://github.com/PhoenixZHC/folotoy-fc)、[BLE 输入经验](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/phoenixzhc/ble-xbox-keyboard.md)

经典游戏模拟、存档、管理页面、部分 BLE 手柄／键盘／遥控器与方向切换。 借鉴外部输入解析、按键状态／菜单事件、暂停恢复和资源管理；型号、固件与测试范围分别记录，不推定任意控制器或游戏都兼容

[原调研记录](research/2026-11-08-ai-passport.md)

#### AP-22

[待机与唤醒经验](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/shinku-chen/idle-power-stages-and-wake-guards.md)、[串口截图协议](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/y2lin/serial-screenshot-protocol.md)、[工程经验索引](https://github.com/FoloToy/ai-passport/blob/main/docs/reference/README.md)

唤醒按键隔离、实际时钟计算、主动断网与重试协调；抓取设备画面；字库、资源包和内存预算案例。 补强生命周期、可观测性与测试。内存／电流数值属于具体 C3 工程测量，迁移时参考方法；截图与日志需要避免争用传输和大块缓冲

[原调研记录](research/2026-11-08-ai-passport.md)

### 源码复用复核

#### RF-01

[本地会话与状态](E:/ESP32-SERVICE/main/application.cc)、[音频队列](E:/ESP32-SERVICE/main/audio/audio_service.cc)、[音频接口](E:/ESP32-SERVICE/main/audio/audio_service.h)、[分页状态](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_screen_priv.h)、[内容与页面](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_flow.cc)、[跨虚拟键触控](E:/ESP32-SERVICE/main/display/lv_adapter_epdiy_touch.cc)

句段输入、Manual／AutoStop、播放输出、页映射、取消缺口

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-02

[Muse 播放](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/components/muse/muse_speech.c)、[缓冲](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/components/muse/muse_speech_buffer.c)、[阅读跟随](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/components/muse/muse_passport_reader.c)、[原文映射](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/android/app/src/main/java/ai/muse/passport/SpeechWire.java)、[作者测试](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/tests/test_speech_follow.py)

已读实际处理代码与测试，不只依据 README；作者测试本轮未重跑

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-03

[LVGL 9.5 拼音说明](https://lvgl.io/docs/open/9.5/widgets/ime_pinyin)、[官方示例](https://lvgl.io/docs/open/9.5/widgets/ime_pinyin#examples)、[本地依赖版本](E:/ESP32-SERVICE/main/idf_component.yml)、[模拟器输入法接口](E:/ESP32-SERVICE/tools/ebook/emulator/lvgl/src/widgets/ime/lv_ime_pinyin.h)、[文本输入接口](E:/ESP32-SERVICE/tools/ebook/emulator/lvgl/src/widgets/textarea/lv_textarea.h)

同框架已有拼音／候选与光标／选区 API；与密码页定制实现区分

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-04

[厂商模式说明](E:/ESP32-SERVICE/README_zn.md)、[蓝牙界面与连接](E:/ESP32-SERVICE/main/display/screen/bluetooth_screen/bluetooth_screen.cc)、[AT 模式切换](E:/ESP32-SERVICE/main/display/screen/bluetooth_screen/bluetooth_uart.cc)、[音频 codec](E:/ESP32-SERVICE/main/boards/common/audio/bt_audio_codec.cc)

已有外置模块模式 2、扫描、连接和音频通路；不是重新搭 ESP 原生蓝牙栈

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-05

[监听模式](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/handle/textHandler/listenMessageHandler.py)、[收音与 abort](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/handle/receiveAudioHandle.py)、[Silero VAD](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/vad/silero.py)、[语音发送](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/handle/sendAudioHandle.py)

Manual／自动 VAD、说完与打断分工、sentence_start 为发送侧事件

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-06

[真实角色切换工具](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/plugins_func/functions/change_role.py)、[配置](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/config.yaml)

预设角色、参数验证和实际提示词替换；不推定独立记忆已实现

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-07

[Edge provider](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/tts/edge.py)、[FunASR provider](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/asr/fun_local.py)、[Sherpa ASR provider](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/asr/sherpa_onnx_local.py)、[edge-tts 原项目](https://github.com/rany2/edge-tts)、[Sherpa-ONNX](https://github.com/k2-fsa/sherpa-onnx)

现成语音适配与费用／部署前提；尚未做本机语音性能比较

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-08

[ESP-SR 官方支持表](https://github.com/espressif/esp-sr)、[官方组件版本](https://github.com/espressif/esp-sr/blob/master/idf_component.yml)、[本地依赖条件](E:/ESP32-SERVICE/main/idf_component.yml)、[本地功能开关](E:/ESP32-SERVICE/main/Kconfig.projbuild)、[当前构建配置](E:/ESP32-SERVICE/sdkconfig)、[无 AFE 路径](E:/ESP32-SERVICE/main/audio/processors/no_audio_processor.cc)

上游 S31 支持与本地实际集成状态分别核对，不能只翻配置开关

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-09

[A2UI 接口](E:/ESP32-SERVICE/main/display/a2ui/a2ui.h)、[按钮事件](E:/ESP32-SERVICE/main/display/a2ui/a2ui_render.c)、[助手初始化](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_fonts.cc)

action.name 回调存在，助手入口未接通

[原调研记录](research/2026-11-08-reuse-review.md)

#### RF-10

[复刻 TTS 接口](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/tts/gpt_sovits_v2.py)、[声纹适配](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/utils/voiceprint_provider.py)、[声纹部署说明](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/docs/voiceprint-integration.md)、[声纹 API](https://github.com/xinnan-tech/voiceprint-api)

有调用代码，但新模型服务／声音／身份数据依赖仍存在

[原调研记录](research/2026-11-08-reuse-review.md)
