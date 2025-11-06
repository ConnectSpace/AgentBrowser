<p align="center">
  <img src="[YOUR_PROJECT_LOGO_URL_HERE]" alt="MetaScreen Logo" width="200"/>
</p>

<h1 align="center">MetaAgent</h1>

<p align="center">
  <b>赋予 AI 智能体“数字身份”与“感知世界”的定制化浏览器核心</b>
</p>

<p align="center">
  <a href="#-核心理念"><b>核心理念</b></a> •
  <a href="#-为什么选择-metascreen"><b>为什么选择 MetaScreen</b></a> •
  <a href="#-核心架构"><b>核心架构</b></a> •
  <a href="#-应用场景"><b>应用场景</b></a> •
  <a href="#-项目蓝图"><b>项目蓝图</b></a> •
  <a href="#-快速开始"><b>快速开始</b></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Project-MetaScreen-blue.svg?style=for-the-badge" alt="Project MetaScreen">
  <img src="https://img.shields.io/badge/Status-Alpha-red.svg?style=for-the-badge" alt="Status Alpha">
  <img src="https://img.shields.io/badge/License-Apache_2.0-green.svg?style=for-the-badge" alt="License">
  <img src="https://img.shields.io/badge/PRs-Welcome-brightgreen.svg?style=for-the-badge" alt="PRs Welcome">
</p>

---

## 💡 核心理念：从“缸中之脑”到“具身智能”

当前的AI（特别是LLM）是强大的“缸中之脑”。它们能思考，但无法“感知”和“行动”。它们被困在API的黑盒中，无法以“可信的身份”与为人类设计的、充满动态JS和指纹检测的互联网进行交互。

**MetaAgent 的使命是成为 AI 智能体（Agent）的“感知运动系统”。**

我们不只是构建另一个浏览器。我们正在构建一个**可被AI原生驱动的、具有可定制数字身份（指纹）的浏览器核心**。

`MetaAgent` 赋予AI两项关键能力：
1.  **身份（Persona）：** “我是谁？”—— 通过深度定制的浏览器指纹，AI不再是可疑的`Headless`脚本，而是可以定义自己为“特定设备上的真实用户”。
2.  **交互（Interaction）：** “我能做什么？”—— AI不再只是调用API，而是能真正“看见”（视觉/DOM）和“操作”（点击/输入）这个世界。

## ✨ 为什么选择 MetaScreen？

| 特性 | 传统的浏览器自动化 (e.g., Playwright) | `MetaAgent` (AI + 指纹) |
| :--- | :--- | :--- |
| **驱动核心** | 预定脚本 (Scripted) | **AI 智能体** (Agent-driven) |
| **交互模式** | 基于选择器 (Selector-based) | **基于意图和视觉** (Intent & Vision-based) |
| **数字身份** | 易被识破 (e.g., `HeadlessChrome`) | **全栈指纹定制** (AOSP层 + Blink层) |
| **可扩展性** | 局限于测试和爬虫 | **AI数字劳动力** (Autonomous Agents) |

---

## 🏛️ 核心架构：两大引擎

`MetaAgent` 的实现依赖于两大深度定制的核心引擎，它们共同构成了AI的“数字肉身”。

### 1. 🎭 引擎一：Persona（数字身份）指纹引擎

我们认为，**指纹的深度**决定了AI智能体能走多远。`MetaAgent` 不仅限于修改`User-Agent`，我们从系统底层重构了“身份”。

* **Blink/Chromium 内核层修改 (C++)**
    * **Canvas/WebGL：** 修改Blink和Skia的底层渲染逻辑，使其返回**一致且真实的**（而非随机或空白的）渲染结果，以匹配特定GPU型号。
    * **WebGL 指纹：** 硬编码修改 `UNMASKED_RENDERER_WEBGL` 和 `UNMASKED_VENDOR_WEBGL`，使其与AOSP层伪造的GPU型号一致。
    * **WebAudio/字体：** 注入噪声或提供“白名单”字体列表，以对抗Audio和字体指纹。
    * **API行为：** 修改 `navigator.platform`、`navigator.hardwareConcurrency` 等JS API的返回值。

