---
title: "RoHM: Robust Human Motion Reconstruction via Diffusion"
title_zh: RoHM：基于扩散的鲁棒人体运动重建
authors: "Zhang, Siwei, Bhatnagar, Bharat Lal, Xu, Yuanlu, Winkler, Alexander, Kadlecek, Petr, Tang, Siyu, Bogo, Federica"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Zhang_RoHM_Robust_Human_Motion_Reconstruction_via_Diffusion_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 10.0
evidence: 基于扩散的三维人体运动模型，处理噪声与遮挡下的去噪和填充
tldr: 从单目视频重建三维人体运动在噪声和遮挡下极其困难。RoHM提出将问题分解为全局轨迹和局部运动两个子任务，分别训练扩散模型，并以条件输入重建完整且合理的运动。全局模型负责全局坐标下的轨迹，局部模型关注关节运动，并保持二者的相关性。实验表明在标准数据集上，RoHM在存在噪声和遮挡时显著优于现有回归优化方法，实现了鲁棒的人体运动重建。该工作展示扩散模型在运动去噪与填充中的强能力。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1780, \"height\": 481, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1732, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 881, \"height\": 181, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 854, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 849, \"height\": 713, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 862, \"height\": 191, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 854, \"height\": 659, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 873, \"height\": 340, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 868, \"height\": 221, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-zhang-rohm-robust-human-motion-reconstruction-via-diffusion-cvpr-2024-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 870, \"height\": 245, \"label\": \"Table\"}]"
motivation: 单目三维运动重建在噪声和遮挡下不可靠，现有方法难以同时处理去噪和填充。
method: 将运动重建分解为全局轨迹与局部运动两个扩散模型，分别进行条件生成，并捕捉二者相关关系。
result: 多个基准上在噪声和遮挡情形下显著优于现有方法，重建出完整合理的全局三维运动。
conclusion: RoHM验证了扩散模型用于鲁棒三维人体运动重建的有效性。
---

## Abstract
We propose RoHM an approach for robust 3D human motion reconstruction from monocular RGB(-D) videos in the presence of noise and occlusions. Most previous approaches either train neural networks to directly regress motion in 3D or learn data-driven motion priors and combine them with optimization at test time. RoHM is a novel diffusion-based motion model that conditioned on noisy and occluded input data reconstructs complete plausible motions in consistent global coordinates. Given the complexity of the problem -- requiring one to address different tasks (denoising and infilling) in different solution spaces (local and global motion) -- we decompose it into two sub-tasks and learn two models one for global trajectory and one for local motion. To capture the correlations between the two we then introduce a novel conditioning module combining it with an iterative inference scheme. We apply RoHM to a variety of tasks -- from motion reconstruction and denoising to spatial and temporal infilling. Extensive experiments on three popular datasets show that our method outperforms state-of-the-art approaches qualitatively and quantitatively while being faster at test time. The code is available at https://sanweiliti.github.io/ROHM/ROHM.html.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

本文聚焦于**在噪声和遮挡条件下，从单目 RGB(-D) 视频中鲁棒地重建 3D 人体运动**这一核心问题。研究背景与动机如下：

- 现有人体运动重建方法存在两类显著缺陷：
  - **回归式方法**（直接训练神经网络从图像/视频回归 3D 姿态）：仅估计局部运动（身体根节点相对坐标），缺乏一致的全局轨迹；在空间或时间上发生遮挡时鲁棒性差。
  - **优化式方法**（如 HuMoR、PhaseMP）：结合数据驱动先验与测试时优化，虽然对噪声和遮挡有一定鲁棒性，但收敛慢、易陷入局部最优，且需要大量人工调参。
- 扩散模型具备迭代去噪的生成特性，适合作为数据驱动的替代方案，但现有基于扩散的运动模型主要面向**运动合成**（如文本/动作标签驱动），不支持噪声条件下的运动重建。
- 本文提出 **RoHM**，利用扩散模型的条件生成能力，从含噪声、不完整、时域不一致的初始姿态估计中，重建出**全局坐标一致、平滑完整、物理合理**的 3D 人体运动。

该工作的整体含义在于：首次系统地验证了扩散模型在**鲁棒运动重建**（而非运动合成）任务中的有效性，并为处理“去噪 + 时空填充”这一复合问题提供了可借鉴的分解思路。

## 2. 方法论

### 2.1 核心思想

将运动重建问题**按解空间解耦**为两个子问题，分别训练扩散模型处理：

- **全局轨迹**（TrajNet）：负责根节点的全局位移、旋转和高度，保证运动在世界坐标系中的一致性。
- **局部运动**（PoseNet）：负责身体关节的局部姿态、形状和脚部接触标签。

同时引入 **TrajControl** 模块捕获全局和局部运动之间的相关性，并通过**迭代推理**方案交替优化二者。

### 2.2 运动表示

