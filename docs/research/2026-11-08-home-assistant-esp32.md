# ESP32 与 Home Assistant 项目调研

调研日期：2026-11-08（Asia/Shanghai）。用于补充[能力池](../CAPABILITY_POOL.md)，与[终端及摄像头调研](2026-11-08-esp32-projects.md)、[服务端生态调研](2026-11-08-server-ecosystem.md)一起使用。

## 1. 范围和参考原则

本轮关注 ESP32 在 Home Assistant（下称 HA）生态中的语音终端、屏幕、遥控器、传感器、网关、灯光与媒体项目。主要借鉴产品行为和底座机制；尺寸、板型、固件与外设差异留给后续自主适配，不作为能力入池的排除条件。

保留三个不同承接位置：我们的墨水屏可以显示和控制家庭状态；其他 ESP32 节点可以提供数据或执行动作；Agent 服务端可以通过 HA 接口进行查询与控制。三者可以组合，不必把网关、传感器或全部自动化都放到墨水屏主设备。

证据来自官方文档、项目 README 和配置代码采样，未在用户环境部署或进行实机验证。下面的“已查到”表示资料或代码存在，不表示所有功能在当前版本组合下已验收。新增场景均为待选择，不改变已确认的问答、想法记录、知识整理方向，也不改变统一聊天记录入口。

## 2. 项目与来源组

HA-00 至 HA-22 为本轮来源编号。部分来源组包含一个项目的配套集成或两个同类实现；编号数量不等于独立项目数量。

### 2.1 语音、屏幕和墨水屏

