---
title: Discrete Flow Matching
title_zh: 离散流匹配
authors: "Itai Gat, Tal Remez, Neta Shaul, Felix Kreuk, Ricky T. Q. Chen, Gabriel Synnaeve, Yossi Adi, Yaron Lipman"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=GTDKo3Sv9p"
tags: ["query:dmg"]
score: 9.0
evidence: 将流匹配扩展到离散数据，支持一般概率路径和通用采样公式
tldr: 流匹配和扩散模型已成功用于连续数据，但高维离散数据（如语言）上的应用仍有限。本文提出离散流匹配，为离散数据生成设计了一种新的流范式。它支持一般的概率路径族，并给出基于学习后验（如x预测和epsilon预测）的通用采样公式，具体聚焦于用扩散定义的特定概率路径，为离散生成建模提供了新框架。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
motivation: 流匹配/扩散在高维离散数据上的生成能力不足。
method: 提出离散流匹配，定义一般概率路径并用学习后验推导通用采样公式。
result: 在离散数据生成上展现了良好的灵活性和有效性。
conclusion: 为语言等离散结构的生成提供了新的匹配范式。
---

## Abstract
Despite Flow Matching and diffusion models having emerged as powerful generative paradigms for continuous variables such as images and videos, their application to high-dimensional discrete data, such as language, is still limited.  In this work, we present Discrete Flow Matching, a novel discrete flow paradigm designed specifically for generating discrete data.  Discrete Flow Matching offers several key contributions:  (i) it works with a general family of probability paths interpolating between source and target distributions; (ii) it allows for a generic formula for sampling from these probability paths using learned posteriors such as the probability denoiser ($x$-prediction) and noise-prediction ($\epsilon$-prediction); (iii) practically, focusing on specific probability paths defined with different schedulers improves generative perplexity compared to previous discrete diffusion and flow models; and (iv) by scaling Discrete Flow Matching models up to 1.7B parameters, we reach 6.7% Pass@1 and 13.4% Pass@10 on HumanEval and 6.7% Pass@1 and 20.6% Pass@10 on 1-shot MBPP coding benchmarks. Our approach is capable of generating high-quality discrete data in a non-autoregressive fashion, significantly closing the gap between autoregressive models and discrete flow models.

---

## 论文详细总结（自动生成）

# 离散流匹配（Discrete Flow Matching）论文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：流匹配（Flow Matching）和扩散模型在连续数据（如图像、视频）上已经取得了巨大成功，但在高维离散数据（如自然语言）上的生成能力仍然有限。现有的离散扩散模型或离散流模型在语言等离散结构上的表现尚不理想，与自回归模型相比仍有较大差距。
- **核心问题**：如何设计一种适用于离散数据的流匹配范式，使其能够像连续流匹配一样灵活地定义概率路径，并实现高效、高质量的非自回归离散数据生成。
- **整体含义**：本文提出 **离散流匹配（Discrete Flow Matching）**，为离散数据生成提供了一种新的理论框架和实用方法，并在大规模语言/代码生成任务上验证了其有效性，显著缩小了离散流模型与自回归模型之间的性能差距。

## 2. 论文提出的方法论：核心思想、关键技术细节与流程

- **核心思想**：将连续流匹配的思想推广到离散空间，定义源分布（如噪声分布）与目标分布（如数据分布）之间的一般概率路径，并利用学习到的后验概率（posteriors）推导出通用的采样公式。
- **关键技术细节**：
  - **一般概率路径族**：支持在源分布和目标分布之间插值的任意概率路径，不局限于特定形式，从而具有广泛的适用性。
  - **通用采样公式**：基于学习到的后验概率进行采样，具体包括两种常见形式：
    - **概率去噪器（$x$-prediction）**：直接预测干净的数据点。
    - **噪声预测（$\epsilon$-prediction）**：预测噪声分量（类似于扩散模型中的噪声预测）。
  - 通过不同的调度器（schedulers）可以定义具体的概率路径，在实验中验证了不同调度器对生成质量的影响。
- **算法流程（文字说明）**：
  1. 定义一个从源分布（如均匀噪声）到目标数据分布的离散插值路径；
  2. 训练一个神经网络，使其在给定中间状态（插值结果）和时刻的条件下，学习估计目标后验概率（例如预测原始数据或预测噪声）；
  3. 采样时，从源分布出发，结合学习到的后验概率，按照定义的路径逐步迭代转换，最终得到生成样本；
  4. 整个过程可以**非自回归**地进行，即一次性生成完整序列，而非逐词生成。

## 3. 实验设计：数据集、Benchmark 与对比方法

