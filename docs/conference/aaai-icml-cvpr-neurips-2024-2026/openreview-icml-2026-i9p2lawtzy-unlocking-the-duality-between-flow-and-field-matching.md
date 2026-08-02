---
title: Unlocking the Duality between Flow and Field Matching
title_zh: 解锁流匹配与场匹配之间的对偶性
authors: "Daniil Shlenskii, Alexander Varlamov, Nazar Buzun, Alexander Korotin"
date: 2026-01-19
pdf: "https://openreview.net/pdf/59422b2930966bc78c725b1ddc254c96f4b38d29.pdf"
tags: ["query:dmg"]
score: 7.0
evidence: 条件流匹配与场匹配框架的理论统一
tldr: 条件流匹配（CFM）统一了扩散模型与流匹配等多种生成范式，而相互作用场匹配（IFM）则源于静电场匹配和泊松流生成模型，两者出发点不同。本文提出基本问题：它们是否真正不同？作者证明对前向IFM这一自然子类，CFM与IFM恰好重合，并构造了两者之间的双射。这一结果揭示了看似不同的生成框架在本质上的对偶性，为理解生成模型的底层结构提供了新视角。
source: ICML-2026-Rejected-Public
selection_source: conference_retrieval
motivation: CFM与IFM从不同对象出发定义生成动态，二者关系尚未明确。
method: 通过构造CFM与forward-only IFM之间的双射，证明两者描述相同生成动态。
result: 证明了CFM与自然子类IFM的等价性，建立了两框架间的严格联系。
conclusion: 为统一理解流匹配与场匹配生成范式提供了理论基础。
---

## Abstract
Conditional Flow Matching (CFM) unifies conventional generative paradigms such as diffusion models and flow matching. Interaction Field Matching (IFM) is a newer framework that generalizes Electrostatic Field Matching (EFM) rooted in Poisson Flow Generative Models (PFGM). While both frameworks define generative dynamics, they start from different objects: CFM specifies a conditional probability path in data space, whereas IFM specifies a physics-inspired interaction field in an augmented data space.
This raises a basic question: **are CFM and IFM genuinely different, or are they two descriptions of the same underlying dynamics?** We show that they coincide for a natural subclass of IFM that we call forward-only IFM. Specifically, we construct a bijection between CFM and forward-only IFM. We further show that general IFM is strictly more expressive: it includes EFM and other interaction fields that cannot be realized within the standard CFM formulation. Finally, we highlight how this duality can benefit both frameworks: it provides a probabilistic interpretation of forward-only IFM and yield novel, IFM-driven techniques for CFM.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：条件流匹配（CFM）是一个统一框架，涵盖扩散模型与流匹配等常见生成范式；而相互作用场匹配（IFM）是较新的框架，它推广了源自泊松流生成模型（PFGM）的静电场匹配（EFM）。两者虽然都描述生成动态，但出发点不同——CFM 在数据空间中指定条件概率路径，IFM 则在增广数据空间中指定物理启发的相互作用场。
- **核心问题**：这两种框架是本质上不同的模型，还是对同一底层动态的两种等价描述？
- **整体含义**：论文通过建立 CFM 与一种自然子类——前向 IFM（forward-only IFM）之间的双射，证明了它们在该子类上完全重合；同时指出一般 IFM 严格更具表达力。这一结果揭示了看似独立的生成式框架之间的深层对偶性，为统一理解生成模型的底层结构提供了新的理论视角。

## 2. 方法论

- **核心思想**：作者不采用经验性的比较，而是从理论上探究两种框架的等价性，具体方式是在 CFM 与 forward-only IFM 之间构造一个双向映射（双射）。
- **关键技术细节**（基于摘要可获知的信息）：
  - 定义了“forward-only IFM”这一 IFM 的自然子类，用于与 CFM 进行对比。
  - 构造了 CFM ↔ forward-only IFM 的双射，证明两者生成相同的条件概率路径/动态。
  - 对一般 IFM，作者证明其严格包含 EFM 以及其他无法在标准 CFM 表达式中实现的相互作用场，因此一般 IFM 的表达能力更强。
  - 这种对偶性还有实际收益：为 forward-only IFM 提供了概率解释，并为 CFM 提供新的、由 IFM 启发的构造技术。
- **公式/算法流程**：摘要中未给出具体公式，也未给出算法伪代码，仅有上述理论构造的描述。

## 3. 实验设计

- 论文摘要中**未提及任何实验**，没有给出数据集、基准任务或对比方法。
- 元数据中标注了会议信息（ICML-2026-Rejected-Public），但未提供实验细节。
- 因此，基于当前提供的文本内容，无法总结实验设计。

## 4. 资源与算力

- 文本中**未提及**任何 GPU 型号、数量、训练时长或其他计算资源信息。
- 因缺乏实验描述，也不存在对应的算力说明。

## 5. 实验数量与充分性

- 当前提供的论文内容（仅摘要）中**未包含实验部分**，无法评估实验数量、消融研究或公平性。
- 从摘要的表述看，论文以理论证明为主（构造双射、论证表达力边界），可能不依赖大规模实验；但鉴于这是公开的被拒论文（Rejected-Public），且缺少实证支撑，其实验充分性无法判断。

## 6. 主要结论与发现

- **CFM 与 forward-only IFM 等价**：在 forward-only IFM 这一自然子类中，CFM 与 IFM 恰好重合，且两者之间存在双射。
- **一般 IFM 严格更强**：一般 IFM 的表达能力超过标准 CFM，能够涵盖 EFM 等无法在 CFM 框架内实现的场。
- **对偶性的双向益处**：
  - 对 forward-only IFM，该对偶性给出其概率路径解释。
  - 对 CFM，该对偶性启发新的构造方法，可用于提升 CFM 的设计能力。

## 7. 优点

- **理论贡献清晰**：直接回答了“CFM 和 IFM 是否不同”的基本问题，并通过构造双射给出了严格回答。
- **统一视角**：将两种源自不同思想的框架（概率路径 vs. 物理场）联系起来，有助于跨框架借鉴。
- **表达力边界明确**：不仅证明了一类等价性，还划清了等价性的边界（forward-only 子类），并指出一般 IFM 的超集关系，避免过度概括。
- **实用潜力**：对偶性带来的概率解释和新构造方法，可能在实际生成任务中带来新的建模手段。

## 8. 不足与局限

- **缺乏实验验证**：摘要中没有提供任何数据集、基准或对比实验结果，无法验证理论结论在实际生成任务中的有效性和增益。
- **公开状态为被拒（Rejected-Public）**：论文为 ICML 2026 被拒绝的公开版本，可能说明审稿人对其贡献或严密性存在疑虑（虽然原因未知）。
- **理论范围有限**：等价性仅针对 forward-only IFM，对更一般的 IFM 只证明了 CFM 无法覆盖，但并未给出两者在一般情况下的完整联系。
- **技术细节缺失**：双射的具体构造、证明思路、适用条件（如数据维度、增广空间假设）等在摘要中均未展开，限制了该结论的直接应用。
- **应用限制**：虽然提到对偶性可为 CFM 提供新技巧，但摘要未说明这些技巧如何落地到端到端生成流程，也没有说明对计算复杂度或稳定性的影响。

---

（完）
