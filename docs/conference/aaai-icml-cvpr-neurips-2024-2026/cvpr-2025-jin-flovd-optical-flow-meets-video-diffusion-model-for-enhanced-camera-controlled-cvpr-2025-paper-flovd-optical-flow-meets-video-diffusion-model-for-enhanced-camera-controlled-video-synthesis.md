---
title: "FloVD: Optical Flow Meets Video Diffusion Model for Enhanced Camera-Controlled Video Synthesis"
title_zh: FloVD：光流与视频扩散模型结合用于增强的相机可控视频合成
authors: "Jin, Wonjoon, Dai, Qi, Luo, Chong, Baek, Seung-Hwan, Cho, Sunghyun"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Jin_FloVD_Optical_Flow_Meets_Video_Diffusion_Model_for_Enhanced_Camera-Controlled_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 8.0
evidence: 利用光流表示运动，基于视频扩散模型实现相机可控的视频合成
tldr: 针对相机可控视频生成中需要精确相机参数的问题，本文提出FloVD视频扩散模型。该方法用光流统一表示相机和物体运动，无需真实相机参数即可训练，并利用背景光流编码的3D相关性实现细致的相机控制。通过两阶段流程生成光流再生成视频，FloVD能合成自然物体运动并保持相机控制精度，为视频合成提供了新工具。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1794, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1745, \"height\": 386, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 778, \"height\": 792, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 873, \"height\": 192, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1726, \"height\": 809, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1715, \"height\": 609, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 815, \"height\": 385, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 873, \"height\": 165, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 787, \"height\": 288, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 261, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 856, \"height\": 162, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-jin-flovd-optical-flow-meets-video-diffusion-model-for-enhanced-camera-controlled-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 740, \"height\": 201, \"label\": \"Table\"}]"
motivation: 现有相机可控视频生成依赖精确相机参数，难以利用任意训练视频。
method: 用光流表示相机与物体运动，构建两阶段视频扩散模型生成光流并据此合成视频。
result: 无需真实相机参数即可达到精细相机控制，并生成自然物体运动。
conclusion: 光流表示简化了训练数据要求，提升了视频扩散模型的可用性和可控性。
---

## Abstract
We present FloVD, a novel video diffusion model for camera-controllable video generation. FloVD leverages optical flow to represent the motions of the camera and moving objects. This approach offers two key benefits. Since optical flow can be directly estimated from videos, our approach allows for the use of arbitrary training videos without ground-truth camera parameters. Moreover, as background optical flow encodes 3D correlation across different viewpoints, our method enables detailed camera control by leveraging the background motion. To synthesize natural object motion while supporting detailed camera control, our framework adopts a two-stage video synthesis pipeline consisting of optical flow generation and flow-conditioned video synthesis. Extensive experiments demonstrate the superiority of our method over previous approaches in terms of accurate camera control and natural object motion synthesis.

---

## 论文详细总结（自动生成）

## FloVD：光流与视频扩散模型结合用于增强的相机可控视频合成

### 1. 核心问题与研究动机

- **背景问题**：视频扩散模型虽然能生成高质量视频，但缺乏对相机运动与视角的精确控制，限制了其在影视制作、虚拟现实等需要精确相机参数控制场景中的应用。
- **现有方法的局限**：已有相机可控视频合成方法主要分为两类：
  - 基于文本或用户绘制的运动描述，仅支持缩放、平移等粗粒度控制。
  - 直接输入相机参数的方案（如 CameraCtrl、MotionCtrl），虽然控制精度高，但训练时需要带有真实相机参数的数据集（如 RealEstate10K），这类数据集多为静态场景，导致模型泛化能力差，生成视频中物体运动不自然、相机控制不精确。
- **核心洞察**：光流可以从任意视频中直接估计，无需真实相机参数；且背景光流天然编码了不同视角间的 3D 相关性，可用于实现精细的相机控制。因此，用光流替代相机参数作为条件输入，可以同时解决训练数据受限和物体运动不自然的问题。
- **问题意义**：开发一种能够在不需要真实相机参数的情况下利用任意视频进行训练、同时支持精细相机控制和自然物体运动的视频生成框架。

