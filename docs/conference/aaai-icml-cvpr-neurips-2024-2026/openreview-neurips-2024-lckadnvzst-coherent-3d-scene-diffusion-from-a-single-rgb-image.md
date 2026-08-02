---
title: Coherent 3D Scene Diffusion From a Single RGB Image
title_zh: 单张RGB图像下的一致3D场景扩散
authors: "Manuel Dahnert, Angela Dai, Norman Müller, Matthias Nießner"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=lckAdnVzsT"
tags: ["query:dmg"]
score: 4.0
evidence: 使用图像条件3D场景扩散模型生成一致3D场景，与扩散概率生成模型相关，但不涉及人体动作。
tldr: 针对单张RGB图像重建一致3D场景的病态问题，提出基于扩散模型的联合去噪方法，同时重建所有物体的位姿与几何，并利用场景级条件建模物体间关系。设计了无需完整真值标注的高效表面对齐损失，在公开数据集上验证了生成式场景先验的有效性。
source: NeurIPS-2024-Accepted
selection_source: conference_retrieval
motivation: 单张图像重建3D场景是病态问题，现有方法难以生成结构一致且关系合理的完整场景。
method: 利用图像条件3D场景扩散模型同时去噪所有物体位姿与几何，并引入表面对齐损失辅助训练。
result: 实验表明该方法能重建更为连贯合理的3D场景，并在缺少完整标注时仍可有效训练。
conclusion: 条件扩散模型可捕捉场景级物体关系，为单图3D场景重建提供新的生成式方案。
---

## Abstract
We present a novel diffusion-based approach for coherent 3D scene reconstruction from a single RGB image. 
Our method utilizes an image-conditioned 3D scene diffusion model to simultaneously denoise the 3D poses and geometries of all objects within the scene.

Motivated by the ill-posed nature of the task and to obtain consistent scene reconstruction results, we learn a generative scene prior by conditioning on all scene objects simultaneously to capture scene context and by allowing the model to learn inter-object relationships throughout the diffusion process.

We further propose an efficient surface alignment loss to facilitate training even in the absence of full ground-truth annotation, which is common in publicly available datasets. This loss leverages an expressive shape representation, which enables direct point sampling from intermediate shape predictions.

By framing the task of single RGB image 3D scene reconstruction as a conditional diffusion process, our approach surpasses current state-of-the-art methods, achieving a 12.04\% improvement in AP3D on SUN RGB-D and a 13.43\% increase in F-Score on Pix3D.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义

- **研究动机**：从单张 RGB 图像重建完整 3D 场景是高度病态（ill-posed）的问题——单目图像丢失了深度、遮挡、物体背面等信息，导致多种合理的 3D 解释同时存在。现有方法通常独立处理每个物体或依赖显式规则，难以生成结构一致、物体间关系合理且完整的场景。
- **核心思路**：将单图 3D 场景重建建模为**条件扩散过程**，利用图像条件 3D 场景扩散模型，在去噪过程中**同时重建所有物体的 3D 位姿与几何**，从而捕获场景级上下文和物体间相互关系，生成连贯的完整场景。

## 2. 方法论：核心思想与关键技术

- **整体框架**：使用一个以 RGB 图像为条件的 3D 场景扩散模型，在扩散采样过程中联合去噪场景内所有物体的姿态（位置、朝向）与形状几何。
- **场景级条件生成先验**：
  - 与独立重建每个物体不同，模型对所有场景物体**同时进行条件建模**，使网络能够学习物体之间的空间关系、语义关系与几何适配关系（如桌子与椅子、地面与家具的支撑关系）。
  - 这种“联合去噪”策略让场景先验成为真正的**生成式先验**，能够在单目信息不足时推断出可能的、合理的场景布局。
- **高效表面对齐损失（surface alignment loss）**：
  - 公共数据集往往缺少完整的物体级真值标注（例如缺少某些物体的完整 3D 模型或姿态）。
  - 为此提出一种**无需完整真值标注**即可训练的损失函数，利用所采用的**表达力强的形状表示**，直接从中间形状预测中采样点，并计算预测表面与可用观测之间的对齐误差。
  - 该损失显著提升了训练可行性与效率。
