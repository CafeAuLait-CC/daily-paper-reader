---
title: "Transition Matching: Scalable and Flexible Generative Modeling"
title_zh: 过渡匹配：可扩展且灵活的生成建模
authors: "Neta Shaul, Uriel Singer, Itai Gat, Yaron Lipman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=An0ePypuOJ"
tags: ["query:dmg"]
score: 8.0
evidence: 统一流匹配与扩散的生成新范式
tldr: 扩散模型和流匹配模型的先进设计空间已较为充分，本文提出Transition Matching（TM），一种离散时间、连续状态的生成范式，将扩散/流模型与连续自回归生成统一。TM将复杂生成分解为马尔可夫转移，支持表达力强的非确定性转移核与任意非连续监督过程，从而解锁新训练目标和方法。在多种生成任务上展示了可扩展性和灵活性，为统一生成模型提供新方向。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有扩散/流模型设计空间挖掘接近瓶颈，而连续自回归模型表现优异但无法统一到同一框架。
method: 将生成任务分解为马尔可夫转移序列，支持通用转移核和非连续监督，统一扩散/流与连续自回归生成。
result: 在多个生成基准上验证了其扩展性和灵活性，性能与现有最强模型相当或更优。
conclusion: 提出了一种统一、可扩展的生成建模范式，连接扩散/流和自回归路线。
---

## Abstract
Diffusion and flow matching models have significantly advanced media generation, yet their design space is well-explored, somewhat limiting further improvements. Concurrently, autoregressive (AR) models, particularly those generating continuous tokens, have emerged as a promising direction for unifying text and media generation, showing improved performance at scale. This paper introduces Transition Matching (TM), a novel discrete-time, continuous-state generative paradigm that unifies and advances both diffusion/flow models and continuous AR generation. TM decomposes complex generation tasks into simpler Markov transitions, allowing for expressive non-deterministic probability transition kernels and arbitrary non-continuous supervision processes, thereby unlocking new flexible design avenues. We explore these choices through three TM variants: (i) Difference Transition Matching (DTM), which generalizes flow matching to discrete-time  by directly learning transition probabilities, yielding state-of-the-art image quality and text adherence. (ii) Autoregressive Transition Matching (ARTM) and (iii) Full History Transition Matching (FHTM) are partially and fully causal models, respectively, that generalize continuous AR methods. They achieve continuous causal AR generation quality comparable to non-causal approaches and potentially enable seamless integration with existing AR text generation techniques. Notably, FHTM is the first fully causal model to match or surpass the performance of flow-based methods on text-to-image task in continuous domains. 
  We demonstrate these contributions through a rigorous large-scale comparison of TM variants and relevant baselines, maintaining a fixed architecture, training data, and hyperparameters.

---

## 论文详细总结（自动生成）

# 论文中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：扩散模型（Diffusion Models）和流匹配模型（Flow Matching）已在媒体生成领域取得显著进展，但这一范式经过大量探索后，其设计空间已趋于饱和，进一步性能提升受到限制。与此同时，自回归（AR）模型，尤其是生成连续 token 的 AR 模型，在统一文本与媒体生成方面展现出强大潜力，并在大规模训练下表现持续提升。
- **核心问题**：能否提出一种新的生成范式，将扩散/流匹配模型与连续自回归生成统一起来，突破现有设计瓶颈，同时兼具可扩展性和灵活性？
- **整体含义**：本文提出 **Transition Matching (TM)**，一种离散时间、连续状态的生成建模新范式，意图统一并推进扩散/流模型与连续自回归生成，为大规模生成模型提供新的设计空间和训练目标。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将复杂生成任务分解为一系列更简单的 **马尔可夫转移（Markov transitions）**。与现有扩散/流模型常用的确定性插值或噪声扰动过程不同，TM 允许使用**表达力强的非确定性概率转移核**，以及**任意非连续的监督过程**，从而解锁更灵活的训练目标和生成路径。
- **技术细节**：TM 是一种离散时间、连续状态的生成范式，每个时间步学习一个条件概率转移核，从而模拟从先验分布到数据分布的演化过程。该框架天然兼容连续自回归生成——只需将每个 token 的生成视为一步马尔可夫转移。
- **三个变体**：
  1. **Difference Transition Matching (DTM)**：将流匹配推广到离散时间，通过学习转移概率（而不是直接学习速度场或得分）来生成，实现了图像质量和文本对齐方面的最先进水平。
  2. **Autoregressive Transition Matching (ARTM)**：部分因果模型，推广了连续自回归方法。
  3. **Full History Transition Matching (FHTM)**：完全因果模型，同样推广连续自回归方法，并且是第一个在连续域文本到图像任务上达到或超过基于流的方法的完全因果模型。
