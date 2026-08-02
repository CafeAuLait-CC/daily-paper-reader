---
title: Controllable Human-centric Keyframe Interpolation with Generative Prior
title_zh: 基于生成先验的可控人体关键帧插值
authors: "Zujin Guo, Size Wu, Zhongang Cai, Wei Li, Chen Change Loy"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=OnViSNPqbT"
tags: ["query:dmg"]
score: 9.0
evidence: 将SMPL-X 3D人体引导信号融入扩散过程，实现可控的人体关键帧插值
tldr: 针对现有视频插值方法在复杂关节人体运动上生成效果不佳且控制有限的问题，本文提出PoseFuse3D-KI框架。它将3D人体引导信号（SMPL-X）整合进扩散过程，通过新颖的SMPL-X编码器将3D几何与形状聚合到2D潜空间，为插值提供丰富的空间结构线索。该方法在可控人体关键帧插值上生成更合理的结果，为扩散模型在3D人体运动合成中的应用提供了新方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 缺乏3D几何指导的插值难以生成合理的复杂关节人体运动，且控制有限。
method: 将SMPL-X编码器嵌入扩散模型，在潜空间聚合3D几何与形状，用于关键帧插值。
result: 与现有方法相比，生成的中间帧更自然，且能提供更多控制。
conclusion: 3D人体先验显著增强扩散模型在人体运动插值和合成中的表现。
---

## Abstract
Existing interpolation methods use pre‑trained video diffusion priors to generate intermediate frames between sparsely sampled keyframes. In the absence of 3D geometric guidance, these methods struggle to produce plausible results for complex, articulated human motions and offer limited control over the synthesized dynamics. In this paper, we introduce PoseFuse3D Keyframe Interpolator (PoseFuse3D-KI), a novel framework that integrates 3D human guidance signals into the diffusion process for Controllable Human-centric Keyframe Interpolation (CHKI). To provide rich spatial and structural cues for interpolation, our PoseFuse3D, a 3D‑informed control model, features a novel SMPL‑X encoder that encodes and aggregates 3D geometry and shape into the 2D latent conditioning space, alongside a fusion network that integrates these 3D cues with 2D pose embeddings. For evaluation, we build CHKI-Video, a new dataset annotated with both 2D poses and 3D SMPL‑X parameters. We show that PoseFuse3D-KI consistently outperforms state-of-the-art baselines on CHKI-Video, achieving a 9\% improvement in PSNR and a 38\% reduction in LPIPS. Comprehensive ablations demonstrate that our PoseFuse3D model improves interpolation fidelity.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **研究动机**：现有视频插值方法通常依赖预训练的视频扩散先验，在稀疏采样的关键帧之间生成中间帧。然而，这类方法缺乏 3D 几何引导，难以生成复杂关节人体运动的合理结果，同时对合成动态的控制能力有限。
- **整体含义**：针对上述问题，本文提出 **PoseFuse3D-KI**（可控人体关键帧插值框架），将 3D 人体引导信号（SMPL-X）注入扩散过程，以增强复杂人体运动的插值质量与可控性，属于“3D 先验 + 扩散模型”在人体运动合成中的重要探索。

## 2. 方法论

- **核心思想**：将 3D 人体几何信息（SMPL-X 参数）作为条件信号融入扩散模型的潜空间，为关键帧插值提供丰富的空间结构线索。
- **关键技术**：
  - **PoseFuse3D 控制模型**：一种 3D 信息驱动的控制网络，包含两个核心组件：
    - **SMPL-X 编码器**：将 3D 几何与形状编码并聚合到 2D 潜空间，为后续生成提供结构指导。
    - **融合网络**：将上述 3D 线索与 2D 姿态嵌入进行融合，形成统一的条件表征。
  - **与扩散过程集成**：通过条件注入方式，使扩散模型在生成中间帧时同时遵循 2D 姿态和 3D 人体几何约束。
- **算法流程（文字说明）**：输入稀疏关键帧 → 提取 2D 姿态嵌入 → 通过 SMPL-X 编码器处理 3D 参数 → 在潜空间内聚合 3D 几何/形状信息 → 融合网络与 2D 嵌入融合 → 作为条件输入扩散模型 → 迭代去噪生成中间帧。
- 论文未给出明确数学公式，重点在于网络架构和特征融合策略。

## 3. 实验设计

- **基准数据集**：作者构建了 **CHKI-Video**，这是一个同时标注 2D 姿态和 3D SMPL-X 参数的新数据集，专门用于评估可控人体关键帧插值任务。
- **对比方法**：与多种当前最先进的插值基线进行了比较（具体方法名称未在摘要中列出）。
- **评测指标**：PSNR 和 LPIPS 等图像相似度与感知质量指标。

## 4. 资源与算力

- 论文摘要和元数据中**未明确提及**使用的 GPU 型号、数量或训练时长，也未涉及推理成本。

## 5. 实验数量与充分性

- 摘要中提到的主要实验包括：
  - 在 CHKI-Video 上与 SOTA 基线的对比实验；
  - 针对 PoseFuse3D 模型的消融实验，验证其有助于提高插值保真度。
- **充分性评估**：由于可获取信息有限，无法判断实验规模是否足够覆盖多场景、多姿态类型。从报告的结果看，实验设计具备对比性和消融验证，但数据集多样性、泛化性测试等细节未知，客观性有待原文补充。

## 6. 主要结论与发现

- PoseFuse3D-KI 在 CHKI-Video 上**一致优于**现有 SOTA 基线：
  - PSNR 提升 **9%**；
  - LPIPS 降低 **38%**。
- 消融实验表明，引入 3D 人体先验（PoseFuse3D）能显著改善插值保真度，验证了 3D 先验在扩散模型人体运动插值中的有效性。

## 7. 优点

- **方法创新**：首次（或代表性）将 SMPL-X 3D 人体参数嵌入扩散模型潜空间，解决现有方法缺乏 3D 几何引导的问题。
- **可控性强**：3D 条件信号支持用户对合成动态进行更精细的控制。
- **性能显著**：PSNR 与 LPIPS 指标的提升幅度较大，具有很强的说服力。
- **数据贡献**：构建了带 2D 姿态和 3D SMPL-X 标注的新数据集 CHKI-Video，为后续研究提供基准。

## 8. 不足与局限

- **信息缺失**：论文摘要未提供模型复杂度、推理速度、训练资源等细节，无法评估实际应用成本。
- **数据范围**：仅提及一个数据集，未说明是否覆盖多种人体姿态、遮挡、复杂背景等挑战场景，泛化性存疑。
- **对比范围**：未列出具体基线方法，难以判断对比是否全面；同时消融实验的具体设置（如是否逐模块验证）未知。
- **角度局限**：主要面向人体关键帧插值，对其他对象或通用插值任务可能缺乏普适性。
- **可复现性**：由于缺少代码、超参数和训练细节，论文的可复现性尚待确认。

（完）
