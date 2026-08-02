---
title: World-consistent Video Diffusion with Explicit 3D Modeling
title_zh: 带显式三维建模的世界一致视频扩散
authors: "Zhang, Qihang, Zhai, Shuangfei, Martin, Miguel Ángel Bautista, Miao, Kevin, Toshev, Alexander, Susskind, Joshua, Gu, Jiatao"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhang_World-consistent_Video_Diffusion_with_Explicit_3D_Modeling_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 7.0
evidence: 利用扩散Transformer结合显式三维建模生成世界一致的视频
tldr: 现有扩散模型在视频生成中难以高效地保持三维一致性。本文提出世界一致视频扩散（WVD），通过引入XYZ图像（每像素全局三维坐标），训练扩散Transformer学习RGB与XYZ的联合分布。该方法支持多种任务，如从RGB预测XYZ或利用XYZ生成新RGB，从而提升多视角一致性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1794, \"height\": 787, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1786, \"height\": 772, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1794, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1691, \"height\": 1996, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1766, \"height\": 862, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1747, \"height\": 1053, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 668, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 760, \"height\": 321, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-world-consistent-video-diffusion-with-explicit-3d-modeling-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 639, \"height\": 545, \"label\": \"Table\"}]"
motivation: 视频扩散模型生成时缺乏显式的三维一致性约束，导致跨帧不一致。
method: 在扩散Transformer中联合建模RGB与XYZ图像，并采用灵活的内绘策略。
result: 实现了多任务适应和更好的三维一致性视频生成。
conclusion: 显式三维坐标监督可增强扩散模型的几何一致性与可控性。
---

## Abstract
Recent advancements in diffusion models have set new benchmarks in image and video generation, enabling realistic visual synthesis across single- and multi-frame contexts. However, these models still struggle with efficiently and explicitly generating 3D-consistent content. To address this, we propose World-consistent Video Diffusion (WVD), a novel framework that incorporates explicit 3D supervision using XYZ images, which encode global 3D coordinates for each image pixel. More specifically, we train a diffusion transformer to learn the joint distribution of RGB and XYZ frames. This approach supports multi-task adaptability via a flexible inpainting strategy. For example, WVD can estimate XYZ frames from ground-truth RGB or generate novel RGB frames using XYZ projections along a specified camera trajectory. In doing so, WVD unifies tasks like single-image-to-3D generation, multi-view stereo, and camera-controlled video generation. Our approach demonstrates competitive performance across multiple benchmarks, providing a scalable solution for 3D-consistent video and image generation with a single pretrained model.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 一、核心问题与研究动机

- **背景**：扩散模型在图像和视频生成领域取得了突破性进展，但在多视角/视频生成任务中，**3D 一致性问题**仍未得到有效解决。
- **现有方法的两大困境**：
  - **隐式方法**（如视频扩散模型、多视角扩散模型）：通过注意力机制隐式学习跨帧一致性，但需要海量数据和算力，且**缺乏显式 3D 保证**，容易出现跨视角不一致。
  - **显式方法**（如引入体渲染、3D 归纳偏置）：虽能施加 3D 约束，但**对数据和架构限制过强**，难以扩展到大规模、多样化的数据集。
- **核心问题**：如何在不牺牲可扩展性的前提下，为视频/多视角扩散模型提供**显式的三维一致性监督**？
- **论文答案**：提出 **WVD（World-consistent Video Diffusion）**，引入 **XYZ 图像**作为显式 3D 监督信号，联合建模 RGB 与 XYZ 帧的分布，从而以统一框架实现多种 3D 相关任务。

## 二、方法论

### 2.1 核心思想

- 利用扩散 Transformer（DiT）**联合学习多视角 RGB 帧与对应 XYZ 帧的联合分布** P(RGB, XYZ)。
- **XYZ 图像**：每个像素记录该点在全局坐标系下的 3D 坐标 (x, y, z)，为无纹理的纯几何表示，与 RGB 图像形状相同，可直接适配现有 2D Transformer 架构。
- 通过**灵活的内绘（inpainting）策略**，在推理时实现多种条件分布（如 P(XYZ|RGB) 或 P(RGB|XYZ)），统一支持多种下游任务。

### 2.2 关键技术细节