| 来源 | 项目与直接资料 | 已查到的能力 | 值得参考的机制 |
| --- | --- | --- | --- |
| HA-00 | [ESPHome Native API](https://esphome.io/components/api/)、[LVGL](https://esphome.io/components/lvgl/)、[Voice Assistant](https://esphome.io/components/voice_assistant/) | 将传感器、控制、界面和语音接到 HA；设备也可调用 HA 动作并处理响应 | 声明式配置、组件分层、状态输入与动作输出、错误响应、可配置实体绑定；ESPHome 是可参考的实现体系，不意味着替换现有固件 |
| HA-01 | [Home Assistant Voice PE](https://www.home-assistant.io/voice-pe/)、[固件](https://github.com/esphome/home-assistant-voice-pe)、[Assist Satellite](https://www.home-assistant.io/integrations/assist_satellite/) | 唤醒、语音交互、计时器、播报、物理静音和状态反馈；ESP32-S3 配合独立音频处理芯片 | 将听取、处理、回应和错误分别反馈；媒体与播报分开管理。语音识别／推理可由本地服务器或云端承担，不是 ESP32 独立完成通用问答 |
| HA-02 | [Satellite1-ESPHome](https://github.com/FutureProofHomes/Satellite1-ESPHome) | 语音助手、TTS 公告、音乐、温湿度／光照、可选存在雷达、按钮与灯环 | “语音＋环境感知＋结果播报”的复合节点；附加 HAT／传感器扩展能力。参考模块组合，不要求将全部硬件集成到主墨水屏 |
| HA-03 | [BigBobbas S3 Box 3 Custom](https://github.com/BigBobbas/ESP32-S3-Box3-Custom-ESPHome) | 触屏控制 HA 实体、传感器、计时器、Alarmo、PTT／唤醒、媒体控制、将声音转给外部 HA 播放器 | 语音与触屏共存；声音输出可独立路由；前台页面、屏保和传感器数据分层。作者将配置定位为可定制模板，Alarmo 也不是所有 HA 警报集成的通用实现 |
| HA-04 | [openHASP](https://github.com/HASwitchPlate/openHASP)、[HA 配套集成](https://github.com/HASwitchPlate/openHASP-custom-component)、[集成说明](https://www.openhasp.com/0.7.0/integrations/home-assistant/howto/) | 自定义屏幕控件、页面、属性更新；触摸事件调用 HA 动作 | JSON 界面对象与实体状态绑定，通过 MQTT 连接。很适合参考“设备只画控件并回传动作，服务端解释业务”的分工；已有 PR-04 本轮补充 HA 侧证据 |
| HA-05 | [NSPanel HA Blueprint](https://github.com/Blackymas/NSPanel_HA_Blueprint) | 按实体生成按钮，灯光、窗帘、恒温、天气、物理按键；可选本地回退 | 通过 Blueprint 配置实体和界面，减少逐页修改代码；常用操作直接完成，长按进入详细设置。部分本地控制只适用于面板实际连接的继电器 |
| HA-06 | [Weatherman Dashboard](https://github.com/Madelena/esphome-weatherman-dashboard) | 门口天气／出行信息；有数据变化且有人活动时刷新；更新时间与刷新计数可见 | 信息随摆放场景组织；把数据变化、人在附近、显示更新三者结合，而非收到每个传感器值都刷新墨水屏。已抽查配置 |
| HA-07 | [pavlojs e-Paper Dashboard](https://github.com/pavlojs/esphome-epaper-dashboard) | 天气、多日预报、日历聚合、传感器、车辆和任务计数；定时联网后休眠 | 启动等待连接及数据、设等待上限、显示快照再休眠；电池与更新时间可见。续航数字为作者记录，本轮不作为用户设备指标；已抽查配置 |

### 2.2 旋钮、遥控器和实体入口

| 来源 | 项目与直接资料 | 已查到的能力 | 值得参考的机制 |
| --- | --- | --- | --- |
| HA-08 | [Skons/M5Dial](https://github.com/Skons/M5Dial)、[Jasionf Smart Home Button](https://github.com/Jasionf/smart-home-button) | 用旋钮／触屏切页和调节音量、温度、亮度；后者还有天气、音乐封面与进度等页面 | 同一个旋钮区分导航与调值；延迟合并连续调节；等待 HA 状态回报时显示待确认。Skons 明确为 PoC，已抽查其配置；后者部分风速／摆风控件仍需绑定实际动作 |
| HA-09 | [SeedLabs SmartKnob 固件](https://github.com/SeedLabs-it/smartknob-firmware)、[HA 集成](https://github.com/SeedLabs-it/smartknob-home-assistant-integration) | 带显示、按压和触觉反馈的 ESP32-S3 旋钮；HA 配置界面与 MQTT 连接 | 让不同控制范围拥有不同手感；把应用与实体绑定放到配置端。SeedLabs 与 Scott 原版不是同一固件／集成；某些发布功能标为 beta 或未验证，不视为全部成熟 |
| HA-10 | [OMOTE 社区固件](https://github.com/OMOTE-Community/OMOTE-Firmware) | 红外电视／功放、BLE 媒体控制、MQTT 智能家居、红外码学习、LVGL 模拟器 | 多种控制通道共用遥控界面；实体键与屏幕动作统一；可先在桌面预览。当前示例需要自行配置／编译，网页图形配置是待办，不计为已有 |
| HA-20 | [ESP32 Tag Reader](https://github.com/Seth-Scott/tagreader-esp32)、[按需扫描的 S3 衍生示例](https://github.com/FizykPSX/ha-rfid-esp32-s3-reader) | NFC 标签触发 HA，灯光／蜂鸣反馈；后者通过按键开启短暂扫描窗口 | 实物卡可触发场景、选择媒体或定位对象；读取标签与执行流程分开。首个项目已采样配置，保留旧版配置迁移备注；不因此新增独立笔记入口 |

### 2.3 存在、网关、环境、能耗和媒体

| 来源 | 项目与直接资料 | 已查到的能力 | 值得参考的机制 |
| --- | --- | --- | --- |
| HA-11 | [ESPresense](https://github.com/ESPresense/ESPresense)、[官方说明](https://espresense.com/) | ESP32 检测可跟踪 BLE 设备，向 MQTT／HA 提供房间定位；也有 Companion 定位路线 | 通过已绑定手机／手表等设备推测所在房间；距离滤波、节点覆盖与数据过期需要处理。它定位设备，不直接识别人；不能与声纹身份视为同一信号 |
| HA-12 | [Everything Presence Lite](https://github.com/EverythingSmartHome/everything-presence-lite)、[产品文档](https://docs.everythingsmart.io/s/products/doc/everything-presence-lite-epl-ZVnBzYzuX2) | 毫米波存在与光照、配置区域、目标位置等 HA 实体 | 房间里是否有活动、哪个区域有目标，可驱动灯光和屏幕；雷达不等于身份识别。官方文档注明不提供运动方向判断；高频目标数据和长期记录可以分别取舍 |
| HA-13 | [ESPHome Bluetooth Proxies](https://github.com/esphome/bluetooth-proxies)、[代理组件](https://esphome.io/components/bluetooth_proxy/) | 将远处蓝牙广播和支持的 GATT 连接通过 ESP32 提供给 HA | 分布式采集节点，扩展蓝牙覆盖；广播采集、主动连接和设备解码是不同能力。是 BLE 代理，不是任意蓝牙音频或键盘协议的通用透明代理 |
| HA-14 | [OpenMQTTGateway](https://github.com/1technophile/OpenMQTTGateway)、[HA 集成](https://docs.openmqttgateway.com/integrate/home_assistant.html) | BLE、红外、射频等通道转为 MQTT；采集温湿度、信标、秤、植物传感器等支持设备 | 把旧电器和异构传感器转为统一实体／事件；协议解码、采集和业务动作分开。可用外部节点承接，不要求主屏承担射频网关 |
| HA-15 | [WLED](https://github.com/wled-dev/WLED)、[HA 集成](https://www.home-assistant.io/integrations/wled/) | 灯带分区、颜色、预设、播放列表、声音响应和多节点同步 | 用外部灯光表达任务或家庭状态；业务只选择预设，设备负责效果。是成熟灯控产品的参考，不把灯光效果运行时并入墨水屏 UI |
| HA-16 | [AirGradient 固件](https://github.com/Open-Air-Foundation/firmware-one-openair)、[HA 集成](https://www.home-assistant.io/integrations/airgradient/) | ESP32-C3 等空气监测设备，按型号提供 CO2、颗粒物、温湿度、VOC／NOx 等；本地接口与配置 | 环境指标、校准与显示反馈；通风建议和联动为我们可组合的场景，不能把某型号传感器全集套到所有设备 |
| HA-17 | [CircuitSetup ESP32 Energy Meter](https://github.com/CircuitSetup/Expandable-6-Channel-ESP32-Energy-Meter) | 多通道功率与电能监测，通过 ESPHome 接入 HA | 把家庭总量、分路和太阳能数据提供给看板／Agent；数据单位、校准、方向与累计量分开。调研仅涉及能力和数据接口，不涉及用户家庭配电施工 |
| HA-18 | [firsttris Energy Dashboard](https://github.com/firsttris/esphome-energy-dashboard) | ESP32 屏幕显示光伏、电网、储能和家庭能量流，日累计、成本及趋势 | 即时功率与累计电能分开；缺失传感器有降级、离线有标志。宣传截图／GIF 明示由桌面预览和示例值生成，不视为全部实机效果证明；墨水屏可借鉴静态概览 |
| HA-19 | [Squeezelite-ESP32](https://github.com/sle118/squeezelite-esp32)、[HA Squeezebox 集成](https://www.home-assistant.io/integrations/squeezebox/) | ESP32 网络播放器、多房间同步、屏幕／旋钮控制，另有 AirPlay／蓝牙等模式 | 回复、公告和媒体可送到指定房间播放。此 HA 集成通过 LMS／Lyrion 音乐服务器控制播放器，不能把它写成无需媒体服务的通用直连方案 |
| HA-21 | [Tasmota](https://github.com/arendst/Tasmota)、[ESP32 功能](https://tasmota.github.io/docs/ESP32/)、[Rules](https://tasmota.github.io/docs/Rules/)、[HA 接入](https://tasmota.github.io/docs/Home-Assistant/) | 本地设备控制、传感器、定时／规则、MQTT、ESP32 上的 Berry 和 LVGL | 将简单、确定的控制放在本地规则中；HA／Agent 承担跨设备协调与解释。规则、脚本和大模型自主行动分别评估；并非所有设备操作都需要经过 LLM |

### 2.4 官方接口来源

| 来源 | 资料 | 本次确认的能力 | 对我们的意义 |
| --- | --- | --- | --- |
| HA-22 | [HA WebSocket API](https://contributors.home-assistant.io/core/internals/websocket-api/)、[MQTT](https://www.home-assistant.io/integrations/mqtt/)、[MCP Server](https://www.home-assistant.io/integrations/mcp_server/) | 状态查询／事件订阅／动作调用；MQTT 发现与在线状态；外部 Agent 可以通过 MCP 使用 HA 工具 | 不必为每种家居品牌单独建立 Agent 工具。接口、目标实体和工具范围按最终场景选择；HA 也可作为既有自动化与历史数据的来源 |

HA 当前 MCP 文档区分 Device control 与 Home Assistant 等工具集，后者可涉及实体、历史和日志；实际可用工具取决于版本和配置。它还区分 MCP Server 与 MCP Client 两种方向：外部 Agent 调用 HA，与 HA 内部助手调用外部工具，不能混为一条链路。[官方说明](https://www.home-assistant.io/integrations/mcp_server/)

## 3. 配置代码采样得到的具体启发

本节是有限范围代码阅读，不是完整审计或兼容测试；链接指向读取时分支，后续内容可能变化。

1. **刷新有条件，展示有时间。** [Weatherman 配置](https://github.com/Madelena/esphome-weatherman-dashboard/blob/main/weatherman.yaml)将数据变化标志与活动传感器结合，定时检查是否刷新，并回报更新时间和刷新次数。我们可用相同思路处理前台阅读、无人时刷新和过期信息，具体规则待选。
2. **等待连接不等于等到完整数据。** [电池墨水屏配置](https://github.com/pavlojs/esphome-epaper-dashboard/blob/main/dashboard.yaml)先等 API，再等部分数据，各自有超时，刷新后进入休眠。可参考可用数据快照和等待上限，不能把条件通过理解为所有实体均已同步。
3. **发送指令和状态生效分开。** [Skons M5Dial](https://github.com/Skons/M5Dial/blob/main/m5dial.yaml)对连续调温延迟合并，并用闪烁表示等待 HA 回报。对墨水屏可以改成静态“正在设置”，再更新最终状态；闪烁和延迟参数不直接照搬。
4. **语音与媒体各有通路。** [Voice PE 配置](https://github.com/esphome/home-assistant-voice-pe/blob/dev/home-assistant-voice.yaml)分开公告与媒体管线，公告／语音时降低媒体音量，结束后恢复；按钮也按计时器、公告、语音和音乐的次序处理停止。可参考共享输出设备的优先级。
5. **实物标识只负责触发。** [Tag Reader 配置](https://github.com/Seth-Scott/tagreader-esp32/blob/master/tagreader.yaml)包含标签读取／写入和反馈。把标签映射到媒体、对象或场景是应用层工作；具体哪些动作触发须由我们定义。

## 4. 纳入能力池的产品场景

H-01 至 H-13 为家庭场景的细分候选，T-06 保留为总体入口。它们可独立选择或组合，并不要求开展完整智能家居产品。

| 能力池 ID | 候选场景 | 主要参考 |
| --- | --- | --- |
| H-01 | 按房间查看灯光、窗帘、温控和设备状态，触屏进行详细控制 | HA-03、HA-04、HA-05 |
| H-02 | 一键／一句话执行离家、睡眠、阅读等家庭场景 | HA-05、HA-10、HA-21、HA-22；具体场景为组合推导 |
| H-03 | 检测房间或区域是否有人，用于显示和自动化 | HA-02、HA-12 |
| H-04 | 根据已绑定的手机／手表等设备推测所在房间，辅助选择显示或播报位置 | HA-11；不直接等同人的身份或精确位置 |
| H-05 | 旋钮、实体键或遥控器快速调亮度、温度、音量 | HA-08、HA-09、HA-10 |
| H-06 | 接入旧电视、空调、功放或射频设备，统一控制 | HA-10、HA-14 |
| H-07 | 通过独立 ESP32 节点扩展蓝牙覆盖、采集远端设备 | HA-13、HA-14 |
| H-08 | 环境看板、空气质量变化与通风提醒／联动 | HA-12、HA-16；提醒与联动属于组合设计 |
| H-09 | 家庭用电、光伏、储能和费用概览／趋势 | HA-17、HA-18；最终展示由已有数据源决定 |
| H-10 | HA／网络不可用时，保留指定的本地按钮或简单规则 | HA-05、HA-21；只适用于设备实际能在本地完成的动作 |
| H-11 | 用 NFC 实物卡触发场景、选择媒体或定位对象 | HA-20；不改变统一聊天记录入口 |
| H-12 | 通过灯带／灯光预设表达任务、提醒或家庭状态 | HA-15；与 Agent 任务的映射由我们实现 |
| H-13 | 查询家庭状态历史，并整理事件、能耗或自动化运行的回顾 | HA-22；Agent 总结是组合推导，相关变化不视为已证实因果 |

以下并入已有能力而不重复新增条目：

- U-01／02／03／05：语音、触屏、状态反馈和可中止播报，补充 HA-00／01／03。
- S-03／04：有人或有变化时显示、待机信息快照，补充 HA-06／07。
- S-07：桌面预览和模拟器，补充 HA-10／18。
- F-02：外部传感器、天气和家庭环境信息，补充 HA-12／16。
- F-04／T-12：回复、公告和媒体可选择外部播放器；多房间播放与设备呼叫分别设计，补充 HA-02／03／19。
- T-03／14：家庭状态可作为简报输入或外部事件源，补充 HA-22。

## 5. 底座收获与对应编号

已有通用底座继续复用，不为每一种家居功能单独建平台。新增五个讨论项：

| 能力池 ID | 底座候选 | 最小要明确的关系 |
| --- | --- | --- |
| B-29 | 家庭实体、空间与连接器 | 设备、实体、房间、别名和可执行动作；主墨水屏、其他节点、HA 与 Agent 分别负责什么 |
| B-30 | 状态订阅与控制回报 | 状态快照和变化订阅；发送／受理／状态生效分开；合并连续调节、超时与断线恢复 |
| B-31 | 传感器与历史数据语义 | 来源、单位、时间、校准、过期、缺失和滤波；即时值、累计量、存在信号与身份线索分别维护 |
| B-32 | 本地规则与控制优先级 | 哪些简单动作留在端侧；物理操作、HA 自动化、Agent 的优先级及恢复后的状态同步 |
| B-33 | 音频输出路由与抢占 | 回答、计时器、公告和音乐选择哪个播放器；静默、暂停／压低音量、停止和恢复语义 |

同时补强 B-09 事件触发、B-11 动作回传、B-12 显示调度、B-15 配置和更新、B-19 上下文快照、B-23 工具／协议适配。HA 的发现、在线状态和实体绑定可供借鉴，采用 Native API、MQTT 或自建连接器仍未定案。

## 6. 对后续讨论最有用的组合

以下是设计推导，先保留为可讨论的结果示例：

- **出门前一眼看完**：天气、通勤和当日日历，按人在附近或数据变化刷新；来自 HA-06／07。
- **说完后继续点选**：语音找到设备，屏幕展示可调参数与执行结果；结合 HA-03／04／05 和已有卡片能力。
- **事情完成后在合适位置告诉我**：任务结果保存在服务端，参考房间线索选择屏幕或音箱，按安静时段决定是否播报；结合 HA-11、HA-19 与既有投递底座。
- **家庭事件连接个人助手**：传感器变化进入事件系统，再查询、解释或提醒；不会默认把所有家庭遥测写进 Obsidian 或 Agent 长期记忆。

本轮没有选择 HA 作为必需部署组件，没有连接用户家庭设备，也没有改变首期范围。后续按用户真正需要的场景决定是否接入 HA、复用哪些机制、怎样适配到本项目。
