---
title: "Diff2Flow: Training Flow Matching Models via Diffusion Model Alignment"
title_zh: Diff2Flow：通过扩散模型对齐训练流匹配模型
authors: "Schusterbauer, Johannes, Gui, Ming, Fundel, Frank, Ommer, Björn"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Schusterbauer_Diff2Flow_Training_Flow_Matching_Models_via_Diffusion_Model_Alignment_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 架起扩散模型与流匹配之间的桥梁，实现高效流匹配微调
tldr: 针对流匹配基础模型微调计算代价高、而扩散模型生态成熟的问题，本文提出 Diff2Flow，通过时间步重标定、插值对齐和从扩散预测推导流匹配兼容的速度场，系统地在扩散模型与流匹配之间建立桥梁。该方法允许从预训练扩散模型直接高效地微调流匹配模型，从而结合两者的优势。实验表明该方法在生成质量和推理效率上均具有显著优势。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 520, \"height\": 303, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 657, \"height\": 206, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 599, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 589, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1372, \"height\": 324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 647, \"height\": 226, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1638, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1565, \"height\": 326, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 832, \"height\": 324, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 826, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 744, \"height\": 190, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 829, \"height\": 370, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1712, \"height\": 565, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-schusterbauer-diff2flow-training-flow-matching-models-via-diffusion-model-alignment-cvpr-2025-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 721, \"height\": 244, \"label\": \"Table\"}]"
motivation: 现成的流匹配基础模型微调成本高，且缺乏对成熟扩散模型知识的高效利用。
method: 通过重标定时间步、对齐插值并从扩散预测推导速度场，将预训练扩散模型知识迁移至流匹配模型。
result: 实现高效的流匹配微调，生成质量和推理效率表现优异。
conclusion: 为流匹配与扩散模型的融合提供了系统方案，降低了流匹配模型的应用门槛。
---

## Abstract
Diffusion models have revolutionized generative tasks through high-fidelity outputs, yet flow matching (FM) offers faster inference and empirical performance gains. However, current foundation FM models are computationally prohibitive for finetuning, while diffusion models like Stable Diffusion benefit from efficient architectures and ecosystem support. This work addresses the critical challenge of efficiently transferring knowledge from pre-trained diffusion models to flow matching. We propose Diff2Flow, a novel framework that systematically bridges diffusion and FM paradigms by rescaling timesteps, aligning interpolants, and deriving FM-compatible velocity fields from diffusion predictions. This alignment enables direct and efficient FM finetuning of diffusion priors with no extra computation overhead. Our experiments demonstrate that Diff2Flow outperforms naive FM and diffusion finetuning particularly under parameter-efficient constraints, while achieving superior or competitive performance across diverse downstream tasks compared to state-of-the-art methods.

---

## 论文详细总结（自动生成）

# Diff2Flow: 通过扩散模型对齐训练流匹配模型

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **问题定义**：如何将预训练扩散模型（如 Stable Diffusion）中海量的图像生成知识高效地迁移到流匹配（Flow Matching, FM）模型中，从而兼顾 FM 模型的快速推理能力与扩散模型的生态优势。

- **背景矛盾**：
  - 扩散模型（如 SD1.5/SD2.1）生成质量高、生态系统成熟，但推理速度慢，且存在 zero-terminal SNR 问题（无法生成纯黑/纯白图像）。
  - 流匹配模型（如 Flux、SDv3）推理速度更快、轨迹更直，但基础模型参数量巨大（>8B），微调成本高，难以在资源受限环境下使用。
  - 尽管扩散与流匹配可统一在一个广义框架下，但两者在插值定义、时间步缩放和训练目标上有本质差异，导致无法直接将预训练扩散模型作为 FM 训练的起点。

- **核心构想**：通过对齐两条轨迹——重标定时间步、对齐插值路径、从扩散预测推导兼容的速度场——将扩散模型"无缝转换"为流匹配模型，仅需极小的微调代价即可完成范式迁移。

## 2. 提出的方法论：核心思想与关键技术

### 核心思想
**Diff2Flow** 不是一个从零训练的生成模型框架，而是一种"系统桥接"策略，目标是在训练和采样过程中将扩散轨迹映射到流匹配轨迹，使预训练扩散模型能够在流匹配目标下进行高效微调。

### 关键技术细节