- **算法流程（文字描述）**：定义一组离散时间步；在每个时间步，给定当前状态（或历史状态），模型预测下一个状态的条件转移分布；通过监督信号（例如真实数据转移或某种非连续指标）训练模型，使其匹配真实数据生成过程中的马尔可夫转移；在推理时，从先验噪声开始，按学到的转移核逐步采样，最终生成数据。

## 3. 实验设计：使用了哪些数据集 / 场景，它的 benchmark 是什么，对比了哪些方法

- **实验场景**：主要集中在**文本到图像生成**任务，并覆盖连续域中的因果/非因果生成。
- **数据集与 benchmark**：论文 PDF 中未明确列出具体数据集名称（如 MS-COCO、Flickr、ImageNet 等）。从摘要看，作者进行了“大规模比较”，但未提供基准细节。元数据中的 result 仅指出“在多个生成基准上验证了扩展性和灵活性”，但未举例。
- **对比方法**：
  - 对比了 TM 的三个变体（DTM、ARTM、FHTM）之间性能差异；
  - 对比了相关基线，包括基于流的方法（flow-based methods）以及现有的连续自回归方法；
  - 所有对比均在**固定架构、固定训练数据、固定超参数**的条件下进行，以保证公平性。
- **实验设计亮点**：采用受控变量设计，确保差异仅来自建模方法本身，而非额外数据、模型规模或调参。

## 4. 资源与算力

- **论文内容中未明确说明**：提取的文本和元数据中没有提供 GPU 型号、数量、训练时长、参数量等资源信息。
- 因此，无法从现有资料判断其算力开销或训练成本，这是信息缺失的部分。

## 5. 实验数量与充分性

- **实验数量**：论文提到进行了“严格的大规模比较”，包含三种 TM 变体和相关基线的对比。但具体实验组数（例如不同数据集、不同规模、消融研究等）在提供的文本中未详细说明。
- **充分性判断**：
  - 从摘要来看，实验覆盖了文本到图像任务，并对比了因果与非因果方法，还特别强调了 FHTM 首次超越流方法，这在一定程度上验证了方法的有效性；
  - 但由于缺少详细实验列表、消融分析、超参数敏感性和公开 benchmark 结果，**无法从现有文本充分评估实验的完备性和客观性**；
  - 固定架构、数据和超参数的对比设计对于公平性有积极作用，但缺乏对模型规模、训练成本、推理效率等的分析。

## 6. 论文的主要结论与发现

- TM 是一种统一扩散/流模型与连续自回归生成的有效新范式，具有可扩展性和灵活性。
- DTM 变体实现了最先进的图像质量和文本对齐性能。
- ARTM 和 FHTM 让连续因果自回归生成达到了与非因果方法相当的质量，说明因果建模不再牺牲性能。
- FHTM 是第一个在连续域文本到图像任务上达到或超过基于流的方法的完全因果模型，为无缝集成现有 AR 文本生成技术提供了可能。
- 在固定架构、数据和超参数下，TM 变体的性能优于或等同于现有基线，证明了该框架的通用性和优势。

## 7. 优点

- **统一性强**：将扩散/流模型和连续自回归生成纳入同一框架，具有理论统一性和实践上的广阔应用前景。
- **设计空间灵活**：允许非确定性转移核和任意非连续监督过程，为未来设计新的生成过程和训练目标提供了巨大空间。
- **变体覆盖全**：从非因果 DTM、部分因果 ARTM 到完全因果 FHTM，系统性地探索了不同因果程度下的表现，揭示了因果性对生成质量的影响。
- **公平对比**：固定架构、数据和超参数的大规模比较增强了结论的可信度。
- **突破性结果**：FHTM 证明完全因果模型也可以达到流方法的性能，这对下一代文本/媒体统一模型具有重要启示。

## 8. 不足与局限

- **信息不完整**：当前提供的论文内容仅有摘要和元数据，缺少完整的方法公式、实验细节、数据集描述等关键信息，无法进行深入的技术复现和客观评价。
- **实验覆盖面不明**：未列出具体数据集、评估指标（如 FID、CLIP Score 等）、模型规模、基线具体配置，也未说明是否进行了消融实验，因此难以判断实验的充分性。
- **算力资源未披露**：没有说明训练所需 GPU 数量和时间，对于可扩展性的主张缺乏成本维度的支撑。
- **潜在偏差风险**：论文强调“大规模比较”，但未展示不同随机种子、多次运行的标准差等统计信息；且由作者自行实现基线，可能存在实现偏差。
- **应用限制**：主要验证了文本到图像任务，未涵盖文本生成、图像到视频、音频等其他模态；完全因果模型的推理效率、长序列稳定性等问题有待进一步研究。

---

（完）
