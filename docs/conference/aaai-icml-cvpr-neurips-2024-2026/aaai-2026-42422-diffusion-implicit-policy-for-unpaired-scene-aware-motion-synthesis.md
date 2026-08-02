---
title: Diffusion Implicit Policy for Unpaired Scene-aware Motion Synthesis
title_zh: 扩散隐式策略用于未配对场景感知运动合成
authors: "Jingyu Gong, Chong Zhang, Fengqi Liu, Ke Fan, Qianyu Zhou, Xin Tan, Zhizhong Zhang, Yuan Xie"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/42422/46383"
tags: ["query:dmg"]
score: 9.0
evidence: 基于扩散的场景感知运动合成，引入隐式策略，无需成对运动-场景数据
tldr: 场景感知运动合成通常依赖配对运动-场景数据，难以泛化到多样场景。本文提出扩散隐式策略（DIP），在训练时将人体-场景交互与运动合成解耦，推理时在扩散去噪中引入基于交互的隐式策略优化。通过在迭代去噪和策略优化间交替，生成的运动在自然性和交互合理性上均有提升，并无需配对数据。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有场景感知运动合成依赖配对数据，难以泛化到多样场景。
method: 将人体-场景交互与运动合成解耦，并在扩散采样中引入隐式策略优化。
result: 在无需配对数据的条件下提升了运动自然性与交互合理性。
conclusion: 扩散隐式策略为未配对场景感知运动合成提供了统一框架。
---

## Abstract
Scene-aware motion synthesis has been widely researched recently due to its numerous applications. Prevailing methods rely heavily on paired motion-scene data, while it is difficult to generalize to diverse scenes when trained only on a few specific ones. Thus, we propose a unified framework, termed Diffusion Implicit Policy (DIP), for scene-aware motion synthesis, where paired motion-scene data are no longer necessary. In this paper, we disentangle human-scene interaction from motion synthesis during training, and then introduce an interaction-based implicit policy into motion diffusion during inference. Synthesized motion can be derived through iterative diffusion denoising and implicit policy optimization, thus motion naturalness and interaction plausibility can be maintained simultaneously. For long-term motion synthesis, we introduce motion blending in joint rotation power space. The proposed method is evaluated on synthesized scenes with ShapeNet furniture, and real scenes from PROX and Replica. Results show that our framework presents better motion naturalness and interaction plausibility than cutting-edge methods. This also indicates the feasibility of utilizing the DIP for motion synthesis in more general tasks and versatile scenes.

---

## 论文详细总结（自动生成）

### 论文总结：扩散隐式策略用于未配对场景感知运动合成

#### 1. 核心问题与整体含义（研究动机和背景）
- **问题背景**：场景感知运动合成（scene-aware motion synthesis）在场景模拟、数字人动画、虚拟/增强现实中有广泛应用。现有主流方法严重依赖**配对的人类运动-三维场景数据**进行训练，例如 SAMP、GAMMA、DIMOS 等，这类数据获取成本高、规模有限。
- **核心矛盾**：人类运动数据（如 AMASS）远比配对运动-场景数据丰富，但以往方法无法直接利用非配对数据，导致合成运动的多样性不足，且训练场景与测试场景差异大时泛化能力差。
- **论文立意**：提出**扩散隐式策略（Diffusion Implicit Policy, DIP）**，在训练时将“人体-场景交互”与“运动合成”解耦，推理时通过迭代的扩散去噪和隐式策略优化同时保证运动自然性和交互合理性，从而**无需任何配对运动-场景数据**即可完成场景感知运动合成。

#### 2. 方法论：核心思想、关键技术细节与流程
- **整体框架**：DIP 将场景感知运动合成转化为一个联合优化问题：
  - 扩散去噪过程提供“运动自然性”先验（每个去噪步骤视为对自然性的梯度优化）；
  - 基于交互的奖励函数作为“隐式策略”，引导采样分布趋向高交互合理性；
  - 随机采样项则用于探索多样化的运动。
- **运动表示与条件扩散模型**：
  - 使用 SMPL-X 表示每帧姿态：全局方向、21 个关节旋转、平移，共 69 维参数；运动序列为 `S×69`。
  - 扩散模型（类似 MDM）直接预测原始运动 `x_0`，条件为动作标签 `a`；额外引入 **ControlNet 分支**提供关键帧关节位置提示（如骨盆轨迹、指定关节位置），使模型可按需控制历史/目标姿态。
- **隐式策略的奖励函数**：设计了一组可微奖励函数，涵盖：
  - 运动连续性：历史一致性奖励 `R_his`、平滑性（加速度）奖励 `R_acc`；
  - 目标达成：目标接近奖励 `R_goal`；
  - 交互合理性：接触奖励 `R_cont`、非穿透奖励 `R_pene`、防滑步奖励 `R_skt`；
  - 总奖励 `R_ip` 为各项加权和。
- **扩散隐式策略的核心技巧**：
  - 在去噪过程中，不直接修改当前隐变量 `μ_t`，而是通过**GAN Inversion** 的方式，对扩散模型预测的 `\hat{x}_0^φ(μ_t, t-1, c)` 求奖励梯度，进而更新 `μ_t`：`\tilde{μ}_t = μ_t + \tilde{β}_t · ∇R_ip(...)`。
  - 这样既能保持运动连续性，又能搜索到交互奖励更高的采样分布。
