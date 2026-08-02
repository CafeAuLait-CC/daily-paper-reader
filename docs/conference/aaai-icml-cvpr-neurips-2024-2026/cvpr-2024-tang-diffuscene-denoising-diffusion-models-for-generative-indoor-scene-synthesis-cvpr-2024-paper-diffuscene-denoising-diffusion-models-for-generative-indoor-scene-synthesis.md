---
title: "DiffuScene: Denoising Diffusion Models for Generative Indoor Scene Synthesis"
title_zh: DiffuScene：用于生成式室内场景合成的去噪扩散模型
authors: "Tang, Jiapeng, Nie, Yinyu, Markhasin, Lev, Dai, Angela, Thies, Justus, Nießner, Matthias"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Tang_DiffuScene_Denoising_Diffusion_Models_for_Generative_Indoor_Scene_Synthesis_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 6.0
evidence: 去噪扩散模型用于生成式三维场景合成
tldr: 室内三维场景生成中，物体布局的联合分布建模充满挑战。DiffuScene提出基于去噪扩散的场景配置生成模型，以无序物体属性集合为对象，逐步去噪生成位置、尺寸、朝向等属性，并检索最相似几何。该方法能生成合理的物体布局与对称关系，支持多种场景生成下游应用。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1765, \"height\": 722, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1643, \"height\": 642, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 914, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1762, \"height\": 1316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 873, \"height\": 213, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 863, \"height\": 182, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1800, \"height\": 258, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1765, \"height\": 376, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 869, \"height\": 697, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1602, \"height\": 455, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 827, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 820, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-diffuscene-denoising-diffusion-models-for-generative-indoor-scene-synthesis-cvpr-2024-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 773, \"height\": 395, \"label\": \"Table\"}]"
motivation: 室内三维场景生成需要对物体属性及布局进行联合建模，现有方法难以处理无序集合。
method: 使用去噪扩散网络直接对无序物体属性集合进行去噪生成，并检索相近几何。
result: 实现了更自然的三维室内场景生成，包括对称布局等特征。
conclusion: 扩散模型能够有效生成三维场景配置，并扩展到多类下游任务。
---

## Abstract
We present DiffuScene for indoor 3D scene synthesis based on a novel scene configuration denoising diffusion model. It generates 3D instance properties stored in an unordered object set and retrieves the most similar geometry for each object configuration which is characterized as a concatenation of different attributes including location size orientation semantics and geometry features. We introduce a diffusion network to synthesize a collection of 3D indoor objects by denoising a set of unordered object attributes. Unordered parametrization simplifies and eases the joint distribution approximation. The shape feature diffusion facilitates natural object placements including symmetries. Our method enables many downstream applications including scene completion scene arrangement and text-conditioned scene synthesis. Experiments on the 3D-FRONT dataset show that our method can synthesize more physically plausible and diverse indoor scenes than state-of-the-art methods. Extensive ablation studies verify the effectiveness of our design choice in scene diffusion models.

---

## 论文详细总结（自动生成）

# DiffuScene：用于生成式室内场景合成的去噪扩散模型 —— 论文总结

## 1. 核心问题与研究动机

- **问题背景**：真实感、语义合理且多样化的室内三维场景合成是计算机图形学长期挑战，可应用于游戏、电影CG、VR、虚拟室内设计等，也可为场景理解/重建提供大规模标注数据。
- **传统方法局限**：依赖人工定义的设计规则、物体类别频率、affordance图等先验知识，再通过优化迭代生成场景；规则定义耗时费力，且受限于先验表达能力。
- **深度生成模型现状**：
  - GAN方法（如DepthGAN）能快速生成高质量结果，但模式覆盖不足、易模式坍塌；
  - VAE方法（如Sync2Gen）多样性较好，但保真度偏低；
  - 自回归模型（如ATISS）逐序预测物体属性，难以准确捕捉物体间相互关系，且存在误差累积。
- **核心研究问题**：如何将场景建模为**无序物体集合**，并利用扩散模型学习其联合分布，从而在保证物理合理性与多样性的同时，支持多种下游任务（场景补全、重排、文本生成）。

## 2. 方法论

### 2.1 核心思想

- 将室内场景表示为一个**无序物体集合**，每个物体用一个向量描述，包含：
  - 位置 `ℓ ∈ R³`
  - 尺寸 `s ∈ R³`
  - 绕竖直轴的旋转角（用 `cosθ, sinθ` 二维向量表示）
  - 语义类别 `c`
  - 潜在形状编码 `f`（由预训练形状自编码器[FoldingNet]提取）
