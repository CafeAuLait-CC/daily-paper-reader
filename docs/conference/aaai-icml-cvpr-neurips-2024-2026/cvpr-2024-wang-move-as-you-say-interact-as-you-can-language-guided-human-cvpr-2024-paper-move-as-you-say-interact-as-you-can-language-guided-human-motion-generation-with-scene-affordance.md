---
title: "Move as You Say Interact as You Can: Language-guided Human Motion Generation with Scene Affordance"
title_zh: 言出则行，可交互：场景可供性引导的语言驱动人体运动生成
authors: "Wang, Zan, Chen, Yixin, Jia, Baoxiong, Li, Puhao, Zhang, Jinlu, Zhang, Jingze, Liu, Tengyu, Zhu, Yixin, Liang, Wei, Huang, Siyuan"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Wang_Move_as_You_Say_Interact_as_You_Can_Language-guided_Human_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 使用场景可供性扩散模型进行语言引导的3D人体运动生成
tldr: 在3D场景中生成语言引导的人体运动极具挑战性，主要源于难以联合建模语言、场景与运动，且高标注数据稀缺。本文提出两阶段框架，以场景可供性为中间表示连接3D场景定位与条件运动生成，其中使用可供性扩散模型（ADM）进行预测。此方法有效缓解了数据需求问题，并实现了符合场景语义与几何约束的3D人体运动生成。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1807, \"height\": 866, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1787, \"height\": 885, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1783, \"height\": 986, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1801, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 330, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1721, \"height\": 457, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1430, \"height\": 313, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 793, \"height\": 276, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1809, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-wang-move-as-you-say-interact-as-you-can-language-guided-human-cvpr-2024-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 814, \"height\": 280, \"label\": \"Table\"}]"
motivation: 语言引导的3D环境内人体运动生成面临联合建模与数据稀缺的双重挑战。
method: 提出两阶段框架，利用场景可供性作为中间表示，并训练可供性扩散模型来连接场景与运动条件生成。
result: 在语言-场景-运动数据有限条件下实现了更符合场景语义与几何约束的人体运动生成。
conclusion: 以场景可供性为桥梁，为3D环境中的语言引导运动生成提供了一种稳健且数据高效的方案。
---

## Abstract
Despite significant advancements in text-to-motion synthesis generating language-guided human motion within 3D environments poses substantial challenges. These challenges stem primarily from (i) the absence of powerful generative models capable of jointly modeling natural language 3D scenes and human motion and (ii) the generative models' intensive data requirements contrasted with the scarcity of comprehensive high-quality language-scene-motion datasets. To tackle these issues we introduce a novel two-stage framework that employs scene affordance as an intermediate representation effectively linking 3D scene grounding and conditional motion generation. Our framework comprises an Affordance Diffusion Model (ADM) for predicting explicit affordance map and an Affordance-to-Motion Diffusion Model (AMDM) for generating plausible human motions. By leveraging scene affordance maps our method overcomes the difficulty in generating human motion under multimodal condition signals especially when training with limited data lacking extensive language-scene-motion pairs. Our extensive experiments demonstrate that our approach consistently outperforms all baselines on established benchmarks including HumanML3D and HUMANISE. Additionally we validate our model's exceptional generalization capabilities on a specially curated evaluation set featuring previously unseen descriptions and scenes.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **任务定义**：在三维场景中，根据自然语言描述生成语义一致且物理上合理的人体运动序列（语言引导的人体运动生成，Language-guided Human Motion Generation in 3D Scenes）。
- **两大核心挑战**：
  1. **联合建模困难**：缺乏能够同时建模自然语言、3D场景和人体运动的生成模型。3D场景提供空间边界（spatial boundaries），语言提供语义方向（semantic direction），两者性质互补且异质，直接对齐或联合学习多模态嵌入空间十分困难。
  2. **数据稀缺**：生成模型通常依赖大规模成对数据，但现有HSI数据集（如PROX等）运动质量与多样性不足、场景布局有限，且缺乏对应的语言描述；HUMANISE虽做了弥补，但动作类型范围窄、语句形式固定，难以支持多样化自由文本描述。
