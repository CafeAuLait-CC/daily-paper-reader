---
title: Motion Diversification Networks
title_zh: 动作多样化网络
authors: "Kim, Hee Jae, Ohn-Bar, Eshed"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Kim_Motion_Diversification_Networks_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 8.0
evidence: 学习生成真实且多样3D人体动作的框架，直接对应合成真实人体运动数据。
tldr: 现有生成模型难以在给定上下文下生成覆盖全部合理范围的真实且多样3D人体动作，尤其影响自动驾驶和机器人等安全关键应用。为此提出Motion Diversification Networks，通过Transformer多样化机制学习有效引导潜码采样，改善生成动作的真实性与多模态性。实验验证该框架能显著提升3D人体动作生成的多样性和自然度，为安全敏感场景提供了更可靠的动作预测基础。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 873, \"height\": 310, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1793, \"height\": 940, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1763, \"height\": 785, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 873, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 835, \"height\": 505, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 669, \"height\": 589, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 883, \"height\": 323, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-kim-motion-diversification-networks-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 883, \"height\": 377, \"label\": \"Table\"}]"
motivation: 现有深度生成动作模型难以在给定上下文下生成足够多样且自然的3D人体动作。
method: 提出Transformer基础的多样化机制，学习引导潜码采样，避免过于简单的采样策略导致模式坍塌。
result: 实验表明该方法显著增强了3D人体动作生成的多样性和真实性，提升多模态预测能力。
conclusion: 通过多样化引导采样，可更好地捕捉3D人体运动的完整分布，提升功能型运动模型性能。
---

## Abstract
We introduce Motion Diversification Networks a novel framework for learning to generate realistic and diverse 3D human motion. Despite recent advances in deep generative motion modeling existing models often fail to produce samples that capture the full range of plausible and natural 3D human motion within a given context. The lack of diversity becomes even more apparent in applications where subtle and multi-modal 3D human forecasting is crucial for safety such as robotics and autonomous driving. Towards more realistic and functional 3D motion models we highlight limitations in existing generative modeling techniques particularly in overly simplistic latent code sampling strategies. We then introduce a transformer-based diversification mechanism that learns to effectively guide sampling in the latent space. Our proposed attention-based module queries multiple stochastic samples to flexibly predict a diverse set of latent codes which can be subsequently decoded into motion samples. The proposed framework achieves state-of-the-art diversity and accuracy prediction performance across a range of benchmarks and settings particularly when used to forecast intricate in-the-wild 3D human motion within complex urban environments. Our models datasets and code are available at https://mdncvpr.github.io/.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：现有深度生成模型在给定上下文（如历史动作、场景信息）下，难以生成覆盖全部合理范围的、真实且多样的 3D 人体动作。该问题在机器人、自动驾驶等安全关键场景中尤为突出，因为细微的手势、视线等动作变化可能蕴含重要的行为意图。
- **核心问题**：
  - 现有生成模型存在**模式坍塌**问题，倾向于生成主流动作模式，忽视罕见但重要的动作。
  - 盲目提升多样性容易导致生成动作不真实，形成“多样性-真实性”权衡。
  - 大多数方法仅针对单一孤立人体动作建模，难以扩展到包含人-场景、人-物体、人-人等复杂交互的真实场景。
- **整体含义**：论文提出一种新的 3D 人体动作生成框架，在提高样本多样性的同时保持动作真实性，从而更好地捕捉真实世界中多模态、细粒度的人体运动分布。

## 2. 论文提出的方法论

- **核心思想**：提出 Motion Diversification Networks（MDN），核心是引入**基于 Transformer 的潜变量多样化模块（z-transformer）**，替代传统简单的独立采样或仿射映射方式，在潜空间有效引导并多样化采样，从而提升生成样本的多样性。
- **关键技术细节**：
  - 从标准正态分布中采样 K 个随机变量作为查询（Query），以编码后的历史/上下文信息作为键（Key）和值（Value），通过交叉注意力机制生成多样化的潜码集合。
  - 注意力公式为：
    - Z = softmax(E·K^T / √N_z) · V
    - 其中 E 是随机采样集合，K、V 由编码输入计算得到。
  - 采用多层（8 层）Transformer 块，结合自注意力和交叉注意力、MLP 以及位置编码。
  - **确定性动作基元（Motion Primitives）**：对训练数据的输入进行 k-means 聚类，得到一组稳定的动作原型，在计算 K、V 时注入，以帮助模型在罕见模式下也能生成合理动作，同时避免随机采样导致的“高多样性、低真实性”问题。
  - 模型采用两阶段训练：
    1. 先按 CVAE 方式预训练编码器与生成器（损失包含 KL 散度和重建误差）。
    2. 冻结生成器，单独训练 z-transformer 多样化模块，损失为重建误差 + 多样性促进损失（基于样本间成对距离）。
- **可扩展性**：模块可以灵活融合额外上下文信息，如 2D 路径、图像特征（Swin Transformer 提取）、社交上下文等；生成器采用多任务输出分支，同时预测 3D 姿态和 2D 路径。

## 3. 实验设计