1. **轨迹变换（Traversing Between Trajectories）**
   - 扩散轨迹插值：`x_t^DM = α_t x_0 + σ_t x_T`（t ∈ [0, T]，离散）
   - 流匹配轨迹插值：`x_t^FM = t x_1 + (1-t) x_0`（t ∈ [0,1]，连续）
   - 构造两个可逆映射：
     - `f_t: [0,T] → [0,1]`，将扩散时间步映射到流匹配时间步
     - `f_x: 将扩散样本映射到流匹配样本`
   - 由于扩散的噪声调度系数（α_t, σ_t）只在离散点上有定义，论文提出在相邻离散点之间做**分段线性插值**，使时间步在连续域上可定义；并实验证明（如图2所示），在非整数时间步（如 t+0.5）上直接推理仍能生成高质量图像，验证了连续化时间步的可行性。

2. **时间步重新参数化**
   - 核心映射：`f_t(t_DM) = α_t / (α_t + σ_t)`
   - 该函数在方差保持（VP）和方差爆炸（VE）调度下均单调，因此可逆。
   - 反向映射 `f_t^{-1}` 通过查找最近邻离散时间步并线性插值实现。

3. **速度场推导（Objective Change）**
   - 关键创新：不强制扩散模型学习新的输出头，而是从扩散预测（如 v-prediction）直接**推导**流匹配速度场。
   - 推导出的速度公式为：
     `v_θ(x_FM, t_FM) = (α_t - σ_t)(x_t^DM - v_θ(x_t^DM, t_DM))`
   - 该方法适用于多种参数化（ε-参数化、v-参数化），论文以 v-参数化演示。

4. **训练与采样流程**
   - **训练**（Algorithm 1）：采样 t_FM → 用 f_t^{-1} 映射为 t_DM → 用 f_x^{-1} 将 x_t^FM 映射为 x_t^DM → 计算速度预测 → 在 FM 损失 (Eq. 5) 上做梯度下降。
   - **采样**（Algorithm 2）：标准 Euler 积分，每一步先重新参数化时间步和样本，再获取速度预测，沿 ODE 推进。

5. **与 PEFT（LoRA）结合**
   - 论文发现：若不做目标对齐，直接在扩散模型上套用 FM 损失，LoRA 效果很差（模型需要"忘记"旧参数化并学习全新范式）。
   - Diff2Flow 消除了一部分参数化转换负担，使 LoRA 只需关注任务本身，效果显著提升。

## 3. 实验设计：数据集、基准与对比方法

### 实验场景 1：文本到图像生成（分辨率变换 + 继续训练）
- **任务设置**：使用 SD2.1（预训练分辨率 768×768）微调至 512×512；或对 SD1.5 在相同分辨率下继续训练并评估性能。
- **数据集**：LAION-Aesthetics 微调集，COCO 2017 作为评估基准。
- **对比方法**：扩散模型继续训练（DM finetuning）、朴素流匹配微调（FM finetuning）、Diff2Flow（有/无 LoRA），以及 SD1.5、Rectified Flow 等基线。
- **关键指标**：FID、CLIP score、Aesthetics score。

### 实验场景 2：轨迹矫直（Reflow / 快速推理）
- **任务设置**：对 SD1.5 施加 Diff2Flow-Reflow（1-rectified flow），在仅为 62M 参数的 LoRA 约束下评估不同步数（2/4/25）的推理性能。
- **对比方法**：SDv1.5 + DPM-Solver、Rectified Flow、PeRFlow。
- **关键指标**：FID、CLIP score。

### 实验场景 3：单目深度估计（域适应下游任务）
- **任务设置**：在合成数据上微调扩散先验，实现零样本仿射不变单目深度估计。
- **数据集**：Hypersim（训练），NYUv2、KITTI、ETH3D、ScanNet、DIODE（零样本评估）。
- **对比方法**：
  - 判别式：Depth Anything v1/v2、Metric3D v1/v2
  - 生成式：Marigold、GeoWizard、DepthFM、E2E-FT、Lotus-G
- **关键指标**：AbsRel ↓、δ1 ↑，NFE=10，集成数=4。

### 消融实验
- 不同训练参数量（全量微调、LoRA-base 222M、LoRA-small 62M）对深度估计性能的影响（Table 4）。

## 4. 资源与算力

- **论文正文未明确披露**使用的 GPU 型号、数量、训练时长等具体算力信息。
- 从实验推测：
  - 使用了 Stable Diffusion v1.5/v2.1 作为基座（约 0.9B–0.86B 参数）。
  - LoRA 变体仅训练约 62M–222M 参数（约总参数量 7%）。
  - 论文提到"收敛仅需约 2.5k 次迭代"（文本到图像任务中），但未说明对应的 wall-clock 时间。
  - 在致谢部分提及使用了 JUWELS 超算中心及 NHR@FAU 的 HPC 资源，但未量化。

## 5. 实验数量与充分性

