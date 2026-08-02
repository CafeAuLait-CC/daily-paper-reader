---
title: Deterministic-to-Stochastic Diverse Latent Feature Mapping for Human Motion Synthesis
title_zh: 确定性到随机性的多样化潜在特征映射用于人体运动合成
authors: "Hua, Yu, Liu, Weiming, Xu, Gui, Hou, Yaqing, Ong, Yew-Soon, Zhang, Qiang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Hua_Deterministic-to-Stochastic_Diverse_Latent_Feature_Mapping_for_Human_Motion_Synthesis_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 8.0
evidence: 通过潜在特征映射使用基于分数的生成模型进行多样化人体运动合成
tldr: 基于分数的生成模型在人体运动合成上表现优异，但训练过程涉及复杂曲率轨迹导致不稳定。本文提出确定性到随机性的多样化潜在特征映射（DSDFM）方法，包含两个阶段：第一阶段学习人体运动的潜在空间分布，第二阶段建立高斯分布到潜在空间分布之间的映射以生成多样化运动。该方法缓解了训练不稳定性，并提升了合成结果的多样性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1415, \"height\": 416, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1597, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1611, \"height\": 507, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1211, \"height\": 462, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 260, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 867, \"height\": 271, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 150, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 863, \"height\": 141, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-hua-deterministic-to-stochastic-diverse-latent-feature-mapping-for-human-motion-synthesis-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 200, \"label\": \"Table\"}]"
motivation: 分数生成模型训练不稳定，影响人体运动合成的多样性和质量。
method: 设计两阶段DSDFM，先重建运动潜在特征，再连接高斯分布与潜在分布以生成多样化运动。
result: 在不稳定训练条件下生成了合理且多样的人体运动序列。
conclusion: 为基于分数生成模型的人体运动合成提供了更稳定的特征映射方案。
---

## Abstract
Human motion synthesis aims to generate plausible human motion sequences, which has raised widespread attention in computer animation. Recent score-based generative models (SGMs) have demonstrated impressive results on this task. However, their training process involves complex curvature trajectories, leading to unstable training process.In this paper, we propose a Deterministic-to-Stochastic Diverse Latent Feature Mapping (DSDFM) method for human motion synthesis.DSDFM consists of two stages. The first human motion reconstruction stage aims to learn the latent space distribution of human motions. The second diverse motion generation stage aims to build connections between the Gaussian distribution and the latent space distribution of human motions, thereby enhancing the diversity and accuracy of the generated human motions. This stage is achieved by the designed deterministic feature mapping procedure with DerODE and stochastic diverse output generation procedure with DivSDE. DSDFM is easy to train compared to previous SGMs-based methods and can enhance diversity without introducing additional training parameters.Through qualitative and quantitative experiments, DSDFM achieves state-of-the-art results surpassing the latest methods, validating its superiority in human motion synthesis.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究任务**：本文聚焦于人体运动合成（Human Motion Synthesis），旨在生成高质量、多样化且真实的 3D 人体运动序列，涵盖**无条件生成**（从随机噪声直接生成运动）和**条件生成**（以动作标签为条件，即 Action-to-Motion）两类任务。
- **现有方法的问题**：
  - **VAE**：需要近似变分推断或蒙特卡洛推断，对复杂模型难以处理。
  - **GAN**：存在数值不稳定和模式崩溃（mode collapse）问题。
  - **基于分数的生成模型（SGMs）/扩散模型（如 DDPM、SDE）**：虽然生成保真度高，但其前向和反向过程被设计为呈现曲率轨迹（curvature trajectories），导致**训练过程不稳定、采样速度慢**；虽然 DDIM 等加速方法可缩短采样过程，但通常带来明显性能下降。
  - **Flow Matching**：相比扩散模型训练更稳定，但源分布与目标分布之间的轨迹仍相对弯曲，且难以生成高度多样化的样本。
- **核心意义**：提出一种训练稳定、采样高效且能兼顾多样性（diversity）和准确性（accuracy）的人体运动生成方法，以替代或改进上述生成范式。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 2.1 总体框架：DSDFM 两阶段结构

DSDFM（Deterministic-to-Stochastic Diverse Latent Feature Mapping）由两个阶段组成：

1. **人体运动重建阶段**（Human Motion Reconstruction）：使用 **VQVAE** 学习人体运动的潜在空间表示与分布。编码器由 Transformer 和 GRU 构成，解码器将量化后的潜在特征重建为运动序列，优化码本与重建损失。
2. **多样化运动生成阶段**（Diverse Motion Generation）：
   - **确定性特征映射过程**：通过所设计的 **DerODE**（Deterministic Ordinary Differential Equation）建立高斯分布 $p(Z_{t=1})$ 与人体运动潜在空间分布 $p(Z_{t=0})$ 之间的连接。
   - **随机多样化输出生成过程**：通过所设计的 **DivSDE**（Diverse Stochastic Differential Equations）增强生成运动的多样性。