- **数据集 / 场景**：
  - **语言生成任务**：评估生成困惑度（perplexity），用于衡量离散流模型的生成质量。
  - **代码生成任务**：
    - **HumanEval**：业界常用的代码生成 benchmark，衡量程序通过率。
    - **MBPP**（Mostly Basic Python Problems）：使用 1-shot 设置。
- **对比方法**：
  - 与之前的**离散扩散模型（discrete diffusion models）** 和**离散流模型（discrete flow models）** 进行困惑度对比。
  - 在大规模模型上，与**自回归模型**的性能进行对比，以验证非自回归离散流模型的竞争力。
- **主要指标**：
  - **Perplexity（困惑度）**：用于生成质量评估。
  - **Pass@1 和 Pass@10**：代码生成任务中，一次生成通过测试的比例（Top-1 和 Top-10）。

## 4. 资源与算力

- **原文信息**：提供的文本摘要中**未明确说明**使用的 GPU 型号、数量、训练时长等计算资源信息。
- **可推断信息**：论文将模型扩展到 **1.7B 参数**，表明实验规模较大，可能使用了大规模分布式训练集群，但具体硬件配置无从得知。
- **结论**：无法从当前内容中总结具体算力消耗，需要查看论文正文或附录获取详细信息。

## 5. 实验数量与充分性

- **实验组数**：
  - 摘要中至少包含两类实验：**困惑度对比实验**（在不同调度器下的生成质量）和**大规模代码生成实验**（HumanEval 和 MBPP）。
  - 还提到了模型规模从较小规模扩展到 **1.7B 参数**，暗示可能有不同规模模型的扩展性实验。
- **充分性与客观性**：
  - 从摘要来看，实验覆盖了语言生成和代码生成两个场景，并且与先前离散扩散/流模型进行了比较，也报告了与自回归模型的差距，说明作者进行了一定的基准测试。
  - **局限性**：摘要中未提及消融实验、不同概率路径的详细对比、超参数敏感性分析等细节；也没有报告训练数据集的具体规模或数据预处理方式。因此，仅凭摘要难以判断实验的充分性和公平性的全部细节，但可以认为核心结论有基本实验支持。

## 6. 论文的主要结论与发现

- 离散流匹配能够支持**一般的概率路径族**，并提供了基于学习后验的**通用采样公式**，包括 $x$-prediction 和 $\epsilon$-prediction 两种形式。
- 使用不同的调度器定义具体概率路径时，可以**改进生成困惑度**，优于先前的离散扩散和流模型。
- 将模型扩展到 **1.7B 参数**后，在代码生成任务上取得了具有竞争力的结果：
  - **HumanEval**：Pass@1 = 6.7%，Pass@10 = 13.4%
  - **MBPP（1-shot）**：Pass@1 = 6.7%，Pass@10 = 20.6%
- 该方法是**非自回归**的，能够生成高质量的离散数据，并且**显著缩小了自回归模型与离散流模型之间的性能差距**。

## 7. 优点

- **理论贡献**：将流匹配扩展到离散数据，提出了一种通用的离散数据生成框架，支持灵活的概率路径定义，具有较好的数学泛化能力。
- **实用采样公式**：同时支持 $x$-prediction 和 $\epsilon$-prediction 两种后验形式，与扩散模型中的常见做法兼容，易于实现和扩展。
- **非自回归生成**：突破了自回归逐词生成的瓶颈，可以并行生成，具有潜在的高效优势。
- **大规模验证**：在 1.7B 参数规模上验证了方法的有效性，展示了可扩展性。
- **性能提升**：在标准 benchmark（HumanEval、MBPP）上给出了明确结果，为后续研究提供了对照基准。

## 8. 不足与局限

- **缺少训练细节**：提供的文本中没有说明训练数据规模、训练步数、优化器、学习率等关键实验设置，降低了结果的可复现性。
- **实验细节不完整**：没有列出所有对比方法的参数规模、训练配置，也没有展示详细的消融实验（例如不同概率路径的作用、后验选择的影响等），因此难以全面评估各设计选择的有效性。
- **算力信息缺失**：未报告所使用的 GPU 资源和训练成本，不利于评估方法的实际计算开销。
- **性能绝对值仍有差距**：尽管缩小了与自回归模型的差距，但 Pass@1 等指标仍相对较低（如 HumanEval 6.7%），说明离散流模型在代码生成等复杂任务上尚未完全超越自回归方法。
- **应用范围有限**：摘要中主要展示了语言和代码生成实验，对于其他类型的离散数据（如分子图、离散时间序列等）的适用性没有提及。
- **偏见风险**：当前内容仅来自摘要和元数据，可能遗漏了论文中的深入分析、失败案例或潜在陷阱，所有结论需要以全文内容为准。

（完）
