---
title: Riemannian MeanFlow for One-Step Generation on Manifolds
title_zh: 黎曼均值流：流形上的一步生成
authors: "Zichen Zhong, Haoliang Sun, Yukun Zhao, Yongshun Gong, Yilong Yin"
date: 2026-04-30
pdf: "https://openreview.net/pdf/81634e766612d082f2c40e6d5d51541e08a66c1f.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 黎曼流形上的 Flow Matching 生成建模
tldr: 针对流匹配在黎曼流形上生成仍需数值积分概率流 ODE 的问题，本文提出黎曼均值流（RMF），通过平移定义平均速度场并推导黎曼均值流恒等式，利用 log-map 切空间表示实现内在监督，避免轨迹模拟和繁重几何计算。同时将目标分解为两项并采用冲突感知多任务学习稳定优化。实验表明该方法支持一步生成并保持流形几何一致性，为流匹配在流形数据上的应用提供了高效新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有流匹配在黎曼流形上生成时采样仍需数值积分 ODE，计算代价高且难以一步生成。
method: 提出黎曼均值流，用平行传递定义平均速度场，推导黎曼均值流恒等式，并结合 log-map 切空间表示与冲突感知多任务学习。
result: 该方法在多种流形数据集上实现一步生成，避免了轨迹模拟，同时保持几何一致性。
conclusion: 为流形数据上的流匹配生成提供了高效、稳定的一步生成框架，拓展了流匹配的适用场景。
---

## Abstract
Flow Matching enables simulation-free training of generative models on Riemannian manifolds, yet sampling typically still relies on numerically integrating a probability-flow ODE. We propose Riemannian MeanFlow (RMF), extending MeanFlow to manifold-valued generation where velocities lie in location-dependent tangent spaces. RMF defines an average-velocity field via parallel transport and derives a Riemannian MeanFlow identity that links average and instantaneous velocities for intrinsic supervision. We make this identity practical in a log-map tangent representation, avoiding trajectory simulation and heavy geometric computations. For stable optimization, we decompose the RMF objective into two terms and apply conflict-aware multi-task learning to mitigate gradient interference. RMF also supports conditional generation via classifier-free guidance. Experiments on spheres, tori, SO(3), and SE(3) demonstrate competitive one-step sampling with improved quality–efficiency trade-offs and substantially reduced sampling cost.

---

## 论文详细总结（自动生成）

# 论文《黎曼均值流：流形上的一步生成》详细总结

## 1. 核心问题与整体含义（研究动机和背景）
- **研究背景**：Flow Matching（流匹配）作为一种生成建模方法，虽然已在黎曼流形上实现了免模拟训练（simulation-free training），但其采样过程仍然依赖对概率流 ODE（Probability-Flow ODE）进行数值积分。这带来了较高的计算代价，也难以实现一步生成。
- **核心问题**：流形数据（如球面、旋转群、刚体变换群等）中的速度向量存在于位置相关的切空间中，如何设计一个能直接一步生成、无需轨迹模拟的流匹配方法是一个重要挑战。
- **论文目标**：提出黎曼均值流（Riemannian MeanFlow, RMF），将均值流（MeanFlow）扩展到流形值生成场景，支持一步采样并显著降低采样成本，同时保持流形几何一致性。这项工作为流匹配在流形数据上的应用提供了新的高效范式。

## 2. 方法论：核心思想、关键技术细节与算法流程
- **核心思想**：通过平行传递（parallel transport）在流形上定义“平均速度场”，并推导出黎曼均值流恒等式，将该恒等式作为内在监督信号用于训练。这样就不再需要模拟轨迹或执行繁重的几何计算。
- **关键技术细节**：
  - **平均速度场的定义**：利用平行传递将不同位置的切向量搬运到公共参考点后进行平均，从而在流形上构造一个全局一致的平均速度场。
  - **黎曼均值流恒等式**：该恒等式将“平均速度”与“瞬时速度”联系起来，作为监督目标，使模型能够以内在方式学习生成方向。
  - **Log-map 切空间表示**：通过对数映射（log-map）将流形数据映射到切空间，使得均值流恒等式在实际计算中可操作化，避免了复杂的测地线计算和轨迹积分。
  - **两项目标分解**：RMF 的优化目标被分解成两个独立的项，降低单目标优化的难度。
  - **冲突感知多任务学习**：采用冲突感知的多任务学习策略，缓解分解后两个目标在梯度层面的相互干扰，保证优化稳定性。
  - **条件生成支持**：通过无分类器引导（Classifier-Free Guidance）扩展，实现了条件生成能力。