- 每帧运动表示为 `X = (R, P)`：
  - **R（全局轨迹）**：包括根节点线性位置 `r_l ∈ R²`、角旋转 `r_a ∈ R`、根高度 `r_z ∈ R`、SMPL-X 全局平移 `γ ∈ R³`、全局朝向 `Φ ∈ R⁶`，以及对应的速度项。
  - **P（局部运动）**：包括 21 个关节的局部位置 `J ∈ R^(21×3)`、关节旋转 `θ ∈ R^(21×6)`、身体形状 `β ∈ R¹⁰`、脚部接触标签 `f ∈ {0,1}⁴`。
- 同时定义可见性掩码 `M_R` 和 `M_P`，用于区分可见与遮挡关节。

### 2.3 两个扩散模型

- **TrajNet**：输入噪声轨迹 `R̃` 和掩码 `M_R`，输出平滑完整的全局轨迹 `R̂₀`：

  `R̂₀ = D_R(R_t, t, c_R)`，其中 `c_R = M_R ⊙ R̃`

  采用 U-Net 编码器-解码器结构，条件信号通过额外编码器注入各层。

- **PoseNet**：以轨迹 `R̂₀`、噪声局部运动 `P̃` 和关节掩码 `M_P` 为条件，输出完整的局部运动 `P̂₀`：

  `(R̂₀, P̂₀) = D_P((R̂₀, P_t), t, c_P)`，其中 `c_P = (R̂₀, M_P ⊙ P̃)`

  采用 Transformer 编码器结构，条件信号经 MLP 编码后注入。

### 2.4 TrajControl 模块

- 问题：单独训练两个模型无法捕获全局与局部运动之间的相关性；直接用含噪不完整的局部运动条件化 TrajNet 过于困难。
- 方案：参考 ControlNet[98]，在预训练 TrajNet 上**冻结原参数**，克隆编码器层作为可训练模块 `E(·)`，通过**零卷积层**（1×1 卷积，零初始化）连接到主网络。仅更新 `E(·)` 的参数，从而在无干净局部运动时仍可用纯轨迹条件化，有干净局部运动时可通过 `E(t, P̂₀)` 精细化轨迹预测。

### 2.5 迭代推理

分 K 轮（论文中 K=2）交替运行 TrajNet 和 PoseNet：

- 第一轮：TrajNet 仅以噪声轨迹为条件；PoseNet 以 TrajNet 输出和噪声局部运动为条件。
- 后续轮次：TrajNet 额外接收上一轮 PoseNet 的局部运动输出作为控制信号；PoseNet 接收本轮改进后的轨迹。

### 2.6 分数引导采样

在 PoseNet 采样过程中引入基于分类器的引导分数，增强物理合理性和与图像证据的对齐：

- **防滑步分数**：`J_skate = || f̂₀ · J̇_foot_3D(R̂₀, P̂₀) ||²`，惩罚预测为触地时脚部速度。
- **2D 重投影一致性**：`J_2D = || c_conf (Π_K(J_3D(R̂₀,P̂₀)) − J_det) ||²`，利用 OpenPose 检测的 2D 关键点进行引导。

采样过程中按 `P_{t−1} ~ N(μ_t + (λ_skate ∇J_skate + λ_2D ∇J_2D)Σ_t, Σ_t)` 进行引导去噪。

### 2.7 训练目标

总损失为：

`L = L_simple + λ_J3D · L_J3D + λ_vel · L_vel + λ_skate · L_skate`

其中：
- `L_simple`：标准扩散去噪损失；
- `L_J3D`：3D 关节位置误差；
- `L_vel`：3D 关节速度误差；
- `L_skate`：脚部滑动惩罚损失。

训练数据使用 AMASS 数据集，训练时合成噪声和部分遮挡，并采用课程训练策略（逐步增大噪声和遮挡比例）。

## 3. 实验设计

### 3.1 数据集

| 数据集 | 用途 | 评估内容 |
|--------|------|----------|
| **AMASS** | 大规模运动捕捉数据集，用官方 SMPL-X neutral 标注，30fps 重采样 | 噪声与遮挡下的运动去噪 + 填充精度、物理合理性 |
| **PROX** | 单目 RGB-D，人与 3D 室内场景交互 | 物理合理性（脚滑、加速误差、地面穿透） |
| **EgoBody** | 人与人交互，含严重遮挡的第三人称 RGB 序列（约 24k 帧） | 全局/局部精度、物理合理性 |

### 3.2 评估设置

- **Occ-L.（遮挡下半身）**：遮蔽全部下肢关节参数，模拟场景中人体的实际遮挡情况。
- **Occ-10%（时间填充）**：遮蔽整个 10% 帧长的子序列，要求模型生成中间运动。
- 两种设置均添加不同级别高斯噪声（级别 3/5/7，对应旋转/平移不同标准差）。
- **测量指标**：MPJPE/GMPJPE（全关节/可见/遮挡分开统计）、加速度误差（Accel）、接触精度（Contact）、脚滑比例（Skating）、地面穿透距离（Dist）。

### 3.3 对比方法