- **XYZ 图像生成公式**：  
  $x_{XYZ} = \mathcal{R}(\mathcal{N}(X), X, C)$  
  其中 $X$ 为点云，$\mathcal{N}$ 为归一化函数（将点云缩放到 [-1, 1]），$\mathcal{R}$ 为栅格化器（将 3D 点投影到图像平面），$C = (P, K)$ 为相机参数（位姿与内参）。

- **RGB-XYZ 联合扩散**：
  - 在预训练 VAE 的潜空间中进行扩散，将 RGB 和 XYZ 潜变量沿通道拼接：  
    $z_n = [\mathcal{E}(x^{RGB}_n); \mathcal{E}(x^{XYZ}_n)] \in \mathbb{R}^{L \times 2D}$
  - XYZ 已预归一化，可直接使用现有 VAE，无需额外微调，大幅提升训练效率。

- **后优化（Post Optimization）**：  
  基于预测的 XYZ 图像，通过最小化重投影损失来优化相机参数和深度图：  
  $\min_{P,K,d} \sum_{u,v} \|\tilde{x}^{XYZ}_{u,v} - \hat{x}^{XYZ}_{u,v}\|_2^2$  
  该步骤可并行化，能得到更物理一致的深度和相机估计。

- **多任务推理策略**：
  - 单图转 3D：从单张 RGB 生成多视角 RGB + XYZ 帧，进而重建点云。
  - 多视图立体：给定多张无位姿 RGB，仅通过扩散预测 XYZ（RGB 部分用观测值替换），并结合 Langevin 校正提升稳定性。
  - 相机可控视频生成：先估计输入图像的 3D 几何 → 将点云投影到目标相机轨迹生成部分 XYZ 图像 → 通过内绘策略同时生成 RGB 和缺失 XYZ。

## 三、实验设计

### 3.1 训练数据集

| 数据集 | 用途/类型 |
|---------|-----------|
| RealEstate10K | 真实场景视频 |
| ScanNet | 室内 RGB-D 场景 |
| MVImgNet | 物体多视角图像 |
| CO3D | 常见物体类别 3D 数据 |
| Habitat | 合成室内场景（提供 GT 点云） |

- RealEstate10K、MVImgNet、CO3D 使用 **DUSt3R 生成的伪真值点云**；ScanNet 使用带深度正则的 NeRF 填充深度空洞；Habitat 直接使用渲染的真值点云。
- 所有图像中心裁剪并缩放到 **256×256**。

### 3.2 评估基准与对比方法

| 任务 | 评估基准 | 对比方法 |
|------|----------|----------|
| 单图转 3D（生成质量） | 验证集（FID / KPM / FC） | CameraCtrl、MotionCtrl |
| 单目深度估计 | NYU-v2、BONN | RobustMIX、SlowTV、DUSt3R-224/512 |
| 视频深度估计 | ScanNet++ | COLMAP、MVSNet、DeepV2D、DUSt3R 等 11 种方法 |
| 相机可控视频生成 | 定性展示（还原真实视频轨迹） | — |
| 消融实验 | 单图转 3D 指标 | WVD vs. WVD w/o XYZ（仅 RGB） |

### 3.3 主要实验发现

- **单图转 3D**：WVD 的 FID 低于 CameraCtrl/MotionCtrl（15.8 vs. 12.1/12.9），但 **KPM（95.8）和 FC（95.4）均优于两者**，表明多视角一致性显著更强。
- **单目深度估计**：WVD 在 BONN 上全面最优（Rel 7.0, δ₁ 96.4）；在 NYU-v2 上优于除 DUSt3R-512 外的所有基线（DUSt3R-512 用了更高分辨率训练）。
- **视频深度估计**：ScanNet++ 上 AbsRel 5.0、δ₁.₀₃ 57.2，与 DUSt3R-512（4.9/60.2）表现相当，优于其余所有传统和学习方法。
- **消融实验**：去掉 XYZ 联合训练后，FID（15.8→18.3）、KPM（95.8→72.3）、FC（95.4→95.0）全部下降，**证明 XYZ 监督的有效性**。

## 四、资源与算力