### 实验数量
- 3 大主要实验场景（文本到图像、轨迹矫直、深度估计）。
- 深度估计覆盖 5 个零样本基准数据集，对比 11 种 SOTA 方法。
- 含多个消融实验：
  - 全量微调 vs LoRA（不同参数量）
  - 有/无 classifier-free guidance
  - 不同 NFE（2/4/25）
  - 不同训练迭代次数收敛曲线对比

### 充分性与客观性评价
- **充分之处**：
  - 多任务验证（生成任务 + 密集预测任务），覆盖面广。
  - 与多种 SOTA 方法对比，包含判别式和生成式两类。
  - 消融实验清晰地展示了目标对齐在不同容量约束下的增益。
  - 开放了代码，有助于复现和验证。
- **不足之处**：
  - 深度估计评估仅使用合成训练数据 + 零样本评估，未展示在真实世界数据上微调后的效果。
  - 未与同期的其他蒸馏/转换方法（如 Progressive Distillation、Consistency Models 等）进行系统比较。
  - 缺乏严格的统计显著性检验（多次运行均值/方差）。
  - 论文中未报告训练阶段的计算成本（FLOPs / 训练时长），难以评估"效率提升"的实际规模。
  - 部分定性结果（Fig. 3/4/6/7）依赖主观视觉判断，缺乏用户研究支持。

## 6. 主要结论与发现

1. **目标对齐是范式迁移的关键**：直接对扩散模型套用 FM 损失会严重拖慢收敛并降低性能；而 Diff2Flow 通过时间步重标定 + 插值对齐 + 速度推导，实现了快速收敛且性能更优。
2. **在 PEFT 约束下优势更明显**：使用 LoRA 时，朴素 FM 微调几乎失效，而 Diff2Flow 仍能维持高性能，说明对齐策略大幅降低了参数化转换的负担。
3. **解决 zero-terminal SNR 问题**：转换到 FM 后，模型能够生成纯黑/纯白图像（物理上合理的末端状态），克服了扩散模型常见的灰偏色问题。
4. **加速推理**：通过 Diff2Flow-Reflow 矫直轨迹，仅用 2 步采样即可获得可用的生成结果（无需一致性蒸馏）。
5. **超越扩散微调**：即使在同一生成任务上（SD1.5 + LAION-Aesthetics），Diff2Flow 的 FID/CLIP/Aesthetics 均优于扩散继续训练，验证了 FM 轨迹的固有优势。

## 7. 优点

- **系统性解决了扩散→流匹配的迁移问题**，首次清晰给出了完整的时间步 + 插值 + 目标的对齐方案，而非经验式 hack。
- **适用范围广**：可用于文本到图像、分辨率适配、轨迹矫直（Reflow）、域适应（深度估计）等多种场景，通用性强。
- **参数量效率高**：与 PEFT 结合良好，可在仅训练约 7% 参数的情况下达到与全量微调/更大型方法相当或更优的性能。
- **训练开销小**：文本到图像任务中约 2.5k 迭代即可收敛，在深度估计任务中训练收敛速度显著优于 Diffusion 微调和朴素 FM 微调。
- **推导清晰**：从扩散系数出发构造单调可逆映射，理论严谨，且实验验证了连续时间步插值的可行性（图2中非整数时间步推理）。
- **对社区友好**：代码开源，方法易于复现和扩展到其他基座模型。

## 8. 不足与局限

- **算力信息缺失**：未披露 GPU 型号、数量、训练时长、内存占用等关键计算资源数据，降低了"高效"主张的可验证性。
- **未验证大规模及跨模态泛化**：实验仅基于 SD1.5/SD2.1（~0.9B），未在 SDXL、Flux、SDv3 等更大规模模型上验证；也未涉及视频、音频等其他模态。
- **深度估计评估范围有限**：零样本评估虽全面，但未报告在训练集分布上微调后的性能；与 Marigold 等扩散方法相比，Diff2Flow 在部分指标（如 NYUv2 AbsRel）上并未完全超越。
- **速度场推导依赖预训练模型的参数化假设**：当扩散模型采用特殊或混合参数化（如 SDv3 的 EDM-style）时，公式需要重新推导，方法的直接通用性有待验证。
- **缺乏与其他蒸馏方法的系统对比**：如 Progressive Distillation、Consistency Distillation、Adversarial Distillation 等，无法准确判断 Diff2Flow 在"速度-质量"权衡中的相对位置。
- **理论分析有限**：对轨迹对齐后的 ODE 曲率、累积误差、逼近误差等缺少形式化分析；连续化时间步的可解释性（为什么非整数 t 有效）依赖经验验证，缺乏严格证明。

---

（完）
