---
title: "EnergyMoGen: Compositional Human Motion Generation with Energy-Based Diffusion Model in Latent Space"
title_zh: EnergyMoGen：潜在空间中基于能量的扩散模型组合式人体运动生成
authors: "Zhang, Jianrong, Fan, Hehe, Yang, Yi"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Zhang_EnergyMoGen_Compositional_Human_Motion_Generation_with_Energy-Based_Diffusion_Model_in_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 基于能量的潜在扩散模型用于组合式文本驱动人体运动生成
tldr: 潜在扩散模型在文生人体运动方面表现优异，但难以将多个语义概念组合成连贯的单一运动序列。本文提出EnergyMoGen，包含两类能量模型：将扩散模型解释为潜在感知能量模型，在潜在空间中组合多个扩散模型；同时基于交叉注意力引入语义感知能量模型，实现对文本嵌入的语义组合和自适应梯度下降。实验表明该方法在组合多概念生成上具有显著优势。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1798, \"height\": 693, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1808, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1472, \"height\": 350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1771, \"height\": 625, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1781, \"height\": 597, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1804, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1798, \"height\": 627, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-zhang-energymogen-compositional-human-motion-generation-with-energy-based-diffusion-model-in-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 922, \"height\": 623, \"label\": \"Table\"}]"
motivation: 潜在扩散模型难以在文本驱动的人体运动生成中有效组合多个语义概念。
method: 将扩散模型作为潜在能量模型进行组合，并提出基于交叉注意力的语义感知能量模型以支持自适应梯度下降。
result: 在组合多概念文本条件下生成了连贯而符合语义的人体运动序列。
conclusion: 为语义可控的组合式人体运动生成提供了基于能量的扩散建模途径。
---

## Abstract
Diffusion models, particularly latent diffusion models, have demonstrated remarkable success in text-driven human motion generation. However, it remains challenging for latent diffusion models to effectively compose multiple semantic concepts into a single, coherent motion sequence. To address this issue, we propose EnergyMoGen, which includes two spectrums of Energy-Based Models: (1) We interpret the diffusion model as a latent-aware energy-based model that generates motions by composing a set of diffusion models in latent space; (2) We introduce a semantic-aware energy model based on cross-attention, which enables semantic composition and adaptive gradient descent for text embeddings. To overcome the challenges of semantic inconsistency and motion distortion across these two spectrums, we introduce Synergistic Energy Fusion. This design allows the motion latent diffusion model to synthesize high-quality, complex motions by combining multiple energy terms corresponding to textual descriptions. Experiments show that our approach outperforms existing state-of-the-art models on various motion generation tasks, including text-to-motion generation, compositional motion generation, and multi-concept motion generation. Additionally, we demonstrate that our method can be used to extend motion datasets and improve the text-to-motion task.

---

## 论文详细总结（自动生成）

# EnergyMoGen 论文详细总结

## 1. 论文的核心问题与整体含义

**研究动机与背景：**

- **核心问题**：潜在扩散模型（Latent Diffusion Models, LDMs）在文本驱动的人体运动生成中表现优异，但难以将多个语义概念（如"举起双臂"+"向前行走"）有效组合成单一、连贯的运动序列。
- **技术瓶颈**：潜在扩散模型通常使用一个（或固定数量的）潜在向量来表示可变长度运动，导致：① 潜在向量与运动之间缺乏显式对应关系（one-to-one 或 one-to-many）；② 潜在向量难以支持逐帧级别的运动组合。
- **研究视角**：论文从能量模型（Energy-Based Models, EBMs）的视角重新审视组合运动生成问题，将扩散模型的生成过程转化为能量组合问题，实现概念之间的**合取（conjunction）** 与**否定（negation）** 操作。
- **引用的思想来源**：约翰·洛克（John Locke）的"复杂观念由简单观念组合而成"的哲学思想，明确体现在论文开篇引言中。

## 2. 论文提出的方法论

**核心思想**：探索两种谱系的能量模型，并通过协同能量融合（Synergistic Energy Fusion, SEF）将二者结合，实现高质量的组合式人体运动生成。

