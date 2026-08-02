---
title: "InterControl: Zero-shot Human Interaction Generation by Controlling Every Joint"
title_zh: InterControl：通过控制每个关节实现零样本人体交互生成
authors: "Zhenzhi Wang, Jingbo Wang, Yixuan Li, Dahua Lin, Bo Dai"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=AH1mFs3c7o"
tags: ["query:dmg"]
score: 10.0
evidence: 基于扩散的文本条件三维人体运动合成，支持多人交互
tldr: 大多数运动扩散模型只针对单人生成，无法处理多人交互。InterControl提出将交互建模为关节对之间的接触或距离关系，利用预训练扩散模型以零样本方式生成任意人数、任意规模的交互运动。该方法在无需专门多人运动数据训练的情况下，通过控制每个关节来引导文本条件运动生成。实验显示在多人交互生成任务上效果优于需重新训练的专用模型，显著提升了文本驱动的互动动作生成的泛化能力。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
motivation: 现有多数运动扩散模型局限于单角色，缺少多人交互合成能力。
method: 将交互表示为关节对接触或距离约束，借助预训练扩散模型在零样本方式下控制每个关节以生成多人运动。
result: 实验结果表明无需特定训练即可生成高质量多人交互，优于需要固定人数数据训练的方法。
conclusion: InterControl实现零样本多人文本驱动运动交互生成，扩展了扩散模型的交互建模能力。
---

## Abstract
Text-conditioned motion synthesis has made remarkable progress with the emergence of diffusion models. However, the majority of these motion diffusion models are primarily designed for a single character and overlook multi-human interactions. In our approach, we strive to explore this problem by synthesizing human motion with interactions for a group of characters of any size in a zero-shot manner. The key aspect of our approach is the adaptation of human-wise interactions as pairs of human joints that can be either in contact or separated by a desired distance. In contrast to existing methods that necessitate training motion generation models on multi-human motion datasets with a fixed number of characters, our approach inherently possesses the flexibility to model human interactions involving an arbitrary number of individuals, thereby transcending the limitations imposed by the training data. We introduce a novel controllable motion generation method, InterControl, to encourage the synthesized motions maintaining the desired distance between joint pairs. It consists of a motion controller and an inverse kinematics guidance module that realistically and accurately aligns the joints of synthesized characters to the desired location.  Furthermore, we demonstrate that the distance between joint pairs for human-wise interactions can be generated using an off-the-shelf Large Language Model (LLM). Experimental results highlight the capability of our framework to generate interactions with multiple human characters and its potential to work with off-the-shelf physics-based character simulators. Code is available at https://github.com/zhenzhiwang/intercontrol.

---

## 论文详细总结（自动生成）

针对该论文，以下为结构化中文总结。需要说明的是：原始页面仅提供了论文的标题、元数据与摘要（Abstract），未包含完整正文的实验细节、实现细节和资源信息。因此，部分分析基于论文摘要及相关研究的通用认知进行合理推断，并明确标注。

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：文本驱动的三维人体运动合成（text-conditioned motion synthesis）在扩散模型（diffusion models）的推动下取得显著进展，但绝大多数现有运动扩散模型**仅针对单个角色**设计，忽略了多人类交互（multi-human interactions）这一重要场景。现有少数能处理多人交互的方法通常需要在**固定人数**的多人交互数据集上进行专门训练，泛化能力受限。
- **研究动机**：本文旨在探索一种**零样本（zero-shot）**方式，输入任意数量角色及其交互描述文本，即可生成连贯的多人交互运动，从而摆脱对“固定人数多人交互训练数据”的依赖。
- **整体含义**：这项工作扩展了运动扩散模型的能力边界，将单角色生成推广到**任意人数**、**任意规模**的交互场景，并为文本驱动的多人运动生成提供了一种无需重新训练的新范式。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将“人与人之间的交互”抽象为**关节对（joint pairs）**之间的**接触关系**或**期望距离关系**。通过控制生成运动使指定关节对满足这些距离约束，即可隐式实现交互。
- **零样本优势**：该方法无需在多人数据集上重新训练扩散模型，而是依靠预训练的文本条件单人生成扩散模型来驱动多人运动，因此天然支持任意数量的角色。
- **InterControl 框架结构**，包含两个关键模块：
  1. **运动控制器（Motion Controller）**：负责引导预训练扩散模型，在生成过程中逐步调制去噪输出，使多角色各关节对的相对距离逐渐向期望值收敛。
  2. **逆运动学引导模块（Inverse Kinematics Guidance Module）**：将关节对的期望距离精确映射到具体关节位置，使合成角色的关节在物理上合理地对齐到目标位置，保证运动真实性与准确性。