- **数据集与场景**：
  - **Human3.6M**：标准室内单人多动作数据集，用于验证基础多样化生成能力。
  - **3DPW**：真实户外场景，SMPL 24 关节表示，用于跨域评估。
  - **HPS**：室内外结合、基于惯性动捕的 23 关节表示，进一步验证泛化性。
  - **DenseCity（自建仿真基准）**：基于 CARLA 0.9.13，密集行人场景（最多 250 个行人），30K 帧、82 条行走序列，平均每帧 21.3 个行人，用于评估复杂城市环境中的人-场景、人-人交互下的动作生成。
  - **YouTube 野外数据**：从多个城市公开视频中提取 288 条真实行人运动序列，用于提升模型在真实复杂环境下的泛化能力。
- **对比方法**：
  - 基线：CVAE、DLow、PoseGPT、Cao et al.、HuMoR 等。
  - 还对比了其他已有方法在 Human3.6M 上的结果（如 STARS、BeLFusion、GSPS、MOJO 等）。
- **评估指标**：
  - 多样性：APD（Average Pairwise Distance）。
  - 准确性：ADE（Average Displacement Error）和 FDE（Final Displacement Error）。
- **额外实验**：
  - 在 Human3.6M、3DPW、HPS、DenseCity 上分别评估；
  - 结合 YouTube 数据训练后的跨数据集泛化实验；
  - 用户感知研究：13 名参与者对比 MDN 生成动作与 CARLA 内置控制器动作的偏好和真实性评分。

## 4. 资源与算力

- **论文未明确说明**所使用的 GPU 型号、数量、训练时长等算力资源信息。仅提到使用 Adam 优化器进行网络训练，未提供可复现所需的具体硬件配置。

## 5. 实验数量与充分性

- **实验组数**：
  - 4 个主要评测数据集（Human3.6M、3DPW、HPS、DenseCity）。
  - 多组基线对比，并包含结合 YouTube 数据的泛化实验。
  - 用户感知研究 1 组。
  - 论文提到更多消融实验见补充材料。
- **充分性分析**：
  - **优点**：覆盖了简单室内、真实户外、仿真密集城市、真实野外视频等多种场景，评估维度较全面；同时兼顾多样性、准确性和用户感知，客观性较强。
  - **不足**：主要对比方法数量有限（3DPW/HPS/DenseCity 中仅对比 CVAE、DLow 等少数基线）；主文中的消融细节较少，很多结果依赖补充材料；YouTube 数据是否引入数据偏差、标注噪声影响等未深入讨论。

## 6. 论文的主要结论与发现

- 提出的 z-transformer 多样化机制相比传统 CVAE 和 DLow 的仿射映射方法，能够显著提升生成样本的多样性，同时不损失甚至提升预测准确性，缓解了“多样性-真实性”权衡。
- 在 Human3.6M 上达到 SOTA：APD 17.450，ADE 0.355，FDE 0.442，在多样性和准确性上均超过现有方法。
- 在 3DPW、HPS 和 DenseCity 上均取得最佳或领先性能；加入 YouTube 野外数据后，模型在 3DPW 和 HPS 上的表现进一步提升，表明该方法能够有效利用大规模嘈杂真实数据提升泛化性。
- 用户研究显示，72.5% 的情况下参与者更偏好 MDN 生成的动作，绝对真实性评分也高于 CARLA 内置控制器，说明生成动作更接近真实行人行为。

## 7. 优点

- **方法创新**：将 Transformer 注意力机制引入潜变量采样过程，打破了传统独立采样和仿射映射的局限，提供了一种更灵活的多样化建模方式。
- **多样性与真实性兼顾**：通过确定性动作基元引导，有效缓解了高多样性与低真实性之间的矛盾。
- **良好扩展性**：模块设计可自然融入图像、2D 路径、社交上下文等多种信息，支持复杂场景中的多模态动作生成。
- **实验覆盖面广**：从标准室内基准到真实户外、仿真密集城市、野外视频，评价维度丰富，并有用户研究支撑，结论较可信。
- **开源可用**：提供模型、数据集和代码，有助于后续研究复现与推进。

## 8. 不足与局限

- **算力信息缺失**：未报告 GPU 型号、训练时间等计算资源，复现成本不透明。
- **横评基线不够全面**：在部分真实/仿真基准上仅对比少量代表性方法，缺少与更多最新方法（如更多扩散模型）的对比。
- **主文消融有限**：关键组件（如动作基元数量、Transformer 层数、上下文融合方式）的消融主要在补充材料中，主文分析不够细化。
- **YouTube 数据噪声问题**：虽然提升了真实感和跨域泛化，但引入的自动提取轨迹可能存在噪声和偏差，对结果的影响未充分分析。
- **DenseCity 仿真数据局限性**：CARLA 内置行人控制器本身存在运动不自然的问题，虽然用户研究支持 MDN 更好，但仿真数据的真实性仍制约实验上限。
- **应用限制**：主要面向短时（2 秒）预测，长时间预测和极端罕见动作模式的效果仍需进一步探索。

（完）