### 2.1 模型架构（基于 MLD 潜在扩散模型扩展）

- **Motion Variational Autoencoder（运动 VAE）**：将 3D 人体运动序列 X ∈ R^(L×dm) 编码为 N 个潜在向量 z ∈ R^(N×d)，再通过解码器重建运动。
- **Motion Latent Diffusion（潜在扩散网络）**：采用基于 Transformer 的去噪自编码器，其中引入**交叉注意力**模块，融合文本嵌入与运动潜在特征。

### 2.2 两个能量模型谱系

**❶ 潜在感知能量模型（Latent-aware EBM）：**

- 将扩散模型的去噪过程（式 5）与 Langevin 动力学采样（式 6）建立等价关系，从而将扩散模型解释为能量模型。
- 通过分类器无引导（Classifier-Free Guidance）实现概念组合：
  - **合取**：ε_θ(zt, t, C) = ε_θ(zt, t) + Σ w_i (ε_θ(zt, t, c_i) − ε_θ(zt, t))（式 7）
  - **否定**：ε_θ(zt, t, C) = ε_θ(zt, t) + w(ε_θ(zt, t, c_i) − ε_θ(zt, t, c_j))（式 8）

**❷ 语义感知能量模型（Semantic-aware EBM）：**

- 基于现代 Hopfield 网络理论，将交叉注意力解释为能量操作。
- 通过**自适应梯度下降（AGD）** 更新文本嵌入（式 3、4），使网络聚焦于多概念文本中语义相关的低能量区域：
  - ∇K log p(K|Q) = [SFM(αKQ^T)Q − M(SFM(K′))K]W_K
  - ĉ = c + γ∇K log p(K|Q)
- 对来自不同概念的交叉注意力输出特征进行加权平均（式 9）实现组合。

### 2.3 协同能量融合（Synergistic Energy Fusion, SEF）

- **发现的问题**：① 潜在感知组合存在**文本错位**问题；② 语义感知组合存在**脚部滑动和运动抖动**问题。
- **解决方案**：融合三部分能量（式 10）：
  - ε̂_θ(zt, t, C, c_1,n) = λ_l ε_l + λ_s ε_s + λ_m ε_θ(zt, t, c_1,n)
  - 其中 λ_l + λ_s + λ_m = 1（实验设置为 λ_s=0.7, λ_l=0.1, λ_m=0.2）

## 3. 实验设计

### 数据集

| 数据集 | 用途 |
|--------|------|
| HumanML3D | 文本到运动生成（主实验） |
| KIT-ML | 文本到运动生成（跨数据集验证） |
| MTT | 组合运动生成 + 多概念运动生成 |
| CompML（自建） | 5000 条组合生成的运动-文本对，用于数据增强验证 |

### 评测指标

- **文本到运动**：R-Precision (Top-1/2/3)、FID、MM-Dist、Diversity、MModality
- **组合/多概念运动生成**：R-Precision、TMR-Score、FID、Transition distance

### 对比方法

- **骨架级扩散模型**：MDM、MotionDiffuse、Fg-T2M、ReMoDiffusion、FineMoGen、M2DM
- **潜在扩散模型**：MLD、GUESS、MotionMamba
- **组合运动生成专用方法**：PriorMDM、GMD（相关工作讨论）

## 4. 资源与算力

- **论文未明确说明**：文中没有报告 GPU 型号、数量、训练时长或参数量等具体算力信息。
- 仅提及了模型架构规模：运动编码器、运动解码器和去噪自编码器各包含 9 层 Transformer 块，维度 d=256，使用 10 个额外 token 采样 N=5 个潜在向量。
- 推理时使用 50 步扩散采样，文本编码器为冻结的 CLIP ViT-L/14。

## 5. 实验数量与充分性

### 实验组数统计

- **文本到运动生成**：2 个数据集（HumanML3D、KIT-ML），对比 8+ 种方法，每个指标重复 20 次取均值与 95% 置信区间。
- **组合/多概念运动生成**：MTT 数据集上对比 6 种方法，包含两组设置（多概念单文本、多概念多文本）。
- **消融实验（Q1-Q3）**：
  - Q1：验证 AGD 对多概念文本一致性提升
  - Q2：验证潜在感知、语义感知各自作用及 SEF 融合效果
  - Q3：通过能量分布可视化分析组合机制
