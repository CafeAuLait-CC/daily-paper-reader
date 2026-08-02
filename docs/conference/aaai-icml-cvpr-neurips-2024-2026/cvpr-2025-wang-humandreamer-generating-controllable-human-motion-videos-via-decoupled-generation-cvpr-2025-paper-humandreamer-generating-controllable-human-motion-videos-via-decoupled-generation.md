---
title: "HumanDreamer: Generating Controllable Human-Motion Videos via Decoupled Generation"
title_zh: HumanDreamer：通过解耦生成实现可控人体运动视频生成
authors: "Wang, Boyuan, Wang, Xiaofeng, Ni, Chaojun, Zhao, Guosheng, Yang, Zhiqin, Zhu, Zheng, Zhang, Muyang, Zhou, Yukun, Chen, Xinze, Huang, Guan, Liu, Lihong, Wang, Xingang"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_HumanDreamer_Generating_Controllable_Human-Motion_Videos_via_Decoupled_Generation_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 使用扩散Transformer从文本生成可控的人体运动视频与姿态
tldr: 针对人体运动视频生成中动作学习困难、现有方法依赖已有视频姿态的问题，本文提出HumanDreamer解耦框架：先用文本生成多样化人体姿态，再将其转换为运动视频。同时构建了最大的姿态生成数据集MotionVid，并提出MotionDiT扩散Transformer生成结构化姿态。实验表明该方法能够生成灵活可控的人体运动视频，显著提升动作多样性。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1608, \"height\": 1254, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1788, \"height\": 349, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1785, \"height\": 571, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1783, \"height\": 663, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1787, \"height\": 388, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 857, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 266, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1569, \"height\": 282, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-humandreamer-generating-controllable-human-motion-videos-via-decoupled-generation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 272, \"label\": \"Table\"}]"
motivation: 现有视频生成依赖已有视频中的姿态，缺乏灵活性，且人体动作学习困难。
method: 采用解耦生成方法，先训练MotionDiT从文本生成姿态，再用姿态生成视频，并构建大规模数据集MotionVid。
result: 提出的方法能生成多样且可控的人体运动视频，数据集和模型的规模与效果优于以往方法。
conclusion: 为人体运动视频生成提供了解耦式生成框架和高质量数据集，提升了灵活性和多样性。
---

## Abstract
Human-motion video generation has been a challenging task, primarily due to the difficulty inherent in learning human body movements. While some approaches have attempted to drive human-centric video generation explicitly through pose control, these methods typically rely on poses derived from existing videos, thereby lacking flexibility. To address this, we propose HumanDreamer, a decoupled human video generation framework that first generates diverse poses from text prompts and then leverages these poses to generate human-motion videos. Specifically, we propose MotionVid, the largest dataset for human-motion pose generation. Based on the dataset, we present MotionDiT, which is trained to generate structured human-motion poses from text prompts. Besides, a novel LAMA loss is introduced, which together contribute to a significant improvement in FID by 62.4%, along with respective enhancements in R-precision for top1, top2, and top3 by 41.8%, 26.3%, and 18.3%, thereby advancing both the Text-to-Pose control accuracy and FID metrics. Our experiments across various Pose-to-Video baselines demonstrate that the poses generated by our method can produce diverse and high-quality human-motion videos. Furthermore, our model can facilitate other downstream tasks, such as pose sequence prediction and 2D-3D motion lifting.

---

## 论文详细总结（自动生成）

# HumanDreamer：通过解耦生成实现可控人体运动视频生成（CVPR 2025）

## 1. 论文的核心问题与整体含义

