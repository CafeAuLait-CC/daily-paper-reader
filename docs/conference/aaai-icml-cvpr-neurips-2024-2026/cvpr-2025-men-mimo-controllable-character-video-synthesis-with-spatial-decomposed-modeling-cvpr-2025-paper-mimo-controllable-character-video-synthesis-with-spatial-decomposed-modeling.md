---
title: "MIMO: Controllable Character Video Synthesis with Spatial Decomposed Modeling"
title_zh: MIMO：基于空间分解建模的可控角色视频合成
authors: "Men, Yifang, Yao, Yuan, Cui, Miaomiao, Bo, Liefeng"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Men_MIMO_Controllable_Character_Video_Synthesis_with_Spatial_Decomposed_Modeling_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 4.0
evidence: 合成可控角色视频，生成真实运动与场景，与人体运动合成仅有弱相关。
tldr: 针对角色视频合成中3D方法需要多视角逐案例训练、2D扩散方法控制和泛化不足的问题，提出MIMO框架，通过空间分解建模将字符、动作和场景解耦，实现简单用户输入下的可控角色视频合成。该方法在保持高逼真度的同时支持任意角色的快速建模与扩展，为角色视频生成提供更灵活的控制和更好的可扩展性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1791, \"height\": 897, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 846, \"height\": 922, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1692, \"height\": 924, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 849, \"height\": 369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1783, \"height\": 1085, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1788, \"height\": 1286, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 845, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 849, \"height\": 344, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 896, \"height\": 259, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-men-mimo-controllable-character-video-synthesis-with-spatial-decomposed-modeling-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 880, \"height\": 298, \"label\": \"Table\"}]"
motivation: 现有角色视频合成方法或需多视角逐案例训练，或难以实现灵活控制、姿态泛化和场景交互。
method: 提出空间分解建模框架MIMO，将字符、动作和场景属性解耦，借助简单输入实现可控合成。
result: 实验表明MIMO能合成逼真角色视频，并具有良好的控制能力和角色可扩展性。
conclusion: 空间分解建模为可控角色视频合成提供了新途径，兼顾质量与灵活性。
---

## Abstract
Character video synthesis aims to produce realistic videos of animatable characters within lifelike scenes. As a fundamental problem in the computer vision and graphics community, 3D works typically require multi-view captures for per-case training, which severely limits their applicability of modeling arbitrary characters in a short time. Recent 2D methods break this limitation via pre-trained diffusion models, but they struggle for flexible controls, pose generality and scene interaction. To this end, we propose MIMO, a novel framework which can not only synthesize realistic character videos with controllable attributes (i.e., character, motion and scene) provided by simple user inputs, but also simultaneously achieve advanced scalability to arbitrary characters, generality to novel 3D motions, and applicability to interactive real-world scenes in a unified framework. The core idea is to encode the 2D video to compact spatial codes, considering the inherent 3D nature of video occurrence. Concretely, we lift the 2D frame pixels into 3D using monocular depth estimators, and decompose the video clip into three spatial components (i.e., main human, underlying scene, and floating occlusion) in hierarchical layers based on the 3D depth. These components are further encoded to canonical identity code, structured motion code and full scene code, which are utilized as control signals of the synthesis process. The design of spatial decomposed modeling enables flexible user control, complex motion expression, as well as 3D-aware synthesis for scene interactions. Experimental results show that the proposed method outperforms prior works by a large margin in character animation synthesis and is effective in providing a high degree of controllability (i.e., arbitrary characters, novel 3D motions, interactive scenes), thus enabling brand-new editing tasks (e.g., video character replacement).

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **任务定义**：角色视频合成（Character Video Synthesis），即根据参考图像等输入，生成逼真的、可动画化的角色在真实场景中的视频。
- **现有方法的两难困境**：
  - **3D 方法（如 NeRF、3DGS）**：能够实现高保真渲染和复杂动作控制，但通常需要多视角采集或单目视频的逐案例训练，训练成本高、数据获取难，难以快速建模任意角色。
  - **2D 扩散方法（如 Animate Anyone、MimicMotion、Champ）**：借助预训练扩散模型，可从单张图像生成动画，但存在三个核心不足：
    1. 控制不够灵活（难以对角色、动作、场景进行分离式属性控制）；
    2. 姿态泛化能力弱，尤其在复杂 3D 人体运动和自遮挡场景下质量下降；
    3. 无法自然处理人-物交互、遮挡以及大范围相机运动的真实场景。