- **数据增强实验**：CompML 数据集微调后性能对比

### 充分性评估

- **优点**：实验覆盖三个任务、三个数据集，同时提供定量（表 1-3）和定性（图 3-4）结果；消融实验设计层次分明，回答了关键设计选择；额外提供可视化能量分布（图 5）增强了可解释性。
- **不足**：训练细节（超参数搜索、收敛曲线）未在正文呈现；不同方法间是否使用完全相同的文本编码器未明确；组合实验仅在 HumanML3D 预训练模型上评估，未跨 KIT-ML 验证泛化性；论文提到可泛化到骨架级扩散模型，但结果只在补充材料中。

## 6. 论文的主要结论与发现

1. **潜在扩散模型可实现组合运动生成**：通过能量视角解释扩散模型，使用合取和否定两种操作，能够将多个简单概念组合为复杂运动。
2. **AGD 有效缓解文本不一致**：自适应梯度下降使 R-Precision Top-1 提升 1.3%，Top-3 提升 0.9%。
3. **SEF 融合优于单一谱系**：潜在感知擅长保持运动质量但语义一致性差，语义感知擅长语义对齐但产生运动失真，融合后效果最佳（R-Precision 15.9% vs. 潜在 9.7% / 语义 15.1%；Transition distance 降至 1.6）。
4. **组合生成可作为数据增强手段**：在 CompML（5000 条合成数据）上微调可进一步提升文本到运动生成性能。
5. **能量分布可视化验证机制有效性**：组合生成与多概念生成的潜在空间能量分布具有一致的高/低能量区域，解释了方法的有效性。

## 7. 优点

1. **首创性视角**：首次从能量模型角度系统解决运动组合问题，为潜在扩散模型的组合式生成提供了新的理论框架。
2. **两种谱系互补设计**：潜在感知（保证运动质量）与语义感知（保证语义对齐）形成互补，SEF 融合策略务实有效。
3. **新颖操作引入**：除传统的概念合取外，还实现了概念否定以及组合+否定的混合操作，拓展了组合生成的能力边界。
4. **模型通用性强**：论文声称可以泛化到骨架级扩散模型，不局限于潜在扩散架构。
5. **数据增强创新应用**：将组合生成用作数据增强手段，为解决训练数据不足问题提供了新思路。
6. **可解释性探索**：通过能量分布可视化揭示了模型组合运动的潜在机制，增加了方法的可解释性。
7. **代码和结果开源**：提供了项目主页（https://jiro-zhang.github.io/EnergyMoGen/），便于复现和比较。

## 8. 不足与局限

1. **算力信息缺失**：未报告训练和推理的硬件配置、时间和能耗，不便于计算资源评估和公平对比。
2. **跨数据集泛化验证有限**：组合运动生成仅在 HumanML3D 预训练模型上于 MTT 数据集评估，未在更多数据集上验证组合性能。
3. **超参数敏感度分析不充分**：λ_l、λ_s、λ_m 和 γ 的设置对结果影响较大，但正文仅给出最优值，消融细节在补充材料中提及。
4. **骨架级泛化验证不透明**：声称可泛化到骨架级模型，但正文未给出具体结果，降低了说服力。
5. **多概念数量的扩展性**：论文主要展示 2-3 个概念的组合，更多概念（5+）的扩展性和退化风险未讨论。
6. **与其他组合方法的直接比较**：未与 PriorMDM、GMD 等专门的组合运动生成方法进行直接定量对比。
7. **应用限制**：方法依赖预训练模型的文本编码空间（CLIP），对复杂/抽象概念的表达能力受限于 CLIP 的语义理解范围；文本错位和运动失真问题虽缓解但未彻底解决。
8. **CompML 数据集质量评估**：仅通过下游任务性能提升来间接验证合成数据质量，缺乏对合成数据本身质量（真实性、多样性）的直接评估。

---

（完）
