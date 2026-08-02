---
title: "ReAlign: Text-to-Motion Generation via Step-Aware Reward-Guided Alignment"
title_zh: ReAlign：基于步骤感知奖励引导对齐的文本到动作生成
authors: "Wanjiang Weng, Xiaofeng Tan, Junbo Wang, Guo-Sen Xie, Pan Zhou, Hongsong Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38035/41997"
tags: ["query:dmg"]
score: 9.0
evidence: 基于扩散模型的文本到3D人体动作生成，直接对应扩散模型在3D动作合成中的应用。
tldr: 针对扩散模型文本到动作生成中文本与动作分布不对齐导致动作语义不一致和质量低的问题，提出ReAlign方法，包含步骤感知奖励模型评估去噪采样过程中的对齐质量，并用奖励引导策略将扩散过程导向最优对齐分布。实验表明该方法能生成更真实且语义一致的3D人体动作，为文本驱动动作生成提供新思路。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 扩散模型在文本到3D人体动作生成中存在文本与动作分布不对齐，导致生成动作语义不一致或质量较低。
method: 提出步骤感知奖励模型与奖励引导采样策略ReAlign，在去噪采样中评估并对齐文本与动作分布。
result: 实验证明ReAlign能有效提高生成动作的语义一致性与质量，优于现有扩散式动作生成方法。
conclusion: 奖励引导对齐可显著缓解扩散模型在文本到动作生成中的错配问题，推动3D动作生成的应用。
---

## Abstract
Text-to-motion generation, which synthesizes 3D human motions from text inputs, holds immense potential for applications in gaming, film, and robotics. Recently, diffusion-based methods have been shown to generate more diversity and realistic motion. However, there exists a misalignment between text and motion distributions in diffusion models, which leads to semantically inconsistent or low-quality motions. To address this limitation, we propose Reward-guided sampling Alignment (ReAlign), comprising a step-aware reward model to assess alignment quality during the denoising sampling and a reward-guided strategy that directs the diffusion process toward an optimally aligned distribution. This reward model integrates step-aware tokens and combines a text-aligned module for semantic consistency and a motion-aligned module for realism, refining noisy motions at each timestep to balance probability density and alignment. Extensive experiments of both motion generation and retrieval tasks demonstrate that our approach significantly improves text-motion alignment and motion quality compared to existing state-of-the-art methods.

---

## 论文详细总结（自动生成）

## 一、论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：基于扩散模型的文本到3D人体动作生成（Text-to-Motion Generation）任务中，文本描述与生成动作之间存在显著分布不对齐问题，导致生成的动作语义不一致或质量低下。
- **问题根源**：现有扩散模型通常依赖在图文对上训练的CLIP文本编码器，而CLIP缺乏对动作时序动态的理解能力；同时，文本-动作对数据稀缺，难以训练通用的动作文本编码器。
- **现有方法的不足**：已有的偏好对齐方法（如ReinDiffuse、MotionRL、SoPo等）主要通过对生成模型进行微调来提升动作质量，但无法处理去噪过程中的带噪动作输入，且对齐问题应在去噪过程中解决，而非事后修正。
- **核心解决思路**：提出ReAlign（Reward-guided sampling Alignment），通过一个**步骤感知（step-aware）奖励模型**在去噪采样过程中实时评估文本-动作对齐质量，并通过奖励引导策略将扩散采样过程导向“最优对齐分布”，无需对扩散模型进行任何微调，即可即插即用地提升多种扩散式动作生成模型的性能。

## 二、论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 1. 核心思想
- 现有扩散模型学习到的采样分布 pₜ(x) 偏向高概率密度区域，而忽视语义对齐；ReAlign 的核心是通过引入一个“奖励分布” pᵣₜ(x|c)，与原始采样分布相乘，构建理想分布，从而在保证概率密度的同时实现文本-动作语义对齐。
- 理想分布定义为：
  - pᴵₜ(x|c) = pₜ(x|c) · pᵣₜ(x|c) / Z(c)
- 该公式使得反向扩散过程的梯度可分解为原始分布梯度与奖励分布梯度之和，从而直接引导采样轨迹。

### 2. 关键技术细节

#### （1）步骤感知奖励模型（Step-Aware Reward Model）
- 采用Transformer编码器-解码器架构（以SkipTransformer为基础）。
- 在动作表示中显式加入时间步令牌 [eₜ]，使模型能够适应不同噪声水平下的对齐模式。
- 训练时对动作在不同时间步施加噪声，通过对比损失 L_C 和表示损失 L_R 联合优化。
- 奖励评分通过动作嵌入 zₓ 与文本嵌入 z_c 的余弦相似度计算：
  - R_φ(x, c) = cos(zₓ, z_c)

#### （2）动作到动作奖励（Motion-to-Motion Reward）
- 针对文本描述固有的歧义性，从训练集中检索与文本最匹配的真实动作作为参照锚点，通过生成动作与检索动作的嵌入余弦相似度评估现实性：
  - x_c = argmax R_φ(x, c)，Rₘ(xₜ, c) = cos(zₓ, z_x_c)

#### （3）奖励分布与引导采样
- 双对齐奖励综合文本对齐与动作对齐：
  - R(xₜ, c) = μR_φ(xₜ, c) + ηRₘ(xₜ, c)
- 奖励分布定义为 pᵣₜ(xₜ|c) = exp(R(xₜ, c)) / Zᵣ(c)。
- 理论推导（定理1-3）：将奖励分布嵌入反向SDE后，可推导出DDPM框架下的离散去噪更新公式：
  - xₜ₋₁ = (1/√αₜ)(x̄ₜ₋₁ + √βₜε) + ∇R(xₜ, c)
