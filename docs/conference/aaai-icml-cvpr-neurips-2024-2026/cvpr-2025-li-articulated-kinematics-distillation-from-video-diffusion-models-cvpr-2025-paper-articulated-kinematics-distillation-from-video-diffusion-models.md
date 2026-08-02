---
title: Articulated Kinematics Distillation from Video Diffusion Models
title_zh: 从视频扩散模型蒸馏关节运动学
authors: "Li, Xuan, Ma, Qianli, Lin, Tsung-Yi, Chen, Yongxin, Jiang, Chenfanfu, Liu, Ming-Yu, Xiang, Donglai"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Li_Articulated_Kinematics_Distillation_from_Video_Diffusion_Models_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 7.0
evidence: 从视频扩散模型中蒸馏关节运动用于骨架角色动画
tldr: 生成高保真角色动画时，传统方法难以同时保持形状一致和运动真实。该方法提出关节运动蒸馏（AKD），基于骨架表示控制角色关节，利用视频扩散模型的分数蒸馏采样，在保持结构完整性的同时生成复杂关节动作，并可用于物理仿真。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1793, \"height\": 648, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1804, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1816, \"height\": 952, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1813, \"height\": 895, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 973, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 870, \"height\": 911, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 871, \"height\": 306, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 876, \"height\": 240, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 866, \"height\": 178, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 422, \"height\": 134, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-articulated-kinematics-distillation-from-video-diffusion-models-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 450, \"height\": 141, \"label\": \"Table\"}]"
motivation: 已有神经变形场难以在生成复杂角色动画时保持形状一致。
method: 以骨架表示降低自由度，通过视频扩散模型的分数蒸馏采样生成关节运动。
result: 生成了高保真、结构一致且物理合理的角色动画。
conclusion: 将骨架控制与扩散模型蒸馏结合，是一种高效的角色动作合成方案。
---

## Abstract
We present Articulated Kinematics Distillation (AKD), a framework for generating high-fidelity character animations by merging the strengths of skeleton-based animation and modern generative models. AKD uses a skeleton-based representation for rigged 3D assets, drastically reducing the Degrees of Freedom (DoFs) by focusing on joint-level control, which allows for efficient, consistent motion synthesis. Through Score Distillation Sampling (SDS) with pre-trained video diffusion models, AKD distills complex, articulated motions while maintaining structural integrity, overcoming challenges faced by 4D neural deformation fields in preserving shape consistency. This approach is naturally compatible with physics-based simulation, ensuring physically plausible interactions. Experiments show that AKD achieves superior 3D consistency and motion quality compared with existing works on text-to-4D generation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- 传统3D角色动画流程（建模、绑定、动捕、重定向）虽能实现高质量控制，但依赖大量人工，难以规模化。
- 视频生成模型可从文本直接生成动画，但缺乏3D信息，常出现结构不一致（如肢体数量错误）、物理不合理（脚滑步、穿地）等问题。
- 现有文本到4D生成方法多采用神经变形场（neural deformation fields），预测空间各点的位移来变形3D形状，自由度极高，优化困难且形状保持能力差。
- 作者提出**Articulated Kinematics Distillation (AKD)**，将骨架动画的低自由度控制与视频扩散模型的丰富运动先验相结合：以骨架参数化运动，通过分数蒸馏采样（SDS）从预训练视频模型中提取复杂关节动作，同时保持结构完整性，并能自然对接物理仿真。

### 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：用骨架（关节角度序列）作为运动参数，将自由度从空间中所有查询点压缩到少量关节，使蒸馏聚焦于整体运动风格而非局部形变。
- **整体流程**：
  1. 用文本到3D方法生成静态mesh资产（如Tet-Splatting），手动嵌入骨架，计算LBS蒙皮权重并传递给3D高斯核。
  2. 将mesh转换为3DGS表示（通过200随机视图重建），利用可微高斯光栅化进行渲染。
  3. 优化变量为每帧关节角度和根骨6-DoF变换，通过可微前向运动学（FK）和3DGS渲染得到视频。
  4. 视频输入预训练视频扩散模型（CogVideoX-5B），计算SDS损失并将其梯度反传至关节参数。
- **关键技术细节**：
  - 使用**v-prediction**扩散模型，SDS梯度简化为：`∇z LSDS = E[w(t)(z - z_hat)]`，其中`z_hat = √αt zt - vθ(zt; t, y)`。
  - 采用梯度检查点技术，使单张A100-40GB即可运行优化。
  - **地面渲染**：用棋盘格地面作为背景，为视频模型提供物体与地面交互的线索，减少浮空和穿透。
  - **相机轨迹**：相机平滑跟随变形物体中心，符合视频模型的object-centric生成特性。