- **核心解决思路**：引入**场景可供性（Scene Affordance）**作为中间表示，桥接3D场景定位与条件运动生成。
- **可供性地图（Affordance Map）的两大优势**：
  1. 精确刻画语言描述所指向的场景区域，增强3D场景定位能力，缓解有限训练数据下的学习难度；
  2. 基于距离度量，提供对场景与人体运动间几何关系的细粒度理解，有助于生成HSI并泛化到未见过的场景几何。

**整体含义**：该工作不仅是提出一个新的生成模型，更是提出一种"以可供性为中间纽带"的建模范式，将复杂的三模态联合分布分解为两个较易学习的条件分布，从而在数据受限条件下实现稳健的语言-场景-运动联合生成。

---

## 2. 论文提出的方法论

### 2.1 总体框架（两阶段模型）

- 整体流程为两阶段级联：
  - **第一阶段**：给定3D场景点云 S 和语言描述 L，用 **Affordance Diffusion Model（ADM）** 生成语言引导的**可供性地图 C**。
  - **第二阶段**：给定可供性地图 C 和语言描述 L（可选同时输入场景 S），用 **Affordance-to-Motion Diffusion Model（AMDM）** 从高斯噪声生成人体运动序列 X。

### 2.2 可供性地图的定义（核心中间表示）

- 对3D场景 S ∈ R^(N×6)（RGB点云）和运动序列 X = {x_i}_{i=1}^F（每帧为SMPL-X关节位置 x_i ∈ R^(J×3)）进行如下计算：
  1. 计算每帧场景点与各人体关节间的 ℓ2 距离，得到距离场 d ∈ R^(N×J)；
  2. 通过高斯函数归一化为距离图 c(n,j) = exp(-d(n,j)² / (2σ²))，σ = 0.8，使靠近关节的点权重更高，稳定训练；
  3. 沿时间维度做 max-pooling，得到最终可供性地图 C ∈ R^(N×J)。

- 可供性地图本质上是"场景中哪些位置与人体哪些关节点在运动过程中相关联"的紧凑表示，既保留了空间定位信息，也编码了人体-场景几何关系。

### 2.3 Affordance Diffusion Model（ADM）

- **目标**：学习分布 pθ(C₀:T | S, L)，以场景和语言为条件生成可供性地图。
- **架构**：基于Perceiver（编码-处理-解码三块结构）：
  - **Encode**：以输入特征（点特征 + 噪声可供性地图的拼接）作为Key/Value，以潜在特征（语言特征 + 扩散时间步嵌入）作为Query，通过交叉注意力实现条件注入；
  - **Process**：用多层自注意力精炼潜在特征；
  - **Decode**：输入特征作为Query，更新后的潜在特征作为Key/Value，实现逐点特征精炼；
  - 最后经线性层输出预测。
- **训练目标**：不预测噪声 ε，而是直接预测输入信号本身（x₀预测），使用MSE损失：L_MSE = E[‖C₀ - G_θ(C_t, t, S, L)‖²]。这种设计简化了训练并提高了稳定性。

### 2.4 Affordance-to-Motion Diffusion Model（AMDM）

- **目标**：学习分布 pϕ(X₀:T | C, S, L)，以可供性地图和语言为条件生成运动。
- **架构**：
  - **可供性编码器**：基于Point Transformer架构提取多尺度特征，再经U-net解码器层处理；
  - **Transformer骨干**：堆叠自注意力和交叉注意力层；将噪声运动序列与语言特征、扩散时间步嵌入拼接后输入骨干网络；在每个交叉注意力层中，拼接特征作为Query，可供性特征作为Key/Value，融合多模态信息；
  - **输出层**：线性层将融合特征映射到运动空间。