- **研究背景**：人体运动视频生成一直极具挑战，核心难点在于人体骨骼运动的高度复杂性和动态变化。尽管现有视频生成模型参数规模庞大、训练数据丰富，但在直接学习"文本→人体视觉数据"的映射时，仍频繁出现肢体扭曲、动作破碎或不真实的问题。
- **现有方法的局限**：以 Animate Anyone、UniAnimate、Champ 等为代表的姿态引导生成方法，虽然通过引入姿态控制提高了生成质量，但**姿态必须从已有视频中提取**，用户无法自由指定动作内容，缺乏灵活性和交互性。
- **核心问题**：如何在不依赖已有视频姿态的前提下，仅通过文本描述即可生成可控、多样、高质量的人体运动视频？
- **解决思路**：论文提出 **解耦生成框架 HumanDreamer**——将"文本直接到像素"这一高复杂度任务分解为两个更可控的子任务：
  1. **Text-to-Pose**：从文本生成结构化的人体姿态序列；
  2. **Pose-to-Video**：基于姿态序列生成人体运动视频。
- **整体含义**：该框架综合了"文本控制的灵活性"与"姿态引导的可控性"，为人体运动视频生成提供了一条新范式，同时构建的大规模数据集也为后续研究提供了基础设施。

---

## 2. 论文提出的方法论

### 2.1 总体框架（解耦生成）

系统分为两个阶段：
- 第一阶段（Text-to-Pose）：文本 → MotionDiT 模型 → 结构化姿态序列；
- 第二阶段（Pose-to-Video）：初始帧图像 + 姿态序列 → 视频生成模型（基于 CogVideoX 改造）→ 最终人体运动视频。

### 2.2 MotionVid 数据集构建

- 规模：约 **120 万**个文本-姿态对，是目前**最大**的 2D 人体姿态生成数据集。
- 数据来源：Kinetics-400/700、ActivityNet-200、Something-Something V2、Charades、HAA500、HMDB51、UBody、DFEW 等公开数据集（约 660 万样本），外加互联网视频（约 340 万样本）。
- 数据清洗管线（四阶段）：
  1. **镜头切分**：使用 TransNetV2 切分视频片段；
  2. **视频质量过滤**：利用 GMFlow 光流过滤低运动强度片段、去除文字占比过大的画面、美学评分筛选、Laplacian 算子检测模糊（过滤约 50%）；
  3. **数据标注**：VLM（ShareGPT4Video）生成动作描述 + DWPose 提取 2D 全身姿态（身体 128 关键点，含脸部和手部）；
  4. **人体质量过滤**：筛选运动幅度足够、人体占比合理、单人场景、面部可见的样本（过滤约 75%）；
  5. **字幕质量过滤**：使用提出的 CLoP 模型计算文本-姿态语义相似度，去除对齐差的样本。

### 2.3 MotionDiT（文本到姿态生成模型）

- 基础架构：扩散 Transformer（DiT），扩展为适合姿态-文本对齐的结构。
- **姿态 VAE**：输入姿态序列 p ∈ R^(f×N×3)（帧数×128关键点×坐标/置信度），采用 1D 卷积编码器+解码器（下采样因子 r=8），使用 KL 散度和重建损失优化。
- **局部特征聚合**：在每层中插入 1D ResNet 块（kernel=3）+ 空间自注意力，增强相邻关节点之间的相关性：

  l_p = F_sa(F_res(l_p) + l_p)

- **文本条件注入**：使用 SD2.1 的 CLIP 文本编码器提取文本特征，通过交叉注意力机制注入网络。
- **全局注意力块**：在中间层输出上，将潜在特征 reshape 为 z ∈ R^((f×n)×c)，在全部帧和全部关节点上执行自注意力，捕捉全局时空依赖关系。只应用于中间层以控制计算量。
- **训练目标（噪声预测）**：

  L_d = E[‖ε − ε_pred‖²]，其中 ε_pred = g_θ(z_t, t, s)

### 2.4 CLoP 与 LAMA 损失

- **CLoP（Contrastive Language-Motion Pre-training）**：基于 MotionVid 训练的文本-姿态对比学习模型，类似 CLIP 的思路，将文本编码器 F_e(·) 与姿态编码器 F_p(·) 在共享语义空间中对齐，通过对比损失优化：

  L_c = [ℓ_ce(ℓ₂(h_e h_pᵀ), y) + ℓ_ce(ℓ₂(h_p h_eᵀ), y)] / 2

