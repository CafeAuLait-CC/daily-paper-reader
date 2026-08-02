---
title: "MoMask: Generative Masked Modeling of 3D Human Motions"
title_zh: MoMask：三维人体动作的生成式掩码建模
authors: "Guo, Chuan, Mu, Yuxuan, Javed, Muhammad Gohar, Wang, Sen, Cheng, Li"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Guo_MoMask_Generative_Masked_Modeling_of_3D_Human_Motions_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 基于分层掩码建模的文本驱动三维人体动作生成
tldr: 现有文本驱动动作生成方法难以在保真度和可控性之间取得平衡。MoMask提出分层量化方案，将人体动作表示为多层离散动作标记，并用掩码Transformer在文本条件下预测掩码标记，从而生成高质量三维动作。实验证明其能生成高保真、多样化的动作序列，为文本到动作生成提供了新的掩码建模范式。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1721, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1808, \"height\": 756, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1814, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1813, \"height\": 1268, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1246, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1818, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 613, \"height\": 539, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1749, \"height\": 896, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-guo-momask-generative-masked-modeling-of-3d-human-motions-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 840, \"height\": 923, \"label\": \"Table\"}]"
motivation: 现有文本驱动三维动作生成方法在动作细节保真度和生成多样性上仍有不足。
method: 采用分层向量量化将动作编码为多层离散标记，并利用双向掩码Transformer在文本条件下迭代预测掩码标记。
result: 在文本到三维动作生成任务上取得了高保真且多样的生成效果。
conclusion: 展示了掩码建模在三维人体动作生成中的有效性，并提供了一套新的生成框架。
---

## Abstract
We introduce MoMask a novel masked modeling framework for text-driven 3D human motion generation. In MoMask a hierarchical quantization scheme is employed to represent human motion as multi-layer discrete motion tokens with high-fidelity details. Starting at the base layer with a sequence of motion tokens obtained by vector quantization the residual tokens of increasing orders are derived and stored at the subsequent layers of the hierarchy. This is consequently followed by two distinct bidirectional transformers. For the base-layer motion tokens a Masked Transformer is designated to predict randomly masked motion tokens conditioned on text input at training stage. During generation (i.e. inference) stage starting from an empty sequence our Masked Transformer iteratively fills up the missing tokens; Subsequently a Residual Transformer learns to progressively predict the next-layer tokens based on the results from current layer. Extensive experiments demonstrate that MoMask outperforms the state-of-art methods on the text-to-motion generation task with an FID of 0.045 (vs e.g. 0.141 of T2M-GPT) on the HumanML3D dataset and 0.228 (vs 0.514) on KIT-ML respectively. MoMask can also be seamlessly applied in related tasks without further model fine-tuning such as text-guided temporal inpainting.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

文本驱动的三维人体动作生成（text-to-motion generation）是计算机视觉与图形学中的重要任务，在游戏、元宇宙、VR/AR 等领域有广泛应用。现有方法主要分为两类：

- **自回归模型**（如 T2M-GPT）：先将动作通过向量量化（VQ）离散化为 token，再用单向 Transformer 逐位生成。其缺点包括：VQ 量化误差限制生成质量；单向解码只依赖前文上下文，误差会逐步累积。
- **离散扩散模型**（如 M2DM）：虽然能双向解码，但通常需要数百次迭代，推理效率低。

本文提出 **MoMask**，核心思想是将动作表示为 **多层离散 token**（基础层 + 残差层），并采用 **生成式掩码建模** 来高效、高质量地生成动作。该方法在生成质量、语义对齐和推理效率上均取得了显著提升。

## 2. 方法论

### 核心思想
MoMask 由三个关键组件构成：

1. **残差量化 VQ-VAE（Motion Residual VQ-VAE）**
   - 使用残差向量量化（RVQ）将动作序列编码为 V+1 层离散 token。
   - 基础层（第 0 层）为标准向量量化结果，后续层逐层量化前一层残差，从而逐步减少量化误差。
   - 量化和训练方式：使用直通梯度估计器、EMA 更新码本、codebook reset。
   - 引入 **量化 dropout**（Quantization Dropout）：训练时随机禁用最后若干量化层（概率 q），增强各层鲁棒性。

