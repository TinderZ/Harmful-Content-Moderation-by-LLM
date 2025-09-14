# Harmful-Content-Moderation-by-LLM

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A knowledge base and learning blog focused on exploring and learning **how to use Large Language Models (LLMs) for harmful content moderation**.

随着LLM的快速发展，其在理解、生成和评估文本方面的强大能力为内容审核领域带来了新的机遇和挑战。本仓库旨在整理和分享利用LLM进行内容审核的前沿技术、主流模型和重要研究成果。

## Table of Contents

- [Introduction: Why Use LLMs for Content Moderation?](#introduction-why-use-llms-for-content-moderation)
- [Mainstream Models](#mainstream-models)
  - [OpenAI Moderation API](#openai-moderation-api)
  - [Perspective API](#perspective-api)
  - [Llama Guard](#llama-guard)
- [Key Research Papers](#key-research-papers)
  - [Aegis: Online Adaptive AI Content Safety Moderation with Ensemble of LLM Experts](#aegis-online-adaptive-ai-content-safety-moderation-with-ensemble-of-llm-experts)
  - [Content moderation by LLM: from accuracy to legitimacy](#content-moderation-by-llm-from-accuracy-to-legitimacy)
- [Practice & Code (Coming Soon)](#practice--code-coming-soon)
- [License](#license)

## Introduction: Why Use LLMs for Content Moderation?

传统的内容审核方法通常依赖于关键词匹配、正则表达式或传统的机器学习模型。这些方法在面对**语义复杂、充满隐喻和不断变化的有害内容**时，往往显得力不从心。

大型语言模型（LLM）的出现为解决这些挑战提供了新的思路：

1.  **强大的语义理解能力**：LLM能够理解上下文、识别讽刺、仇恨言论的微妙变体以及其他形式的“隐性”有害内容。
2.  **零样本/少样本分类**：通过精心设计的提示（Prompt），LLM可以在没有大量标注数据的情况下，对各种类型的有害内容进行分类。
3.  **可解释性和灵活性**：LLM不仅可以判断内容是否有害，还能提供判断的理由，这为审核决策的透明度和申诉机制提供了支持。
4.  **适应性**：LLM可以快速适应新型的有害内容模式，只需更新其知识或微调即可，而无需重新训练整个模型。

本仓库将深入探讨如何利用这些优势来构建更高效、准确和公平的内容审核系统。

## Mainstream Models

内容审核领域有几个广为人知且功能强大的模型/API，它们代表了不同的技术路径和应用场景。

### OpenAI Moderation API

**OpenAI Moderation API** 是由OpenAI提供的一种即用型内容审核工具。它旨在帮助开发者识别和过滤其平台上的潜在有害内容。

-   **核心功能**：该API可以将文本分为多个类别，如**仇恨言论（hate）、威胁（hate/threatening）、自残（self-harm）、性（sexual）、暴力（violence）**等。它不仅返回分类结果，还为每个类别提供一个置信度分数。
-   **优势**：
    -   **简单易用**：只需通过API调用即可获得结果，无需自己训练或部署模型。
    -   **高性能**：基于OpenAI强大的基础模型构建，对多种语言和有害内容变体都有很好的识别效果。
    -   **持续更新**：模型由OpenAI维护和迭代，能够持续对抗新型的有害内容。
-   **适用场景**：适用于需要快速集成、稳定可靠的内容审核功能的各类应用，如社交媒体、聊天机器人、论坛等。

### Perspective API

**Perspective API** 是由Google的Jigsaw团队开发的一款工具，旨在帮助开发者和发布者理解和分析在线评论和对话的“毒性”（toxicity）。

-   **核心功能**：该API的核心是**评估文本的“毒性”程度**，即一段文本可能让其他人离开对话的可能性。除了主要的`TOXICITY`属性外，它还提供多种实验性属性，如**严重毒性（SEVERE_TOXICITY）、侮辱（INSULT）、威胁（THREAT）**等。
-   **优势**：
    -   **专注于对话健康**：其设计初衷是为了改善在线对话环境，而不仅仅是过滤内容。
    -   **提供实时反馈**：可以集成到评论系统中，在用户输入时提供实时反馈，引导其发表更健康的言论。
    -   **多语言支持**：支持多种主流语言。
-   **适用场景**：非常适合用于在线社区、新闻网站评论区、游戏聊天等场景，旨在促进积极和健康的互动。

### Llama Guard

**Llama Guard** 是由Meta AI发布的一款基于Llama 2构建的开源模型，专门用于**保护人类与AI之间的对话安全**。它是一个**LLM本身的安全防护层**。

-   **核心功能**：Llama Guard可以对**用户输入（Prompt分类）**和**AI生成的内容（Response分类）**进行安全评估。它将内容风险分为不同的类别，如暴力、仇恨言论、不当内容等，并判断内容是“安全”还是“不安全”。
-   **优势**：
    -   **开源与可定制**：作为一个开源模型，开发者可以根据自己的需求对其进行微调，以适应特定的安全标准和分类体系。
    -   **双向审核**：同时保护用户免受不安全AI回复的影响，也保护AI免受恶意用户输入的攻击。
    -   **分类精细**：提供了详细的风险分类，便于进行精细化的安全策略控制。
-   **适用场景**：适用于构建基于LLM的聊天机器人、AI助手等应用，作为其输入和输出的“安全门”。

## Key Research Papers

学术界也在积极探索LLM在内容审核中的应用边界和理论基础。以下是两篇值得关注的论文。

### Aegis: Online Adaptive AI Content Safety Moderation with Ensemble of LLM Experts

-   **核心思想**：这篇论文提出了一个名为 **Aegis** 的系统，它**通过多个专攻不同有害内容领域的LLM专家模型集成（Ensemble）**来提升内容审核的准确性和适应性。
-   **关键贡献**：
    -   **专家模型集成**：不同于单一通用模型，Aegis为每种有害内容（如仇恨言论、虚假信息）训练一个专家LLM，并通过一个路由模型将输入内容分发给最合适的专家。
    -   **在线自适应学习**：系统能够**根据新出现的数据和审核员的反馈进行在线学习和调整**，从而快速适应不断变化的有害内容策略和模式。
    -   **解决了“灾难性遗忘”问题**：通过专家模型的架构，避免了在学习新知识时忘记旧知识的问题。
-   **启发**：该研究为构建动态、高精度的工业级内容审核系统提供了一个非常有效的架构思路。

### Content moderation by LLM: from accuracy to legitimacy

-   **核心思想**：这篇论文超越了单纯的技术准确性讨论，深入探讨了**使用LLM进行内容审核的“合法性”（legitimacy）问题**。
-   **关键贡献**：
    -   **合法性的多维度框架**：文章指出，一个可信赖的审核系统不仅要准确，还必须在**程序正义（procedural justice）、透明度（transparency）和可申诉性（contestability）**方面具有合法性。
    -   **LLM的角色**：探讨了LLM如何在这些方面发挥作用。例如，LLM可以生成审核决策的详细解释（透明度），或者模拟不同社群的价值观来辅助决策（程序正义）。
    -   **挑战与风险**：同时也分析了过度依赖LLM可能带来的风险，如**偏见固化、权力集中和对人类审核员的冲击**。
-   **启发**：这篇论文提醒我们，在追求技术方案的同时，必须关注其社会、伦理和治理层面的影响，构建负责任的AI审核系统。

## Practice & Code (Coming Soon)

本部分计划提供以下内容：

-   使用上述API和模型的Python示例代码。
-   持续推出......

欢迎关注本仓库的更新！


## License

本仓库采用 [MIT License](LICENSE) 许可证。