- **核心主张**：现有 2D 方法失败的根本原因在于仅在 2D 特征空间中对视频进行解析，忽视了视频内在的 3D 特性。本文提出 MIMO，通过“空间分解建模”将视频分解为层次化的 3D 空间组件，实现灵活可控、高质量、且能处理复杂场景交互的角色视频合成。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
将 2D 视频中的像素提升到 3D 空间（借助单目深度估计），按深度将视频分解为三个层次化空间组件：**主要人物（human）**、**底层场景（scene）** 和 **漂浮遮挡物（occlusion）**。每个组件被编码为独立的潜在代码，作为扩散解码器的条件，实现对角色、动作、场景的分离控制与三维感知合成。

### 技术流程（算法流程概览）

1. **层次化空间分解（Spatial Layer Decomposition）**
   - 对每一帧，使用预训练单目深度估计器（Depth Anything）获取深度图。
   - 通过人类检测和视频跟踪获得人物 masklet \( M_h \)。
   - 将平均深度小于人物的物体划分为遮挡层，得到 masklet \( M_o \)。
   - 场景 masklet \( M_s = 1 - M_h - M_o \)。
   - 各组件视频通过原视频与 masklet 逐元素相乘得到：\( v_i = v \odot M_i, \; i \in \{h, o, s\} \)。

2. **解耦的人物编码（Disentangled Human Encoding）**
   - **结构化运动码（Structured Motion Code, SMR）**：
     - 在 SMPL 模型的 6890 个顶点上锚定一组可学习的潜在码 \( Z = \{z_1, ..., z_{6890}\} \)。
     - 对每帧，使用预训练模型（如 Humans in 4D）估计 SMPL 参数和相机参数，将顶点位置变换到 3D 空间并投影到 2D 平面。
     - 通过可微光栅化器（rasterizer）和顶点插值，生成连续值 2D 特征图 \( F_t \)，堆叠时间轴后经姿态编码器 \( E_p \) 得到运动码 \( C_{mo} \)。
   - **规范外观迁移（Canonical Appearance Transfer）**：
     - 用预训练人体重姿态模型将姿态化的人体图像变换为标准 A-pose 的 canonical 图像。
     - 通过“CLIP 图像编码器 + ReferenceNet”结构提取全局与局部特征，得到身份码 \( C_{id} \)，实现身份与动作的完全解耦。

3. **场景与遮挡编码（Scene and Occlusion Encoding）**
   - 场景分支：对场景视频 \( v_s \) 先进行视频修复（Video Inpainting）以消除 mask 边缘干扰，然后输入共享 VAE 编码器得到场景码 \( C_s \)。
   - 遮挡分支：将遮挡视频 \( v_o \) 输入同一 VAE 编码器得到遮挡码 \( C_o \)。
   - 将 \( C_s \) 与 \( C_o \) 拼接为完整场景码 \( C_{so} \)，用于合成时联合控制。

4. **组合解码（Composed Decoding）**
   - 基于 Stable Diffusion（SD 1.5）的 UNet + AnimateDiff 时序层作为去噪骨干。
   - \( C_{so} \) 与潜在噪声拼接后经 3D 卷积融合；\( C_{mo} \) 加到融合特征上；\( C_{id} \) 的局部特征通过自注意力、全局特征通过交叉注意力注入 UNet。
   - 解码得到生成的视频帧。

5. **训练目标**
   - 使用标准扩散噪声预测损失：
     \[
     \mathcal{L} = \mathbb{E}_{x_0, c_{id}, c_{so}, c_{mo}, t, \epsilon \sim \mathcal{N}(0,1)} \left[ \|\epsilon - \epsilon_\theta(x_t, c_{id}, c_{so}, c_{mo}, t)\|_2^2 \right]
     \]
   - 采用无标注的 2D 视频进行训练，实现自动属性分离与重建。

## 3. 实验设计：数据集、基准与对比方法

- **训练数据集 HUD-7K**：
  - 5K 真实人物视频（无标注，自动分解）；
  - 2K 合成动画视频（用 En3D 渲染复杂动作和多视角，具有精确标注）。
- **测试集**：
  - 100 个真实世界人物视频，截取为 150 帧片段，覆盖舞蹈、体育、电影等多样内容。
- **评估指标**：PSNR、SSIM、LPIPS（图像质量）、FVD（视频质量）。
- **对比方法**：
  - Animate Anyone
  - MimicMotion
  - Champ
  - 以及多种消融变体（w/o SDM、w/ 2D skeleton、w/ 3D maps、w/o CA）。
- **任务评估场景**：
  - 任意角色控制（真实人物、卡通角色、拟人角色）；
  - 新颖 3D 运动控制（AMASS、Mixamo 动作库；从真实视频提取的运动）；
  - 交互场景控制（视频角色替换、人-物交互、遮挡场景）。