- **训练目标**：同样采用直接预测X₀的MSE损失：L_MSE = E[‖X₀ - G_ϕ(X_t, t, C, S, L)‖²]。

### 2.5 实现细节

- 语言特征提取：冻结的CLIP-ViT-B/32。
- 优化器：AdamW，固定学习率 1×10⁻⁴。
- Transformer使用PyTorch原生实现。

---

## 3. 实验设计

### 3.1 数据集与Benchmark

| 数据集 | 用途 | 说明 |
|---|---|---|
| **HumanML3D** | 语言→运动生成基准 | 源自AMASS的动作捕捉序列，带文本描述；因缺少3D场景，作者**添加地板平面**进行扩展；使用原始运动表示和官方划分。 |
| **HUMANISE** | 语言-场景-运动HSI基准 | 首个大规模语义丰富的HSI数据集，将AMASS运动与ScanNet场景对齐，描述自动来自Sr3D；作者移除空间指代描述并分块场景。 |
| **新颖泛化评估集（Novel Evaluation Set）** | 泛化能力测试 | 由16个来自ScanNet、PROX、Replica、Matterport3D的场景 + 80条Turker人工书写的HSI描述构成；仅包含语言-场景-运动三元组中的语言和场景，无GT运动。训练集合并了HumanML3D、HUMANISE、PROX数据，并用ModelNet家具随机放置增强HumanML3D，共63,770个HSI样本（48,470带语言标注）。 |

### 3.2 评估指标

- **HumanML3D**：R-Precision（Top 1/2/3）、FID、MultiModal Dist.、Diversity、MultiModality。
- **HUMANISE**：goal dist.（定位精度）、APD（运动多样性）、contact（接触率）、non-collision（非碰撞率）、quality score（质量）、action score（动作语义一致性），其中quality和action score来自人工感知评分。
- **ADM评估补充指标**：min dist.、pelvis dist.、all dist.三种接地距离度量。
- 所有指标在5次运行上报告95%置信区间，再训练运动/文本特征提取器以保证指标一致。

### 3.3 对比的基线方法

- **HumanML3D**：Language2Pose、T2M、MDM（MDM还报告了修复评估代码bug后的修正结果）。
- **HUMANISE**：
  - cVAE（即HUMANISE原方法）；
  - **one-stage扩散模型变体**：直接处理场景点云、跳过可供性地图生成（@ Enc和@ Dec两种变体，即encoder型与decoder型）；
  - **Ours @ Enc / @ Dec**：两阶段方法在不同AMDM集成方式下的变体。
  - ADM架构消融：对比MLP、Point Transformer、Perceiver三种架构。

---

## 4. 资源与算力

- 论文在Implementation Details中明确说明了**GPU配置与批大小**：
  - **ADM训练**：2张NVIDIA A100 GPU，每GPU批大小64；
  - **AMDM训练**：4张NVIDIA A100 GPU，每GPU批大小32。
- **未明确说明的信息**：
  - 未报告具体的**训练时长（小时/天/轮数）**；
  - 未报告单次完整训练的总GPU小时数（GPU-hours）；
  - 未报告推理阶段的单条生成时间。

---

## 5. 实验数量与充分性

### 实验组数概览

- **3个评估场景（Benchmark）**：HumanML3D、HUMANISE、新颖泛化评估集。
- **定量实验**：
  - HumanML3D上与3个基线（Language2Pose、T2M、MDM）对比，报告6项指标；
  - HUMANISE上与4个基线/变体对比，报告6项指标；
  - 泛化评估集上与2个one-stage变体对比，报告9项指标；
  - 可供性地图生成质量评估（ADM的3种架构对比，3项接地指标）。
- **消融实验**：
  - ADM架构消融（MLP vs. Point Transformer vs. Perceiver），在Table 3中报告接地指标；
  - ADM架构对下游运动生成的影响（Table 5中报告goal dist./contact/non-collision）。
