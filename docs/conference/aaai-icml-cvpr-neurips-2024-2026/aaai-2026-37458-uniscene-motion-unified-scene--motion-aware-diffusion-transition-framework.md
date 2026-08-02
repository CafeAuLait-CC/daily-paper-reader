---
title: "UniScene-MoTion: Unified Scene & Motion-aware Diffusion Transition Framework"
title_zh: UniScene-MoTion：统一场景与运动感知的扩散转场框架
authors: "Rui Jiang, Chongmian Wang, Xinghe Fu, Yehao Lu, Teng Li, Xi Li"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37458/41420"
tags: ["query:dmg"]
score: 7.0
evidence: 结合深度感知3D推理的扩散模型用于尺度感知视频转场
tldr: 视频转场需要保持时间连贯性，但现有方法常依赖手工效果或相对尺度轨迹，缺乏物理结构。本文提出UniScene-MoTion，将深度感知的3D推理融入扩散生成流程，利用单图深度预测将相机运动与公制尺度几何对齐，并通过双向条件控制模块和渐进训练策略减少对精确相机输入的依赖，从而产生物理一致的视频转场。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 视频转场缺乏物理结构感知，导致时间连贯性差。
method: 整合单图深度预测与扩散生成，加入双向条件控制模块和对齐相机运动。
result: 生成的视频转场物理一致，对相机输入依赖降低。
conclusion: 3D推理显著提升扩散视频转场的物理合理性和稳健性。
---

## Abstract
Video transitions are critical for ensuring temporal coherence in edited media, yet existing methods often rely on handcrafted effects or relative-scale trajectories that fail to capture the physical structure of real-world scenes. In this work, we introduce a scale-aware video transition framework that explicitly incorporates depth-aware 3D reasoning into a diffusion-based generation pipeline. Built upon a powerful I2V foundation, our method leverages single-image depth prediction to align camera motion with metric-scale geometry, enabling physically consistent transitions. To reduce reliance on precise camera inputs, we propose a bidirectional conditional control module and a progressive training strategy with conditional dropout, enhancing generalization to loosely specified or missing camera trajectories. Extensive experiments demonstrate that our approach achieves state-of-the-art performance, delivering realistic, geometrically coherent transitions across diverse scenes and applications with minimal input guidance.

---

## 论文详细总结（自动生成）

# UniScene-MoTion 论文详细总结

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：视频转场（Video Transition）是视频编辑中保证时间连续性和叙事连贯性的关键环节，但现有方法存在明显的物理结构感知缺失问题。
- **现有方法的不足**：
  - **传统方法**（硬切、溶解、擦除等）：简单高效，但无法捕捉复杂场景的几何结构与运动动力学，容易产生感知不连续和视觉流不自然。
  - **基于深度学习的语义辅助方法**：引入了语义级约束，但在涉及相机运动的真实场景中，仍缺乏对场景几何、3D物体位置和动态运动的准确理解，容易出现空间错位。
  - **文本驱动的相机控制方法**（如 I2VGen、EasyAnimate 等）：直观易用，但在需要精确控制相机参数（位置、尺度、复杂轨迹）时表达能力不足。
  - **轨迹引导的方法**（如 MotionCtrl、CameraCtrl 等）：存在两个关键局限：
    1. 依赖**相对尺度**相机轨迹，未与真实世界的公制尺度（metric scale）对齐，导致对场景整体物理尺度缺乏感知，易产生物体异常缩放、前后景错位等视觉不一致问题；
    2. 难以平衡生成质量与易用性——精确相机轨迹难以获取，而纯文本引导又缺乏精细控制能力。
- **核心洞察**：深度信息（depth）本身携带绝对尺度，可以作为显式先验，将相机运动与真实场景几何对齐，从而获得物理一致的转场效果。同时，深度先验为用户提供了一个更结构化、可解释、可控制的交互空间。
- **整体含义**：本文提出一个**尺度感知（scale-aware）的视频转场框架**，将公制尺度轨迹推理融入扩散生成管线，仅需单图深度预测即可实现物理一致的相机转场，并显著降低对精确相机输入的依赖。

