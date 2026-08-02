---
title: On the Guidance of Flow Matching
title_zh: 论流匹配的引导
authors: "Ruiqi Feng, Chenglei Yu, Wenhao Deng, Peiyan Hu, Tailin Wu"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=pKaNgFzJBy"
tags: ["query:dmg"]
score: 8.0
evidence: 流匹配的通用引导框架
tldr: 流匹配在图像生成、决策等任务上表现出色，但其引导机制比扩散模型更一般且差异显著，缺乏系统研究。本文提出首个面向一般流匹配的引导框架，推导出一族引导技术，包括免训练的渐近精确引导、基于训练的引导损失以及两类近似引导。该框架为流匹配在能量引导生成任务中的应用提供了统一且可扩展的工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 一般流匹配的引导机制不同于扩散模型，尚缺乏统一和理论化的框架。
method: 构建通用引导框架，并由此导出免训练精确引导、训练式引导损失及近似引导变体。
result: 给出了多种可落地的流匹配引导方法，支持能量引导下的生成。
conclusion: 系统化推进了流匹配引导的理论与方法，拓展了其应用范围。
---

## Abstract
Flow matching has shown state-of-the-art performance in various generative tasks, ranging from image generation to decision-making, where generation under energy guidance (abbreviated as guidance in the following) is pivotal. However, the guidance of flow matching is more general than and thus substantially different from that of its predecessor, diffusion models. Therefore, the challenge in guidance for general flow matching remains largely underexplored. In this paper, we propose the first framework of general guidance for flow matching. From this framework, we derive a family of guidance techniques that can be applied to general flow matching. These include a new training-free asymptotically exact guidance, novel training losses for training-based guidance, and two classes of approximate guidance that cover classical gradient guidance methods as special cases. We theoretically investigate these different methods to give a practical guideline for choosing suitable methods in different scenarios. Experiments on synthetic datasets, image inverse problems, and offline reinforcement learning demonstrate the effectiveness of our proposed guidance methods and verify the correctness of our flow matching guidance framework. Code to reproduce the experiments can be found at https://github.com/AI4Science-WestlakeU/flow_guidance.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- 流匹配（Flow Matching）在图像生成、决策制定等多种生成任务中已达到最先进水平，其关键在于“能量引导下的生成”（即引导，guidance）机制。
- 然而，流匹配的引导机制比其前身扩散模型（Diffusion Models）更为一般化，且与后者存在本质差异。现有对扩散模型引导的理论和方法不能直接迁移到一般流匹配中。
- 目前针对一般流匹配的引导问题缺乏系统研究，没有一个统一、理论化的框架来理解和设计引导方法。
- 本文目的是填补这一空白，提出**首个面向一般流匹配的通用引导框架**，并从中推导出一系列可落地的引导技术，为流匹配在能量引导生成任务中的应用提供统一且可扩展的工具。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：构建一个统一的理论框架来描述一般流匹配中的引导，并基于该框架系统性地导出不同类型的引导方法，而非像以往那样针对特定情形设计启发式算法。
- **关键方法与技术细节**：
  1. **免训练的渐近精确引导**：提出一种新的、无需额外训练的引导方法，理论上可以渐近精确地实现能量引导下的生成。
  2. **基于训练的引导损失**：设计了新颖的训练损失函数，使模型可以通过训练显式地学习引导条件，适用于需要高精度引导的场景。
  3. **两类近似引导**：推导出两类近似引导方法，它们将经典的梯度引导方法（如扩散模型中的 classifier guidance 类方法）作为特例包含在内，从而在统一框架下衔接了已有方法。
- **理论分析**：论文对这些方法进行了理论层面的对比研究，给出了一个实用指南，帮助用户在不同应用场景下选择最合适的引导方法。
- 具体公式和算法流程在摘要中未给出详细展开，但可以确定其方法论是从统一框架出发，通过理论推导得到系列方法。

## 3. 实验设计

- **实验场景与数据集**：
  - 合成数据集（synthetic datasets）：用于验证基本引导机制的正确性。
  - 图像逆问题（image inverse problems）：如图像修复、去模糊等，检验在真实图像数据上的生成与引导效果。
  - 离线强化学习（offline reinforcement learning）：将流匹配引导用于决策任务，验证其泛化能力。
- **Benchmark**：文章未明确列出具体 benchmark 名称，但实验覆盖了生成、逆问题、决策三个典型领域，足以体现方法的广泛适用性。
- **对比方法**：摘要中提到“覆盖经典梯度引导方法作为特例”，暗示实验中会与已有的梯度引导类方法进行对比，但由于信息有限，具体基线方法未列出。

## 4. 资源与算力

- 论文摘要和提供的元数据中**未提及任何关于计算资源的信息**，如 GPU 型号、数量、训练时长、显存等。
- 需要指出：由于缺乏这些信息，无法评估方法的计算开销或可复现性中的算力依赖。

## 5. 实验数量与充分性

- 摘要提到在“合成数据集、图像逆问题和离线强化学习”三类场景上进行了实验，总共应包含多组实验。
- 由于未提供消融实验的具体细节，无法判断是否存在针对不同引导方法、不同超参数的系统性消融。
- 从覆盖范围看，实验场景具有代表性，能够初步验证框架的有效性和通用性。但**充分性无法完全确认**，因为没有实验细节表格、具体结果数值或统计显著性分析。
- 公平性方面：由于将经典梯度引导方法作为特例包含，理论上对比应为公平的；但缺乏实现细节，无法客观判断。

## 6. 论文的主要结论与发现

- 提出了第一个适用于一般流匹配的通用引导框架，统一了此前零散的方法。
- 从框架中推导出多种引导方法，包括免训练的渐近精确引导、训练式引导损失和两类近似引导。
- 理论分析表明这些方法在不同场景下各有优劣，可为用户提供选择依据。
- 实验验证了所提引导方法的有效性，证实了流匹配引导框架的正确性。
- 整体上，论文系统化推进了流匹配引导的理论与方法，拓展了流匹配在能量引导生成任务中的应用范围。

## 7. 优点

- **理论创新**：首次为一般流匹配建立统一引导框架，填补研究空白。
- **方法全面**：同时包含免训练、训练式、近似引导的多种变体，覆盖面广。
- **统一性**：经典梯度引导方法被视为所提出近似引导的特例，体现了框架的包容性和理论深度。
- **实践指导**：给出“实用指南”帮助选择合适方法，具有直接应用价值。
- **应用广泛**：在图像、决策等任务上均验证，展现了跨领域适用性。
- **开源**：提供了代码仓库（GitHub），有利于复现和后续研究。

## 8. 不足与局限

- **信息受限**：由于提供的文本仅为摘要和元数据，无法了解方法的完整数学细节、算法伪代码和具体实验结果。
- **算力缺失**：未报告任何计算资源，可能导致可复现性评估困难。
- **实验细节不足**：没有给出具体数据集规模、指标数值、与已有方法的定量对比结果，难以全面评估性能优势。
- **偏差风险**：摘要由作者自述，可能存在选择性地报告实验结果的倾向；且未提及方法的失败案例或局限条件。
- **应用限制**：虽然框架统一，但免训练精确引导可能在某些复杂能量函数下计算代价高昂；训练式引导需要额外训练，可能有稳定性问题。这些在摘要中未讨论。
- **对比公平性**：未明确说明对比方法的具体配置和调参过程，无法确认比较的公平性。

---

（完）