- **公式与算法流程（文字说明）**：
  - 前向过程：对场景中所有物体的位姿和几何添加噪声。
  - 反向过程：以单张 RGB 图像为条件，网络逐步去噪，每一步同时更新所有物体的状态。
  - 训练目标：结合扩散重建损失（预测噪声/原始信号）与表面对齐损失，在仅有部分标注时也能监督几何质量。

## 3. 实验设计

- **数据集与 benchmark**：
  - **SUN RGB-D**：大规模室内场景数据集，包含 RGB-D 图像与 3D 场景标注，用于评估 3D 物体检测/重建指标（AP3D）。
  - **Pix3D**：单张图像 3D 物体重建基准，包含图像与对应 3D 模型，用于评估重建精度（F-Score）。
- **对比方法**：论文声称与“当前最先进方法”对比，但摘要中未列出具体名称；从上下文推断应包含以往的单图场景重建、物体检测+重建流水线、以及非生成式或独立去噪的扩散基线。
- **主要结果**：
  - 在 SUN RGB-D 上，AP3D 相对 SOTA 提升 **12.04%**。
  - 在 Pix3D 上，F-Score 相对 SOTA 提升 **13.43%**。
- **注**：由于仅提供摘要与简略元数据，具体基线、消融细节、定性比较在原文中应有更详细说明。

## 4. 资源与算力

- **未明确说明**：摘要和给定元数据中没有提及 GPU 型号、数量、训练时长或显存占用等具体算力信息。
- **推断**：由于方法涉及 3D 场景扩散，通常需要较高显存的多卡 GPU（如 A100 或 RTX 3090 以上），但具体细节需查阅论文原文实验章节。

## 5. 实验数量与充分性

- **已知实验**：
  - 两个公开数据集上的主实验（场景级 3D 检测/重建精度）。
  - 提及“消融”相关设计（通过表面对齐损失辅助训练），但未在摘要中给出完整消融数量。
- **充分性评估**：
  - **优点**：跨数据集验证（室内场景 vs 物体重建）能说明一定泛化性；且由于使用了缺失标注的数据集，验证了损失设计的实用性。
  - **不足**：提供的文本信息不足以全面评估消融数量、基线多样性、误差分析等。需要原文补充“无场景级条件/独立去噪”“无表面对齐损失”等消融，以及更多类别/场景泛化测试，才能使实验更充分。

## 6. 主要结论与发现

- 将单图 3D 场景重建重新定义为**条件扩散过程**，联合去噪所有物体的位姿与几何，能够有效捕捉物体间关系，生成比现有一 stage 式或独立重建方法更连贯、合理的完整场景。
- 提出的**表面对齐损失**使得模型在**缺乏完整真值标注**的现实数据集上仍能高效训练，拓展了该方法在真实数据上的可用性。
- 在 SUN RGB-D 与 Pix3D 上均显著超越现有最优方法，验证了生成式场景先验的有效性。

## 7. 优点

- **创新性**：将场景级联合生成先验引入单图 3D 重建，而非逐物体独立预测，更符合真实场景的结构约束。
- **鲁棒性**：扩散模型天然适用于病态逆问题，能从多模态分布中采样合理场景解释。
- **实用性**：设计无需完整标注的损失函数，缓解了公共数据集标注不完整的痛点。
- **结果领先**：在两个主流基准上提升超过 12%，说明方法切实有效。

## 8. 不足与局限

- **信息不完整**：当前文本未给出具体网络架构、去噪步数、采样策略、推理时间等关键细节，难以完全复现。
- **算力未披露**：缺少训练资源信息，无法评估部署成本。
- **实验细节有限**：缺乏消融实验数量、对比基线名称、误差分解和失败案例分析，客观性需原文进一步佐证。
- **场景范围**：主要验证在室内场景（SUN RGB-D）和物体级基准（Pix3D）上，对室外、大尺度或动态场景的泛化未知。
- **标注依赖**：尽管损失支持部分标注，但仍是监督/弱监督方法，在无任何标注场景下自适应能力未知。
- **单图通道限制**：仅使用 RGB 图像输入，未融合深度（虽然 SUN RGB-D 有深度，但方法本身未利用），可能限制几何精度。

（完）
