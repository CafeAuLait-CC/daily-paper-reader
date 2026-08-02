---
title: "PC-Flow: Preference Alignment in Flow Matching via Classifier"
title_zh: PC-Flow：基于分类器的流匹配偏好对齐
authors: "Shaomeng Wang, He Wang, Longquan Dai, Jinhui Tang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37971/41933"
tags: ["query:dmg"]
score: 8.0
evidence: 提出了面向流匹配模型的偏好对齐方法
tldr: 本文将直接偏好优化（DPO）思想扩展到流匹配模型，提出无参考模型的PC-Flow框架。核心是将确定性ODE重解释为等价SDE以支持DPO式学习，并用轻量级分类器建模相对偏好，避免了大规模微调和参考模型依赖。实验显示PC-Flow能有效提升流匹配生成与人类偏好的一致性。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 流匹配模型与人类偏好对齐的研究不足，现有DPO方法难以直接应用于ODE框架且资源消耗高。
method: 将流匹配的确定性ODE等价为SDE，并引入轻量级分类器建模相对偏好，实现无参考模型的偏好对齐。
result: 所提方法在偏好对齐任务上表现优异，同时降低了计算成本并摆脱对参考模型质量的依赖。
conclusion: 为流匹配模型提供了高效、无参考的偏好对齐新途径。
---

## Abstract
Flow Matching (FM) is an efficient generative modeling framework, but aligning it with human preferences remains underexplored.~Although applying Direct Preference Optimization (DPO) to diffusion models has yielded improvements, directly extending DPO-like methods to FM poses three challenges: 1) Incompatibility with ODE-based models, 2) Heavy computational cost from full model fine-tuning, and 3) Reliance on reference model quality. To address these limitations, we propose Preference Classifier for Flow Matching (PC-Flow), a novel reference-free preference alignment framework. Specifically, we  reinterpret FM’s deterministic ODE as an equivalent SDE to enable DPO-style learning. Then, we introduce a lightweight classifier to model relative preferences exclusively. This approach decouples alignment from the generative model, eliminating the need for costly fine-tuning or a reference model. Theoretically, PC-Flow guarantees consistent preference-guided distribution evolution, achieves a DPO-equivalent objective without a reference model, and progressively steers generation toward preferred outputs. Experiments show that PC-Flow achieves DPO-level alignment with significantly lower training costs.

---

## 论文详细总结（自动生成）

# PC-Flow: Preference Alignment in Flow Matching via Classifier — 中文详细总结

## 1. 论文的核心问题与整体含义

### 研究动机与背景
- **Flow Matching (FM)** 是一种高效的生成建模框架，通过确定性 ODE 将噪声分布映射到数据分布，在图像和视频生成中表现出色且推理效率高。
- 然而，FM 模型在**与人类主观偏好对齐**方面仍存在不足，例如审美感知、语义对齐等细粒度需求难以满足。
- 已有方法（如 Direct Preference Optimization, DPO）在扩散模型中取得了成功，但**直接将其扩展到 FM 存在三大挑战**：
  1. **与 ODE 框架不兼容**：DPO 本质上是为 SDE 设计的，依赖概率转移核的比较，而 FM 是确定性 ODE。
  2. **计算成本高**：DPO 需要对整个生成模型进行微调，资源消耗大。
  3. **依赖参考模型质量**：参考模型的质量直接影响训练稳定性和最终效果，且可能引入偏差。

### 核心问题
如何在**不微调生成模型、不依赖参考模型**的前提下，将人类偏好有效地融入 Flow Matching 的生成过程中？

## 2. 论文提出的方法论

### 核心思想
提出 **PC-Flow (Preference Classifier for Flow Matching)**——一种**无参考模型（reference-free）**的偏好对齐框架。核心思路是：

> 将偏好学习从生成模型中解耦出来，交给一个**轻量级可训练分类器**完成，生成模型本身保持冻结。

### 关键技术细节

#### (1) ODE 到 SDE 的转换
- 将 FM 的确定性 ODE 解释为**保持边缘分布不变的等价 SDE**：

  \[
  dx_t = \left(v_t(x_t,t) - \frac{\sigma_t^2}{2}\nabla \log p_t(x_t,t)\right)dt + \sigma_t dW
  \]