- **算法流程（文字说明）**：输入流形数据 → 使用 log-map 映射到切空间 → 训练网络预测满足黎曼均值流恒等式的速度场 → 采用冲突感知多任务学习联合优化两个目标项 → 采样时通过一步映射直接生成流形数据（可选配合无分类器引导完成条件生成）。

## 3. 实验设计：数据集、场景与基准对比
- **数据集/场景**：
  - 球面（sphere）
  - 环面（torus）
  - SO(3)（三维旋转群）
  - SE(3)（三维刚体变换群）
- **Benchmark 情况**：元数据/摘要中未明确列出具体对比方法（如标准 Riemannian Flow Matching、其他一步生成方法等），也未说明 benchmark 的构建方式。不过从实验结果描述看，对比指标主要涉及采样质量（quality）与样本效率（efficiency）之间的权衡。
- **对比方法**：由于无法访问完整论文文本，具体对比方法名称不明。但从摘要表述“competitive one-step sampling with improved quality–efficiency trade-offs and substantially reduced sampling cost”可以推断，至少与已有流匹配类方法进行了对比。

## 4. 资源与算力
- 元数据与摘要中**均未提供**任何关于 GPU 型号、数量、训练时长、参数量或能耗等信息。
- 因此，本文的算力开销无法从现有信息中获知。若需评估其在真实应用中的计算可行性，需要查阅论文正文或补充材料。

## 5. 实验数量与充分性
- 从元数据可见，实验覆盖了 4 种流形（球面、环面、SO(3)、SE(3)），说明方法在不同几何结构上均进行了验证。
- 论文提到采用“冲突感知多任务学习”来稳定优化，通常这类方法会包含对应的消融实验（如对比无冲突感知/单一目标的变体），但当前摘要中并未明确说明是否开展了消融实验，也未提及实验重复次数和统计显著性检验。
- **评价**：覆盖的流形类型较为多样性，初步具备说服力；但缺乏关于消融、基线细节、计算开销和实验重复性的信息，因此对实验充分性的直接判断受限，有待全文验证。

## 6. 主要结论与发现
- RMF 在球面、环面、SO(3) 和 SE(3) 上均实现了竞争性的一步采样效果。
- 相比现有方法，RMF 在质量-效率权衡上表现更优，大幅降低了采样成本。
- 平行传递 + 均值流恒等式 + log-map 表示的组合有效避免了轨迹模拟和繁重的几何运算。
- 冲突感知多任务学习成功实现了稳定优化，并支持通过无分类器引导完成条件生成。
- 总体结论：RMF 为流形数据上的流匹配生成提供了高效、稳定的一步生成框架，拓展了流匹配的适用场景。

## 7. 优点
- **一步生成**：无需数值积分 ODE，采样效率高，成本大幅降低。
- **内在监督**：利用黎曼均值流恒等式实现切空间监督，数学上严谨且能保持流形的几何一致性。
- **计算简化**：采用 log-map 切空间表示，避免了测地线计算和轨迹模拟等重计算环节。
- **优化稳健**：冲突感知多任务学习考虑了两个目标项之间的梯度干扰，提升了训练稳定性。
- **支持条件生成**：引入无分类器引导，增强了方法的实用性（可用于条件生成任务）。
- **多流形验证**：在包括矩阵群 SE(3) 在内的多个流形上进行了验证，体现了方法的通用性。

## 8. 不足与局限
- **信息不完整**：本文解析来源受到访问限制，无法获得完整正文、算法伪代码和具体实验设置，因而无法全面评估实现细节与实验严密性。
- **资源信息缺失**：没有提供算力需求（GPU 类型/数量、训练时间等），难以对实际应用成本做出判断。
- **基线对比不明确**：由于缺少具体对比方法的描述和数值结果（如 likelihood、FID 等指标），无法从摘要层面判断优势的显著性。
- **潜在偏差风险**：缺少消融实验信息和统计显著性验证，难以排除模型性能受特定初始化、超参数调优或数据处理细节影响的风险。
- **应用限制**：RMF 依赖平行传递和 log-map 操作，对于不具备良好解析结构的流形或高维复杂流形，其适用性和计算可负担性仍有待验证。
- **未来工作**：论文未在元数据中讨论方法的局限、失败场景或可扩展性，这在一定程度上限制了读者对该方法边界条件的理解。

（完）
