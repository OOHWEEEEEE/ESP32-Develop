# 已讨论能力的复用与迁移成本复核

日期：2026-11-08（Asia/Shanghai）。对应[能力池](../CAPABILITY_POOL.md)与[范围决策](../SCOPE_DECISIONS.md)。

用户要求：先核对参考实现；相关实现存在且容易迁移时纳入首期，并重新审视刚讨论过的选择。本轮覆盖 U-01 至 U-05 已讨论的 13 项子能力及朗读跟页，不重新扩充产品能力池。

## 1. 复核口径

- **低**：本机工程已有实现，主要保留、改配置或补小接口；或服务端已有独立、短小的业务实现，可以沿用原语音通道。
- **低至中**：同类实现和主要依赖已有，仍需对接两端协议、文本位置或输入组件；先完成有边界的验证，再启用产品功能。
- **中及以上**：参考能力真实存在，但需升级算法依赖、部署独立模型、维护声音／身份数据，或验证复杂音频行为。

成本是基于源码的相对判断，不是实测工期。功能存在、迁移工作量与实机可用分别记录。本轮只读源码、文档及公开项目快照；没有修改厂商固件、安装模型、编译、刷机或实机联调。低成本的前提不包括搬入整套手机 App、云账号平台或管理后台。

本地厂商源码：`E:/ESP32-SERVICE`，提交 `2b2c36ae58f32a9cb1a721d1000883a2693651a4`。临时只读参考快照：Muse Passport 的 `passport` 分支提交 `664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e`；社区小智服务端提交 `4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b`。快照仅用于核对，具体摘取时仍应保留相关来源和许可说明。

## 2. 逐项结果