- **LAMA 损失（LAtent seMantic Alignment）**：将 MotionDiT 中间层的潜在特征经两层 MLP 投影后，与 CLoP 提取的真值姿态语义特征计算距离（MSE 或余弦相似度）：

  L_f = d(g_ω(h_l^d), h_p)

- **总目标**：L = L_d + λ_f · L_f

  作用：一方面改善生成姿态的保真度和多样性，另一方面增强文本条件对姿态生成的语义控制力。

---

## 3. 实验设计

### 3.1 数据集

- 主实验使用 MotionVid 的 **50K 子集**（占全量约 4%），覆盖舞蹈、深蹲、举重等多样动作，兼顾代表性和计算效率。
- 缩放实验额外使用 250K、500K、1M、1.25M 数据规模。
- 定性可视化实验使用全量 1.2M 数据进行训练。

### 3.2 评估指标

- FID（分布相似度，特征取自 CLoP）
- R-precision top1/top2/top3（文本-姿态检索对齐度）
- Diversity（整体多样性）
- MultiModality（单一文本下生成的多样性）
- MM Dist（文本与生成姿态的距离/文本遵循度）

### 3.3 对比方法（Text-to-Pose）

| 方法 | 类型 |
|------|------|
| T2M-GPT | 3D 动作生成（GPT 离散表示） |
| PriorMDM | 3D 动作生成（扩散先验） |
| MLD | 3D 动作生成（潜在扩散） |
| **Ours (MotionDiT)** | 2D 姿态生成 |

> 注：Tender（Holistic-Motion2D）是目前唯一同类 2D 姿态生成方法，但其代码和数据集未公开，无法直接对比；将其输入转换为 2D 姿态后重新训练以上 3D 方法作为替代。

### 3.4 Pose-to-Video 定性实验

- 将生成姿态输入 Pose-to-Video 模型，与 **Mochi1**、**CogVideoX** 等 SOTA 文本生成视频模型进行定性对比。
- 展示生成视频在动作幅度、运动连贯性、人脸细节等方面优于直接文本生成视频方法。

### 3.5 下游任务验证

- **姿态序列预测**：给定首尾帧，条件补全中间姿态；
- **2D-3D Motion Lifting**：将生成的 2D 姿态通过 MotionBERT 提升为 3D 运动。

---

## 4. 资源与算力

- **训练硬件**：8 张 **NVIDIA H20 GPU**；推断阶段使用单张 H20。
- **优化器**：AdamW，学习率 1×10⁻⁵。
- **训练时长**：**论文未明确报告**各阶段的具体训练时长（小时数）。
- **模型规模**：MotionDiT 共 13 层，文本嵌入维度为 1×1024。
- **其他细节**：实验代码和更多配置细节在补充材料中，但论文正文未给出完整的参数量和计算量（FLOPs）报告。

---

## 5. 实验数量与充分性

### 主要实验组

| 实验类型 | 对应表/图 | 说明 |
|----------|-----------|------|
| 主对比实验（Text-to-Pose） | Tab.1 | 与 3 种 SOTA 3D 方法对比，6 项指标全面领先 |
| 消融实验 | Tab.2 | 4 个配置逐步加入 Local→Global→LAMA，验证每个模块的有效性 |
| 数据缩放实验 | Tab.3 | 5 种数据规模（50K~1.25M），验证扩展性 |
| 定性对比（Pose-to-Video） | Fig.5 | 与 Mochi1、CogVideoX 对比 |
| 定性对比（Text-to-Pose） | Fig.4 | 与 T2M-GPT、PriorMDM、MLD 视觉对比 |
| 下游任务 | Fig.6, Fig.7 | 姿态序列预测、2D→3D 提升 |

### 充分性分析

- **充分之处**：
  - 消融实验设计规范，逐项剥离各模块，清晰归因每个技术贡献；
  - 数据规模实验（scaling law）验证了数据驱动路线的可扩展性；
  - 对比方法涵盖不同类型代表性模型。
