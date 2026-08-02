---
title: "MMM: Generative Masked Motion Model"
title_zh: MMM：生成式掩码运动模型
authors: "Pinyoanuntapong, Ekkasit, Wang, Pu, Lee, Minwoo, Chen, Chen"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Pinyoanuntapong_MMM_Generative_Masked_Motion_Model_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 用于从文本生成3D人体运动的掩码运动模型
tldr: 针对文本到运动生成中实时性、保真度和可编辑性难以兼得的问题，本文提出MMM生成式掩码运动模型。它将3D人体运动编码为离散token，用条件掩码运动变换器随机预测被掩码的运动token，充分建模运动token关联和文本语义映射。实验表明MMM在保持高质量生成的同时支持实时推理和运动编辑，克服了扩散与自回归模型的局限。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1789, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 858, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1458, \"height\": 615, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 873, \"height\": 296, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1711, \"height\": 543, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1457, \"height\": 198, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 875, \"height\": 446, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1534, \"height\": 646, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1535, \"height\": 648, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 759, \"height\": 367, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 860, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 861, \"height\": 358, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-pinyoanuntapong-mmm-generative-masked-motion-model-cvpr-2024-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 816, \"height\": 294, \"label\": \"Table\"}]"
motivation: 现有扩散和自回归文本到运动生成模型在实时性、高保真和可编辑性之间存在权衡。
method: 结合运动tokenizer和条件掩码变换器，通过预测随机掩码的运动token来生成3D运动。
result: 在文本到运动生成任务上实现了高保真、可编辑且实时的运动生成，效果优于现有方法。
conclusion: 提出了一种新的运动生成范式，为实时、可编辑的运动合成提供了简单有效方案。
---

## Abstract
Recent advances in text-to-motion generation using diffusion and autoregressive models have shown promising results. However these models often suffer from a trade-off between real-time performance high fidelity and motion editability. To address this gap we introduce MMM a novel yet simple motion generation paradigm based on Masked Motion Model. MMM consists of two key components: (1) a motion tokenizer that transforms 3D human motion into a sequence of discrete tokens in latent space and (2) a conditional masked motion transformer that learns to predict randomly masked motion tokens conditioned on the pre-computed text tokens. By attending to motion and text tokens in all directions MMM explicitly captures inherent dependency among motion tokens and semantic mapping between motion and text tokens. During inference this allows parallel and iterative decoding of multiple motion tokens that are highly consistent with fine-grained text descriptions therefore simultaneously achieving high-fidelity and high-speed motion generation. In addition MMM has innate motion editability. By simply placing mask tokens in the place that needs editing MMM automatically fills the gaps while guaranteeing smooth transitions between editing and non-editing parts. Extensive experiments on the HumanML3D and KIT-ML datasets demonstrate that MMM surpasses current leading methods in generating high-quality motion (evidenced by superior FID scores of 0.08 and 0.429) while offering advanced editing features such as body-part modification motion in-betweening and the synthesis of long motion sequences. In addition MMM is two orders of magnitude faster on a single mid-range GPU than editable motion diffusion models. Our project page is available at https://exitudio.github.io/MMM-page/.

---

## 论文详细总结（自动生成）

# MMM：生成式掩码运动模型——中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：文本驱动的3D人体运动生成是动画、影视、VR/AR和机器人等领域的重要任务，但现有方法在“实时性、高保真度、可编辑性”三者间存在明显权衡。
- **现有三类方法的局限**：
  - **语言-运动潜空间对齐方法**（如T2M、TEMOS）：强制对齐语言与运动特征空间，容易产生语义偏差，生成质量有限。
  - **扩散模型**（如MDM、MotionDiffuse、MLD）：在原始运动空间或潜空间做扩散，保真度较好，但推理极慢；潜空间扩散虽提速却损失细粒度语义，难以编辑。
  - **自回归模型**（如T2M-GPT、AttT2M、MotionGPT）：质量高，但采用单向顺序解码，速度慢且几乎不支持运动编辑。
- **本文目标**：提出一种同时满足**高保真、实时、可编辑**的运动生成范式——**MMM（生成式掩码运动模型）**，突破扩散与自回归模型的局限。

## 2. 方法论

- **核心思想**：借鉴BERT、MaskGIT等掩码建模思想，将运动生成视为“条件掩码token预测”问题：把运动序列离散化为token，用双向Transformer随机预测被掩码的token，从而实现并行解码与天然可编辑性。
- **两阶段架构**：
  1. **阶段一：运动Tokenizer（VQ-VAE）**
     - 将3D人体运动编码为潜空间离散token序列。
     - 使用**大规模码本（8192个码）**，并采用**因子化码本（factorized code）**解耦码查找与码嵌入，缓解码本崩塌。
     - 结合moving average更新和dead code重置，提升码本利用率。
     - 向量量化目标函数：`LVQ = ||sg(z)-e||^2 + β||z-sg(e)||^2`，使用最近邻查找得到token索引。
  2. **阶段二：条件掩码运动Transformer**
     - 输入包括：运动token序列、CLIP提取的**句子嵌入**（前置）、**词嵌入**（通过cross-attention引入）、以及`[MASK]`、`[PAD]`、`[END]`特殊token。
     - 训练时，按比例r随机掩码运动token，目标是最大化被掩码token的条件对数似然：`Lmask = -E[Σ log p(y_i | Y_M, W)]`。
     - 推理时，采用**并行迭代解码**：初始全为`[MASK]`，每轮保留高置信度token，低置信度token被重新掩码，下一轮并行预测；掩码数量按**余弦衰减函数**逐步减少。