| 能力 | 原选择 | 现成实现与证据 | 我们仍需完成的工作 | 成本与复核结果 |
| --- | --- | --- | --- | --- |
| U-01 按住说话、右滑取消 | 首期做 | 本地 PTT、文字／音频通道已有；触控分发有虚拟键按压和抬起（RF-01） | 将中间键与跨键滑动作为完整手势处理；取消前不提交本轮，处理迟到结果；现有切键会先发旧键抬起，不能直接沿用为发送 | 基础语音低；指定取消手势低至中。保留首期，单列手势验收 |
| U-02 连续对话 | 后续做 | 本地保留 AutoStop／Realtime 状态与回答后回到 Listening 的分支；社区服务端有 Silero VAD 和自动收尾处理（RF-01、RF-05） | 当前 PTT 入口仍硬编码 ManualStop 和“必须按住”；需独立模式、收尾／退出规则和两端联调 | 低至中，前提是复用兼容语音通路。改为首期复用验证：仅半双工连续问答，语音自动打断仍后续 |
| U-02 语音唤醒 | 后续做 | ESP-SR 官方现已列 S31；本地也保留 Wake Word 接口（RF-08） | 本地 esp-sr 依赖仍是 ~2.2.0 且仅对 S3／P4加载；S31 当前关闭唤醒，需要升级依赖、模型与前台／待机状态验证 | 中。存在路线，不能再以 S31 没有支持为由排除；目前保留后续 |
| U-02 实时语音打断 | 后续做 | 小智服务端有 VAD 触发 abort；本地有 Realtime、参考输入与 AFE 接口（RF-01、RF-05、RF-08） | 当前 NoAudioProcessor 不做 AEC；需打通播放中采集、回声处理、有效打断及旧轮次取消 | 中及以上。保留后续；不能把按键 abort 视为已完成语音自动打断 |
| U-03 触屏选择／确认 | 首期最小版 | 本地 A2UI 已渲染 Button、保存 action.name 并分发回调（RF-09） | 助手初始化的 on_action 仍为空，需接回调、请求关联与服务端处理；防止重复和过期动作 | 低至中，保留首期最小版；主要工作是补交互闭环 |
| U-03 中文触屏编辑 | 后续做 | 本地已有英数符号键盘；LVGL 9.5 官方有拼音、候选面板、textarea 与示例，本地模拟器也带对应源码（LOCAL-12、RF-03） | 现有自定义密码键盘不能只开开关就变中文；需接标准键盘／IME或适配事件，配字库／字典及刷新策略；笔记保存另接业务接口 | 短文本输入低至中。先列首期复用验证：中文短文本纠错／标题输入组件；完整笔记编辑仍后续 |
| U-04 角色与表达偏好 | 首期最小版 | 小智服务端有 prompt 配置与 change_system_prompt（RF-06） | 把个人职责、称呼和风格接入所选 Agent；与记忆归属分开 | 低，保留首期；无需单独角色平台 |
| U-04 多角色切换 | 后续做 | 服务端有真实 change_role.py：预设字典、参数检查、替换系统提示词（RF-06） | 换成适合本项目的少量预设，接聊天工具或最小选择入口；明确切换后的会话上下文 | 简单预设切换低，按用户低成本复用原则改为首期最小版。独立记忆、多 Agent 和角色管理平台仍单独讨论 |
| U-04 预设音色 | 首期最小版 | TTS provider 已读取 voice／private_voice 等配置（RF-07） | 选可用语音服务与一个默认声音，测实际首音延迟 | 低，保留首期配置项 |
| U-04 声音复刻 | 后续做 | 服务端已有 GPT-SoVITS、FishSpeech 等适配器，含参考音频与参考文本参数（RF-10） | 对接已部署服务可较省事；当前尚无既定模型服务，仍需部署、音色材料管理与效果／延迟验证 | 现成服务前提下接入低；从当前基线出发中及以上。保留后续 |
| U-04 说话人识别 | 后续做 | 有 voiceprint_provider 与基于 3D-Speaker 的独立 API 服务（RF-10） | 声纹登记、模型服务、身份／偏好映射与错误识别处理；项目示例另依赖数据库 | 中及以上，保留后续。识别到姓名不等于已建立各人会话／记忆隔离 |
| U-05 本机朗读／手动停止 | 首期最小版 | 本地已有 Opus 解码、I2S 输出、TTS 开关、AbortSpeakingToIdle 和清播放队列（RF-01） | 自建服务端接 TTS 音频，映射停止入口并隔离迟到音频；文字保留 | 低，保留首期；无需重新写播放器 |
| U-05 外部播报 | 后续做 | 厂商 README §12.1 明示模式 2 经带麦蓝牙耳机对话；源码有模式切换、扫描、AT+CONNECT 与耳机恢复（RF-04） | 保留并验证既有耳机模式与新语音通路；任意音箱／HA／网络播放器还需路由适配 | 既有带麦耳机路径低，改为首期保留／复用；泛化外部播放器仍后续。没有证明所有蓝牙音箱都支持同一路径 |
| U-05 朗读跟页 | 正在讨论 | Muse Passport 有实际播放驱动的原文定位、手动翻页暂停、恢复跟随与旧轮次隔离（RF-02）；本地已有句段文本与 flow→page 关系（RF-01） | 补句段标识／来源位置，穿过音频队列，在输出时发播放进度，再映射本地页；适配为本地分页，不引入 Muse 的远程阅读接口 | 低至中，列首期复用验证。首期目标是句段首所在页跟随，逐字高亮和任意文本精确对齐不随之纳入 |

## 3. 朗读跟页：可复用到什么程度

### 3.1 查到的真实链路

Muse Passport 的 `SpeechWire` 在清理 Markdown 等内容时，保留“合成文字→原文 Unicode 位置”的映射。发送的语音段带原文起点，设备缓冲器保存该位置；`muse_speech.c` 在音频写出后调用 `muse_passport_reader_speech_position()`。阅读器维护 following 状态和 generation：手动翻页暂停自动跟随，恢复操作回到播放位置，旧轮次的位置不更新新轮次。

该项目阅读页由其远端接口查询；本机墨水屏已经自行分页，所以复用状态与位置机制，页码改为查询本地 `flow_first_page`／页面区间。它不是可直接复制整套 UI 的单文件功能。

### 3.2 本机已有与缺口