## 2. 提出的方法论

### 2.1 核心思想

将深度感知的3D推理显式地融入基于扩散模型的图像到视频（I2V）生成框架中，通过**公制尺度对齐（metric-scale alignment）** 的相机轨迹作为物理先验来引导生成，使相机运动符合真实场景的几何结构。同时，设计轻量级条件控制网络与渐进式训练策略，兼顾生成质量与易用性。

### 2.2 三个关键技术模块

#### （1）公制尺度数据对齐（Metric-Scale Data Alignment）

- **动机**：SfM（如 COLMAP）得到的相机轨迹是相对尺度的，缺乏真实世界的绝对尺度信息。
- **实现流程**：
  1. 对视频序列逐帧进行**单目公制深度预测**（如 Metric3D），得到公制尺度视差图 {D_abs^i}；
  2. 从 SfM 重建中获得相对尺度视差 {D_rel^i}；
  3. 求解全局场景级尺度因子 γ，最小化公制视差与相对视差之间的差异。
- **关键公式**：
  - 优化目标：γ = argmin_γ Σᵢ ‖D_absⁱ − γ·D_relⁱ‖²₂
  - 闭式最小二乘解：γ* = (Σᵢ D_absⁱ·D_relⁱ) / (Σᵢ (D_relⁱ)²)
  - 校准后的相机位姿：E = [R, γ*·t] ∈ R³ˣ⁴
- **工程细节**：丢弃上下 5% 的极端视差值（对应噪声较大的近/远深度区域），仅保留置信度前 50% 的像素，确保尺度对齐的稳定性。深度图转为视差图（disparity，即深度的倒数），以稳定远场区域的数值行为并增强对近场几何的敏感度。

#### （2）先验引导的双向控制器网络（Prior-Guided Bidirectional Controller Network）

- **结构基础**：受 ControlNetXS 启发，在 DiT（Diffusion Transformer）架构中设计轻量级可插拔控制网络。
- **关键设计**：
  - **文本解耦**：在控制路径的专用控制层中，显式排除文本嵌入（T_text）的直接输入，确保控制层的特征变换主要由控制信号驱动，避免文本干扰控制；
  - **双向信息流**：控制层输出 F'_control 注入主 DiT 解码路径，与 DiT 层隐藏状态 H 交互；同时隐藏状态 H 也作为控制层的输入参与融合；
  - **Zero Up/Down Proj 模块**：在控制层的起始和结束位置融合 F_control 与 H，映射到相同维度；参数零初始化以保证训练稳定性。
- **控制层公式**：F'_control = G(F_control, H, T_timestep)
- **优势**：实现控制信号对生成的精确引导，同时文本提示保留对整体内容和风格的贡献，降低网络复杂度与可训练参数量。

#### （3）渐进式训练与动态条件丢弃（Progressive Training with Dynamic Dropout）

采用三阶段渐进式训练管线：

| 阶段 | 分辨率 | 输入条件 | 目的 |
|------|--------|----------|------|
| 第一阶段 | 81×224×448（低分辨率） | 起始帧 + 相机轨迹 + 文本提示 | 学习从单一视觉锚点生成合理相机运动与场景动态；**引入视差视频辅助监督** |
| 第二阶段 | 引入结束帧 x_end | 起始帧 + 结束帧 + 相机轨迹 + 文本 | 提供更强的时间约束，学习内容保持的时空插值 |
| 第三阶段 | 81×768×1360（高分辨率） | 随机丢弃相机轨迹条件 | 增强对不完整或缺失条件下生成的鲁棒性 |