- 算法流程：从标准高斯噪声出发，先检索参照动作，然后在每个去噪时间步中结合奖励梯度进行采样引导。

## 三、实验设计：数据集、基准与对比方法

### 1. 数据集
- **HumanML3D**：主流文本-3D动作生成基准数据集。
- **KIT-ML**：较小规模的动作-语言数据集。

### 2. 评估指标
- R-Precision（Top 1/2/3）：度量文本-动作语义匹配精度。
- FID（Fréchet Inception Distance）：度量生成动作分布与真实分布的差异。
- MM Dist（多模态距离）：度量文本条件与生成动作的匹配程度。
- Diversity：度量生成动作的多样性。

### 3. 对比方法
- 文本到动作生成任务对比：T2M、MDM、T2M-GPT、ReMoDiffuse、Mo.Diffuse、OMG、MotionLCM、Mo.Mamba、CoMo、ParCo、MARDM、MG-MotionLLM、EnergyMoGen、MLD、MLD++等。
- 文本-动作检索任务对比：TEMOS、T2M、TMR、LaMP等。
- 消融实验中还验证了ReAlign在不同基础模型（Mo.Diffuse、MDM、MLD、MotionLCM、MLD++）上的即插即用效果。

## 四、资源与算力

- 论文正文及附录中**未明确说明**使用的GPU型号、数量、训练时长或具体计算资源投入。
- 仅提及使用AdamW优化器（学习率1e-4，batch size 512）进行奖励模型训练，并使用Big Data Computing Center of Southeast University提供计算支持，但无具体硬件细节。

## 五、实验数量与充分性

### 实验数量
- **文本到动作生成实验**：在HumanML3D和KIT-ML两个数据集上进行了系统评估，涵盖十余种SOTA方法对比。
- **文本-动作双向检索实验**：在HumanML3D和KIT-ML上评估文本到动作与动作到文本检索，对比4种以上基线。
- **即插即用能力实验**：将ReAlign集成到5种不同的扩散模型（Mo.Diffuse、MDM、MLD、MotionLCM、MLD++）中。
- **消融实验**：
  - 对T2M奖励、M2M奖励和步骤感知训练三项进行组合消融（7组）。
  - 不同去噪步数（1~50步）下的性能对比。
  - 与CFG（classifier-free guidance）的兼容性消融。

### 充分性评估
- **优点**：实验维度较全面，覆盖生成质量、语义对齐、检索性能、模型泛化性和模块可插拔性，对比方法较新（截至2025年），结果报告了标准差，具有一定客观性。
- **不足之处**：未报告计算资源细节，实验仅局限于两个数据集，多样性指标在部分方法上有下降但解释较简略，缺少用户研究或更细粒度的定性分析。

## 六、论文的主要结论与发现

- ReAlign通过步骤感知奖励模型与奖励引导采样，在**不微调扩散模型**的前提下，显著提升了文本-动作对齐质量和生成动作的逼真度。
- 集成ReAlign后，MLD++在HumanML3D上达到新的SOTA：R@3达85.2%（+2.8%），FID降至0.055（+24.7%），MM Dist降至2.648（+5.8%）。
- 对MLD的提升尤为显著：R@1提升17.9%，FID改善58.8%。
- ReAlign在KIT-ML数据集上也使MDM达到SOTA，R@3提升7.3%，FID改善44.5%。
- 步骤感知（step-aware）训练策略对处理去噪过程中的带噪动作输入至关重要，能有效避免奖励黑客问题（reward hacking）。
- ReAlign与CFG兼容，且无需训练即可即插即用，具有较强的泛化性和实际应用价值。

## 七、优点

- **方法创新性**：首次将步骤感知奖励模型引入文本-动作扩散采样过程，显式建模噪声水平与对齐质量的关系，解决扩散模型文本-动作错配问题。
- **理论严谨性**：通过三条定理逐步推导了奖励引导反向SDE及其离散近似，理论基础扎实。
- **即插即用**：无需对扩散模型进行任何微调即可直接集成到多种现有方法中，适用性强，拓展成本低。
- **双奖励机制**：结合文本对齐（语义一致性）与动作对齐（现实性），互相补充，兼顾“说得对”和“做得像”。
- **实验全面**：覆盖生成、检索、消融、跨模型泛化、不同去噪步数等多个维度，较有说服力。
- **检索与生成的统一视角**：利用检索得到的真实动作为生成提供参考锚点，打通了生成与检索任务之间的壁垒。

## 八、不足与局限

- **资源信息缺失**：论文未说明具体GPU型号、训练时长和总体算力开销，不利于复现和资源评估。
- **数据集覆盖有限**：仅使用HumanML3D和KIT-ML两个数据集，均以英文文本为条件，未覆盖多语言、多样化动作风格或长序列场景。
- **多样性指标下降**：部分实验结果显示Diversity略有下降，作者解释为合理现象，但缺少更深入的分析或用户研究来验证生成动作的实际可接受度。
- **奖励模型依赖训练集检索**：M2M奖励需要从训练集中检索参照动作，当训练集本身多样性不足时可能限制生成动作的多样性。
- **超参数敏感性**：μ、η等奖励权重及噪声概率等超参数的选取缺乏敏感性分析，其鲁棒性有待进一步验证。
- **跨任务泛化未充分验证**：论文指出ReAlign可扩展至物理奖励、轨迹奖励等，但未实验验证。
- **定性分析有限**：定性结果主要依赖图1展示，缺少系统性的用户偏好评估。

（完）
