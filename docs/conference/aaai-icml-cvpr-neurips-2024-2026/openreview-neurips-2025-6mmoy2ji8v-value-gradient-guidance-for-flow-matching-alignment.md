---
title: Value Gradient Guidance for Flow Matching Alignment
title_zh: 用于流匹配对齐的值梯度引导
authors: "Zhen Liu, Tim Z. Xiao, Carles Domingo-Enrich, Weiyang Liu, Dinghuai Zhang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=6MmOy2Ji8V"
tags: ["query:dmg"]
score: 8.0
evidence: 基于最优控制与值梯度的流匹配微调对齐方法
tldr: 现有流匹配模型的对齐方法难以兼顾适应效率与概率先验保持。本文基于最优控制理论，提出VGG-Flow：通过让微调速度场与预训练模型的差匹配值函数的梯度，结合值函数的启发式初始化，实现快速自适应。该方法利用奖励模型的一阶信息，同时保持预训练分布特性。实验表明在多个奖励对齐任务上，VGG-Flow比现有方法更高效，且生成质量和多样性兼顾，为流匹配模型对齐提供了新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有的流匹配对齐方法无法同时实现高效适应和可靠的先验保持。
method: 基于最优控制，将速度场差匹配值函数梯度，并利用启发式初始化值函数实现快速微调。
result: 实验显示该算法在多种对齐任务上适应更快、生成质量更高，且保持先验分布。
conclusion: VGG-Flow提供了一种理论上合理的流匹配对齐方法，兼具效率与质量保障。
---

## Abstract
While methods exist for aligning flow matching models––a popular and effective class of generative models––with human preferences, existing approaches fail to achieve both adaptation efficiency and probabilistically sound prior preservation. In this work, we leverage the theory of optimal control and propose VGG-Flow, a gradient matching–based method for finetuning pretrained flow matching models. The key idea in this algorithm is that the optimal difference between the finetuned velocity field and the pretrained one should be matched with the gradient field of a value function. This method not only incorporates first-order information from the reward model but also benefits from heuristic initialization of the value function to enable fast adaptation. Empirically, we show on a popular text-to-image flow matching model, Stable Diffusion 3, that our method can finetune flow matching models under limited computational budgets while achieving effective and prior-preserving alignment.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：流匹配（Flow Matching）是一类流行的生成模型范式，已应用于高分辨率文本到图像生成（如 Stable Diffusion 3）。在实际部署中，这类模型需要与人类偏好或下游任务奖励进行“对齐”（alignment）。
- **核心问题**：现有的流匹配对齐方法无法同时满足两个关键要求：
  - **适应效率**：在有限计算预算下快速适配新的奖励信号；
  - **概率先验保持**：微调过程中不破坏预训练模型学到的数据分布与生成多样性。
- **整体含义**：论文试图从最优控制理论出发，解决“既要快速适应奖励、又要保持先验分布”的这一矛盾，为流匹配模型的对齐提供一种理论上更合理、实践上更高效的方案。

## 2. 方法论：VGG-Flow

- **核心思想**：将“流匹配模型的对齐”建模为最优控制问题。最优的微调速度场与预训练速度场之差，应当匹配某个**值函数（value function）**的梯度场。
- **关键设计**：
  - 微调后的速度场 \( u_{\text{ft}} \) 与预训练速度场 \( u_{\text{pre}} \) 的差 \( u_{\text{ft}} - u_{\text{pre}} \) 被约束为值函数 \( V \) 的梯度 \( \nabla V \)；
  - 利用值函数的**启发式初始化**，使模型在微调初期就能获得较好的引导方向，从而实现快速适应；
  - 通过**梯度匹配（gradient matching）** 而非直接奖励最大化，隐式融入了奖励模型的一阶信息，并保留预训练分布的结构约束。
- **算法流程（文字说明）**：
  1. 给定预训练流匹配模型和一个奖励/偏好模型；
  2. 构造/初始化一个值函数 \( V \)；
  3. 训练微调速度场，使其与预训练速度场的差值逼近 \( \nabla V \)；
  4. 在较少的优化步数内完成对齐，同时通过值函数的约束保持先验分布。

## 3. 实验设计

- **主要场景**：文本到图像生成（text-to-image），使用了主流的流匹配模型 **Stable Diffusion 3**。
- **评估目标**：在有限计算预算下，检验对齐方法的**适应效率**、**生成质量**与**先验保持能力**。
- **对比方法**：由于提供的文本仅包含摘要，**具体对比的基线方法未列出**；论文提到“比现有方法更高效”，但未给出基线名称（如 DPO、RLHF 类方法等）。
- **Benchmark/数据集**：论文正文未在提供的片段中出现，具体使用的奖励数据集或评估基准无法从当前内容确认。

## 4. 资源与算力

- 论文摘要与元数据中**未说明 GPU 型号、数量、训练时长等具体算力信息**。
- 仅从“在有限计算预算下进行微调”这一表述可知，方法设计目标是低资源适应，但量化细节缺失。

## 5. 实验数量与充分性

- 当前提供的文本仅包含摘要和元数据，**无法统计实验组数、消融设置或对比轮次**。
- 从摘要判断，实验至少覆盖了 Stable Diffusion 3 上的文本到图像对齐任务，并进行了与现有方法的对比；但**实验的充分性、客观性和公平性无法基于现有信息评估**。
- 元数据中结果描述为“在多种对齐任务上适应更快、生成质量更高，且保持先验分布”，但任务种类和具体数值未给出。

## 6. 主要结论与发现

- **方法有效性**：VGG-Flow 能够在有限计算预算下，对 Stable Diffusion 3 进行有效的微调对齐。
- **效率与质量兼顾**：相比现有方法，VGG-Flow 实现更快适应，同时保持较高生成质量与先验分布特性。
- **理论价值**：基于最优控制的值函数梯度匹配框架，为流匹配模型对齐提供了一条新的、理论上合理的路线。

## 7. 优点

- **理论支撑**：从最优控制出发，不是经验调参，而是给出了“最优速度场差 = 值函数梯度”的清晰刻画。
- **利用一阶信息**：方法直接使用奖励模型的一阶信息（梯度），比仅使用标量奖励的方法信息利用率更高。
- **先验保持**：通过值函数约束，在提升奖励的同时避免破坏预训练分布，缓解了对齐中的“奖励 hacking”和模式坍缩风险。
- **计算友好**：强调在有限预算下快速适应，适合实际部署场景中的迭代微调。
- **实际验证**：在 Stable Diffusion 3 这一代表性流匹配模型上进行了实证验证，结论具有应用参考价值。

## 8. 不足与局限

- **信息不完整**：由于论文 PDF 被 OpenReview 的验证页面拦截，仅获取到摘要与元数据，**无法对实验细节、数据集、基线和消融进行严格评估**。
- **实验覆盖范围未知**：目前只看到文本到图像这一场景，**没有证据表明方法在视频、音频或离散生成任务上同样有效**。
- **泛化风险**：值函数的启发式初始化可能依赖任务或模型结构，跨领域泛化性尚待验证。
- **公平性风险**：现有方法的对比公平性（如超参数调优、训练步数对齐）无法从现有信息确认。
- **理论边界**：最优控制框架的假设（如连续时间、可微奖励、光滑速度场）在真实大规模模型中可能不完全成立，实际实现需近似处理。

---

（完）