- 其中边际得分 \(\nabla \log p_t(x_t,t)\) 与速度场 \(v_\phi\) 之间存在确定性关系，使得 FM 具备了概率转移结构，从而支持 DPO 式的学习目标。

#### (2) 偏好分类器定义
- 引入轻量级分类器 \(S_\theta(x): \mathbb{R}^d \to (0,1)\)，为样本分配偏好分数。
- 定义偏好引导分布：
  \[
  \hat{p}_\theta^\phi(x_t) \propto p_\phi(x_t) S_\theta(x_t)
  \]
- 定义偏好引导的转移核：
  \[
  \hat{p}_\theta^\phi(x_{t-1}|x_t) = p_\phi(x_{t-1}|x_t)\exp(\log S_\theta(x_{t-1}) - \log S_\theta(x_t))
  \]

#### (3) 无参考模型的训练目标
- 推导出 **PC-Flow Loss**：

  \[
  \mathcal{L}_{PC-Flow}(S_\theta) = -\mathbb{E}\left[\log \sigma\left(\beta T \log \frac{S_\theta(x^w_{t-1})}{S_\theta(x^w_t)} - \beta T \log \frac{S_\theta(x^l_{t-1})}{S_\theta(x^l_t)}\right)\right]
  \]

- **Theorem 1**：偏好引导分布可以在时间步之间一致传播，无需修改基础模型。
- **Theorem 2**：PC-Flow 的训练目标与 DPO 目标数学等价，但**不需要参考模型**。

#### (4) 偏好引导采样
- 结合分类器梯度，构造偏好引导速度场：
  \[
  v_\theta(x_t,t) = v_\phi(x_t,t) + \gamma \frac{t}{1-t}\nabla_{x_t}\log S_\theta(x_t)
  \]
- 其中 \(\gamma\) 为可调引导权重，控制偏好校正的强度。
- **Theorem 3**：该采样策略能够从偏好引导分布中有效采样。

### 算法流程（文字说明）
1. 将 FM 的 ODE 重写为等价 SDE，获得概率转移结构。
2. 训练轻量级分类器 \(S_\theta\)（冻结基础生成模型），使用 PC-Flow Loss 在偏好数据集上优化。
3. 推理时，在每个采样步通过分类器梯度修正速度场，逐步引导生成过程朝向人类偏好方向。

## 3. 实验设计

### 数据集
| 用途 | 数据集 |
|---|---|
| 训练偏好分类器 | **Pick-a-Pic**（包含成对偏好标注） |
| 测试基准 | **PartiPrompts** 和 **HPSV2 benchmark** |

### 对齐任务
1. **审美对齐（Aesthetic Alignment）**：提升生成图像的视觉效果与审美品质。
2. **文本到图像对齐（Text-to-Image Alignment）**：评估生成图像对文本语义和细节的忠实度。

### 基础模型
- **Stable Diffusion 3.5 Medium (SD-3.5-M)**，配备 MMDiT 架构。

### 对比方法
- **SD-3.5-M**（未对齐的基础模型）
- **Flux1.dev**
- **AuraFlow**
- **SANA-1.5 1.6B**

### 评估指标
- **自动指标**：PickScore、HPS、LAION Aesthetics、CLIP
- **用户研究**：一般偏好、视觉吸引力、提示对齐三个维度

### 分类器架构
- **审美对齐**：冻结的 U-Net（不含下采样层）+ 可训练两层 MLP，并注入时间嵌入。
- **文本到图像对齐**：在审美分类器基础上增加可训练的交叉注意力模块以捕获文本语义。

## 4. 资源与算力

- **GPU 型号与数量**：2 块 **NVIDIA A6000** GPU。
- **训练步数**：2,000 步。
- **优化器**：AdamW，学习率 \(1\times10^{-5}\)，batch size 8（梯度累积 2 步），常数学习率调度 + warm-up。
- **图像分辨率**：512 × 512。
- **推理步数**：50 步，CFG 引导尺度 7.0，PC-Flow 引导权重 \(\gamma = 0.1\)。
- **训练时长**：论文**未明确说明**具体训练耗时。

## 5. 实验数量与充分性

