# LogicVibe: A Neuro-Symbolic Approach to Visual Programming

> **LogicVibe: 一种基于模糊草图的神经符号化视觉编程方法**

![Vibe Coding](https://img.shields.io/badge/Vibe%20Coding-Neuro--Symbolic-blueviolet) ![Status](https://img.shields.io/badge/Status-Prototype-green) ![Platform](https://img.shields.io/badge/Platform-Full--Stack-orange) [![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](LICENSE)

---

## 🌟 项目愿景 (Vision)

LogicVibe 旨在构建下一代 **"Neuro-Symbolic Vibe Coding"** 平台。我们超越了传统的 "Prompt Coding"（提示词编程），提出了一种**所画即所得、逻辑可溯源**的全新开发范式。

目前的 SOTA（State of the Art）生成工具（如 Make Real, v0.dev）主要依赖 **"视觉（像素） -> 大模型 -> 前端代码"** 的端到端映射。这导致了严重的**不可控性**。

**LogicVibe 的核心突破在于：**

> **"视觉 + 拓扑数据（双模态） -> 神经符号推理 -> 后端逻辑/全栈系统"**

---

## 🎯 解决痛点 (The "Why")

目前的 "Prompt Coding" (提示词编程) 或 "Vibe Coding" 存在两个致命的核心问题：

1.  **模糊性困境 (The Ambiguity Problem)**：
    自然语言提示词（Prompt）在描述复杂逻辑时往往显得苍白无力且存在歧义。AI 常常"猜"不对你想要的具体交互细节，导致生成结果总是差点意思。
2.  **维护性黑洞 ( The Maintenance Trap)**：
    一旦 AI 生成了项目，如果后续需要修改底层逻辑（例如改变一个状态机的流转条件），往往异常困难。你不得不重新调整提示词并祈祷 AI 不会破坏现有的功能——这使得生成的项目往往是一次性的，难以维护和迭代。

---

## 💡 四大核心创新点 (Core Innovations)

### 1. 技术创新：双流模态对齐 (Dual-Stream Grounding)

**现状 (The Problem)**：
目前的 Make Real 类工具本质上是把画布**截图 (PNG)** 发给 GPT-4V。

- ❌ **缺点**：这是一个黑盒。如果 GPT 没看清箭头指向了哪个方块（比如线条交叉时），或者把两个靠近的方块误认为是父子关系，逻辑就会出错。

**我们的创新 (Our Solution)**：
我们不只发图片，而是构建一个**"混合 Prompt"**。

- ✅ **输入 A（视觉流）**：截图（保留 Vibe 和空间感）。
- ✅ **输入 B（拓扑流）**：利用 `tldraw/tlschema` 中的精准数据。
  - 我们通过代码提取出绝度事实：`Arrow(ID:1) connects Shape(A) to Shape(B)`。
  - 这是一个**绝对事实**，不是 AI 猜出来的。
- **价值**：解决了大模型"视觉幻觉"的问题。利用 tldraw 已经写好的 bindings（绑定）系统，为模糊的视觉草图提供了数学上的确定性。

### 2. 交互创新：模糊语义推理 (Fuzzy Semantic Reasoning)

**现状 (The Problem)**：
传统低代码平台强制用户遵守规则。比如："菱形"必须代表判断，"圆角矩形"必须代表开始。

- ❌ **缺点**：这就没有 Vibe 了，这相当于是在画工程图，限制了思维的流动。

**我们的创新 (Our Solution)**：
引入 **"基于上下文的意图推断" (Context-Aware Intent Inference)**。

- ✅ 我们允许用户**"乱画"**，然后用 AI 分析**空间关系**和**自然语言**来推导逻辑。
  - _例子_：用户在一个箭头旁边随便写了句"只有管理员能进"。
  - _传统工具_：报错，或忽略。
  - _我们的工具_：
    1.  计算文字与箭头的欧几里得距离。
    2.  判定这段文字属于这个"连接关系"的属性。
    3.  语义分析："只有管理员能进" = `if (user.role == 'admin')`。
- **学术定义**：这是一中 **"Relaxed Syntax" (松弛语法)** 编程环境，将非形式化的草图"编译"为形式化的逻辑。

### 3. 架构创新：神经符号编译 (Neuro-Symbolic Compilation)

**现状 (The Problem)**：
由 LLM 直接输出最终代码（Python/JS）。

- ❌ **缺点**：如果代码错了，用户很难排查是逻辑图画错了，还是 AI 写错了。

**我们的创新 (Our Solution)**：
引入 **"中间表示层" (Intermediate Representation, IR)**。我们不直接生成代码，而是先生成一个 DSL（领域特定语言）或伪代码谱。

- ✅ **流程**：`草图 -> [ 结构化逻辑图 (Graph IR) ] -> 最终代码`
- **价值**：
  - **可解释性**：我们可以在生成代码前，先用自然语言告诉用户："我理解这是一个需要登录的循环流程，对吗？"
  - **多语言支持**：一旦我们有了中间逻辑 (IR)，我们可以一键生成 Python、Go、Java 或者 Mermaid 图。

### 4. 体验创新：可视化运行时反馈 (Visual Runtime Feedback)

**现状 (The Problem)**：
代码生成后，图和代码就"断连"了。代码跑起来出了 Bug，你不知道对应图上的哪一步。

**我们的创新 (Our Solution)**：
建立 **"代码-视觉映射" (Code-to-Visual Mapping)**。

- ✅ 利用 tldraw 的渲染能力，当生成的代码（比如后端逻辑）在运行时：
  - 如果走到 Step A，画布上的方块 A 会发光。
  - 如果 Step B 报错，画布上的箭头变红，并弹出气泡显示错误日志。
- **价值**：这将 tldraw 从一个"绘图板"变成了一个**"可视化的 Debugger"**。

---

## 📊 核心卖点对比 (Feature Comparison)

| 维度         | 别人做的 (Baseline)                    | 我们做的 (Innovation)                           |
| :----------- | :------------------------------------- | :---------------------------------------------- |
| **输入数据** | 纯像素 (Image-only)                    | **像素 + 向量拓扑 (Image + Graph Topology)**    |
| **规则限制** | 要么无规则(生成UI)，要么强规则(低代码) | **松弛规则 (Vibe-based Logic)，由 AI 补全约束** |
| **生成目标** | 静态网页 (HTML/CSS)                    | **动态业务逻辑 (Backend/Workflow)**             |
| **错误处理** | 重试生成                               | **可视化 Debug (Live Trace)**                   |

---

## 🚀 核心工作流 (Workflow)

1.  **Draft (绘图)**：在 LogicVibe 画板上勾勒你的后端逻辑流和前端交互流。
2.  **Generate (生成)**：AI 引擎分析双流数据（视觉+拓扑），自动构建全栈项目结构。
3.  **Run (运行)**：一键启动应用，见证你的设想落地。
4.  **Evolve (演进)**：利用可视化运行时反馈，直接在图上 Debug 和迭代。

---

> _LogicVibe —— 让编程回归逻辑，让 AI 成为真正的执行者，而非猜测者。_

---

## 协议 (License)

本项目采用 [GNU Affero General Public License v3.0 (AGPL v3)](LICENSE) 协议开源。