- **流程匹配损失（Flow Matching Loss）**：L_FM = E[‖dx(t)/dt − v_θ(x(t), t, C)‖²]，其中 x(t) = (1−t)x₀ + tx₁ 为干净数据与噪声之间的线性插值路径。
- **视差辅助监督（Disparity Supervision）**：L_disp = (1/THW) Σₜ ‖D̂ₜ − D_GTₜ‖²₂，将控制网络最终输出特征通过线性头 H_disp 预测视差图，与标注视差视频计算 MSE 损失，增强模型的 3D 运动推理能力。
- **条件丢弃机制**：ĉᵢ = cᵢ（以概率 1−pᵢ）+ 0（以概率 pᵢ），对相机轨迹条件实施随机丢弃，提高模型对粗略或无轨迹输入的鲁棒性。

## 3. 实验设计

### 3.1 数据集

| 数据集 | 规模 | 内容覆盖 |
|--------|------|----------|
| RealEstate10K | 500 个视频片段 | 广泛的真实室内外环境，多样的相机运动和几何结构 |
| Pexels（补充） | 50 个高质量视频片段 | 自然景观、室内外环境、人像、烹饪场景、艺术风格等；涵盖相机运动、物体动态、人物动作、面部表情变化等 |

### 3.2 评估指标

- **图像质量**：LPIPS、FID（Fr ́echet Inception Distance）
- **视频质量**：FVD（Fr ́echet Video Distance）、FVMD（Fr ́echet Video Motion Distance，更强调运动一致性）
- **多维评估**：VBench（包含主题一致性 SC、背景一致性 BC、运动平滑度 MS、动态程度 DD、美学质量 AQ、图像质量 IQ 等维度）

### 3.3 对比方法

- **转场专用方法**：SEINE
- **扩散生成方法**：DynamiCrafter、TRF、GI（Generative Inbetweening）、FCVG、VideoX-Fun（1.3B/14B）、FLF2V

### 3.4 实验设置

- 采用两种帧间隔设置（23 帧和 79 帧）评估不同运动条件下的性能；
- 多个分辨率设置对比（如 16×768×1344、25×768×1344、81×768×1360 等）。

## 4. 资源与算力

- **GPU**：8 张 NVIDIA A100（80GB）
- **训练迭代**：70k iterations
- **优化器**：AdamW，学习率 1×10⁻⁴，β₁=0.9，β₂=0.999
- **基础模型**：CogVideoX1.5-5B I2V（冻结）
- **其他说明**：论文未明确说明总训练时长（天数/小时），也未提供推理阶段的算力开销细节。每个训练分辨率阶段使用内存允许的最大 batch size。

## 5. 实验数量与充分性

### 实验构成

1. **主实验（两个数据集）**：在 RealEstate10K 和 Pexels 上进行定量评估，对比 7 种以上 SOTA 方法，覆盖多个指标（LPIPS、FID、FVD、FVMD、VBench）。
2. **定性对比**：多个挑战性场景的可视化比较（第一帧→中间帧→最后一帧）。
3. **消融实验（两组）**：
   - w/o Bidirection：去除双向交互特征注入；
   - w/o Progressive：去除渐进式训练策略（直接训练首尾帧对，无 L_disp 监督）。
4. **应用展示**：粗粒度轨迹引导、跨视频片段拼接等。

### 充分性评估

- **优点**：
  - 定量实验覆盖两个不同来源的数据集，兼顾了场景多样性；
  - 对比方法较全面，涵盖早期和近期方法，且包含不同参数规模的模型（1.3B、5B、14B）；
  - 使用多种评估指标，包括近期提出的 FVMD 和 VBench。
- **不足**：
  - **消融实验仅有两组**，未对以下组件分别消融：尺度对齐模块、视差辅助监督损失、条件丢弃策略、文本解耦机制等，无法确定各组件各自的贡献大小；
  - 消融实验仅报告了 VBench 指标的少量维度，未报告 LPIPS/FID/FVD/FVMD 等核心指标，说服力有限；
  - 未报告在 Pexels 上的消融结果，无法验证结论在不同数据集上的一致性；
  - Pexels 仅 50 个视频片段，规模偏小，统计显著性存疑；
  - 未提供用户研究（user study）来验证主观视觉质量；
  - 论文也承认这些指标无法精确评估生成视频的时间稳定性，需要人工观看补充视频判断，暗示评估体系存在局限。

