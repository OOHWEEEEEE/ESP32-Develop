# ESP32 屏幕与摄像头项目调研

调研日期：2026-11-08（Asia/Shanghai）。

本文记录参考项目和实现证据，供[能力池](../CAPABILITY_POOL.md)后续筛选。尚未确定首期范围，也未决定采用哪套第三方框架。本轮没有编译、烧录或实机测试，没有修改厂商固件。

后续讨论已明确：主要参考产品能力和底座机制，硬件尺寸、板型与固件差异不作为排除理由，适配或迁移由我们自主完成。下文硬件和代码细节保留作实施资料。服务端部分另见[小智生态与通用服务端补充调研](2026-11-08-server-ecosystem.md)。

## 1. 证据和硬件边界

- **本地源码**：阅读了用户提供的工程及相关调用链，可以确认代码存在；不能据此声称用户实机已验证。
- **项目文档**：作者或官方说明列出了功能，不代表本次已验证功能可用。
- **代码采样**：核对了板型定义、接口或关键实现，不等同于完整代码审计。
- **作者实机记录**：仅表示作者记录了相应检查，未覆盖的项目仍待验证。
- **设计推导**：由参考项目产生的候选用途，不宣称参考项目已经实现完整场景。

### 1.1 本次两款硬件并不是同一平台

| 项目 | 微雪 ESP32-S3-ePaper-3.97 | 用户的 Metalio E-Ink4-Plus |
| --- | --- | --- |
| 主控 | ESP32-S3 | 本地工程目标为 ESP32-S31 |
| 显示 | 800×480，SSD1677，SPI，通常以按键导航 | ED047TC2 并行屏，原生 1216×684，逻辑竖屏 684×1216 |
| 输入 | 物理按键／三向拨动控制；所查该型号无触摸屏 | FT6336U 触控、盖板虚拟键、BOOT、电源和音量键 |
| 音频 | ES8311 | 外置蓝牙音频芯片配合 I2S、UART AT |
| 传感器 | 文档列出 QMI8658、SHTC3、PCF85063 等，应用是否使用须分别核对 | SC7A20H 三轴加速度计、PCF8563、BQ27220 等 |
| 摄像头 | 所查板型资料不以板载摄像头为功能 | 源码接入 GC2145 DVP 摄像头 |