### 2. 方法论

#### 2.1 核心思想

采用光流表示视频中相机的运动与物体运动，构建两阶段视频合成管线：**先生成光流，再基于光流生成视频**。光流分为相机光流（由相机参数与3D结构推导）与物体光流（由生成模型合成），二者融合后作为视频合成模型的条件输入。

#### 2.2 关键技术细节

**阶段一：光流生成（Flow Generation）**

- 相机光流生成：
  1. 用现成的单目深度估计网络（Depth Anything V2）从输入图像估计深度图。
  2. 将输入图像每个像素反投影到3D空间，按目标帧相机参数旋转/平移并重新投影回2D平面，得到所有像素的位移向量，构造相机光流图。
- 物体光流合成（OMSM，Object Motion Synthesis Model）：
  - 基于潜视频扩散模型（Stable Video Diffusion）构建，由去噪U-Net和VAE编解码器组成。
  - 输入图像编码后与带噪潜特征拼接，U-Net迭代去噪，最后VAE解码输出物体光流图（仅取输出RGB通道中的前两通道作为x/y分量）。
  - 训练采用两阶段策略：先用全集数据预训练，再用无相机运动的精选数据微调，消除背景中的相机运动对光流的影响（如图4所示）。
- 光流融合：
  - 用现成分割模型（SAM 2）从输入图像估计物体掩膜。
  - 对掩膜区域内的像素，先加物体光流位移得到新位置，再利用相机参数进行变换，最终合并为相机-物体光流图。
  - 公式：ft,x = (1−M·)f_c(t,x) + M·f'(t,x)，即静态区域用相机光流，动态区域用相机+物体合成光流。

**阶段二：光流条件视频合成（FVSM，Flow-Conditioned Video Synthesis）**

- 同样基于SVD构建，额外引入一个T2I-Adapter风格的流编码器。
- 流编码器将相机-物体光流图编码为多尺度嵌入，并逐层加到去噪U-Net各层特征上，条件化视频生成过程。
- 训练时仅更新流编码器，其余组件（U-Net、VAE）固定不动，以保留预训练模型的视频生成质量。

#### 2.3 训练方式

- 使用内部数据集（500K视频片段）及其无相机运动子集（约100K视频片段）。
- 光流标签用现成光流估计器（RAFT）从训练视频直接估计。
- OMSM通过降噪分数匹配训练；FVSM同样采用该训练方式，并使用二次时间步采样策略（QTS）增强相机可控性。

### 3. 实验设计

#### 3.1 数据集与基准

- **相机可控性评估**：使用 RealEstate10K 测试集，随机采样 1,000 个视频片段及其相机参数。
- **视频合成质量评估**：
  - Pexels-random：从 Pexels 数据集随机采样 1,500 个视频。
  - Pexels-small / Pexels-medium / Pexels-large：各 500 个视频，按物体光流平均幅值（<20、20–40、≥40像素）分类，用于评估不同物体运动规模下的合成质量。
- **对比方法**：MotionCtrl 和 CameraCtrl（均为支持精细相机控制的代表性方法）。

#### 3.2 评估指标

- 相机可控性：平均旋转误差（mRotErr）、平均平移误差（mTransErr）、相机外参矩阵平均误差（mCamMC）。用 GLOMAP 从合成视频中估计相机参数，与输入参数对比。
- 视频质量：FVD、FID、IS。

#### 3.3 模型变体

- Ours (RE10K)：FVSM 在 RealEstate10K 上训练（不使用相机参数标签）。
- Ours (Internal)：FVSM 在内部数据集上训练。
- Ours w/ OMSM：加入 OMSM（OMSM 由内部数据集训练）。
- 消融实验：Baseline（无 OMSM，RE10K训练）→ +OMSM → +large-scale data（最终模型）。