- **定性实验**：HUMANISE定性对比、泛化集定性对比、失败案例展示。
- **人类感知评估**：quality score和action score通过人工评分获得。

### 充分性评价

**充分之处**：
- 覆盖了从基础语言→运动生成（HumanML3D）到复杂语言-场景-运动交互（HUMANISE）再到举未见过的场景与描述（泛化集）的完整层次；
- 消融实验覆盖了核心设计选择（ADM架构、AMDM编码方式），能支撑"Perceiver优于MLP/Point Transformer"的结论；
- 定量+定性+人工评估相结合，证据链条较完整。

**有待加强之处**：
- 新建泛化评估集**不含GT运动**，无法像标准benchmark那样用FID等分布距离精确评估，只能依赖统计指标和人工评分；
- HUMANISE中的基线cVAE未考虑更新方法（如CoC等后续方法），也未见与MotionDiffuse、T2M-GPT等近期文本生成SOTA的对比；
- 未见对语言描述不同复杂度/多种空间关系的细粒度分层分析；
- 未见对两阶段误差累积的定量分析（ADM预测误差如何影响AMDM输出）。

**总体判断**：实验规模中等偏充分。核心主张（可供性地图作为中间表示有效）有较为直接的对证据（one-stage vs. two-stage对比 + 架构消融），数据充分性上可接受。

---

## 6. 主要结论与发现

1. **场景可供性地图作为中间表示是有效且高效的设计**：在有限的数据条件下，通过将"语言-场景-运动"三模态联合建模拆解为"语言-场景→可供性→运动"两个阶段，显著降低了多条件联合建模的难度。
2. **在HumanML3D上取得了最优FID（0.352）**，相比MDM（0.544）大幅提升，同时在R-Precision和MultiModal Dist.上也有改善——即便场景只是简单的"地板"，可供性信息也提升了运动的细节质量（如关节轨迹）。
3. **在HUMANISE上全面超越基线**：goal dist.从cVAE的0.422和one-stage的0.185/0.326降至0.156，contact score从84.06提升至96.04，质量与动作分也显著提升。定位更精确、接触更强、碰撞更少。
4. **泛化能力出色**：在全新场景和人工书写的未见过描述上，接触率达到88.63%（one-stage基线仅为26.75%~46.64%），FID（7.887）优于one-stage（11.848/12.268），证明了可供性中间表示对场景几何变化的鲁棒性。
5. **Perceiver是ADM的最佳架构选择**：相比MLP（缺少点间信息交换）和Point Transformer，Perceiver通过交叉注意力高效融合语言与点特征，取得了最佳的接地精度。
6. **APD多样性下降不代表模型退化**：作者指出APD较低主要因为生成的运动会更准确地接地到目标物体，从而主动减少不必要的无关移动，这反而体现了生成精度的提高。

---

## 7. 优点

- **创新性**：
  - 首次将**场景可供性地图**系统性地作为语言-场景-运动三模态生成中的中间表示；
  - 可供性地图的定义（时间维max-pooled的距离场）简洁、几何可解释性强、无需额外标注，可直接从现有数据中自动计算；
  - 两阶段解耦（ADM+AMDM）巧妙规避了多模态联合分布难以端到端学习的问题。
- **通用性好**：
  - 设计不依赖于特定场景语义标签，可迁移至多种3D场景数据集（ScanNet、PROX、Replica、Matterport3D）；
  - 联合训练数据跨多个数据集并统一为关节位置表示（同时用ModelNet家具增强HumanML3D），凸显了框架的数据可扩展性。
- **泛化验证扎实**：专门构建了含未见过场景和人工描述的评估集，做了鲁棒性验证；这是很多运动生成工作未曾做的。
- **对比实验设计合理**：one-stage扩散模型作为关键消融对照，直接验证了"可供性中间表示"的不可替代性，排除了"只要用扩散模型就能更好"的混淆解释。
- **对反直觉结果做了解释**（APD下降的原因），说明作者对指标有深入理解。

