---
title: "Mean Flow Distillation: Robust and Stable Distillation for Flow Matching Models"
title_zh: 均值流蒸馏：面向流匹配模型的稳健稳定蒸馏方法
authors: "An Zhao, Shengyuan Zhang, Zhongjian Sun, Yixiang Zhou, Zejian Li, Ling Yang, Tianrun Chen, Lingyun Sun"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8a2564e88694d94f48baf55728284cc4a5c72cb3.pdf"
tags: ["query:dmg"]
score: 8.0
evidence: 面向流匹配生成模型的蒸馏方法，用于降低采样开销
tldr: 流匹配依赖ODE迭代采样，计算开销大，而现有蒸馏方法训练不稳定且生成质量下降。本文提出专门针对流匹配模型的均值流蒸馏（MFD），利用流的内在几何结构，并在理论上证明其相当于时间低通滤波器，能抑制高频误差。MFD在保持稳定训练的同时提升了生成质量，为流匹配的实时应用提供了高效蒸馏方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 流匹配采样开销大，现有蒸馏方法不稳定、方差高、质量下降。
method: 提出面向流匹配的均值流蒸馏，利用时间低通滤波特性抑制高频误差。
result: MFD训练更稳定，生成质量优于现有蒸馏方法，并显著降低采样代价。
conclusion: 该工作为流匹配模型提供了稳健高效的蒸馏框架，助力实时生成场景应用。
---

## Abstract
Flow Matching models have demonstrated strong performance across a wide range of generative tasks.
However, their reliance on ODE-based iterative sampling incurs substantial computational overhead, which limits their applicability in real-time scenes. 
While distillation is a promising solution, existing approaches largely borrow from diffusion-based score matching, often failing to exploit the intrinsic geometric structure of flows and suffering from training instability, high variance, and degraded generation quality.
In this paper, we propose Mean Flow Distillation (MFD), a novel distillation framework tailored for flow matching models.
We theoretically demonstrate that MFD acts as a temporal low-pass filter, effectively suppressing the high-frequency optimization noise inherent in variational score distillation (VSD) while ensuring global trajectory consistency. We further prove the Mean Flow Matching Theorem, establishing that matching expected average velocities is sufficient for strict distribution alignment. Empirically, on challenging high-dimensional manifolds including 4D occupancy forecasting and text-to-image generation, MFD achieves state-of-the-art performance, enabling high-fidelity single-step generation.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **背景**：流匹配（Flow Matching）模型在各类生成任务中表现优异，但其依赖基于 ODE 的迭代采样，导致计算开销巨大，难以应用于实时场景。
- **核心问题**：现有的蒸馏方法大多直接借鉴扩散模型中的得分匹配思想，未充分利用流匹配模型内在的几何结构，导致训练不稳定、方差高、生成质量下降。
- **整体含义**：本文旨在为流匹配模型设计一种专门、稳健且高效的蒸馏框架，在保持训练稳定性的同时，实现高保真度的单步生成，从而推动流匹配在实时生成任务中的落地。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **方法名称**：均值流蒸馏（Mean Flow Distillation, MFD）。
- **核心思想**：
  - 利用流匹配模型的内在几何结构，而非简单移植扩散模型的蒸馏策略。
  - 通过对流的速度场（velocity field）进行“均值”匹配，实现对整体轨迹的一致性约束。
- **关键技术细节**：
  - **时间低通滤波特性**：论文从理论上证明 MFD 等价于一个时间域低通滤波器，能够有效抑制变分得分蒸馏（VSD）中固有的高频优化噪声。
  - **全局轨迹一致性**：相比局部逐点匹配，MFD 强调整条生成轨迹上的期望一致性，避免单步蒸馏时轨迹漂移。
  - **均值流匹配定理**：论文证明了一个理论结果——只要配准期望的平均速度，就足以实现严格的分布对齐。这为“用均值速度替代瞬时速度”的做法提供了理论依据。
- **算法流程（文字说明）**：
  - 训练阶段：对预训练的流匹配模型，沿时间轴采样多个速度场，计算其期望均值，作为蒸馏目标。
  - 学生模型以单步（或少量步数）方式直接预测该均值速度场，并通过分布匹配损失进行优化（而不是直接回归瞬时速度）。
  - 推理阶段：学生模型仅需一次前向传播即可生成样本，大幅降低采样成本。