### 4. 资源与算力

- 论文**未明确说明**使用的 GPU 型号、数量及具体训练时长。
- 仅提及训练迭代次数：OMSM 在全量数据集上训练 100K 次迭代，精选数据集微调 50K 次迭代，batch size 为8；FVSM 训练 50K 次迭代，batch size 为16（使用16个视频片段及其光流图）。
- 由于缺乏具体硬件信息，无法定量评估计算资源需求。

### 5. 实验数量与充分性

- **实验组数**：主要包括四大部分：
  1. 相机可控性的定量评估（4个模型变体对比）。
  2. 视频合成质量的定量评估（4个数据集 × 3个指标 × 7种相机运动轨迹）。
  3. 主成分消融实验（3个版本对比）。
  4. 大量定性比较图（包括X-t切片分析）、应用演示（视频编辑、dolly zoom）。
- **充分性评价**：整体实验较为充分。消融设计清晰，逐步验证了 OMSM 与大规模训练数据的贡献；对比方法覆盖了当前主流方法；在相机可控性与视频质量之间做了平衡评价。但部分详细分析（如时间步采样策略对比、更多定性图）放在了补充材料中。相机可控性评估仅基于 RealEstate10K（静态场景），未在动态场景数据集上评估相机控制精度，是其覆盖面上的不足。

### 6. 主要结论与发现

- 光流作为相机可控视频生成的条件输入是完全可行的，无需真实相机参数即可实现与 CameraCtrl（使用相机参数训练）相当甚至更优的相机控制精度。
- 光流表示允许使用任意视频训练，显著改善生成视频中物体运动的自然度，克服了静态场景数据集训练的固有缺陷。
- 两阶段分解（相机光流+物体光流→融合→条件视频合成）能够有效解耦相机运动和物体运动，使模型兼具精确相机控制和自然物体运动两大能力。
- FVSM 对光流输入具有鲁棒性，即使相机光流存在因深度估计不完善导致的瑕疵，仍能生成无伪影的高质量视频。

### 7. 方法优点

- **训练数据不受限**：光流可直接从任意视频估计，摆脱了对带相机参数数据集的依赖，显著提升数据多样性和模型泛化能力。
- **相机控制精度高**：利用背景光流的3D相关性，无需相机参数即可实现对标甚至超越基于相机参数训练的方法。
- **相机与物体运动解耦**：两阶段分解架构使模型可分别控制静态背景运动和动态物体运动，是已有方法不具备的能力。
- **工程实现精巧**：复用预训练VAE直接编解码光流图、采用两阶段OMSM训练策略消除相机运动干扰、利用掩膜融合光流降低错误传播，多处设计兼顾简洁性和有效性。
- **应用延展性好**：支持时间一致的视频编辑、dolly zoom 等电影化相机控制，无需额外训练。

### 8. 不足与局限

- **误差级联**：管道依赖深度估计、光流估计、语义分割等多个现成模块的精度，任一环节出错都可能影响最终合成质量（作者承认 OMSM 和分割模型的误差会导致不自然的物体运动）。
- **物理精确性不足**：相机与物体光流的融合缺少z轴（深度方向）物体运动信息，融合结果并非物理精确的光流，依赖 FVSM 的生成能力来补偿。
- **实验覆盖有限**：相机可控性仅在 RealEstate10K 上评估，该数据集为静态场景，无法充分验证动态场景下的相机控制表现；未与更多最新方法（如 CamCo、CamI2V、VD3D）直接对比。
- **缺乏算力信息**：未报告 GPU 型号、数量和训练耗时，可复现性和资源评估不透明。
- **缺乏用户研究**：对于视频质量的主观评价（如自然度、相机运动的观感）以定量指标和定性展示为主，没有进行用户偏好测试。
- **分辨率限制**：合成分辨率固定为 320×576、14帧，相比最新方法在高分辨率、长视频生成方面存在差距。

（完）