- **VPoser-t**：基于 VPoser 的优化方法，加入 3D 关节平滑；
- **HuMoR**：CVAE 运动先验 + L-BFGS 优化的代表性方法；
- **MDM++**：对 MDM 的改进版，支持对含噪观测的条件化；
- **LEMO**（RGB-D 场景）：学习确定性先验的方法；
- **PhaseMP**（RGB 场景）：基于相位条件的运动先验方法（结果由作者提供）；
- **CLIFF**：单帧回归方法，作为下界参照。

### 3.4 初始化方案

- 对 PROX：使用现成回归器（如 CLIFF、ExPose、MeTRAbs）进行逐帧预测；RGB-D 场景额外用深度数据进行粗略对齐。
- 对 EgoBody：与 HuMoR 一致，使用 VPoser-t 初始化，确保公平比较。

## 4. 资源与算力

- 论文正文**未明确说明**训练所使用的 GPU 型号与数量。
- 训练基于 AMASS 数据集，序列裁剪为 144 帧的短片段；TrajNet 和 PoseNet 分别独立训练。
- 据作者在补充材料中所述，训练在 2 块 RTX 3090 GPU 上进行，约需 2 周时间（此项信息正文未提及）。

## 5. 实验数量与充分性

- **实验覆盖**：3 个数据集（AMASS、PROX、EgoBody）、2 种合成遮挡设置、3 种噪声级别，以及真实场景的 RGB 和 RGB-D 两种输入模态。
- **消融实验**：在 PROX 和 AMASS 上分别验证了 TrajControl、迭代推理、测试时分数引导的贡献，并单独考察了 2D 重投影引导 J_2D 的效果。
- **公平性**：
  - 在 AMASS 上与 HuMoR、MDM++ 等在同一噪声条件下对比；
  - 在 EgoBody 上与 HuMoR 共享同一初始化，公平地反映后处理能力；
  - 在 PROX 上使用比基线更差的初始化（Ours-init 的脚下滑/抖动更严重），仍然取得更好的结果，说明方法本身有较强去噪能力。
- **总体评价**：实验数量充足、任务类型多样、消融设计合理、对比基准具有代表性，能够有效支撑论文结论。但 PROX 无真值标注，只能评估物理合理性指标，缺乏精度基准。

## 6. 主要结论与发现

1. RoHM 在 AMASS 的两种遮挡设置下均**大幅优于** SOTA 优化式方法。例如，在 Occ-L. 噪声级别 3 时，GMPJPE 遮挡关节误差比 HuMoR 降低约 66%（57.4 vs 167.9），脚滑比例降低 44% 以上。
2. 在真实场景（PROX、EgoBody）中，RoHM 生成的运动的物理合理性（脚滑、地面穿透、加速度）显著优于 HuMoR、LEMO、PhaseMP 等基线。
3. **推理速度**比 HuMoR 快约 30 倍（剔除初始化阶段）。
4. TrajControl + 迭代推理是有效组合：仅迭代而不使用 TrajControl 效果次优；仅用 TrajControl 而不引导也有改善。
5. 测试时分数引导能有效增强与图像证据的匹配度，但会略微影响运动平滑性——迭代推理可在一定程度上补偿这一损失。

## 7. 优点

1. **方法论创新性强**：将运动重建按全局/局部解耦，用两个扩散模型分别处理，并设计 TrajControl 模块沟通两者，结构清晰、可解释性强。
2. **适用场景广泛**：能统一处理运动重建、去噪、空间填充、时间填充等多种任务，适用于 RGB 和 RGB-D 输入。
3. **工程性好**：推理速度快，无需人工调参，避免了优化法的局部最优问题。
4. **超越现有方法的鲁棒性**：对训练时未见过的噪声级别（如 7 级）仍有较优表现。
5. **充分借鉴现有成果**：如从 ControlNet 引出的零卷积机制、从 HuMoR 引用的物理合理性指标等，站在已有研究基础上做增量贡献。
6. **代码开源**，有利于后续研究者复现与扩展。

## 8. 不足与局限

1. **无法在线实时运行**：TrajNet 需 100 步去噪、PoseNet 需 1000 步去噪，推理虽比优化法快，但尚未达到实时水平（作者在限制中也承认此点）。
2. **未显式建模 3D 场景环境**：RoHM 依赖 2D 重投影和物理分数引导，缺乏对场景几何（如地面、障碍物）的显式建模；在复杂人-场景交互中可能产生穿透等问题。
3. **仅关注身体主体**：未建模手部姿态与面部表情，仅使用 SMPL-X 的主干参数，在需要全身重建的场景中受限。
4. **对极端遮挡仍可能不稳定**：虽然鲁棒性优于基线，但面对长时遮挡或多关节大面积缺失时，方法仍可能产生不合理的运动（论文中的消融实验表明较大噪声下精度仍会下降）。
5. **依赖现成回归器的初始化质量**：最终输出质量与初始估计质量相关，在初始化极差时（如严重截断），RoHM 的恢复能力存在上限。
6. **扩散模型未采用潜在空间加速**：相比潜在扩散方法，直接在高维运动空间做扩散导致采样步数大、计算开销偏高。
7. **迭代推理的收敛性未作理论保证**：文中只凭经验设定 K=2，未对此做更深入的分析或自适应终止策略。

（完）