2. **掩码 Transformer（M-Transformer）**
   - 用于生成基础层 token。
   - 训练时：随机遮蔽部分 token，以文本为条件，预测被遮蔽 token（负对数似然损失）。
   - 遮蔽比例采用余弦调度函数 γ(τ) = cos(πτ/2)，τ 从 0 到 1 随机采样。
   - 采用 BERT 风格的替换策略：80% 替换为 [MASK]，10% 替换为随机 token，10% 保持不变。
   - 推理时：从全遮蔽序列开始，迭代填充 token，每次保留高置信度的预测，重新遮蔽低置信度 token，迭代 L 次（文中 L=10 即可）。

3. **残差 Transformer（R-Transformer）**
   - 用于预测后续残差层的 token（第 1 到 V 层）。
   - 输入为前序所有层 token 的嵌入之和、文本嵌入以及层编号 j。
   - 训练时随机选择一层 j，并行预测该层所有 token。

### 推理流程
- 第一步：M-Transformer 迭代生成基础层 token（约 10 次迭代）。
- 第二步：R-Transformer 逐层生成残差层 token（V−1 步）。
- 第三步：所有 token 经 RVQ-VAE 解码器映射回动作序列。
- 使用**无分类器引导（CFG）**：训练时以 10% 概率无条件训练，推理时按公式 ω_g = (1+s)·ω_c − s·ω_u 调整 logits。

### 关键技术细节
- 整体迭代次数仅约 15 次，与动作长度无关，远少于扩散模型。
- 残差层数 V 和量化 dropout 比例 q 是关键超参数，实验中 V=5（即 6 层量化）效果最佳。

## 3. 实验设计

### 数据集与基准
- **HumanML3D**：14,616 个动作，44,970 条文本描述，来自 AMASS 与 HumanAct12。
- **KIT-ML**：3,911 个动作，6,278 条文本描述，小规模基准。
- 采用 T2M 的 pose 表示，数据做镜像增强，划分为训练/测试/验证（0.8 / 0.15 / 0.05）。

### 评估指标
- **FID**：生成动作与真实动作的特征分布距离（衡量动作质量）。
- **R-Precision（Top-1/2/3）** 与 **多模态距离**：衡量文本与动作的语义对齐。
- **多模态性（Multimodality）**：同一文本生成动作的多样性（文中强调作为次要指标）。

### 对比方法
- VAE 类：T2M
- 扩散类：MDM、MLD、MotionDiffuse、ReMoDiffuse
- 自回归/离散类：TM2T、T2M-GPT、MotionGPT、M2DM
- 额外对比：MoMask（仅用基础层 token）作为自身消融。

### 主要结果
- HumanML3D：**FID 0.045**（T2M-GPT 为 0.141，ReMoDiffuse 为 0.103）；R-Precision Top-3 0.807；多模态距离 2.958。
- KIT-ML：**FID 0.204**（T2M-GPT 为 0.514，ReMoDiffuse 为 0.155；虽然 ReMoDiffuse 稍优，但其依赖检索增强）。
- 用户研究：MoMask 在 42 位 AMU 用户侧面对比中胜率高于 MDM、MLD、T2M-GPT，甚至 42% 情况下被认为与真值相当。

### 附加应用实验
- **时序动作修复（Temporal Inpainting）**：无需微调即可修复动作序列中间、开头或结尾的指定区间，与 MDM 对比用户偏好 68%。

## 4. 资源与算力

论文正文**未明确说明**具体的 GPU 型号、数量或训练时长。仅提及：

- 使用 PyTorch 实现。
- 推理效率测试在 **单张 Nvidia 2080Ti** 上进行（仅用于推理时间对比）。
- 训练时 mini-batch 大小：RVQ-VAE 为 512，Transformer 在 HumanML3D 上为 64、KIT-ML 上为 32。
- 未提供训练总耗时或 GPU 卡时数。