## 4. 资源与算力

- **文中明确提到的资源**：
  - 8 张 NVIDIA Tesla A100 GPU，80GB 显存。
  - 训练约 50k 迭代，24 帧视频，batch size 为 8。
- **未明确说明的方面**：
  - 具体的训练总时长（小时/天）未给出；
  - 测试/推理时的计算成本也未说明。

## 5. 实验数量与充分性

- **实验组数**：
  1. 主实验：与 3 个 SOTA 方法的定性、定量对比（含整体指标对比 + 图像/视频质量指标）。
  2. 消融实验：
     - 去除空间分解建模（w/o SDM）；
     - 去除独立遮挡编码（w/o occ.）；
     - 用 2D 骨架替代结构化运动码（w/ 2D skeleton）；
     - 用 3D maps 替代（w/ 3D maps）；
     - 去除规范外观迁移（w/o CA）。
  3. 额外应用展示：任意角色、AMASS/Mixamo 动作、视频角色替换等定性结果。
- **充分性评估**：
  - **优点**：覆盖了核心设计的每个主要模块，对比多种替代方案，且定量指标完整（4 项指标），能够清晰验证各贡献的有效性。
  - **不足**：
    - 测试集规模较小（100 个视频），多样性有限；
    - 缺乏用户研究或主观评测；
    - 未提供与近期视频生成模型（如基于大模型的方法）的对比；
    - 对失败案例的分析不足；
    - 消融实验的部分替代方案（如 2D 骨架）可能未调整到最优超参数，公平性有待考量。

## 6. 论文的主要结论与发现

- 提出的 MIMO 框架能够在统一框架中实现：
  - **任意角色的扩展性**（真实/卡通/拟人角色）；
  - **新颖 3D 运动的泛化性**（AMASS/Mixamo 等大动作库、真实视频运动）；
  - **交互真实场景的适用性**（人-物交互、遮挡、相机运动）。
- 空间分解建模比直接学习整体 2D 视频特征效果更好，能实现更可靠的背景生成和遮挡感知合成。
- 结构化运动码（SMR）比 2D 骨架和 3D maps 具有更强的姿态表达能力，显著提升对复杂 3D 动作的泛化。
- 规范外观迁移有效消除身份与动作的纠缠，减少手/脚混淆等伪影。
- 定量结果大幅优于现有方法（PSNR 提升约 4.16 以上，SSIM 提升约 0.152，LPIPS 和 FVD 也显著改善）。

## 7. 优点

- **问题定义清晰且具有实际价值**：提出了“可控属性（角色/动作/场景）”的合成范式，用户输入简单多样（单图、姿态序列、视频）。
- **创新性强**：首次将视频分解为基于深度的层次化 3D 空间组件，并引入“结构化运动码”锚定在 SMPL 顶点上，使动作表示更稠密、更符合 3D 人体空间。
- **统一框架**：同时解决角色可扩展、动作泛化、场景交互，实现视频角色替换等新编辑任务。
- **无需额外标注**：训练数据为无标注 2D 视频，利用自动分解机制，方便大规模扩展。
- **模块设计合理**：身份与动作完全解耦、场景与遮挡独立编码，各模块作用清晰，消融验证充分。
- **实验比较全面**：与多个当前主流方法对比，并补充了多种消融和跨域应用展示。

## 8. 不足与局限

- **依赖预训练模型的质量**：深度估计、人体检测/追踪、SMPL 估计、视频修复、重姿态模型等任一环节的误差都会影响分解和生成结果，整体流程较长，误差可能累积。
- **测试集规模较小**：基准仅 100 个视频，难以反映复杂真实世界的完整分布，统计显著性未知。
- **场景建模仍有限**：场景码通过 VAE 编码，难以处理大范围相机运动下的复杂动态背景，可能造成模糊或失真（虽然在复杂案例上优于对比方法，但仍与真实视频有差距）。
- **遮挡控制能力有限**：仅支持“漂浮遮挡物”，对于与人物紧密接触且相互遮挡的交互（如拥抱、手持道具）可能难以精确建模。
- **训练资源门槛高**：需要 8×A100 80GB，训练迭代 50k，普通研究团队复现成本较高。
- **缺乏实时性**：扩散模型基于迭代去噪，推理速度较慢，不利于交互式应用。
- **未见负面对比**：未与最新的大规模视频生成模型（如 SVD、I2VGen-XL 等）或更强的 3D 方法作量化对比，实验公平性需谨慎解读。
- **伦理风险**：该技术可被用于深度伪造或未经授权的角色替换，论文未讨论相关社会影响与限制措施。

（完）
