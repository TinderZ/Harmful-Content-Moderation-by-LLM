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
  
  - [A Holistic Approach to Undesired Content Detection in the Real World (OpenAI)](#a-holistic-approach-to-undesired-content-detection-in-the-real-world-openai)
  - [Llama Guard: LLM-based Input-Output Safeguard for Human-AI Conversations](#llama-guard-llm-based-input-output-safeguard-for-human-ai-conversations)
  - [AEGIS: Online Adaptive AI Content Safety Moderation with Ensemble of LLM Experts](#aegis-online-adaptive-ai-content-safety-moderation-with-ensemble-of-llm-experts)
  - [Content moderation by LLM: from accuracy to legitimacy](#content-moderation-by-llm-from-accuracy-to-legitimacy)
- [Practice & Code (Coming Soon)](#practice--code-coming-soon)
- [Contribution](#contribution)
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

**OpenAI Moderation API** 是一个功能强大的商业化内容审核工具，旨在帮助开发者近乎实时地识别和过滤有害内容。

-   **核心功能**：该 API **将内容分为多个具体的类别并提供置信度分数**。其最新模型甚至支持多模态内容审核。
    -   **最新模型**：OpenAI 在 2024 年推出了基于 GPT-4o 构建的 **`omni-moderation-latest`** 模型，该模型在**处理文本和图像**方面都比其前代产品更准确、更稳健。
    -   **文本模型**：它也提供纯文本模型，如 `text-moderation-latest` 和 `text-moderation-stable`。
    -   **分类体系**：审核类别非常详细，包括 `hate`, `hate/threatening`, `harassment`, `harassment/threatening`, `self-harm`, `self-harm/intent`, `sexual`, `sexual/minors`, `violence`, `violence/graphic` 等。
-   **优势**：
    -   **业界领先的准确性**：基于 OpenAI 最前沿的模型构建，性能强大。
    -   **多模态能力**：最新的模型能够同时处理文本和图像，满足复杂场景的需求。
    -   **简单易用**：通过 API 调用即可集成，无需自行部署和维护。
-   **相关资料**：
    -   [升级多模态审核模型的博客文章](https://openai.com/index/upgrading-the-moderation-api-with-our-new-multimodal-moderation-model/)

### Perspective API

**Perspective API** 是由 Google 的 Jigsaw 部门开发的工具，其核心目标是**评估文本对一场对话可能产生的“负面影响”**，通常被称为“毒性”（Toxicity）。

-   **核心功能**：该 API 会为输入的文本在多个维度上**返回一个 0 到 1 之间的分数**。分数越高，代表文本在该维度上的负面属性越强。
    -   **主要评估属性**：`TOXICITY` (毒性), `SEVERE_TOXICITY` (严重毒性), `IDENTITY_ATTACK` (身份攻击), `INSULT` (侮辱), `PROFANITY` (亵渎), `THREAT` (威胁) 等。
-   **优势**：
    -   **专注于对话健康**：旨在帮助平台改善社区对话环境，而不仅仅是删除内容。
    -   **实时反馈**：非常适合在用户评论时提供即时反馈，鼓励更健康的表达方式。
    -   **免费易用**：对于中低使用量的场景，API 是免费的，集成方便。
-   **适用场景**：新闻网站评论区、在线论坛和社交媒体，用于识别和减少攻击性言论。

### Llama Guard 

[![Hugging Face Model](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Llama%20Guard-brightgreen)](https://huggingface.co/meta-llama/Llama-Guard-4-12B)

**Llama Guard** 是 Meta AI 开源的一款**专门用于保障人机对话安全的 LLM**。它本身就是一个经过指令微调（Instruction-tuned）的语言模型，用于分类用户输入和模型输出是否安全。

-   **核心功能**：Llama Guard 被设计为一个**防护层（Safeguard）**，可以对用户发给 LLM 的提示（Prompt）和 LLM 生成的回复（Response）进行安全风险分类。
    -   **分类体系**：它有一个预定义的风险分类策略，涵盖了如 `暴力与仇恨言论`, `色情内容`, `武器`, `自残` 等类别。
    -   **输出格式**：对于一段文本，它会判断是 `safe` (安全) 还是 `unsafe` (不安全)。如果不安全，它会指出具体违反了哪个风险类别。
-   **优势**：
    -   **开源与可定制**：开发者可以完全控制模型，并根据自己的安全标准对其进行进一步的微调。
    -   **本地部署**：可以在本地环境中运行，保障了数据隐私和低延迟。
    -   **为对话设计**：专注于保障 LLM 应用的输入和输出安全，非常适合用于构建安全的聊天机器人。
-   **相关资料**：
    -   [官方 GitHub 仓库 (Purple Llama)](https://github.com/meta-llama/PurpleLlama.git)

## Key Research Papers

学术界也在积极探索LLM在内容审核中的应用边界和理论基础。以下是几篇值得关注的论文。

### A Holistic Approach to Undesired Content Detection in the Real World (OpenAI)
-   **论文地址**: [https://arxiv.org/abs/2208.03274](https://arxiv.org/abs/2208.03274)
-   **核心思想**: 这篇论文阐述了 OpenAI 构建其内容审核系统的哲学和方法论。它强调了**在真实世界中部署审核系统所面临的整体挑战**，包括需要处理对抗性攻击、适应不断变化的违规内容以及在准确性和覆盖面之间进行权衡。该研究为 OpenAI Moderation API 的开发奠定了理论基础，重点关注如何构建一个**可靠、可扩展且能应对现实世界复杂性**的审核系统。

### Llama Guard: LLM-based Input-Output Safeguard for Human-AI Conversations
-   **论文地址**: [https://arxiv.org/abs/2312.06674](https://arxiv.org/abs/2312.06674)
-   **项目地址**: [https://github.com/meta-llama/PurpleLlama.git](https://github.com/meta-llama/PurpleLlama.git)
-   **核心思想**: 这篇论文详细介绍了 Llama Guard 的设计理念和技术实现。它展示了如何通过收集高质量数据对 Llama 2 进行指令微调，使其成为一个高效的对话安全分类器。论文还对比了 Llama Guard 与其他内容审核工具（如 OpenAI Moderation API）的性能，证明了其在多种场景下的有效性。


### AEGIS: Online Adaptive AI Content Safety Moderation with Ensemble of LLM Experts
-   **论文地址**: [https://arxiv.org/abs/2404.05993](https://arxiv.org/abs/2404.05993)
-   **核心思想**: 这篇论文提出了一个名为 **Aegis** 的系统，它**通过多个专攻不同有害内容领域的LLM专家模型集成（Ensemble）**来提升内容审核的准确性和适应性。
-   **关键贡献**:
    -   **专家模型集成**：不同于单一通用模型，Aegis为每种有害内容训练一个专家LLM，并通过路由模型将输入分发给最合适的专家。
    -   **在线自适应学习**：系统能够**根据新出现的数据和审核员的反馈进行在线学习和调整**，从而快速适应不断变化的有害内容策略和模式。

### Content moderation by LLM: from accuracy to legitimacy
-   **论文地址**: [https://link.springer.com/article/10.1007/s10462-025-11328-1](https://link.springer.com/article/10.1007/s10462-025-11328-1)
-   **核心思想**: 这篇论文超越了单纯的技术准确性讨论，深入探讨了**使用LLM进行内容审核的“合法性”（legitimacy）问题**。
-   **关键贡献**:
    -   **合法性的多维度框架**：文章指出，一个可信赖的审核系统不仅要准确，还必须在**程序正义、透明度和可申诉性**方面具有合法性。
    -   **LLM的角色**：探讨了LLM如何在这些方面发挥作用，例如生成审核决策的详细解释（透明度）。

## Practice & Code (Coming Soon)

本部分计划提供以下内容：

-   使用上述API和模型的Python示例代码。
-   Coming Soon......

欢迎关注本仓库的更新！

## Contribution

你可以通过以下方式参与：

1.  **Fork** 本仓库。
2.  创建一个新的分支 (`git checkout -b feature/your-feature`)。
3.  提交你的修改 (`git commit -m 'Add some feature'`)。
4.  推送到你的分支 (`git push origin feature/your-feature`)。
5.  创建一个 **Pull Request**。

## License

本仓库采用 [MIT License](LICENSE) 许可证。
