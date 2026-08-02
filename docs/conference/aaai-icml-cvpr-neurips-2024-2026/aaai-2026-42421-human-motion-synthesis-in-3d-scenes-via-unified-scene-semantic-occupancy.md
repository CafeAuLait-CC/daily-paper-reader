---
title: Human Motion Synthesis in 3D Scenes via Unified Scene Semantic Occupancy
title_zh: 通过统一场景语义占用进行三维场景中的人体运动合成
authors: "Jingyu Gong, Kunkun Tong, Zhuoran Chen, Chuanhan Yuan, Mingang Chen, Zhizhong Zhang, Xin Tan, Yuan Xie"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/42421/46382"
tags: ["query:dmg"]
score: 6.0
evidence: 三维场景中的人体运动合成，利用语义占用表示；不涉及扩散/流匹配
tldr: 三维场景中的人体运动合成依赖场景理解，现有方法忽视语义。本文提出SSOMotion，采用统一场景语义占用（SSO）表示，通过双向三平面分解压缩SSO，并使用CLIP编码和共享线性降维映射场景语义。该方法能获得细粒度语义结构并减少冗余计算，结合指令中的场景提示和运动方向进行运动控制，提升人体动作与场景的语义一致性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有三维场景人体运动合成只关注场景结构，忽略语义理解。
method: 引入统一场景语义占用表示，结合双向三平面分解与CLIP语义映射。
result: 在生成动作与场景语义一致性上取得提升，并降低计算冗余。
conclusion: 场景语义占用为三维场景中的人体运动合成提供了有效的表示方式。
---

## Abstract
Human motion synthesis in 3D scenes relies heavily on scene comprehension, while current methods focus mainly on scene structure but ignore the semantic understanding. In this paper, we propose a human motion synthesis framework that take an unified Scene Semantic Occupancy (SSO) for scene representation, termed SSOMotion. We design a bi-directional tri-plane decomposition to derive a compact version of the SSO, and scene semantics are mapped to an unified feature space via CLIP encoding and shared linear dimensionality reduction. Such strategy can derive the fine-grained scene semantic structures while significantly reduce redundant computations. We further take these scene hints and movement direction derived from instructions for motion control via frame-wise scene query. Extensive experiments and ablation studies conducted on cluttered scenes using ShapeNet furniture, as well as scanned scenes from PROX and Replica datasets, demonstrate its cutting-edge performance while validating its effectiveness and generalization ability.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：三维场景中的人体运动合成高度依赖场景理解能力。然而，现有方法大多仅关注场景的**结构信息**（如几何、距离与碰撞规避），**忽略了与人类行为高度相关的场景语义信息**。例如，同是坐着的动作，坐在沙发上和坐在地板上的语义含义不同，但结构特征可能相似。因此，语义信息在现有运动合成框架中未能被有效建模和利用。
- **研究动机**：作者观察到场景语义占用（Scene Semantic Occupancy, SSO）这一表示形式可以同时包含场景的**语义**和**结构**信息，符合人体运动合成对场景理解的综合需求；但直接在SSO上进行特征提取计算开销极大，且不同数据集的语义类别定义各不相同，难以实现跨数据集泛化。
- **整体意义**：通过提出一种轻量化、统一语义空间的场景表示方法（SSOMotion），在保留细粒度场景语义结构的同时大幅减少计算冗余，使语义信息第一次被显式、高效地引入到场景感知运动合成中。

### 2. 提出方法论：核心思想、关键技术细节、公式或算法流程

**核心思想**：以场景语义占用（SSO）作为统一场景表示，通过双向三平面分解压缩数据维度，利用CLIP文本编码器映射统一语义空间，并借助扩散模型和帧级场景查询实现指令感知的运动合成。

**关键技术细节**：

- **人体表示**：采用SMPL-X参数化人体模型。人体姿态由全局平移τ∈R³、全局朝向θg∈R³和21个身体关节旋转θp∈R⁶³组成，表示为P= {τ, θg, θ₁:₂₁}∈R⁶³。
- **场景语义占用（SSO）**：使用紧凑形式的场景占用表示S∈R^{N×8}，每个元素包含xyz坐标、rgba颜色和语义标签s。体素尺寸设为4cm。
- **双向三平面分解**：将局部语义占用Ol沿±xyz轴投影，得到Oyz、Ozy、Ozx、Oxz、Oxy、Oyx六个语义占用图（Oyx因天花板对行为影响较小而弃用）。每个语义占用图包含颜色、深度和语义标签三种通道。通过局部传感器变换公式Ig = R(θJz)Il + τJ，将人体周围的传感器转换到世界坐标中感知局部场景。
- **统一语义表示**：
  - 使用CLIP文本编码器将不同数据集的语义类别嵌入统一语义空间。
  - 由于CLIP特征维度高且语义在图中大量重复，通过**共享线性层降维**后再散播回语义图，大幅降低冗余计算。
  - 深度图使用高斯核激活：Oda = (1/(σ√2π))·e^{−(Od)²/(2σ²)}，聚焦近处物体。
  - 最终场景特征fscene = fsem ⊕ fgeo ⊕ ftex，融合语义、几何、纹理特征。
- **运动控制器**：
  - **动作意图线索**：对于移动任务，计算目标方向d = o − J₁,₀；对于交互任务，采样目标姿态并计算关节级方向。方向归一化公式：dn = min(||d||, 1) + ε / (||d|| + ε) · d。
  - **目标引导的人-场景相关性**：通过多头注意力机制建模：首先将运动特征转化为帧级查询，与方向提示键值做注意力（Eq. 8），得到目标引导的运动特征fgmot；再以fgmot为查询，与场景特征键值做注意力（Eq. 9），获得目标引导的人-场景相关性fgsmot，送入控制分支。
  - **零初始化线性层**将控制信号注入主分支。