- 已有：`application.cc` 接收 TTS `sentence_start` 的 text；助手引擎管理 flow、`flow_first_page` 和 `page_flow_begin`；音频服务按队列解码后统一 `OutputData()`。
- 缺口：当前 AudioServiceCallbacks 没有句段播放位置回调；AudioTask 没有段号／原文锚点。收到 sentence_start 只证明服务端开始发送，并不等于扬声器已经播到该句。
- 适配范围：服务端发句段标识／起点；设备将标识随音频队列保留；输出端上报当前句段；助手页按锚点切页并尊重用户手动操作。取消和新轮次更新 generation。
- 位置口径：原文 UTF-8 字节、Unicode 码点与清理后的语音文本须明确转换；不靠字符串第一次匹配处理重复句子。
- 输出口径：先以设备端音频输出进度驱动；外置蓝牙耳机可能另有链路缓冲，耳机上的跟页体验需单独验收，不预先承诺与扬声器相同的精度。

### 3.3 首期验证门槛

1. 人为增加下行缓冲后，屏幕仍跟随已开始播放的句段，而非提前收到的文字。
2. 一段跨页时，最小版定位段首所在页；语音段内翻页／逐字位置留待扩展。
3. 手动翻页暂停跟随，恢复操作回到当前播放页。
4. 停止、取消、断线或新一轮开始后，旧语音进度不会抢回屏幕。
5. 只有目标页改变才请求显示更新，重复进度合并；与现有显示调度共用。

这些是后续适配的验收要求，本轮没有声称它们已在本机通过。

## 4. ASR／TTS 的快速、免费路线

社区小智服务端的接口已经封装了本地 FunASR、Sherpa-ONNX ASR 和 Edge TTS；默认配置也提供了 FunASR／EdgeTTS 组合。可将这些适配器作为快速闭环候选，不要求立即采用全部管理平台。已有工程使用 Opus 与兼容控制消息，优先保留音频链路，减少重复实现。

- **ASR**：在待选服务端环境上比较现成的 FunASR 与 Sherpa-ONNX 路线。模型部署和推理都在主机侧；开源本地推理与“已有免费的公共托管 API”是不同条件，速度须在目标主机测量。
- **TTS**：Edge TTS 有现成调用与音色参数，可作为免个人 API Key 的在线候选；它是社区对 Edge 在线语音的封装，不能据此承诺托管服务长期免费或可用性。Sherpa-ONNX 等本地 TTS 是另一条路线，需另核对中文模型、资源和延迟。
- **跟页**：不要求免费 TTS 提供逐字时间戳。首期可按我们自己的合成句段绑定原文起点，再由设备实际播放进度驱动翻页。

尚未选定服务端部署、模型或供应商；本轮没有安装依赖、发起语音服务调用或产生调用费用。

## 5. 来源与可追查入口

RF-01 至 RF-10 是本轮来源组；远端代码链接固定到本轮核对的提交，框架文档按注明版本。