### 主要实验组成
| 实验类型 | 数量/内容 |
|---|---|
| 自动指标对比 | 在 PartiPrompts 和 HPS 两个基准上，对比 5 种模型 × 4 个指标 |
| 胜率对比（Win-rate） | 在 PartiPrompts 和 HPS 上，PC-Flow 对 4 个基线的胜率统计 |
| 定量评分表 | 在 PartiPrompts 和 HPS 上，5 个模型的 4 指标绝对分数 |
| 用户研究 | 300 个提示（100 个来自 PartiPrompts，200 个来自 HPSV2），3 个评估维度 |
| 消融实验 | β 消融（5/20/200/2000）、γ 消融（0.05/0.10/0.15/0.20） |
| 定性比较 | 多个提示的可视化对比（含文本到图像对齐示例） |

### 实验充分性评估
- **优点**：覆盖了任务（审美 + 文本到图像）、指标（4 种自动指标 + 用户研究）、对比方法（4 个基线）和消融（2 个关键超参数），整体较为全面。
- **不足**：
  - 基础模型仅使用 SD-3.5-M 一个，未验证在其他 FM 架构（如 Flux、SANA）上的可迁移性。
  - 消融实验仅在 HPSV2 上进行，未在 PartiPrompts 上验证。
  - 用户研究的样本量相对有限（300 个提示），未报告参与人数和统计显著性。
  - 未与其他 **DPO 类对齐方法**（如 Diffusion-DPO、SPO 等）进行直接比较，只与未对齐的 FM 模型对比。

## 6. 论文的主要结论与发现

1. **PC-Flow 实现了与 DPO 相当的对齐效果**，但训练成本显著更低。
2. **无参考模型设计有效**：通过分类器直接建模相对偏好，避免了参考模型带来的不稳定性和偏差。
3. **理论保证完备**：三个定理分别保证了偏好引导分布的一致性传播、与 DPO 目标的等价性、以及偏好引导采样的正确性。
4. **性能均衡且优越**：在审美质量和语义一致性上取得了良好平衡，尤其在 HPS 和 CLIP 指标上超过所有基线。
5. **超参数敏感性合理**：\(\beta=200\) 和 \(\gamma=0.1\) 是最优设置，过大或过小都会导致性能下降。

## 7. 优点

### 方法设计亮点
- **真正的 reference-free 框架**：彻底摆脱了对参考模型的依赖，简化了训练流程。
- **解耦偏好学习与生成模型**：基础模型完全冻结，偏好对齐由轻量级分类器独立完成，即插即用。
- **理论扎实**：提供了三个定理支撑方法的正确性，并非纯工程技巧。
- **ODE-to-SDE 转换巧妙**：弥合了 DPO 与 FM 之间的理论鸿沟，使得概率式偏好学习在确定性模型中成为可能。
- **计算效率高**：仅训练轻量级分类器（U-Net 部分冻结 + 小 MLP），训练成本远低于全模型微调。

### 实验设计亮点
- 同时覆盖审美和语义两个维度的对齐评估。
- 同时使用自动指标和用户研究，评估方式较为多元。
- 提供了 win-rate 对比表和绝对分数表两种视角。
- 对核心超参数（β 和 γ）进行了消融分析。

## 8. 不足与局限

### 实验覆盖不足
- **仅使用单一基础模型（SD-3.5-M）**，未验证方法在 Flux、SANA、AuraFlow 等其他 FM 架构上的泛化能力。
- **未与其他 DPO 类对齐方法（如 Diffusion-DPO、DSPO）进行直接实验对比**，削弱了"与 DPO 相当"这一结论的直接说服力。
- 消融实验仅在 HPSV2 上进行，缺少在 PartiPrompts 上的验证。
- 文本到图像对齐任务仅展示了定性结果，**缺少量化指标**。

### 潜在偏差风险
- 训练数据来自 Pick-a-Pic（由 SDXL-beta 和 Dreamlike 生成），偏好信号可能存在**数据偏差**，未必能泛化到所有生成模型和提示分布。
- 用户研究的样本量和统计效力未充分披露。

### 方法局限
- 偏好分类器 \(S_\theta\) 的能力可能成为对齐效果的**瓶颈**——消融实验中 β 过大时分类器容量不足导致训练崩溃即为例证。
- 引导权重 γ 需要人工调节，不同任务/模型可能存在最优值差异，需要额外调参成本。
- 在推理时额外引入分类器梯度计算，虽然避免了训练成本，但**推理开销略有增加**。

### 资源细节不透明
- 论文未明确报告训练时长、参数量对比等具体资源消耗数据，"显著降低训练成本"的定量证据不够充分。

（完）