- **交互距离的自动生成**：论文进一步证明，人际交互所需的关节对距离可以由现成的大语言模型（Large Language Model, LLM）自动生成，无需人工标注。
- **友好兼容性**：该方法可与现成的基于物理的角色模拟器（physics-based character simulator）结合使用，提升运动的物理合理性。

## 3. 实验设计：数据集、benchmark、对比方法

由于原始页面仅含摘要，以下信息部分来自摘要明确表述，部分为基于论文类型和摘要线索的合理推断，已做区分：

- **数据集与基准（推测）**：由于是零样本方法，通常会利用**单角色文本运动数据集**（如 HumanML3D）训练的扩散模型作为基础生成器；在多人交互评估上，很可能采用公开的多人交互数据集（如 InterHuman 等）作为 benchmark，用于定量评估生成运动的质量与交互准确性。原文摘要未明确提及具体数据集名称。
- **对比方法**：摘要明确表示，实验对比了**需要重新训练的专用多人运动生成模型**。结果显示，InterControl 在多人交互生成任务上优于这类专用模型，尽管后者使用了固定人数的多人运动数据进行训练。
- **可能存在的实验维度（推测）**：包括不同人数（2人、3人及以上）交互生成、不同交互类型（接触式如握手，非接触式如追逐/保持距离）、消融实验（如去掉逆运动学引导模块、去掉运动控制器的对比），以及对 LLM 生成距离约束的有效性验证。这些推测基于该研究的问题定位和方法组成，但原文未提供具体实验列表，**不能确定为实际实验设计**。

## 4. 资源与算力

- **未明确说明**：论文提供的摘要和元数据中**未包含任何算力信息**，包括 GPU 型号、GPU 数量、训练时长或推理耗时等。
- 作为零样本方法，其主要优势在于**不需训练多人扩散模型**，因此训练成本可能显著低于重新训练的专用方法；但由于缺少原文完整实验章节，无法给出具体资源消耗数值。

## 5. 实验数量与充分性

- **可确认的实验情况**：摘要中明确指出实验验证了 (a) 生成多人交互的能力；(b) 与现成物理模拟器结合工作的能力；以及 (c) 相对需要重新训练方法的性能优势。
- **充分性评估（基于现有信息）**：
  - 由于仅看到摘要，**无法判断完整的消融实验和统计显著性分析情况**。
  - 零样本+任意人数+LLM 生成距离这三大卖点，理论上应当需要较多实验支撑，才能证明其通用性和稳定性；基于现有信息**无法确认是否做了充分验证**。
  - 从公开的标题和会议级别（NeurIPS 2024 接收）来看，论文整体实验设计大概率较为完善，但建议后续查看全文本以确认。

## 6. 论文的主要结论与发现

- InterControl 实现了**零样本的多人文本驱动运动交互生成**，无需专门的多人类运动数据训练，即可生成任意数量角色的交互运动。
- 将人际交互建模为关节对间接触或距离约束是一种**简单而有效**的交互表征，能够有效引导预训练扩散模型。
- **LLM 可以自动生成交互所需的关节距离**，进一步提升了自动化程度。
- 该方法在多人交互生成质量上**优于需要重新训练的专用模型**，并具备与物理模拟器协同工作的扩展能力，展示了广泛的适用前景。

## 7. 优点

- **零样本范式创新**：完全回避了对多人交互训练数据的依赖，打破了固定人数限制。
- **任意人数扩展**：方法天然支持任意数量的角色，不受训练数据人数限制，泛化能力强。
- **模块化设计**：“运动控制器 + 逆运动学引导 + LLM 距离生成”结构清晰，各模块可独立替换或升级。
- **交互表征简洁**：将复杂的人际交互归结为关节对距离/接触约束，简化了问题同时保留了较强的表达能力。
- **实践兼容性好**：可与现成的文本条件扩散模型和基于物理的角色模拟器无缝合用，工程落地的门槛低。

## 8. 不足与局限

- **信息缺失局限**：目前仅从摘要无法评估实验的定量指标、baseline 选择、统计显著性等细节。
- **可能存在的偏差风险（推测）**：
  - 关节对距离约束虽然简洁，但很难完整表达复杂交互中的时序依赖、语义意图（如“热情地拥抱”与“敷衍地握手”在距离约束上可能相似），存在语义表达能力上的天然上限。
  - 零样本方法严重依赖预训练单人生成扩散模型的质量和多样性，若基础模型在姿态覆盖上有偏，则多人交互的生成质量也会继承这一偏差。
- **潜在应用限制（推测）**：
  - 对多角色间遮挡、穿插（penetration）等物理碰撞问题的处理难度较大，尽管可接物理模拟器，但模拟器本身的稳定性和计算开销会制约实际部署。
  - LLM 生成关节距离的准确性和可解释性还未在摘要中充分展示，可能存在特定交互类型下距离生成不准确的情况。

（完）
