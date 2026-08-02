---
title: Few-step Flow for 3D Generation via Marginal-Data Transport Distillation
title_zh: 基于边际数据迁移蒸馏的少步流3D生成
authors: "Zanwei Zhou, Taoran Yi, Jiemin Fang, Chen Yang, Lingxi Xie, Xinggang Wang, Wei Shen, Qi Tian"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/38394/42356"
tags: ["query:dmg"]
score: 8.0
evidence: 面向3D生成的基于流的少步蒸馏方法
tldr: 针对流式3D生成模型推理步数多的问题，本文提出MDT-dist少步蒸馏框架，通过边际数据迁移蒸馏学习速度匹配和速度蒸馏两个可优化目标，避免直接积分速度场。所提方法将多步采样压缩到少步，显著加速3D生成同时保持生成质量，扩展了一致性模型在3D领域的应用。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 流式3D生成模型推理需要几十步采样，而一致性模型等少步蒸馏方法在3D任务中尚未充分探索。
method: 通过边际数据迁移蒸馏，用速度匹配和速度蒸馏两个目标替换不可行的积分目标，实现少步生成。
result: 在3D生成任务上以少步采样获得与多步方法相当的质量，显著提升推理效率。
conclusion: 为流式3D生成提供了有效的少步蒸馏路径，缩小了2D与3D生成加速差距。
---

## Abstract
Flow-based 3D generation models typically require dozens of sampling steps during inference. Though few-step distillation methods, particularly Consistency Models (CMs), have achieved substantial advancements in accelerating 2D diffusion models, they remain under-explored for more complex 3D generation tasks. In this study, we propose a novel framework, MDT-dist, for few-step 3D flow distillation. Our approach is built upon a primary objective: distilling the pretrained model to learn the Marginal-Data Transport. Directly learning this objective needs to integrate the velocity fields, while this integral is intractable to be implemented. Therefore, we propose two optimizable objectives, Velocity Matching (VM) and Velocity Distillation (VD), to equivalently convert the optimization target from the transport level to the velocity and the distribution level respectively. Velocity Matching (VM) learns to stably match the velocity fields between the student and the teacher, but inevitably provides biased gradient estimates. Velocity Distillation (VD) further enhances the optimization process by leveraging the learned velocity fields to perform probability density distillation. When evaluated on the pioneer 3D generation framework TRELLIS, our method reduces sampling steps of each flow transformer from 25 to 1–2, achieving 0.68s (1 step x2) and 0.94s (2 steps x2) latency with 9.0x and 6.5x speedup on A800, while preserving high visual and geometric fidelity. Experiments demonstrate that our method significantly outperforms existing CM distillation methods, and enables TRELLIS to achieve superior performance in few-step 3D generation.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究背景**：流式（flow-based）3D生成模型虽然能生成高质量的3D资产，但推理时需要数十步迭代采样，计算开销大，难以满足大规模3D内容生成、具身智能仿真、实时交互编辑等实际应用需求。
- **现有方法的不足**：少步蒸馏技术（尤其是一致性模型CMs）在2D扩散模型加速上取得了显著进展，但扩展到3D生成领域仍处于探索阶段。现有唯一的3D相关工作FlashVDM基于PCM方法，且只能生成形状（无外观）。3D生成比2D具有更大挑战：3D表示（网格、3D高斯）离散且稀疏、几何纹理细节更丰富、潜在空间维度更高。
- **核心问题**：如何在保持3D生成质量的前提下，将流式3D生成模型的推理步数从25步压缩到1-2步，实现高效少步生成。
- **整体含义**：本文提出MDT-dist框架，通过从“边际数据迁移”（Marginal-Data Transport）这一主要目标出发，设计两个可优化目标——速度匹配（VM）与速度蒸馏（VD），直接替代一致性模型中依赖相邻时间步一致性约束的间接学习方式，实现了3D流模型的高效少步蒸馏，填补了3D生成加速领域的空白。