| 来源 | 直接入口 | 核对重点 |
| --- | --- | --- |
| RF-01 | [本地会话与状态](E:/ESP32-SERVICE/main/application.cc)、[音频队列](E:/ESP32-SERVICE/main/audio/audio_service.cc)、[音频接口](E:/ESP32-SERVICE/main/audio/audio_service.h)、[分页状态](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_screen_priv.h)、[内容与页面](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_flow.cc)、[跨虚拟键触控](E:/ESP32-SERVICE/main/display/lv_adapter_epdiy_touch.cc) | 句段输入、Manual／AutoStop、播放输出、页映射、取消缺口 |
| RF-02 | [Muse 播放](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/components/muse/muse_speech.c)、[缓冲](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/components/muse/muse_speech_buffer.c)、[阅读跟随](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/components/muse/muse_passport_reader.c)、[原文映射](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/android/app/src/main/java/ai/muse/passport/SpeechWire.java)、[作者测试](https://github.com/FalkoWing/muse-passport/blob/664f5c2a3c9fb9c0b0bf4ed9801907c7f01fdb3e/esp32/tests/test_speech_follow.py) | 已读实际处理代码与测试，不只依据 README；作者测试本轮未重跑 |
| RF-03 | [LVGL 9.5 拼音说明](https://lvgl.io/docs/open/9.5/widgets/ime_pinyin)、[官方示例](https://lvgl.io/docs/open/9.5/widgets/ime_pinyin#examples)、[本地依赖版本](E:/ESP32-SERVICE/main/idf_component.yml)、[模拟器输入法接口](E:/ESP32-SERVICE/tools/ebook/emulator/lvgl/src/widgets/ime/lv_ime_pinyin.h)、[文本输入接口](E:/ESP32-SERVICE/tools/ebook/emulator/lvgl/src/widgets/textarea/lv_textarea.h) | 同框架已有拼音／候选与光标／选区 API；与密码页定制实现区分 |
| RF-04 | [厂商模式说明](E:/ESP32-SERVICE/README_zn.md)、[蓝牙界面与连接](E:/ESP32-SERVICE/main/display/screen/bluetooth_screen/bluetooth_screen.cc)、[AT 模式切换](E:/ESP32-SERVICE/main/display/screen/bluetooth_screen/bluetooth_uart.cc)、[音频 codec](E:/ESP32-SERVICE/main/boards/common/audio/bt_audio_codec.cc) | 已有外置模块模式 2、扫描、连接和音频通路；不是重新搭 ESP 原生蓝牙栈 |
| RF-05 | [监听模式](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/handle/textHandler/listenMessageHandler.py)、[收音与 abort](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/handle/receiveAudioHandle.py)、[Silero VAD](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/vad/silero.py)、[语音发送](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/handle/sendAudioHandle.py) | Manual／自动 VAD、说完与打断分工、sentence_start 为发送侧事件 |
| RF-06 | [真实角色切换工具](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/plugins_func/functions/change_role.py)、[配置](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/config.yaml) | 预设角色、参数验证和实际提示词替换；不推定独立记忆已实现 |
| RF-07 | [Edge provider](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/tts/edge.py)、[FunASR provider](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/asr/fun_local.py)、[Sherpa ASR provider](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/asr/sherpa_onnx_local.py)、[edge-tts 原项目](https://github.com/rany2/edge-tts)、[Sherpa-ONNX](https://github.com/k2-fsa/sherpa-onnx) | 现成语音适配与费用／部署前提；尚未做本机语音性能比较 |
| RF-08 | [ESP-SR 官方支持表](https://github.com/espressif/esp-sr)、[官方组件版本](https://github.com/espressif/esp-sr/blob/master/idf_component.yml)、[本地依赖条件](E:/ESP32-SERVICE/main/idf_component.yml)、[本地功能开关](E:/ESP32-SERVICE/main/Kconfig.projbuild)、[当前构建配置](E:/ESP32-SERVICE/sdkconfig)、[无 AFE 路径](E:/ESP32-SERVICE/main/audio/processors/no_audio_processor.cc) | 上游 S31 支持与本地实际集成状态分别核对，不能只翻配置开关 |
| RF-09 | [A2UI 接口](E:/ESP32-SERVICE/main/display/a2ui/a2ui.h)、[按钮事件](E:/ESP32-SERVICE/main/display/a2ui/a2ui_render.c)、[助手初始化](E:/ESP32-SERVICE/main/display/screen/assistant_screen/assistant_fonts.cc) | action.name 回调存在，助手入口未接通 |
| RF-10 | [复刻 TTS 接口](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/providers/tts/gpt_sovits_v2.py)、[声纹适配](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/main/xiaozhi-server/core/utils/voiceprint_provider.py)、[声纹部署说明](https://github.com/xinnan-tech/xiaozhi-esp32-server/blob/4f6e9ec6b1169ac6f3dbd78b5d8b1f717e493b9b/docs/voiceprint-integration.md)、[声纹 API](https://github.com/xinnan-tech/voiceprint-api) | 有调用代码，但新模型服务／声音／身份数据依赖仍存在 |

## 6. 本轮范围调整

按用户“已有且低成本就做”的原则：

- **改为首期最小版**：少量角色预设切换。
- **改为首期保留与复用**：厂商已有带麦蓝牙耳机模式；任意外部播放器路由仍后续。
- **列首期复用验证**：句段朗读跟页、半双工连续对话、中文短文本输入／纠错。完成上文对应验证后启用；若发现需引入额外平台或大改架构，回到范围讨论，不默认扩建。
- **保留后续**：语音唤醒、自动语音打断、声音复刻、说话人识别、完整笔记编辑及通用外部播放路由。
- **既定首期继续保留**：按住说话与右滑取消、触屏选项／确认、一个默认助手及表达偏好、默认音色、本机朗读／手动停止。

之后每个能力先给出“源码证据—剩余适配—成本前提—首期最小边界”，再确定范围，不再仅按功能名称或假设从零开发作出建议。