## 6. 主要结论与发现

1. **尺度先验有效**：将深度感知的3D推理和公制尺度相机轨迹纳入扩散生成管线，显著提升视频转场的物理合理性、空间连续性和运动真实感。
2. **SOTA 性能**：在 RealEstate10K 和 Pexels 两个数据集上，UniScene-MoTion 在大多数指标上优于所有对比方法。例如在 Pexels 上 FID 从 9.583 降至 8.964，FVD 从 308.298 降至 274.478（相比第二名）。
3. **长帧间隔鲁棒性**：即使在帧间隔为 79 的情况下，仍能保持最佳整体性能，说明方法对大运动/大语义差距场景具有良好鲁棒性。
4. **易用性提升**：通过条件丢弃训练，模型对粗略或不完整相机输入的容忍度显著提高，缩小了"高质量生成"与"易用性"之间的鸿沟。
5. **消融验证**：双向交互机制和渐进式训练策略均对最终性能有正向贡献。

## 7. 方法优点

- **物理一致性**：首次将公制尺度对齐的相机轨迹显式融入视频转场扩散生成，解决相对尺度轨迹缺乏物理意义的核心问题，生成结果更符合真实 3D 场景几何。
- **尺度对齐的鲁棒设计**：使用视差（disparity）而非原始深度进行对齐，数值更稳定；丢弃极端值和低置信度像素提高对齐鲁棒性；闭式最小二乘解简单高效。
- **轻量级可插拔设计**：控制器网络基于 ControlNetXS 思想，参数量少、即插即用，基础扩散模型保持冻结，方便适配不同 I2V 基座。
- **双向信息融合**：文本解耦 + 双向交互的设计兼顾了控制精度与语义/风格保持，是一个值得借鉴的架构创新。
- **渐进式训练策略**：从低分辨率单独条件到高分辨率多条件 + 条件丢弃的三阶段设计，兼顾了训练稳定性与实际部署中的灵活性。
- **广泛的适用性**：除视频转场外，还展示了视频循环（looping）、插值、自动转场、跨场景拼接等多种扩展应用。
- **多维度评估**：采用传统指标（LPIPS/FID/FVD）与近期新指标（FVMD/VBench）结合，评估视角较为全面。

## 8. 不足与局限

- **消融深度不足**：
  - 仅 2 组消融实验，无法单独验证尺度对齐、视差监督、条件丢弃等关键组件的各自贡献；
  - 消融仅报告 VBench 部分维度，未报告 FID/FVD/LPIPS 等直接生成质量指标；
  - 未在多个数据集上做消融验证，结论泛化性存疑。
- **评估指标固有局限**：
  - 论文自述现有所有指标均无法精确评估生成视频的时间稳定性，这削弱了定量结论的可靠性；
  - 未提供用户研究，缺少对主观视觉体验的直接评估。
- **数据集规模与多样性**：
  - Pexels 测试集仅 50 个片段，样本量较小；
  - 训练数据的规模、来源和预处理细节未充分披露，影响可复现性。
- **对深度预测的依赖**：方法依赖单目公制深度估计的准确性，在极端场景（遮挡、透明物体、低纹理区域等）下深度预测的误差可能传导至尺度对齐和最终生成结果，但论文未讨论这一失败模式。
- **参数与数据规模未充分讨论**：未提供完整的模型参数量对比、推理时间、显存占用等信息，无法完整评估其实际部署成本。
- **对比公平性问题**：不同方法在帧数、分辨率上不完全一致（如 SEINE 为 16 帧、Ours 为 25/81 帧），一定程度影响指标比较的公平性，论文对此未作深入讨论。
- **应用边界**：论文展示了视频循环和插值等应用，但缺乏对失败案例的讨论，限制了对其适用边界的认知。

## 补充说明

- 本文为 AAAI-26 接收论文（The Fortieth AAAI Conference on Artificial Intelligence, AAAI-26），发表在 AAAI 2026 会议卷上。

（完）