## 5. 实验数量与充分性

### 实验数量
- **主实验**：两个数据集（HumanML3D 和 KIT-ML）上与 8+ 种方法对比，每个实验重复 20 次并报告置信区间。
- **消融实验**：
  - RVQ 层数 V 从 0 到 7 的对比（表 2）。
  - Quantization Dropout 比例 q（0, 0.2, 0.4, 0.6, 0.8）的对比。
  - 去掉 RQ、去掉 QDropout、去掉 Remask 的对比。
  - 与单层 VQ 方法（TM2T、M2DM、T2M-GPT）的重构质量对比（FID 和 MPJPE）。
- **超参数分析**：CFG 引导尺度 s 和迭代次数 L 的扫描（图 7）。
- **用户研究**：两个（生成质量对比、inpainting 对比）。
- **可视化**：定性对比和时序修复示例。

### 充分性评价
- **优点**：消融覆盖了核心设计组件，超参数扫描验证了推理设置的合理性，用户研究增加了结论的可信度。两个数据集规模差异明显（一个大型、一个中小型），能反映泛化性。
- **不足**：
  - 未报告训练资源细节，复现成本不透明。
  - KIT-ML 上 FID 未超越 ReMoDiffuse（虽然论文归因于检索增强，但缺少公平配置下的对比）。
  - 多模态性指标略低于部分方法（如 MoMask 多模态性 1.241 vs. MLD 2.413），论文将其解释为次要指标，但未深入讨论多样性偏低的潜在原因。
  - 没有在更长/更复杂的动作序列或罕见动作上进行压力测试。

## 6. 主要结论与发现

1. MoMask 首次将生成式掩码建模引入文本驱动 3D 动作生成，并实现了 SOTA 性能。
2. 残差量化（RVQ）显著优于单一 VQ，能有效降低量化误差，提升动作重构质量。
3. 掩码 Transformer 用少量迭代（约 10 次）即可生成基础层 token，比自回归和扩散模型效率更高。
4. 残差 Transformer 能逐层补充细节，进一步提升生成动作的质量。
5. 量化 dropout 和“替换与重掩码”策略均能提升生成性能。
6. MoMask 可无缝支持文本引导的时序动作修复，无需额外微调。

## 7. 优点

- **创新性**：将掩码生成建模与残差量化结合，提出 M-Transformer + R-Transformer 双阶段生成架构，思路新颖。
- **性能卓越**：FID 指标大幅优于现有方法（HumanML3D 0.045，接近真值分布）。
- **效率高**：推理仅需约 15 次迭代，显著低于扩散模型的数百次迭代。
- **架构简洁**：无需复杂的检索增强或额外监督，即可获得优秀结果。
- **灵活性好**：生成与修复任务共用同一套框架，无需专门训练。
- **实验规范**：指标报告带 95% 置信区间，消融设计全面。

## 8. 不足与局限

- **KIT-ML 上 FID 非最佳**：ReMoDiffuse 仍领先（0.155 vs 0.204），论文解释为检索增强的差异，但未提供去检索条件下的公平对比。
- **多样性指标偏弱**：MoMask 的多模态性（1.241）低于多个基线（如 MLD 2.413、T2M 2.219），说明同一文本下的动作多样性不足。论文将其淡化，但没有给出原因或针对性改进。
- **训练细节缺失**：未报告 GPU 数量/型号、训练时间，不利于复现比较。
- **超参敏感**：CFG 尺度 s、迭代数 L、残差层数 V 等需要调优，不同数据集使用不同超参，可能限制实际应用的简易性。
- **动作长度与复杂度**：实验集中在短动作序列（约几秒），对长序列、全身复杂交互动作（如双人交互）未做验证。
- **评估指标局限性**：FID、R-Precision 等指标依赖特征提取器，可能无法完全反映动作的自然度和物理合理性；用户研究规模较小（42 人）。
- **应用范围**：目前仅支持文本条件，未扩展到其他条件（如音频、动作类别）或多模态控制。

（完）