- **不足与偏见风险**：
  - 主实验仅在 50K（4%）子集上完成，论文并未说明 50K 子集的采样是否完全随机，存在选择偏差可能；
  - 缺乏与同类 2D 方法（Tender）的直接定量对比（因其代码未公开）；
  - Pose-to-Video 阶段仅有定性可视化结果，**没有定量指标**（如 FVD、SSIM、LPIPS 等）对比；
  - 与传统 Text-to-Video 基线的对比仅展示局部定性画面，未见完整视频或用户研究（user study）结果；
  - 评估指标完全依赖自训练的 CLoP 提取的表征，一定程度上存在"自证"风险。

---

## 6. 论文的主要结论与发现

- 解耦框架（Text-to-Pose → Pose-to-Video）有效降低了人体运动视频生成的复杂度，在灵活性和可控性之间取得良好平衡。
- MotionDiT + LAMA 损失在 50K 子集上取得了显著领先：
  - **FID 降低 62.4%**（从 MLD 的 396.949 降至 149.007）；
  - **R-precision top-1/top-2/top-3 分别提升 41.8%、26.3%、18.3%**；
  - Diversity 达到 68.220，MM Dist 降至 32.761，均优于对比方法。
- 三个关键组件（局部特征聚合、全局注意力、LAMA 损失）各自贡献显著，联合使用效果最佳。
- 数据规模从 50K 扩展到 1.25M 时，R-precision top-1 从 0.451 提升至 0.513，MM Dist 从 32.761 降至 30.139，证明二维姿态数据具备良好的规模扩展潜力。
- 生成的姿态可以直接支持姿态序列预测和 2D-3D 运动提升，展现出广泛的下游应用价值。

---

## 7. 优点

1. **问题切分巧妙**：将文本到像素的高维映射分解为文本到姿态（结构空间）和姿态到视频（视觉空间）两个子问题，语义与视觉生成各司其职，降低学习难度。
2. **大规模数据贡献**：MotionVid（1.2M 文本-姿态对）是当前最大的 2D 全身体姿态生成数据集，并公开了系统的数据清洗流程，具有领域复用价值。
3. **架构设计有针对性**：局部特征聚合（关节相关性）+ 全局注意力（时空依赖）+ 扩散 Transformer 的组合，贴合姿态数据的多尺度结构特性。
4. **创新性损失设计**：LAMA 损失将扩散模型中间表征与 CLIP 式对比学习的语义空间对齐，直接强化文本控制力，思路简洁且有效。
5. **验证了数据扩展规律**：表格展示了性能随数据量递增的稳定趋势，说明其数据采集管线具有成本效益和规模化潜力。
6. **代码和模型公开**：项目页面已公开，便于复现与后续研究。

---

## 8. 不足与局限

1. **实验规模偏小**：核心对比和消融实验仅在 50K（4%）子集上完成，虽然论文声称"保持代表性和效率"，但 4% 的数据能否代表完整 1.2M 数据集的分布有待商榷。
2. **Pose-to-Video 定量缺失**：没有提供视频生成质量的定量评估（如 FVD、CLIP score 等），仅依赖少量可视化样例，说服力有限。
3. **对比方法不公平的风险**：
   - 3D 方法（T2M-GPT 等）被迫转为 2D 姿态输入，可能无法发挥其原始设计优势；
   - 与 Tender 的缺失对比（代码不可用）导致无法直接证明优于当前最强 2D 姿态生成方法。
4. **评估指标的自依赖性**：FID、R-precision 等指标均基于自训练的 CLoP 模型提取的表征，缺乏第三方标准的独立验证。
5. **场景简化**：训练数据经过严格过滤，仅保留单人、面部可见、运动幅度充分等简化场景，面对多人物交互、复杂遮挡、极端姿态等真实场景时泛化能力未知。
6. **算力信息不完整**：未报告训练总时长、模型参数量、FLOPs 等关键信息，不利于公平复现和效率对比。
7. **文本控制粒度的局限**：示例多集中在动作类型级别的控制，对细粒度控制（如动作速度、幅度大小、风格修饰等）能力的验证不足。

---

（完）