- **优化损失**：`L = LSDS + λ1Lsmooth + λ2Lground`，其中`smooth`为参数时间二阶差分的MAE，`ground`为骨骼立方体顶点穿透地面的惩罚。
- **物理追踪**：使用Warp实现半隐式刚体模拟器，通过PD控制器输出关节力矩，以最小化仿真与蒸馏运动的骨位差异，并使用细粒度梯度裁剪解决长程反传时的梯度爆炸。

### 3. 实验设计：数据集 / 场景、benchmark、对比方法
- **场景与数据**：共生成29个静态3D资产，涵盖动物（狮子、骆驼、大象、暴龙等）和人形（宇航员），均为行走/跑步等地面运动。
- **基准**：使用VideoPhy自动评分，包括语义一致性（SA）和物理常识（PC）两个指标；同时进行用户研究（20名评估者），从运动量（MA）、物理合理性（PP）、文本对齐（TA）三方面对比。
- **对比方法**：与SOTA开源方法TC4D（Trajectory-conditioned text-to-4D）比较。TC4D支持长轨迹运动，而其他方法（如4D-Fy、DreamGaussian4D）仅限于局部运动，故未纳入主对比。
- **消融研究**：分别去掉地面渲染、地面穿透惩罚、平滑损失；更换视频扩散模型（VideoCrafter vs CogVideoX）；更换文本到3D模块（从TC4D中提取资产）。

### 4. 资源与算力
- 文中明确说明：所有实验可在**单个NVIDIA A100-40GB**显卡上运行。
- 每个资产的SDS优化为**10,000次迭代，约需25小时**。
- 未说明使用的GPU总数量、具体并行配置或总计算量，仅强调单卡可行性。

### 5. 实验数量与充分性
- **主要对比实验**：29个资产上的自动评分 + 20人用户研究，覆盖了多个物种和动作。
- **消融实验**：针对三个重要组件（地面渲染、穿透惩罚、平滑损失）进行去除测试，并给出定量结果；还做了视频模型替换和文本到3D模块替换的验证。
- **多样性实验**：不同资产、不同运动模式（行走/跑步）展示。
- **物理追踪实验**：展示追踪前后对比。
- **充分性评估**：实验较全面，但存在一定不足：用户研究偏好比例仅略高于50%（MA 51%、PP 53%、TA 53%），优势不算显著；自动指标中PC分数虽更高但标准差较大；消融实验仅针对少量组件，未对骨架设定、优化超参、相机策略等做系统分析；与TC4D的公平性上，作者特意在PC评估时去除地面渲染，但其他方法是否公平仍有讨论空间。

### 6. 论文的主要结论与发现
- AKD生成的关节运动在**语义一致性**（SA 0.81 vs 0.40）和**物理常识**（PC 0.39 vs 0.31）上显著优于TC4D。
- 通过骨架低维参数化，可有效保持3D结构一致，避免TC4D常见的模糊伪影和缺乏交替腿运动的问题。
- 棋盘格地面渲染提供关键的物理位置线索，明显减少物体浮空或穿地。
- 生成的运动可通过物理仿真追踪进一步投影到符合重力、摩擦接触的轨迹上，同时保持运动风格。
- 方法支持多样化的资产类型和运动模式，且文本到3D模块可替换。

### 7. 优点
- **低维参数化**：大幅减少优化自由度，使蒸馏过程稳定高效，同时保持关节结构永久性。
- **形状一致性**：相比神经变形场，骨架变形不会破坏局部几何结构，解决4D生成常见模糊问题。
- **物理兼容性**：骨架表示天然适合刚体仿真，可实现“生成-仿真”闭环。
- **实用地面线索**：非均匀地面渲染这一简单设计有效提高物理合理性，具有推广价值。
- **模块化**：文本到3D、视频扩散模型均可替换，泛化潜力大。
- **资源友好**：单卡可运行，便于复现。

### 8. 不足与局限
- **视觉质量尚不理想**：生成资产的纹理或几何精细度有限，与真实视频分布仍有差距。
- **运动多样性受限**：最终运动风格依赖于视频扩散模型的能力，如果模型本身无法产生某种动作，则蒸馏结果也会受限。
- **仅适用于刚性关节运动**：不适用于软体变形、布料、流体等非骨架驱动动态。
- **需要手动装配骨架**：虽然每个实例只需几分钟，但无法全自动规模化；文中建议未来使用RigNet等自动绑定方法。
- **训练时间较长**：每个资产约25小时，迭代成本较高。
- **物理合理性仍有限**：即使经SDS优化，部分结果仍存在浮空或滑步，必须借助物理追踪进一步修正。
- **实验局限**：未在更多类别（如鸟类、鱼类）或更复杂动作（跳跃、翻滚）上验证；对比方法有限，未包含最新4D生成模型；用户研究偏好比例较低，可能反映主观感受差异大。

（完）