---

## 8. 不足与局限

- **推理速度慢**：两阶段均使用扩散模型，迭代式去噪导致推理开销大，不利于实时或大规模应用，作者在Limitations中也明确承认了该问题。
- **数据问题仍是大短板**：虽然可供性缓解了数据不足，但语言-场景-运动三元组数据的稀缺仍然是核心瓶颈；数据集上的动作类型与场景多样性有限，影响模型覆盖的交互范围。
- **失败的典型案例揭示了覆盖盲区**：
  - 完全不熟悉的HSI（如洗手

- 完全不熟悉的HSI（如洗手、擦拭桌面等），由于训练数据中缺乏对应动作–场景–文本的联合示例，生成结果出现明显的语义偏差或物理不合理，表明模型对分布外交互的泛化能力依然受限。
- **评估指标存在歧义**：如APD的下降既可能源自生成质量提升（更精确地接地）也可能源自运动多样性衰退，作者虽然有解释，但缺乏更细粒度的分解指标来彻底区分这两种效应；goal dist.等接地指标也仅关注末端位移，未充分刻画空中轨迹的语义合理性。
- **人类评估样本量有限**：quality score和action score作为主要的主观质量证据，未报告评价者人数、评分者一致性（如Kappa）以及评分尺度说明，弱化了这部分结论的可重复性。
- **几何-语义一致性缺失**：可供性地图虽然能约束“哪里接触”，但无法显式编码动作的动词语义（如“坐”与“蹲”在几何上相似但语义不同），对细粒度动作区分仍需依赖语言特征本身的判别力。
- **两阶段误差传导未量化**：论文未分析ADM预测误差的分布特性及其对AMDM输出的具体传导路径，也未见对端到端联合微调（两阶段联合训练）的探索，无法判断解耦设计是否存在性能上限。

## 9. 尚待回答的问题与未来方向

- **如何加速采样**：两阶段扩散的迭代式去噪是实际部署的主要瓶颈，未来可采用一致性模型、蒸馏或少量步数采样器（如DPM-Solver）来压缩推理时间，而不显著牺牲质量。
- **能否扩展到动作序列的动态场景**：当前场景是静态点云，但真实世界存在门、抽屉等可交互动态物体；如何将可供性地图扩展到含时变场景的表示是一个值得探索的方向。
- **数据增强与合成**：作者已经用ModelNet家具增强HumanML3D，未来可利用大规模合成场景与LLM生成描述，进一步扩充多样化的HSI三元组，缓解数据稀缺。
- **更细粒度的语言控制**：现有模型只能实现整体动作生成，无法对动作片段（如“先走到沙发前，再坐下”）做分段式条件控制；将可供性地图逐帧化（而非时间池化）可能支持更精细的时空对齐。
- **与基础模型结合**：将语言编码器从CLIP升级为更强的大规模多模态模型（如LLaVA、GPT-4V），或将场景点云与预训练3D表示对齐，有望提升对复杂空间语义的理解。

## 10. 总结

本论文以**场景可供性地图**为桥梁，将语言引导的三维场景运动生成解耦为“语言-场景→可供性”与“可供性-语言→运动”两个条件扩散阶段，在数据受限的设定下实现了优于单阶段端到端建模的定位精度与运动质量。方法设计简洁、可解释性强，在HumanML3D、HUMANISE及自建泛化评测集上均取得了显著改进。其核心贡献不在于复杂的网络结构，而在于**表征层面的创新**——用距离场派生的可供性吸收了场景与运动之间的隐式几何约束，从而降低了多模态联合分布的学习难度。当然，推理效率、数据覆盖与细粒度语言控制仍是未来需要攻克的痛点。整体而言，该工作为语言-场景-人体交互生成提供了一个范式清晰、验证充分的基准性方案，对该领域后续研究具有重要的启发意义。

（完）