微雪依据：[官方资料目录](https://docs.waveshare.com/ESP32-S3-ePaper-3.97/Resources-And-Documents)、[FolloUp 的板型说明](https://github.com/alxv2016/folloup-sticky/tree/folloup-waveshare)。Metalio 依据为下文 LOCAL-01。

迁移以产品行为、服务端接口和组件设计为主；屏幕、音频、休眠、摄像头和蓝牙必须按目标板重新核对。CrossMux 中的 Metalio E-Ink 4 是 ESP32-S3 的非 Plus 型号，不等于用户的 ESP32-S31 Plus。

## 2. 微雪 ESP32-S3-ePaper-3.97 项目

以下来源编号可在能力池中检索。

| 编号 | 项目与直接来源 | 查到的功能 | 证据和迁移边界 |
| --- | --- | --- | --- |
| WS-00 | [微雪官方示例](https://github.com/waveshareteam/ESP32-S3-ePaper-3.97)、[资料目录](https://docs.waveshare.com/ESP32-S3-ePaper-3.97/Resources-And-Documents) | 外设示例、Arduino／ESP-IDF 开发入口和社区项目索引 | 官方基础示例不等于完整 Agent 产品；目录所收录第三方项目独立维护 |
| WS-01 | [ALXV FolloUp，folloup-waveshare 分支](https://github.com/alxv2016/folloup-sticky/tree/folloup-waveshare) | 录音后转写、摘要，将想法／待办／笔记分类，重要项目置为便签 | 目标板明确；AI 使用 Gemini 云端，材料保存在 SD。原仓库 main 面向另一块 Sticky，必须看指定分支 |
| WS-02 | [Chroninkle](https://github.com/mach1na/chroninkle) | 主题关联、按主题回顾、按需摘要、待办锁屏和 TXT 阅读 | 基于 FolloUp 的微雪路线；主题汇总不等于 Obsidian 跨笔记自动归并 |
| WS-03 | [Rustmix Wave](https://github.com/aimindseye/rustmix-wave) | 阅读、录音暂停／继续和回放、词典、日历、RTC 闹钟、体感小游戏 | 文档提供应用状态表。Wear OS 翻页遥控使用单独 BLE 构建，该构建关闭 Wi-Fi；不能把两种构建能力简单相加 |
| WS-04 | [Draftling](https://github.com/clackups/draftling)、[硬件表](https://github.com/clackups/draftling/blob/main/HARDWARE.md) | BLE 键盘输入、Markdown 编辑，减少干扰的写作界面 | 明确列出微雪 3.97 板；移植到 Plus 需验证通用 BLE HID 主机支持，外置蓝牙音频通路不能代替键盘通路 |
| WS-05 | [QuotaFrame](https://github.com/eMUQI/QuotaFrame)、[设备能力表](https://github.com/eMUQI/QuotaFrame/blob/main/docs/devices.md) | 桌面 Bridge 通过 BLE 推送 AI 用量、重置倒计时，微雪目标可保存趋势、显示温湿度和时钟 | 设备表逐型号列出能力。实验性摄像头手势属于另一个 ESP-Mosaico 目标，不能算到微雪 3.97 上 |
| WS-06 | [CrossMux](https://github.com/0x1abin/crossmux)、[微雪目标记录](https://github.com/0x1abin/crossmux/blob/main/docs/engineering/waveshare-epaper-397.md) | 中文阅读、摘录、词典、阅读统计、书籍传输；项目还提供插件和轻量应用 | 微雪处于 Nightly／实验目标。作者记录过启动、阅读和休眠等实机检查，也明确列出待验项；全项目功能不保证逐项覆盖该板 |
| WS-07 | [OnlyClaws ESP](https://github.com/shinjiyu/onlyclaws-esp)、[构建配置](https://github.com/shinjiyu/onlyclaws-esp/blob/main/rlcd/platformio.ini) | Agent 下发 Lua 应用，设备绘制、发声、读传感器、回传事件；服务端控制平面可自建 | 已查到 esp32-s3-epaper-397 配置；这个目标为节省 TLS 堆内存关闭 BLE。部分宣传画来自模拟器，不能作为该板实机证明 |
| WS-08 | [小智官方微雪板型代码](https://github.com/78/xiaozhi-esp32/blob/main/main/boards/waveshare/esp32-s3-epaper-3.97/waveshare-s3-epaper-3.97.cc) | 将该板接入小智语音、音频和显示体系 | 已核对板型代码；不意味着上游每项扩展或任意第三方插件均适配 |
| WS-09 | [SolarOS 的硬件目标文档](https://solar-os.eu/docs/manual/boards.html) | 明确列有 waveshare_esp32_s3_epaper_3_97，提供可扩展终端路线的参考 | 本轮只核对到板型及文档入口；各固件 flavor 的应用和功能需后续逐项核查，暂不当作已完成应用计入 |

### 2.1 新增的产品启发

1. **记录后的再处理**：先留下想法，再按主题回顾、标记需要跟进的内容；可用于项目周报、想法复盘。来源 WS-01／02，跨知识库整理仍是我们的目标。
2. **把重要内容留在待机画面**：锁屏、休眠甚至断电后保留静态待办；这是展示快照，不表示关机后仍会联网或更新。
3. **阅读到知识的连接**：摘录、词典、阅读统计可连接语音批注和知识整理；后半段是设计推导，尚非现有 Metalio Agent 功能。
4. **多种输入方式**：键盘写作、手表遥控、网页推送可与语音共存，具体传输不能脱离板型验证。
5. **可扩展小应用**：声明式卡片和设备脚本是两种不同方案，脚本意味着额外的运行时、资源和更新管理。

### 2.2 排除一次型号误判

[InkCast](https://github.com/Blisart/InkCast)使用 LILYGO T-Energy-S3 加 GDEM0397T81P 屏和外部适配板。它是相近尺寸的天气屏参考，**不是微雪 ESP32-S3-ePaper-3.97 的直接适配项目**。能力池可借鉴天气图表与低频更新，不据此评估微雪板固件兼容性。

## 3. Metalio E-Ink4-Plus 本地源码核对

源码位置：E:/ESP32-SERVICE。远程为 CloudZao/Metalio-E-INK4-Plus。

本次读取的 Git 提交：2b2c36ae58f32a9cb1a721d1000883a2693651a4。CMake 项目版本为 2.0.74。读取时只有讨论纪要为未跟踪文件；本轮未修改此目录。

| 编号 | 能力与源码入口 | 核对结果 | 接入我们的系统时的边界 |
| --- | --- | --- | --- |
| LOCAL-01 | [板型定义](E:/ESP32-SERVICE/main/boards/metalio-e-ink4-plus/config.h)、[产品说明](E:/ESP32-SERVICE/README_zn.md) | 并行墨水屏、触摸与按键、冷暖前光、SD、音频、RTC、三轴加速度计、摄像头等已有定义 | 是源码板型基线；实物版本、外设装配和表现仍需实机确认 |
| LOCAL-02 | [助手说明](E:/ESP32-SERVICE/main/display/screen/assistant_screen/README.md)、[会话实现](E:/ESP32-SERVICE/main/application.cc) | PTT、小智模式、识别和回复显示、会话分页及临时历史 | 切换页面或待机会影响会话；SD 聊天历史开机清空，不可充当服务端长期记忆 |
| LOCAL-03 | [A2UI](E:/ESP32-SERVICE/main/display/a2ui/README.md)、[初始化](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_fonts.cc) | 富文本、公式、图片、卡片及按钮渲染；助手初始化将 on_action 置空 | 渲染按钮与把操作送回服务端是两项工作，完整交互闭环尚需接通 |
| LOCAL-04 | [阅读代码](E:/ESP32-SERVICE/main/reader/)、[书签数据](E:/ESP32-SERVICE/main/reader/book_bookmarks.h) | 电子书、EPUB、TXT、书签、阅读进度、字体和排版；文档说明图像书及自动方向 | 当前页内容／书签尚需显式暴露给 Agent，不能直接视为已支持阅读问答 |
| LOCAL-05 | [首页应用](E:/ESP32-SERVICE/main/display/screen/home_screen/home_screen.cc)、[待机页](E:/ESP32-SERVICE/main/display/screen/standby_screen/) | 清单、最近阅读、天气和待办待机摘要、壁纸、多个首页主题 | 云端业务端点当前为空；本地界面存在不等于自建服务端已有同步能力 |
| LOCAL-06 | [文件传输说明](E:/ESP32-SERVICE/docs/ap-file-transfer.md)、[产品说明](E:/ESP32-SERVICE/README_zn.md) | AP／局域网文件管理、USB MSC、云端文件接收、字体和书籍导入 | 文件访问与 SD 挂载需协调；USB 接管 SD 时不能假设其他应用仍可同时操作文件 |
| LOCAL-07 | [WorkBuddy](E:/ESP32-SERVICE/main/workbuddy/README.md) | 扫码绑定、语音提交、按受理编号读取回复、同步文字历史、待机暂停 | 依赖其服务端／账号体系。可参考任务编号和结果快照机制，不等于现成的通用电脑 Agent 桥 |
| LOCAL-08 | [DVP 采集](E:/ESP32-SERVICE/main/boards/common/camera/dvp_camera.cc)、[相机适配](E:/ESP32-SERVICE/main/boards/common/camera/dvp_camera_adapter.cc)、[MCP](E:/ESP32-SERVICE/main/mcp_server.cc) | GC2145 以 640×480 RGB565 采集，硬件编码 JPEG；MCP 拍照后用 HTTP 上传图片与问题 | 视觉服务由 MCP 初始化中的 vision.url 配置；该路径尚无本地识图模型 |
| LOCAL-09 | [助手拍照](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_boot_photo.cc) | 双击 BOOT 的拍照入口、原图上传尝试、灰度图插入会话；上传失败仍可继续本地插图 | 上传业务使用 api::VisionUploadUrl，与 MCP 拍照解释地址独立；不是持久影像笔记的完整实现 |
| LOCAL-10 | [电源策略](E:/ESP32-SERVICE/main/boards/common/power_policy/README.md)、[共享电源](E:/ESP32-SERVICE/main/boards/metalio-e-ink4-plus/display/epd_board_metalio_eink4_plus.c) | 业务声明电源需求、待机收尾、网络暂停、浅睡眠切片、恢复和关机 | 不能套用其他 S3 项目的深睡代码；主动通知和远程任务必须处理设备离线／待机 |
| LOCAL-11 | [端点配置](E:/ESP32-SERVICE/main/cloudzao_endpoints.c)、[配置下发](E:/ESP32-SERVICE/main/ota.cc)、[协议](E:/ESP32-SERVICE/main/protocols/websocket_protocol.cc) | 开源端点为空；对话配置可下发 URL、Token、协议版本；音频和控制消息已有协议 | 自建服务端仍需实现配置、会话、鉴权及业务接口。固件升级检查和对话配置请求独立 |
| LOCAL-12 | [网络页键盘](E:/ESP32-SERVICE/main/display/screen/network_screen/network_keyboard.cc)、[键盘接口](E:/ESP32-SERVICE/main/display/screen/network_screen/network_keyboard.h)、[构建配置](E:/ESP32-SERVICE/sdkconfig) | 已有用于 Wi-Fi 密码的自定义触屏键盘：大小写、两页数字／符号、空格、末尾退格、长按清空和确认；有墨水屏按键反馈、末尾静态光标 | 当前是密码页专用缓冲与回调，最长 64 字节；中文拼音输入未启用，未见该输入框的自由光标／选区编辑。可抽取键盘布局和刷新逻辑，完整中文笔记编辑仍需输入法与文本编辑适配 |

### 3.1 摄像头和显示的实际资源约束

- 采集代码通过 s_operation 保证相机操作互斥，并使用 EpdFlashGuard；DVP 控制器涉及与面板共享的 LCD_CAM，DVP／JPEG 的 PSRAM DMA 与刷屏互斥。
- GC2145 的复位脚与触摸／4G 使用的 P12 有共享关系，运行期采用传感器软件复位，不应照搬独立摄像头板的硬复位流程。
- JPEG 采集／编码结束后释放相关资源，再执行 HTTP 上传；网络等待不应持有采集与显示资源。
- 每次采集有初始化、预热和收尾。当前接口适合按需静态照片，不能据此宣称已有连续视频、周期抽帧性能或可同时刷新取景画面。
- 芯片或传感器标称能力不能替代当前固件能力：本工程固定 640×480；更高分辨率拍纸面文字、细字 OCR 和长期采集均需另行验证。

## 4. ESP32 摄像头项目

| 编号 | 项目与直接来源 | 查到的能力 | 对用户设备的意义和限制 |
| --- | --- | --- | --- |
| CAM-00 | [Espressif esp32-camera](https://github.com/espressif/esp32-camera) | 传感器采集、格式转换、JPEG／HTTP 示例，是多款摄像头固件的基础 | 所查 README 支持列表为 ESP32／S2／S3；传感器列表有 GC2145，也不代表 S31 和本板可直接使用 |
| CAM-01 | [ESP32-CAM_MJPEG2SD](https://github.com/s60sc/ESP32-CAM_MJPEG2SD) | 运动触发录制、连续／延时录像、SD AVI、回放、RTSP、通知、HA、浏览器对讲 | 摄像头产品功能参考，面向特定 ESP32／S3 与传感器。ML 部分是用户模型接口，不是内置通用识物；Plus 需重新评估采集、编码和资源争用 |
| CAM-02 | [esp32cam-rtsp](https://github.com/rzeldent/esp32cam-rtsp) | RTSP Motion-JPEG、HTTP 视频流、静态抓拍；兼容板可提供音频 | 借鉴将画面交给浏览器／NAS，再由服务端抽帧。其 MJPEG 不等于 H.264，也不代表墨水屏能流畅显示视频 |
| CAM-03 | [ESP-WHO](https://github.com/espressif/esp-who)、[官方入门例程](https://developer.espressif.com/blog/2026/05/esp-who-get-started/) | 人脸检测和识别、行人检测、二维码，以及图形界面结合 | 官方可读示例；所查支持板为 S3／P4 等，未列出 Metalio Plus。适合作为识别事件和界面联动参考 |
| CAM-04 | [ESP32QRCodeReader](https://github.com/alvarowolfx/ESP32QRCodeReader) | 使用 Quirc 读取二维码并输出内容；示例以 OV2640 和 PSRAM 板为基础 | 可推导扫码录入链接／物品标识，不依赖通用大模型。需将我们的图像缓冲适配给解码器，不能直接复制其相机驱动 |
| CAM-05 | [ESP-DL](https://github.com/espressif/esp-dl) | 量化小模型推理、模型转换和部署，可用于特定目标检测／分类 | 是部署工具链和模型基础，不是现成个人视觉助理。训练数据、模型大小、目标芯片和延迟均待评估 |
| CAM-06 | [ESP-VISION S31 指南](https://docs.espressif.com/projects/esp-vision/en/latest/esp32s31/index.html)、[支持表](https://docs.espressif.com/projects/esp-vision/en/latest/esp32s31/target-support/index.html) | Python 视觉开发框架，S31 参考板具有图像处理、二维码、AprilTag、模型推理等入口 | S31 有参考路线，但支持表未列 Metalio Plus；它是另一套固件／运行时路线，不能将其包视为现有 C++ 固件中的即插即用功能 |
| CAM-07 | [PP-OCRv6 官方组件](https://components.espressif.com/components/espressif/pp_ocr_v6/versions/0.1.1/readme?language=en) | 中文、英文等文字识别，检测与识别两阶段 | 所查组件 v0.1.1 的支持表只有 ESP32-P4。OCR 可加入能力池，Plus 端侧运行未获验证；服务器 OCR／视觉模型是另一条候选路线 |
| CAM-08 | [ESPHome Camera](https://esphome.io/components/esp32_camera/) | 摄像头作为 Home Assistant 可接入的图像实体 | 借鉴外置相机接入智能家居与 Agent 的方法；不作为 Metalio 固件直接兼容证明 |

### 4.1 从项目推导出的场景

以下为候选应用，仍需产品规则和实测：

- **拍照提问／视觉笔记**：拍物品或场景，加上口述说明，保存原图、问题、识别结果和后续修订。
- **纸面与屏幕内容采集**：OCR 后摘要、翻译或进入知识库；640×480 下的文字清晰度需要单独验收。
- **扫码录入**：从二维码取得链接或标识，再由用户意图决定打开、查询或入库。
- **变化提醒／周期观察**：设置观察目标、间隔和条件，命中后生成事件；简单画面变化与语义判断分开。
- **过程记录**：事件照片、延时摄影、短片与回看；不承诺当前板能同时完成全部能力。
- **外部摄像头作为视觉源**：固定摄像头或 ESP32-CAM 将图片／视频送到本机，墨水屏负责交互与结果展示，可减轻主终端资源争用。
- **特定目标与标记识别**：二维码、AprilTag、小模型检测可作为工具触发条件；相应资源预算和板型适配待验证。

## 5. 与此前调研合并的来源索引

下表为本对话前几轮已查阅的来源。本轮保留其角色和验证边界，没有重新实测所有项目。

| 编号 | 来源 | 在能力池中的角色 |
| --- | --- | --- |
| PR-01 | [小智官方固件](https://github.com/78/xiaozhi-esp32)、[协议](https://github.com/78/xiaozhi-esp32/blob/main/docs/websocket_zh.md)、[MCP 示例](https://github.com/78/mcp-calculator) | 语音会话、双向工具能力、按需视觉；官方托管云与开源固件分开 |
| PR-02 | [社区小智服务端](https://github.com/xinnan-tech/xiaozhi-esp32-server) | 可替换语音／模型／记忆／工具、测试工具、轻量部署；不是官方云源码 |
| PR-03 | [InkHub](https://github.com/strincake/InkHub)、[TRMNL](https://github.com/usetrmnl/trmnl-firmware) | 显示调度、常驻回退、定时看板；硬件适配独立 |
| PR-04 | [Sticky](https://github.com/cagataycali/sticky-the-reterminal)、[openHASP](https://www.openhasp.com/0.7.0/)、[FreeTouchDeck](https://github.com/DustinWatts/FreeTouchDeck) | 可操作卡片、动作回传、控制面板与快捷操作 |
| PR-05 | [Pala Note 作者页](https://ko-fi.com/s/674a1a82e0)、[Forrest Note](https://github.com/Forrest404/forrest-notes)、[Glane Notes](https://github.com/qinwenshi/GlaneNotes) | 快速记录、离线保留、摘要、任务、简报。Pala 2.0 依据作者说明；Forrest 明确不将同名笔记直接合并 |
| PR-06 | [unidex](https://github.com/Forrest404/unidex)、[Pala Nekogotchi](https://github.com/defcon1702/pala-nekogotchi) | 提醒、日历、插件、游戏和宠物；Nekogotchi 作者注明尚未实机验证 |
| PR-07 | [Hearth](https://github.com/shantanugoel/hearth)、[EInk-Push](https://github.com/moyubyte/EInk-Push) | 家庭清单、菜单、提醒、间隔复习、语音练习、轻量应用 |
| PR-08 | [vibecoding-plus](https://github.com/MaydayV/vibecoding-plus)、[Claude 状态桥](https://github.com/BarryBarrywu/claude-eink-bridge)、[Codex 看板](https://github.com/BarryBarrywu/codex-zectrix-dashboard) | 电脑任务、方案选择、任务状态和用量；部分客户端仅 macOS |
| PR-09 | [Obsidian Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api)、[MCPVault](https://github.com/bitbonsai/mcpvault) | 笔记读写／搜索的插件和直接文件两条接入路线 |
| PR-10 | [Knowledge Inbox](https://github.com/HortenseJ/knowledge-inbox)、[Audio Inbox](https://github.com/andsea007/obsidian-audio-inbox)、[LLM Wiki 原始说明](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) | 原始材料、持久任务、整理产物、知识维护；LLM Wiki 是方法参考 |
| PR-11 | [Letta](https://docs.letta.com/concepts/memfs)、[OpenClaw](https://docs.openclaw.ai/concepts/memory-architecture)、[Mem0](https://docs.mem0.ai/core-concepts/memory-operations/add) | Agent 自主记忆、后台整理、系统提取记忆的不同机制 |
| PR-12 | [Watcher](https://wiki.seeedstudio.com/getting_started_with_watcher_task/)、[StackChan](https://github.com/m5stack/StackChan)、[AInk](https://github.com/BatsIhor/UkieLab-AInk)、[小智 Pro](https://github.com/hougeai/xiaozhiPro) | 事件任务、陪伴反馈、自描述屏幕、外部 Agent 接入；额外硬件和第三方能力不算官方标配 |

## 6. 后续讨论需要保持的区别

1. 已有 UI、端侧代码、兼容协议、完整业务闭环和实机可用是不同证据。
2. 语音记录、对话记忆、用户知识库、任务清单和媒体文件分别维护；可以互相关联。
3. 自动摘要、主题汇总和自动合并更新知识页是不同层级，后者仍需来源、版本和冲突规则。
4. 屏幕刷新和动作回传分别验收；卡片与设备脚本分别评估。
5. 相机采集、流传输、识别推理和墨水屏呈现分开选择；S3、S31、P4 的能力不互相代替。
6. 首期取舍应以场景收益和实际代价判断；本轮仅扩充能力池，没有新增必须实现的产品功能。
