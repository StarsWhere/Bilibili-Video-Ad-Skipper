
# B站视频广告跳过助手 (Bilibili Ad Skipper)

![项目Logo](./png/icon.png)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Greasy Fork](https://img.shields.io/greasyfork/v/YOUR-SCRIPT-ID?label=Greasy%20Fork)](https://greasyfork.org/zh-CN/scripts/YOUR-SCRIPT-ID)
[![Language](https://img.shields.io/badge/language-JavaScript-orange.svg)](https://www.javascript.com/)
[![Status](https://img.shields.io/badge/status-active-success.svg)](#)



这是一款功能强大的油猴脚本，它利用 AI 代理（Agent）智能分析 Bilibili 视频的弹幕和评论，以概率形式精准检测并自动跳过视频中内置的商业广告（恰饭）部分。

## ✨ 功能特点

-   **🤖 AI 驱动分析**：调用大语言模型（如 GPT 系列）作为智能代理，深度理解弹幕和评论的上下文语境，而非简单的关键词匹配。
-   **🎯 多维度检测**：同时分析**海量弹幕**和**置顶评论**，结合两种信息源，大幅提升广告识别的准确率。
-   **📈 概率化结果**：AI 会给出广告的概率评估（0-100%），并根据广告时长进行智能惩罚调整，让判断更科学。
-   **⚙️ 高度可配置**：用户可以自由配置 API Key、API Base URL、AI 模型、自动跳过概率阈值和时长惩罚系数。
-   **🎨 友好用户界面**：
    -   悬浮设置按钮，方便随时调整参数。
    -   清晰的 AI 分析结果弹窗，展示概率、时间、分析依据等信息。
    -   实时的 Toast 通知，反馈脚本运行状态。
    -   可拖拽的弹窗，不影响正常观看体验。
-   **⚡️ 智能自动跳过**：当检测到的广告概率超过设定阈值时，脚本将在播放到广告开始时间时，自动将视频进度条跳转到广告结束时间。

## 📸 效果截图

#### 设置界面
用户可以轻松配置自己的 AI 服务参数。

![设置界面](./png/settings.png)

#### AI 分析结果
分析完成后，脚本会以弹窗形式展示详细结果，用户可根据结果选择是否启用自动跳过。

![AI分析结果](./png/window.png)

## 🚀 安装步骤

1.  **安装脚本管理器**
    首先，你的浏览器需要安装一个用户脚本管理器扩展。推荐使用 [**Tampermonkey**](https://www.tampermonkey.net/)。
    -   [Chrome 安装地址](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)
    -   [Firefox 安装地址](https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/)
    -   [Edge 安装地址](https://microsoftedge.microsoft.com/addons/detail/tampermonkey/iikmkjmpaadaobahmlepofghlfgfgbfp)

2.  **安装本脚本**
    -   从源代码安装：打开 Tampermonkey 管理面板，新建脚本，将项目中的 `.js` 文件内容完整复制进去并保存。

## 🛠️ 配置说明

本脚本**需要您提供自己的 AI 服务 API Key** 才能正常工作。

1.  打开任意一个 Bilibili 视频页面。
2.  点击页面右侧出现的**齿轮图标**⚙️，打开“AI 广告跳过设置”窗口。
3.  填写以下配置项：
    -   **API Base URL**: 你的 AI 服务 API 地址。
        -   如果你使用 OpenAI 官方服务，通常是 `https://api.openai.com`。
        -   如果你使用第三方代理或自建服务，请填写对应的地址。
    -   **API Key**: 你的 API 密钥。请注意保密，不要泄露。
    -   **模型名称**: 你想使用的 AI 模型，例如 `gpt-3.5-turbo` 或 `gpt-4`。
    -   **概率阈值 (%)**: AI 分析出的广告概率**高于**此值时，才会默认勾选“自动跳过”。默认 `70`。
    -   **时长惩罚 (%/分钟)**: AI 识别出的广告时间每增加一分钟，广告概率会降低的百分比。用于防止将过长的正常内容误判为广告。默认 `5`。
    -   **默认启用自动跳过**: 总开关。如果取消勾选，即使概率达标，也不会默认开启跳过功能。
4.  点击**保存**。配置完成后，脚本将在新打开的视频页自动运行。

## 💡 使用方法

1.  完成安装和配置后，打开任意一个 Bilibili 视频页面。
2.  脚本会自动在后台开始执行分析流程（获取信息 -> 获取弹幕 -> 发送给 AI）。你会看到右下角弹出系列状态提示。
3.  分析完成后，右下角会弹出**“AI 分析结果”**卡片。
4.  卡片上会清晰地展示**广告概率**、**预估的起止时间**和**AI的分析依据**。
5.  如果广告概率达到了你设定的阈值，**“自动跳过广告”**的复选框会默认勾选。
6.  当视频播放到广告开始时间时，脚本会自动帮你跳过这段内容。你也可以随时在结果卡片上手动取消勾选来禁用本次跳过。

## 核心提示词 (Prompt)
本脚本通过以下核心提示词（Prompt）指导 AI Agent 完成分析任务，保证了分析的专业性和输出格式的稳定性。

```
### Agent Prompt (提示词)

**角色 (Role):**
你是一个智能agent，专门分析Bilibili视频的弹幕和评论文件以检测其中包含的商业广告(硬广)时间段。

**任务 (Task):**
你收到的内容包含两部分：
1. 经过整理后的弹幕文本，格式为 `[HH:MM:SS] 弹幕内容`
2. 视频的第一条评论内容（如果存在且为置顶评论）

你的核心任务是根据这些信息，判断视频是否含有广告，确定广告的时间段，并给出广告概率评估。

**工作流程与逻辑 (Workflow & Logic):**
... (详细逻辑见脚本源码) ...

**输出格式 (Output Format):**
统一返回以下JSON格式：
{
  "probability": 75,
  "start": "HH:MM:SS",
  "end": "HH:MM:SS",
  "note": "详细说明分析依据和判断理由"
}

**最终指令 (Final Instruction):**
你的输出**必须且只能是**一个纯粹的、格式正确的JSON对象。**绝对禁止**包含任何JSON之外的文本。
```

## 🤝 贡献

欢迎任何形式的贡献！如果你有好的想法、建议或发现了 Bug，请随时提交 [Issues](https://github.com/YOUR-USERNAME/YOUR-REPO/issues) 或 [Pull Requests](https://github.com/YOUR-USERNAME/YOUR-REPO/pulls)。

## 📜 许可证

本项目基于 [MIT License](./LICENSE) 开源。

## ⚠️ 免责声明

-   本脚本为开源的本地工具，仅供学习和技术交流使用，作者不对其造成的任何后果负责。
-   使用本脚本调用 AI 服务产生的**一切费用由用户自行承担**。
-   Bilibili 网站的结构可能随时变化，可能导致脚本部分或全部功能失效，作者会尽力维护，但不作任何保证。