### 2.2 关键技术细节

- **DerODE（确定性特征映射）**：
  - 基于最优传输（Optimal Transport, OT）规划 $\pi$，最小化两分布之间的位移代价（式 5），得到匹配的数据样本对 $(z_0, z_1)$。
  - 定义动态过程 $p(z_t,t) = \mathcal{N}(t z_1 + (1-t) z_0, 0)$（式 6），由 Proposition 1 推导出漂移函数 $u(z_t,t) = z_1 - z_0$（式 7）。
  - 训练目标包含：
    - **漂移估计损失** $J_{drift}$（式 8）：预测网络 $v_\theta(z_t,t)$ 逼近 $z_1 - z_0$。
    - **漂移一致性损失** $J_{CL}$（式 9）：使不同时间插值点的网络输出一致，提升生成结果的连贯性。
    - 总损失 $J_{DerODE} = J_{drift} + \lambda_{cl} J_{CL}$（式 10）。
  - 训练完成后，直接从高斯噪声采样：$\hat{z}_{0,i} = \hat{z}_{1,i} - v_\theta(\hat{z}_{1,i}, t=1)$（式 11），再由解码器生成运动。

- **DivSDE（随机多样化输出生成）**：
  - 为克服 DerODE 的确定性导致多样性不足的问题，引入随机微分方程：$dz_t = -\frac{1}{1-t}z_t dt + \eta\sqrt{\frac{2t}{1-t}}dw_t$（Proposition 3）。
  - 该 SDE 的均值满足 $p(z_t) = \mathcal{N}((1-t)z_i, \eta^2 t^2 I)$，其中扩散项 $\eta\sqrt{\frac{2t}{1-t}}dw_t$ 在采样过程中注入噪声，增强多样性；参数 $\eta$ 控制多样性强度。
  - 关键优点：**无需引入额外训练过程或网络**，可直接利用 DerODE 得到的 $\hat{z}_{0,i}$ 作为参考，通过式（13）的离散反向过程完成多样化采样。相较于传统 score-based 方法需单独训练 score 网络，本方法避免了额外训练开销。

### 2.3 算法流程

Algorithm 1 描述了完整的生成过程：从高斯分布初始化 $\hat{z}_1$ → 使用 DerODE 获取 $\hat{z}_0$ → 在时间步上迭代执行 DivSDE 反向过程（计算 score 项、漂移项、扩散项和噪声项）→ 最终通过解码器 Dec 生成人体运动序列 $\hat{E}$。

## 3. 实验设计

### 3.1 数据集

- **HumanAct12**：包含 1,191 条原始运动序列，12 类动作标注（每序列有动作类别标签）。
- **HumanML3D**：较新的数据集，包含 14,616 条运动序列，由 AMASS 得到，并配有 44,970 条文本描述。

### 3.2 评估指标

- **准确性指标**：FID（越低越好）、KID（越低越好）、Precision、Recall、Accuracy（越高越好）。
- **多样性指标**：Diversity、Multimodality（越高越好）。

### 3.3 对比方法

- **无条件生成对比**：VPoser、Action2Motion、ACTOR、MDM、MLD、Modi。
- **条件生成（Action-to-Motion）对比**：Action2Motion、ACTOR、INR、MLD、MDM、MotionDiffuse。
- **消融实验基线**：VPSDE、VESDE、DDPM++、NCSN++（用于对比训练/推理效率与多样性增强效果）。

### 3.4 实现细节

- VQVAE：4 层 Transformer，8 头注意力，码本大小 512×512。
- 批大小 128，初始学习率 $10^{-2}$，每 10 轮 decay 0.98，训练 500 epochs。
- 时间间隔 $\Delta t = 0.01$，多样性强度 $\eta = 0.1$，扩散步数 100 步，平衡参数 $\lambda_{cl} = 0.3$。

## 4. 资源与算力

- 论文**未明确说明使用的 GPU 型号、数量**等具体硬件配置。
- 但提供了训练和推理时间的量化数据：
  - **HumanAct12 数据集**（500 epochs）：DSDFM 训练时间 25.33 分钟，而 VPSDE 为 42.93 分钟、VESDE 为 40.57 分钟；推理时间（100 步）0.1s/FID 13.61。
  - **HumanML3D 数据集**（500 epochs）：DSDFM 训练时间 7.02 分钟，而 VPSDE 为 12.54 分钟、VESDE 为 12.57 分钟；推理时间（100 步）1.01s/FID 0.073。
  - 模型参数量：DSDFM 仅 15M，显著低于对比方法（如 MLD 27M、MDM 24M、Modi 23M 等）。
- 推理时间测试在 **NVIDIA A100** 上进行。

## 5. 实验数量与充分性

### 5.1 实验组数