## 2. 论文提出的方法论

- **核心思想**：直接学习“边际数据迁移”——将任意扩散时间步 t 的边际分布 qt 直接输送到数据分布 qdata，即通过训练 ϕθ 让其在一步内完成生成。
- **主要目标问题**：直接优化 marginal-data transport 需要对速度场做积分 ∫₀ᵗv_pretrain(xτ,τ)dτ，该积分无法实现（intractable），因此需将目标从“传输层面”等价转化为可操作的层面。
- **速度匹配（Velocity Matching, VM）**：
  - 对主要目标关于 t 求导，将传输损失转化为对速度场的监督。
  - 目标函数为 min E[‖ϕθ(xt,t) + t·dϕθ(xt,t)/dt − v_pretrain(xt,t)‖²]。
  - 导数项离散近似为 (1/Δt)(ϕθ(xt,t) − ϕθ(xt−Δt, t−Δt))，其中 xt−Δt = xt − v_pretrain(xt,t)Δt，Δt=1e-2。
  - 训练时对导数项停止梯度传播，避免二阶导计算。
  - **局限**：梯度估计存在偏差（biased）。
- **速度蒸馏（Velocity Distillation, VD）**：
  - 将主要目标等价转换为学生边际分布 ptθ 与教师边际分布 qt 之间的KL散度最小化。
  - 用学生速度场 uθ 替代 −∇log ptθ（学生score），用教师速度场 v_pretrain 替代 −∇log qt（教师score），进行概率密度蒸馏。
  - 相当于间接监督：以速度差作为分布差异的度量，通过更新 xt 来优化 ϕθ。
  - 弥补VM的偏差问题，增强少步生成能力。
- **联合优化**：最终损失 L = LVM + λLVD，论文中λ=1.0。
- **与现有方法的区别**：
  - 与CM/PCM/sCM相比：无需一致性约束，直接学习边际数据迁移，更直接、更稳定。
  - 与MeanFlow相比：不需要两个时间变量输入，适合蒸馏预训练流模型。
  - 与SDS/VSD相比：SDS用噪声作student score导致Dirac分布估计；VSD需额外微调一个扩散模型ϵϕ，增加内存开销和学习误差。本文仅用一个模型同时充当生成器和分布度量器，低开销且更准确。

## 3. 实验设计

- **训练数据集**：约50万个3D资产，来自Objaverse (XL)、ABO、3D-FUTURE和HSSD数据集。
- **评估数据集**：Toys4k数据集的全部3,218个3D资产。
- **评估基准**：基于TRELLIS框架（SLAT结构化潜变量表示，包含稀疏体素和特征，两个流transformers分别生成坐标与特征）。
- **对比方法**：
  - 非扩散方法：LGM（大多视图高斯模型）。
  - 非蒸馏3D扩散方法：3DTopia-XL、Ln3Diff、教师模型TRELLIS。
  - 蒸馏3D扩散方法：FlashVDM（评估几何指标ULIP I，因其不生成外观）。
  - 一致性模型方法：CM（一致性模型）、PCM（相位一致性模型）、sCM（连续时间一致性模型）。
- **评估指标**：
  - 外观质量：FD_inception、FD_dinov2。
  - 几何质量：ULIP-I。

## 4. 资源与算力

- 论文中提及推理时间在NVIDIA A800 GPU上测量，未明确说明训练所用GPU数量、型号或训练时长。
- 推理端数据：在A800上，1步×2（两个transformer各1步）推理时间0.68s（9.0×加速）；2步×2推理时间0.94s（6.5×加速）；教师模型TRELLIS为25步×2，推理时间6.1s。
- **注意**：论文未公开训练阶段的具体算力配置（如GPU型号、数量、训练时长等）。

## 5. 实验数量与充分性