- **运动编辑能力的实现**：
  - 运动插值：在需要填补的位置放置`[MASK]`，模型自动补全。
  - 长序列生成：为每个文本片段生成运动，并利用掩码填充过渡段（单步生成过渡，而PriorMDM需上千步）。
  - 上半身编辑：分别训练上下半身Tokenizer，在第二阶段以上半身token为预测目标、下半身token为条件（并对其施加轻微掩码增强），实现部位级语义替换。

## 3. 实验设计

- **数据集**：
  - **HumanML3D**：最大规模的文本-3D运动数据集，14,616个运动序列、44,970条文本描述，20FPS，时长2~10秒。
  - **KIT-ML**：3,911个运动序列、6,278条文本描述，12.5FPS。
- **评估指标**：R-Precision（Top-1/2/3）、FID、Multimodal Distance（MM-Dist）、Diversity、MModality，均按标准协议重复20次取95%置信区间。
- **对比方法**：覆盖三类主流方法——
  - 潜空间对齐类：VQ-VAE、TEMOS、T2M、TM2T。
  - 扩散类：MDM、MotionDiffuse、MLD、Fg-T2M、M2DM。
  - 自回归类：T2M-GPT、AttT2M。
- **额外实验**：
  - 运动编辑任务评估（in-betweening、upper body editing），与MDM对比，并测试“有/无文本条件”两种设置。
  - 定性可视化：生成效果对比、编辑效果对比、长序列生成示例。
  - 消融实验（见第4部分）。

## 4. 资源与算力

- 文中**未明确说明**训练时使用的GPU型号、数量、训练时长、参数量等细节。
- 仅明确给出**推理速度测试环境**：单块NVIDIA RTX A5000。
- 实测推理速度：MMM生成单条运动的平均推理时间（AITS）为**0.081秒**，远快于MDM（28.112秒）、MotionDiffuse（10.071秒）、MLD（0.220秒）、T2M-GPT（0.350秒）、AttT2M（0.528秒）。
- 长序列生成示例：生成约10.873分钟的运动序列仅耗时1.658秒。
- 因此，关于训练算力，论文提供的信息不完整。

## 5. 实验数量与充分性

- **实验组数充足**：
  - 两个数据集（HumanML3D、KIT-ML）上的全量指标对比，各20次重复。
  - 编辑任务定量评估（2种任务 × 2种条件，与MDM对比）。
  - 定性对比多个代表性方法。
  - 三组消融实验：训练掩码比例、推理迭代次数、码本大小与维度。
- **充分性评价**：
  - **优点**：覆盖面广，既比较生成质量与速度，又验证编辑能力；消融实验直接对应方法关键设计（掩码策略、迭代次数、码本配置），较有说服力。
  - **潜在不足**：
    - 对比方法中未包括最新的离散扩散模型（如DiverseMotion）或更多2024年方法，时效性有限。
    - 编辑任务的定量指标仅与MDM对比，未与MLD、T2M-GPT等其他可编辑/不可编辑方法对比。
    - 消融实验只报告部分指标，未对编辑任务本身做消融。
    - 未提供用户研究或感知评估，所有结论依赖自动指标。

## 6. 主要结论与发现

- MMM在HumanML3D上取得**FID=0.080**（无GT长度）和**0.089**（使用GT长度），均优于所有对比方法；KIT-ML上FID=0.429，同样最优。
- R-Precision、MM-Dist也达到最优或次优，表明生成运动与文本语义高度对齐。
- 推理速度比自回归模型快至少2倍，比运动空间扩散模型快**两个数量级**。
- 运动编辑能力（插值、上半身替换、长序列生成）无需额外训练即可实现，且定量和定性均优于MDM。
- 大规模码本（8192）配合低维因子化码（32维）能提升重建质量；余弦调度比线性调度更优；迭代10次时FID最低、速度质量兼顾。

## 7. 优点

- **方法新颖简洁**：首次将掩码生成范式系统引入文本到运动生成，避开扩散与自回归的固有缺陷。
- **三者兼得**：同时实现高保真、实时推理、可编辑性，在FID与速度上同时领先。
- **可编辑性设计优雅**：无需训练即可完成多种编辑任务，掩码机制天然支持时空编辑。
- **工程细节扎实**：因子化码本、码本重置、特殊token、CLIP句子+词双粒度文本编码等设计合理。
- **实验全面**：质量、速度、编辑、长序列、消融多维度验证，定量与定性结合。

## 8. 不足与局限

- **训练资源信息缺失**：未报告训练GPU数量、时长、模型参数量，不利于复现和公平比较资源开销。
- **对比范围有限**：
  - 未与最新的离散扩散运动模型（如DiverseMotion）对比。
  - 编辑任务仅对比MDM，未对比同样支持的Fg-T2M、OmniControl等。
- **编辑实验缺乏更细粒度评估**：如对编辑区域的“语义正确性”没有专用指标。
- **长序列生成缺少定量评估**：仅给出定性示例和单次耗时，没有对长序列质量进行客观度量。
- **数据规模依赖**：HumanML3D上优势明显，KIT-ML上提升幅度较小，说明小数据下优势减弱。
- **方法限制**：运动Tokenizer引入离散化信息损失，MModality指标明显低于部分扩散方法，多模态多样性可能受限。
- **应用风险**：未讨论生成运动的物理合理性（如穿模、滑步）以及安全/伦理问题。

（完）