论文共包含以下主要实验：

1. **无条件运动合成**（HumanAct12）：对比 6 种 SOTA 方法（表 1）。
2. **条件生成 Action-to-Motion**（HumanAct12）：对比 6 种 SOTA 方法（表 2）。
3. **训练/推理时间消融**（HumanAct12 和 HumanML3D）：与 VPSDE、VESDE 对比不同扩散步数（100/500/1000）下的推理时间和 FID（表 3、表 4）。
4. **多样性增强消融**（HumanAct12）：与 VPSDE、VESDE、DDPM++、NCSN++ 在 FID、KID、Precision、Recall、Diversity 及参数量上对比（表 5）。
5. **定性与可视化**：无条件生成和条件生成的可视化结果（图 3），以及推理时间对比可视化（图 4）。

### 5.2 充分性与公平性评估

- **充分**：实验覆盖两个数据集、两个任务（无条件/条件）、多个指标、多种对比方法，并包含消融实验，整体较为系统。
- **相对公平**：对比方法均使用相同输入长度设置，评估指标规范（95% 置信区间、→ 表示更接近真实数据更好）。
- **存在局限**：
  - 表 2 中 Diversity 指标上 DSDFM 比 MotionDiffuse 略低 0.01%，作者解释为以 0.01% 的多样性代价换取更低的置信区间（稳定性提升），但该解释存在一定辩解成分。
  - 消融对比未涉及 GAN、VAE、Flow Matching 等非 SGM 方法，对比范围仍有拓展空间。
  - 训练/推理时间的对比仅与 VPSDE/VESDE 两种 SDE 变体进行，未与最新的 Flow Matching 类方法（如 Rectified Flow）或蒸馏加速方法比较。

## 6. 论文的主要结论与发现

- DSDFM 在**无条件人体运动合成**任务上全面超越现有 SOTA 方法（FID 12.86、KID 0.10、Precision 0.75、Recall 0.85、Diversity 18.41），且参数量最少（15M）。
- 在**条件生成（Action-to-Motion）** 任务上取得与最佳方法相当的性能，同时显著降低参数量和置信区间，说明生成更稳定可靠。
- DerODE 的直线轨迹设计使训练过程**更稳定、更高效**：训练时间较 VPSDE/VESDE 减少约 40-44%，推理时间也显著缩短（100 步时减少约 36-40%）。
- DivSDE 在不引入额外训练参数的情况下，有效提升了生成多样性，同时保持较高准确性。
- 可视化结果表明，DSDFM 能够生成多样且连贯的人体运动序列，与动作标签语义一致。

## 7. 优点

- **方法设计新颖**：提出"确定性→随机性"的两阶段映射范式，合理结合 ODE（高效确定性映射）与 SDE（多样化随机注入）的优点，思路清晰且具有理论支撑（三个 Proposition 附有证明）。
- **训练高效稳定**：相对于传统扩散模型，DerODE 避免了复杂的曲率轨迹和 score 网络训练，显著降低训练时间和参数量。
- **无需额外训练成本**：DivSDE 在采样阶段直接复用 DerODE 的结果，不引入额外训练过程或参数，实用性强。
- **广泛适用性**：方法同时适用于条件生成（动作标签）和无条件生成，在多个数据集上均验证有效。
- **实验较全面**：涵盖准确性、多样性、训练/推理效率、参数量、可视化等多个维度的评估，对比方法多样。

## 8. 不足与局限

- **多样性提升有限**：虽然 DivSDE 对多样性有提升（Diversity 18.41 vs VPSDE 17.00），但提升幅度不算突出，且表 2 中条件生成多样性甚至略低于 MotionDiffuse。
- **实验覆盖不足**：
  - 未在文本条件（text-to-motion）任务上进行验证，而该任务是人体运动合成领域的主流场景之一。
  - 未与 Flow Matching、Rectified Flow 等同类"直线轨迹"方法进行直接对比，缺乏对该类方法优势的充分论证。
  - 未提供 HumanML3D 上无条件生成和条件生成的完整对比结果（仅给出消融中的 FID），与 SOTA 方法在 HumanML3D 上的对比不足。
- **算力信息不透明**：未说明 GPU 型号/数量、显存占用、总计算量等关键资源信息，影响可复现性评估。
- **潜在偏差风险**：
  - 消融实验仅与 SDE 类基线对比，DivSDE 的增益可能是相对于较弱的基线的结果。
  - 训练/推理时间对比未考虑模型架构差异带来的不公平因素（如参数量不同）。
  - $\eta$（多样性强度）和 $\lambda_{cl}$（平衡参数）为固定值，未提供敏感性分析，参数选择依据不明确。
- **应用限制**：方法依赖 VQVAE 的潜在空间质量，若潜在表示不佳则生成性能受限；且生成运动长度固定，可能不适合需要变长输出的实际应用场景。

（完）