- 使用**去噪扩散概率模型（DDPM）**，对物体集合的联合属性分布进行建模与生成。
- 物体集合无序化处理：通过 padding “空物体” 将场景统一到固定物体数量 `N`，从而支持集合扩散。

### 2.2 扩散过程

- **前向过程**：给定干净场景配置 `x₀`，按照线性噪声调度 `β₁ < ... < β_T` 逐步加入高斯噪声，得到一系列带噪场景 `x₁, ..., x_T`：
  - `q(x_t | x_{t-1}) = N(x_t; √(1-β_t) x_{t-1}, β_t I)`
  - 可直接采样：`x_t = √(ᾱ_t) x₀ + √(1-ᾱ_t) ε`，其中 `ᾱ_t = ∏_{s=1}^t α_s`。
- **生成（反向）过程**：从标准正态噪声 `x_T ~ N(0, I)` 开始，通过可学习的高斯转移逐步去噪：
  - `p_ϕ(x_{t-1} | x_t) = N(x_{t-1}; μ_ϕ(x_t, t), σ_t² I)`
  - 不直接预测均值，而是预测噪声 `ε_ϕ(x_t, t)`，通过贝叶斯定理重参数化得到均值：
    - `μ_ϕ(x_t, t) = (1/√α_t)(x_t - (β_t / √(1-ᾱ_t)) ε_ϕ(x_t, t))`

### 2.3 去噪网络结构与训练

- **网络架构**：基于 1D 卷积（带 skip connection）的 UNet-1D，卷积块之间插入**注意力块**，用于聚合不同物体特征、显式建模物体间关系与全局场景上下文。
- **多预测头**：针对不同属性（边界框、类别、形状码）分别使用不同的编码与预测头，避免单一头对某些属性产生偏置。
- **训练目标**由两部分组成：
  1. **场景分布损失 `L_sce`**：最大化负对数似然的变分上界，简化为噪声预测 MSE：
     - `L_sce = E_{x₀, ε, t} [ || ε - ε_ϕ(√ᾱ_t x₀ + √(1-ᾱ_t) ε, t) ||² ]`
  2. **交并比正则化损失 `L_iou`**：对去噪得到的中间场景估计中的任意两个物体边界框计算 IoU 并累加惩罚，用于减少物体穿透：
     - `L_iou = Σ_t 0.1 * ᾱ_t * Σ_{o_i,o_j} IoU(o_i, o_j)`
- **形状检索**：生成形状码后，在 3D-FUTURE CAD 模型中检索语义相同且形状码最相似的物体几何，再根据生成的位置/尺寸/朝向放置。

### 2.4 下游任务适配

- **场景补全（Scene Completion）**：给定部分场景 `y`，只对缺失物体进行去噪生成，已知物体保持不变。
- **场景重排（Scene Re-arrangement）**：给定一组物体及其语义、尺寸、形状，仅对位置和朝向进行扩散去噪，生成合理布局。
- **文本条件场景合成（Text-conditioned）**：使用预训练 BERT 提取文本嵌入，通过交叉注意力层将语言条件注入去噪网络。

## 3. 实验设计

### 3.1 数据集与基准

- **数据集**：3D-FRONT（合成室内场景数据集），物体来自 3D-FUTURE 数据集。
- **场景类型**：三类房间——卧室（4,041）、餐厅（900）、客厅（813）；每类房间按 80% 训练、20% 测试。
- **评估指标**：
  - FID（Fr´echet Inception Distance，越低越好）
  - KID（×0.001，越低越好）
  - SCA（场景分类准确率，越接近 50% 越好——表示分类器无法区分生成与真实）
  - CKL（×0.01，类别KL散度，越低越好）
  - 额外客观指标：每场景物体数量（Obj）、对称物体对数量（Sym）、物体间平均 IoU（PIoU），均与 GT 统计值比较。

### 3.2 对比方法

- **DepthGAN**：基于多视点语义分割深度图的体积 GAN。
- **Sync2Gen**：基于 VAE + 贝叶斯优化的场景生成（含无优化变体 Sync2Gen*）。
- **ATISS**：自回归 Transformer 场景生成模型，是主要对比对象。
- 场景重排任务还对比了 **LEGO-Net**。

### 3.3 主要实验

| 实验类型 | 内容 |
|---------|------|
| 无条件场景合成 | 在卧室、餐厅、客厅三种房间上分别生成，定量与定性对比 DepthGAN、Sync2Gen、ATISS。 |
| 消融实验（在卧室上进行） | 5 组配置：C1（DALLE-2 transformer 替换 UNet-1D+Attention）、C2（去掉多预测头）、C3（去掉 IoU 损失）、C4（去掉几何特征扩散）、C5（完整模型）。 |
| 场景补全 | 输入仅 3 个物体，对比 ATISS，定性+定量。 |
| 场景重排 | 输入随机位置的物体集合，对比 ATISS 与 LEGO，定量、定性。 |
| 文本条件合成 | 对比 ATISS，并进行了用户研究：45 名用户、225 个场景，评估“与文本匹配度”和“真实合理性”。 |