* **AOSP 系统层修改 (来自我们云手机的沉淀)**
    * **设备属性：** 在C++层（`build_info.cc`）修改 `ro.build.model`、`ro.build.fingerprint` 等系统属性。
    * **一致性：** 确保AI在App内（通过WebView）和在Web上（通过浏览器）暴露的指纹是**完全一致**的。

* **网络与地理层**
    * 将IP、时区、`navigator.language` 和地理位置（`Geolocation API`）进行绑定，形成一个**“逻辑自洽”**的数字身份。

### 2. 🤖 引擎二：Agent-Bridge（AI智能体桥接器）

浏览器不能只是“被动”的。`MetaAgent` 的设计初衷就是为了让AI“驾驶”它。

* **原生API驱动**
    * 提供比 `Playwright` / `Puppeteer` 更底层的控制API，允许AI直接控制浏览器的核心行为。
    * **“无头”已死：** 我们的目标是运行**“有头”但“无人”**（Headful but Human-less）的实例，以通过所有反爬虫检测。

* **LLM / Agent 框架原生接入**
    * **工具提供：** `MetaScreen` 作为“工具（Tool）”无缝接入 `LangChain` / `LlamaIndex` 等框架。
    * **任务执行：** AI（如GPT-4）负责**规划**（"登录这个网站并发布一篇帖子"），`MetaScreen` 负责**执行**（处理登录、点击、输入、上传图片等所有具体交互）。

* **多模态“视觉”输入**
    * AI不仅能读取 `DOM`，还能**“看到”屏幕截图**。
    * `MetaScreen` API提供“视觉反馈”功能，允许AI智能体（特别是多模态模型）像人一样，通过“看”屏幕来进行下一步决策，而不是依赖脆弱的HTML选择器。

## 🎯 应用场景

* **AI数字劳动力（AI-Native RPA）**
    部署AI智能体“员工”，7x24小时自主执行复杂业务流程，如社媒运营、客户支持、数据核查。

* **下一代自动化测试（QA）**
    AI智能体扮演“真实用户”，在**具有真实指纹**的浏览器环境中，对Web应用进行探索性测试和回归测试。

* **动态数据智能（Data Intelligence）**
    AI智能体模拟“访客”，在高度动态化、强反爬的网站（如电商、社交）中浏览、理解和提取数据。

## 🗺️ 项目蓝图 (Roadmap)

* **[✅] 阶段一：指纹浏览器核心 (Persona Core)**
    * [✅] AOSP 12-15 / Blink (Chromium) 源码编译。
    * [✅] 实现 `WebGL` 和 `Canvas` 关键指纹的C++层修改。
    * [✅] 实现 `navigator` 和设备属性的定制化。
* **[🚧] 阶段二：AI智能体桥接 (Agent-Bridge V1)**
    * [🚧] 暴露稳定、低延迟的浏览器控制API (gRPC / WebSocket)。
    * [🚧] 实现截图与DOM的同步反馈。
    * [ ] 提供 `Playwright` / `Puppeteer` 兼容的API接口。
* **[ ] 阶段三：LLM 原生集成 (Agent-Bridge V2)**
    * [ ] 提供 `LangChain` / `Python` 的原生工具包。
    * [ ] 实现基于“意图”的API（例如 `agent.goto_and_login("website.com", "user", "pass")`）。
* **[ ] 阶段四：自主智能体 (Autonomous Agent)**
    * [ ] 完整的“规划-执行-反思”（ReAct）循环。
    * [ ] 智能体自主学习与工作流管理面板。

## 🚀 快速开始

*(我们正在全力准备第一个Alpha版本，文档即将发布！)*

```bash
# 敬请期待...
# 1. 克隆仓库
git clone [https://github.com/](https://github.com/)[YourOrg]/AgentBrowser.git

# 2. 启动服务 (示例)
cd AgentBrowser/
docker-compose up -d