- **训练策略**：
  - **基础扩散模型**：遵循MDM (Tevet et al. 2023)，在AMASS等标准动作捕捉数据集上训练，以动作标签和掩蔽关节为条件。
  - **控制分支**：在HUMANISE场景数据集上单独训练，联合优化基础扩散模型和控制分支参数。
  - 通过运动混合（motion blending）处理重叠帧，支持无限长的运动序列生成。

### 3. 实验设计：数据集、基准、对比方法

| 实验阶段 | 使用的数据集 | 任务/基准 | 对比方法 |
|---------|------------|----------|----------|
| 基础模型训练 | AMASS（含Babel动作标签、HumanML3D文本标注） | — | — |
| 控制分支训练 | HUMANISE（AMASS动作+ScanNet场景对齐） | — | — |
| 场景导航评估 | DIMOS构造的ShapeNet家具杂乱场景 | 目标距离、足部接触、穿透率、任务完成时间 | SAMP、GAMMA、DIMOS、OmniControl |
| 人-场景交互评估 | ShapeNet中10类家具场景 | 任务完成时间、平均穿透、最大穿透 | SAMP、DIMOS |
| 长期运动合成 | PROX、Replica场景 | 用户研究（自然度、多样性、合理性、目标达成度，4,080份评分、17名参与者） | 与同类竞争方法视觉对比 |

### 4. 资源与算力

- **论文未明确说明**所使用的GPU型号、数量、训练时长、批次规模等硬件资源信息。
- 仅给出了场景理解与运动-场景相关性的**单样本计算开销**消融数据（如表3所示），未涉及训练阶段的总算力消耗。

### 5. 实验数量与充分性

- **实验组数**：共包含四大类实验：
  1. 场景导航任务（表1）；
  2. 人-场景交互任务（表2，涵盖sit和lie两个动作）；
  3. 长期运动合成用户研究（4,080份评分、4个维度）；
  4. 计算成本消融实验（表3，4种配置）。
- **充分性评估**：
  - **优点**：覆盖了导航与交互两大类任务，跨合成场景（ShapeNet）和真实扫描场景（PROX、Replica）验证了泛化能力；用户研究样本量较大；消融实验验证了两项核心设计（双向三平面分解和维度降维）对计算效率的显著贡献。
  - **不足**：消融实验仅报告了计算成本（GFLOPs），**缺少对运动质量指标的完整消融对比**（如各组件去掉后对穿透率、目标距离的影响）；交互任务仅覆盖"坐"和"躺"两个动作，覆盖面有限；实验对比方法数量在交互任务上较少；未报告训练时间等资源开销。

### 6. 论文的主要结论与发现

- SSOMotion在场景导航任务中取得了**最低的目标距离误差（0.02m）**和**最好的穿透率（0.95）**，任务完成时间优于SAMP和DIMOS，但略慢于OmniControl。
- 在交互任务中，SSOMotion在"坐"和"躺"两个动作上都实现了**最快的任务完成时间**和**最低的平均/最大穿透**，显著优于SAMP，全面优于DIMOS。
- 长期运动合成的用户研究显示，SSOMotion在自然度、多样性、合理性、目标达成度**四个维度均取得最高评分**。
- 双向三平面分解与语义特征降维将单样本计算成本从20,783.78 GFLOPs降至0.49 GFLOPs，降幅超过4个数量级，验证了轻量化设计的高效性。
- 双向三平面分解和统一语义空间设计能够有效支持跨数据集泛化，无需针对不同数据集的语义类别重新标注。

### 7. 优点

- **语义驱动的场景理解**：首次将场景语义占用（SSO）以高效方式引入运动合成，有效建模了人类行为与场景语义的关联。
- **统一语义空间**：利用CLIP文本编码器嵌入语义类别，支持不同数据集间语义标签的无缝迁移，提升了跨数据集泛化能力。
- **计算效率高**：双向三平面分解利用了场景占用的固有稀疏性，语义共享线性降维消除了高维CLIP特征的冗余计算，实现了超4个数量级的计算缩减。
- **解耦训练策略**：基础扩散模型与控制分支分离训练，缓解了场景-动作数据集稀缺的问题。
- **长期运动合成能力**：支持通过历史运动约束和运动混合实现无限长度、多子任务连续的运动序列生成。

### 8. 不足与局限

- **足部接触指标欠佳**：在导航任务中足部接触分数（0.90）低于DIMOS（0.99），作者承认仅关注足部顶点接触状态而非内部关节，仍有改进空间。
- **消融实验不全面**：仅报告了计算成本的变化，未对各项设计（如语义特征、双向三平面、目标相关性模块）进行运动质量指标上的系统性消融验证。
- **交互任务覆盖面有限**：仅评估了sit和lie两类交互动作，对更多样的日常交互（如抓取、开门、倚靠等）缺乏验证。
- **真实动态场景未涉及**：论文局限部分明确表示当前方法面向静态场景，未来需要支持动态环境中的实时部署。
- **资源信息缺失**：未报告训练所涉及的GPU型号、数量、显存占用和训练时长，限制了结果的可复现性评估。
- **目标位置依赖外部模型**：指令中的目标位置/姿态依赖COINS等人群填充方法预先提供，未能实现从文本指令直接推理目标姿态的端到端方案。

（完）