## 4. 资源与算力

- 论文明确说明：
  - 在**单个 RTX 3090 GPU** 上训练；
  - batch size 为 128；
  - 训练迭代数为 **100,000 epochs**（原文如此；通常实际可能指迭代步数）；
  - 学习率初始化为 `2e-4`，每 15,000 epochs 衰减 0.5；
  - 扩散模型采用 DDPM 默认设置：噪声线性从 0.0001 增至 0.02，共 1,000 个时间步。
- **未说明**：不同房间类型训练的具体耗时、GPU 数量（仅说明单卡）、推理时间等细节。

## 5. 实验数量与充分性评价

- **实验数量**：
  - 三大类房间的无条件生成对比（3组场景 × 5种方法）；
  - 5 组消融实验；
  - 场景补全、重排各 1 组定量对比；
  - 文本条件用户研究。
- **充分性评估**：
  - **优点**：覆盖了主要生成任务和核心设计组件，消融对照清晰，指标多样（FID、KID、SCA、CKL、Obj、Sym、PIoU），且包含用户研究。
  - **潜在不足**：
    - 消融仅在卧室类型上完成，未在所有房间类型验证；
    - 文本条件任务缺少自动化定量指标（如 CLIP Score），仅依赖用户研究主观判断；
    - 对检索出的形状质量没有精确度量，主要依赖间接指标；
    - 与 LEGO-Net 只对比了重排任务，缺少无条件生成的对比（LEGO-Net 是相邻工作）；
    - 未报告训练/推理效率的对比。

## 6. 主要结论与发现

- 提出的 DiffuScene 在**所有自动指标上优于三个 SOTA 基线**（DepthGAN、Sync2Gen、ATISS），能生成更真实、多样、物理上更合理（更少穿透）的室内场景。
- 几何特征扩散显著提升了**对称布局**的生成能力（如床两侧对称床头柜），证明联合扩散形状码与布局有助于发现自然场景关系。
- 消融验证了各设计组件的有效性：
  - UNet-1D + Attention 优于 DALLE-2 transformer；
  - 多预测头优于单头；
  - IoU 损失减少穿透并增强合理性；
  - 几何特征扩散对对称性提升最明显（Sym 从 0.50 提升到 0.72）。
- 模型生成的场景与训练数据最邻近场景有明显差异，证明其具备**生成新场景**而非记忆训练数据的能力。
- 文本条件合成用户研究显示，超过半数用户认为 DiffuScene 的结果比 ATISS 更真实（62%）且与文本匹配更好（55%）。

## 7. 优点

- **表示创新**：将场景视为无序集合进行扩散，简化了联合分布学习，避免了自回归误差累积。
- **属性联合扩散**：同时扩散语义、位置、尺寸、朝向、形状码，促进对场景结构和几何的整体理解。
- **几何特征扩散带来对称性**：形状码参与扩散后，能更自然地产生真实世界常见的对称关系。
- **良好的泛化能力**：一个统一扩散框架支持补全、重排、文本生成多种下游任务，修改成本低。
- **实验较扎实**：多房间类型、多指标、多对比方法，并有消融与用户研究。

## 8. 不足与局限

- **形状检索局限**：检索只能返回同语义最近的 CAD 模型，可能出现风格不匹配。
- **纹理/材质生成缺失**：纹理依赖检索的 CAD 模型，无法生成新纹理。
- **大场景能力不足**：只支持单房间、每类房间单独训练模型，无法生成多房间大规模场景。
- **依赖3D标注数据**：需要大量带语义和布局的 3D 室内数据集，限制了其应用到仅 2D 标注的场景数据。
- **实验覆盖有限**：消融仅限卧室；文本条件缺乏客观自动评估；效率未报告。
- **固定最大物体数 N**：使用 padding 空物体，但极端物体数量超出 N 的场景无法处理（论文未明确 N 取值，但该限制是结构性的）。

## 9. 总结

DiffuScene 是首个面向室内场景配置的无序集合扩散生成模型，通过联合去噪物体属性与潜形状编码，配合形状检索，实现了高真实感、高多样性、支持多任务的三维室内场景生成，在 3D-FRONT 基准上全面超越现有方法，并为后续扩散模型在三维场景生成中的应用提供了重要参考。

（完）
