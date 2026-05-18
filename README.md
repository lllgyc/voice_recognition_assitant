# 语音识别助手 - 本地版

基于 Whisper + ECAPA-TDNN + BERT 的全本地语音识别与身份认证系统。

## 项目简介

本项目实现了一个 **100% 本地运行** 的语音助手，集成语音识别、声纹验证、意图分类和系统控制四大核心能力，彻底阻断云端依赖，保障用户隐私数据零上传。

## 系统架构

```
麦克风采集 → 预加重 → 谱减法降噪 → 能量VAD → 分帧加窗
    ↓
Whisper 推理 (INT8量化) → 文本转写
    ↓
NLU意图分类 (BERT / 关键词匹配) → 指令解析
    ↓
系统指令执行 (12种操作)
    ↓
ECAPA-TDNN 声纹验证 (注册/登录)
```
## 本人负责模块
-  GUI 桌面客户端 (PyQt5）
-  音频电平实时可视化
-  AI 推理管线 ↔ UI 异步架构
-  模型性能评估仪表盘
## 项目结构

```
├── main.py                    # 命令行交互入口
├── gui.py                     # PyQt5 图形界面
├── global_config.py           # 全局配置
├── evaluator.py               # 评估脚本 (CER/EER/延迟/鲁棒性)
├── benchmark.py               # 基准测试 (量化对比/谱减法效果)
├── requirements.txt           # 依赖清单
├── audio/
│   ├── audio_capture.py       # 麦克风采集
│   └── audio_preprocess.py    # 音频预处理 (谱减法/VAD/Mel)
├── asr/
│   └── speech_recognizer.py   # 语音识别 (Whisper多后端)
├── speaker/
│   └── speaker_verifier.py    # 声纹验证 (ECAPA-TDNN)
├── nlu/
│   └── intent_classifier.py   # 意图分类 (BERT)
└── controller/
    ├── command_parser.py       # 指令解析 (三级匹配)
    └── system_controller.py    # 系统控制 (12种指令)
```
## 许可证

本项目仅供学术用途。