- **主要实验组**：
  1. 与LGM、3DTopia-XL、Ln3Diff、TRELLIS、FlashVDM的量化对比（Table 1）。
  2. 与CM、PCM、sCM的量化对比（Table 2）。
  3. 定性可视化对比（图2-图4）。
  4. 消融实验：单独VM、VM+VD联合（Table 3，图5）。
- **充分性分析**：
  - 对比方法覆盖了非扩散、非蒸馏扩散、蒸馏扩散和一致性模型多类方法，对比较为全面。
  - 消融实验验证了两个损失函数各自的贡献与互补性，设计合理。
  - 有量化指标与定性可视化双重视角的验证。
  - 也包含1步和2步两种推理配置的效果对比。
  - 总体上实验数量尚可、覆盖面较广，**但**FlashVDM仅比较了几何指标（因其无法生成外观），外观对比上存在不完整的部分；ULIP-I和FD指标的可靠性依赖具体评估协议，论文未充分讨论潜在偏差。

## 6. 论文的主要结论与发现

- MDT-dist可将TRELLIS两个流transformers的采样步数从各25步（共50步）降低到各1-2步（共2-4步），在保持高质量的前提下实现0.68s/0.94s的推理延迟。
- 在以FD_inception、FD_dinov2（外观）和ULIP-I（几何）为指标的评测中，显著优于CM、PCM、sCM等一致性模型蒸馏方法。
- 在几何指标上超越FlashVDM，同时在TRELLIS框架上实现少数步采样下与教师模型相近的质量。
- 速度匹配（VM）能显著减少多余的几何生成、修复缺失结构；速度蒸馏（VD）进一步消除多余几何并完善剩余不完整区域；二者联合优化效果最佳。
- 该方法提供了比一致性模型更直接、更稳定的一条3D少步生成蒸馏路径，缩小了2D与3D生成加速的差距。

## 7. 优点

- **方法创新性**：不依赖一致性约束，从边际数据迁移这一更根本的视角出发设计蒸馏目标，方法推导有理论支撑（误差界证明）。
- **目标分解巧妙**：将不可行的积分目标等价转化为速度层面（VM）和分布层面（VD）两个可操作的目标，两者互补，分别提供稳定梯度和增强的少步性能。
- **低开销**：相比VSD等方案，不需要额外训练扩散模型作为分布度量器，节省内存和计算开销。
- **实用性强**：在SOTA框架TRELLIS上实现有效的少步加速，推理延迟大幅缩短，且有完整的代码和项目页面开源。
- **实验覆盖较全面**：与多种类型方法（非扩散、非蒸馏、蒸馏、一致性模型）对比，并完成消融验证。

## 8. 不足与局限

- **训练成本高**：少步蒸馏训练需要大量条件图像和高质量几何数据，而高质量3D几何数据稀缺且昂贵，蒸馏训练开销大。作者提出可能的解决方案是只依赖条件图像、移除几何数据依赖，从而利用互联网上海量图像扩展蒸馏规模。
- **梯度偏差问题**：VM的根本缺陷——网络输出的连续和离散形式均无法正确反向传播，导致梯度估计存在偏差，需借助VD进行弥补，本质上增加了一个额外的优化环节。
- **实验范围的局限**：
  - 仅在一个3D生成框架（TRELLIS）上验证，缺乏在其他3D生成框架（如Direct3D、Hunyuan3D等）上的泛化验证。
  - 与FlashVDM的对比仅限几何指标，无法比较外观质量。
  - 评估仅基于Toys4k数据集，数据分布多样性有限。
- **适配约束**：该方法基于预训练流模型进行蒸馏，若没有可用的高质量预训练模型，蒸馏无从谈起。
- **超参数依赖**：λ超参数（设为1.0）、Δt（设为1e-2）等缺乏敏感性分析讨论。
- **未报告训练算力细节**：论文未说明训练所需的GPU数量、型号和训练时长，复现成本难以准确评估。

（完）