- **长时运动合成**：
  - 针对多任务（如“先坐在床上→走到角落→坐到椅子上”），利用历史帧的关节位置做条件，并用 **inpainting** 保持关键帧姿态；
  - 提出**旋转矩阵幂空间混合**：平移直接线性插值，旋转通过插值旋转矩阵的幂实现平滑过渡，避免欧拉角/轴角线性插值的失真。

#### 3. 实验设计：数据集、基准与对比方法
- **训练数据**：
  - 运动数据：AMASS（动作捕捉数据）；
  - 动作标签：Babel、HumanML3D 提供的动作标注和起止帧。
- **测试场景**：
  - 合成场景：ShapeNet 家具随机摆放场景，用于原子任务（移动、坐、躺）；
  - 真实扫描场景：PROX 和 Replica 数据集，用于长时多任务运动合成。
- **评估任务与指标**：
  - **场景导航（locomotion）**：完成时间、最终距离、脚接触得分、穿透率；
  - **场景物体交互（interaction）**：时间复杂度、平均穿透、最大穿透；
  - **长时运动合成**：用户研究（15 名参与者，1~5 分制，从自然性、多样性、交互合理性、总体表现评分）。
- **对比方法**：SAMP、GAMMA、DIMOS（导航与交互）；DIMOS、OmniControl（长时运动用户研究）。
- **主要结果**：
  - 导航任务：DIP 完成时间最短、距离目标最近、穿透率最低；脚接触得分略低于 DIMOS（论文解释因接触计算基于脚关节而非脚顶点）。
  - 交互任务：坐/躺任务的平均穿透和最大穿透均优于 SAMP 和 DIMOS。
  - 用户研究：DIP 在多样性、交互合理性、总体表现上取得最高分；自然性与 DIMOS 相当。

#### 4. 资源与算力
- 论文文本中**未明确说明**使用的 GPU 型号、数量、训练时长或推理时间等算力信息，因此无法从公开文本中获得相关细节，这在一定程度上影响可复现性评估。

#### 5. 实验数量与充分性
- **实验组数**：
  - 三大类任务（导航、交互、长时运动），每类有定量指标或用户研究；
  - 用户研究包括 15 名参与者、每组方法 1200 条评分，覆盖 PROX 和 Replica 两类真实场景。
- **充分性评价**：
  - 优点：在多种场景（合成+真实）上验证了泛化性；定量与感知评价结合；对比方法覆盖了传统优化和扩散类方法。
  - 不足：**缺少消融实验**（如各奖励项贡献、GAN Inversion 策略与直接优化对照、运动混合方式对比等）；对比方法数量有限（交互任务只有 SAMP/DIMOS；长时任务只有 DIMOS/OmniControl）；长时运动合成只采用主观用户研究，缺乏客观指标（如穿透率、接触率统计）；未与最新强基线（如 SceneDiffuser、LAMA 等）全面比较。

#### 6. 主要结论与发现
- DIP 在**完全不需要配对运动-场景数据**的情况下，能够生成自然且交互合理的场景感知运动，在 ShapeNet 合成场景和 PROX/Replica 真实场景中均表现良好。
- 将“扩散去噪”与“隐式策略优化”结合，可在一次生成过程中同时优化运动自然性和交互合理性，避免了以往两阶段方法中“重交互、轻自然性”的缺陷。
- 旋转矩阵幂空间运动混合有效支持长时多任务无缝衔接，可作为多任务运动合成的一种实用方案。
- 该工作表明利用大规模纯运动数据和场景语义进行解耦训练，是突破配对数据瓶颈的可行路径。

#### 7. 优点
- **思路新颖**：将交互从运动训练中解耦，开创了“未配对数据 + 扩散隐式策略”的场景感知运动合成范式。
- **技术细节扎实**：GAN Inversion 方式调整采样分布中心，既保证交互优化又不破坏运动连续性；控制扩散模型配合关键帧提示，使运动可控性强。
- **长时合成方案设计巧妙**：旋转矩阵幂空间插值比传统线性插值更符合人体运动学特性。
- **验证范围较广**：在合成家具场景和真实室内场景中均开展实验，且使用同一个模型，无需针对场景重新训练，体现强泛化能力。

#### 8. 不足与局限
- **算力信息缺失**：未报告训练/推理资源，不利于复现和社区比较。
- **消融缺失**：没有量化各奖励权重、ControlNet 提示密度、混合策略等关键设计的影响，说服力有所折扣。
- **交互细节尚不完美**：脚接触得分低于 DIMOS，说明脚部接触建模（尤其是接触几何精度）仍需改进。
- **长时任务客观指标不足**：用户研究虽然提供主观评价，但缺少客观的穿透、接触、运动速度等统计，可能引入主观偏差。
- **依赖外部模块**：目标位置依赖 COINS 预训练模型，任务分解依赖 LLM，这些前置模块的误差会传播到最终结果。
- **对比不够全面**：对手方法偏旧，未与更多近期工作（如 SceneDiffuser、LAMA、AMDM）在相同条件下比较，公平性可能受限。

（完）