## 3. 实验设计：使用的数据集 / 场景、基准与对比方法
- **评测场景1**：4D 占用预测（4D occupancy forecasting）——高维流形上的时序预测任务。
- **评测场景2**：文生图（text-to-image generation）——大规模生成任务。
- **基准**：以流匹配模型为教师模型，评测学生模型的单步生成质量。
- **对比方法**：论文提及与变分得分蒸馏（VSD）为代表的一类扩散蒸馏方法进行对比，但摘要中未列出具体方法名称（如 Score Distillation Sampling、Consistency Distillation 等）。需要从全文获取完整对比列表。

## 4. 资源与算力
- 论文摘要和元数据中**未明确说明**训练所使用的 GPU 型号、数量、训练时长等算力信息。
- 仅在实验部分可能有所涉及，但在给定内容中无法获取。
- 若需要评估方法的实际成本，建议查阅论文正文的实验设置章节。

## 5. 实验数量与充分性
- 从摘要看，实验覆盖**两个高维场景**：4D 占用预测和文生图。
- 论文提到 MFD 在两个场景上均取得**最先进性能**（state-of-the-art），并支持高保真单步生成。
- 但**是否有消融实验**（如对均值窗口长度、不同时间采样策略、损失权重等）在摘要中未体现。
- 整体来看，两个任务的覆盖面较广，但**实验数量相对有限**。对于蒸馏方法而言，通常还需要：
  - 多步采样性能对比（如 2 步、4 步）；
  - 不同教师模型（如不同规模的流匹配模型）的泛化性实验；
  - 与其他蒸馏方法（如一致性蒸馏、对抗蒸馏）的全面比较。
- 结论的充分性取决于正文中是否有更详细的消融和对比。仅从摘要看，证据还不够全面。

## 6. 论文的主要结论与发现
- **理论发现**：MFD 是一种时间低通滤波器，可抑制 VSD 中的高频优化噪声，从而解决训练不稳定的问题。
- **理论保证**：提出并证明了均值流匹配定理，说明期望平均速度匹配足以实现严格分布对齐。
- **实验结论**：MFD 在训练稳定性、生成质量上优于现有蒸馏方法，并显著降低采样代价，能实现高保真度的单步生成。
- **应用价值**：为流匹配模型的实时部署提供了稳健高效的蒸馏框架。

## 7. 优点：方法与实验设计上的亮点
- **方法创新性强**：专门针对流匹配模型设计，而非简单迁移扩散蒸馏策略；利用流的内在几何结构，具有较好的理论动机。
- **理论支撑扎实**：
  - 从频域角度解释蒸馏稳定性问题，视角新颖；
  - 均值流匹配定理为算法提供了严格的理论保障，增强了方法的可信度。
- **训练稳定性提升**：明确针对 VSD 不稳定、方差大的缺陷，提出低通滤波解决方案，逻辑清晰。
- **应用场景具有挑战性**：选择 4D 占用预测和文生图两个高维、复杂分布任务进行验证，能体现方法的实际能力。

## 8. 不足与局限
- **实验细节缺失**：给定材料中未给出具体量化指标（如 FID、精度、召回率等），无法客观判断“最先进”的程度。
- **对比方法有限**：仅提及与 VSD 类方法对比，未说明是否涵盖当前主流的扩散蒸馏（如 Consistency Distillation, Rectified Flow, Adversarial Distillation）等强基线。
- **消融研究未知**：未明确是否验证了均值时间窗口大小、损失函数形式、不同采样步数等关键因素对性能的影响。
- **算力与效率报告不足**：未报告训练资源、训练时间、收敛速度等，难以评估实际部署成本。
- **泛化性存疑**：仅两个场景（虽然高维）不足以全面证明方法在各类流匹配任务（如音频、视频、3D）上的普适性。
- **理论假设限制**：均值流匹配定理可能依赖于某些理想条件（如速度场的连续性、分布满足特定光滑性），在实际离散化采样中可能不完全成立，正文需给出详细假设和证明。
- **单步生成的固有瓶颈**：即使蒸馏成功，单步生成在极复杂分布上可能仍存在质量上限，需要与多步生成或扩散迭代做比较。

（完）