- **模型规模**：扩散 Transformer 约 **20 亿参数**（2B），采用旋转位置嵌入和 RMSNorm。
- **训练配置**：学习率 3×10⁻⁴，AdamW 优化器，β=(0.99, 0.95)，训练 **100 万步**，有效 batch size 为 128。
- **算力消耗**：**64 块 A100 GPU，训练约两周**（约 336 GPU·天）。
- **说明**：论文明确给出了上述训练资源和时间信息。

## 五、实验数量与充分性分析

- **实验组数**：约 4 个主要任务 + 1 组消融实验，涵盖定量（表 1-3）和定性（图 4-6）评估。
- **充分性评价**：
  - **优点**：任务覆盖广（生成、深度估计、视频深度、可控生成），展现了统一框架的多任务能力；消融实验直接证明了核心设计（XYZ 监督）的必要性。
  - **不足**：
    - 对比方法数量在生成任务上偏少（仅对比 2 个视频生成模型），未与 CAT3D、Zero123++ 等多视角扩散模型直接对比。
    - 单目深度估计中，与 DUSt3R 的对比存在**分辨率不公平**问题（DUSt3R-512 为 512 分辨率，WVD 为 256），论文虽指出这一点，但仍影响结论的严谨性。
    - 相机可控视频生成仅有定性展示，缺少定量评估指标（如姿态精度、FID 等）。
    - 训练数据包含 DUSt3R 伪真值，与 DUSt3R 的对比存在一定"同源偏差"风险（但评测集不同，影响有限）。

## 六、主要结论与发现

1. **显式 3D 监督有效**：联合学习 XYZ 帧能为扩散模型提供显式 3D 一致性约束，显著提升多视角一致性（KPM +23.5 vs. RGB-only），同时不损害外观质量。
2. **统一框架的可行性**：一个预训练模型通过灵活的内绘策略，即可适配单图转 3D、多视图立体、相机可控视频生成等多种任务，验证了作为 3D 基础模型的潜力。
3. **XYZ 图像是一种优秀的 3D 表示**：与现有 2D Transformer 架构天然兼容，无需额外相机控制，避免了相机归一化等复杂问题，利于扩展到大规模数据。
4. **生成式深度估计的竞争力**：WVD 在多个深度估计基准上达到了与 SOTA 显式方法相当甚至更优的性能，且无需在深度基准上专门训练。

## 七、优点

- **方法设计新颖**：将 3D 几何显式编码为 XYZ 图像并融入扩散训练，简单有效，绕开了传统 3D 表示（如 NeRF、点云）与 2D 架构不兼容的难题。
- **架构友好**：可直接微调预训练的图像/视频扩散模型，无需重新设计 VAE 或架构，训练效率高。
- **免相机控制**：XYZ 图像已蕴含全局 3D 信息，无需额外的相机条件，减少了相机表示模糊性带来的扩展困难。
- **统一多任务能力**：以联合分布为基础，通过内绘策略实现多种生成和判别任务，体现了"基础模型"的设计理念。
- **有明确的应用价值**：后优化步骤（PnP/重投影优化）能进一步恢复相机姿态和深度，对下游任务友好。
- **消融实验设计清晰**：通过 RGB-only 对比清晰验证了 XYZ 监督的贡献。

## 八、不足与局限

- **仅限静态场景**：目前只在静态数据集上训练，无法处理动态场景（如人体运动、物体形变），限制了作为世界模型的适用范围。
- **无置信度建模**：缺少置信度图，对于无界、室外等大场景难以可靠处理，论文明确承认这一限制。
- **训练分辨率较低**：256×256 的分辨率限制了生成细节质量，在高分辨率场景（如 512/1024）下的表现尚未验证。
- **数据依赖问题**：大量训练数据使用 DUSt3R 生成的伪真值点云，伪真值的误差可能被模型"学习"并放大。
- **生成质量仍有差距**：单图转 3D 的 FID 仍落后于 CameraCtrl/MotionCtrl，说明显式 3D 约束在提升一致性时可能部分牺牲了帧内外观质量。
- **实验覆盖不足**：未在动态视频数据集上测试；缺少与更多最新多视角扩散模型（CAT3D 等）的直接对比；可控生成的定量评估缺失。
- **算力需求高**：2B 参数模型在 64×A100 上训练两周，对于一般研究团队的门槛较高。

（完）
