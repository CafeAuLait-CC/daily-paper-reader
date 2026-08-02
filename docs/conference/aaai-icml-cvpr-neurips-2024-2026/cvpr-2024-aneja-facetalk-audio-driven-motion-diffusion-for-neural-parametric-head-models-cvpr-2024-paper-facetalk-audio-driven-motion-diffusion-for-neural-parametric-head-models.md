---
title: "FaceTalk: Audio-Driven Motion Diffusion for Neural Parametric Head Models"
title_zh: FaceTalk：神经参数化头部模型的音频驱动运动扩散
authors: "Aneja, Shivangi, Thies, Justus, Dai, Angela, Nießner, Matthias"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Aneja_FaceTalk_Audio-Driven_Motion_Diffusion_for_Neural_Parametric_Head_Models_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 8.0
evidence: 用于音频驱动的3D头部运动序列的潜在扩散模型
tldr: 现有方法难以从音频生成包含头发、耳朵和细微眼部运动的高保真3D说话头部序列。本文提出FaceTalk，将语音信号与神经参数化头部模型的潜在空间耦合，提出在表情空间中运行的潜在扩散模型，以合成时序连贯且逼真的音频驱动头部运动。针对缺少NPHM表情与音频对应数据集的问题，作者优化对应关系并构建了时序优化数据集，展示了高质量合成效果。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1720, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1788, \"height\": 661, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1782, \"height\": 1000, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1796, \"height\": 964, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 653, \"height\": 442, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 855, \"height\": 696, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 353, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-aneja-facetalk-audio-driven-motion-diffusion-for-neural-parametric-head-models-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 610, \"height\": 286, \"label\": \"Table\"}]"
motivation: 高保真3D说话头部合成需要模型同时表达精细结构并实现音频驱动的时序连贯运动。
method: 在神经参数化头部模型的表情空间上构建潜在扩散模型，并优化音频-表情对应关系以生成数据集。
result: 能够合成包含头发、耳朵和细粒度眼部运动的高保真、时序连贯的3D说话头部序列。
conclusion: 为音频驱动的3D头部运动生成提供了一种高保真的潜在扩散建模方法。
---

## Abstract
We introduce FaceTalk a novel generative approach designed for synthesizing high-fidelity 3D motion sequences of talking human heads from input audio signal. To capture the expressive detailed nature of human heads including hair ears and finer-scale eye movements we propose to couple speech signal with the latent space of neural parametric head models to create high-fidelity temporally coherent motion sequences. We propose a new latent diffusion model for this task operating in the expression space of neural parametric head models to synthesize audio-driven realistic head sequences. In the absence of a dataset with corresponding NPHM expressions to audio we optimize for these correspondences to produce a dataset of temporally-optimized NPHM expressions fit to audio-video recordings of people talking. To the best of our knowledge this is the first work to propose a generative approach for realistic and high-quality motion synthesis of volumetric human heads representing a significant advancement in the field of audio-driven 3D animation. Notably our approach stands out in its ability to generate plausible motion sequences that can produce high-fidelity head animation coupled with the NPHM shape space. Our experimental results substantiate the effectiveness of FaceTalk consistently achieving superior and visually natural motion encompassing diverse facial expressions and styles outperforming existing methods by 75% in perceptual user study evaluation

---

## 论文详细总结（自动生成）

# FaceTalk：神经参数化头部模型的音频驱动运动扩散——论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：3D 人类动画在数字媒体（动画电影、游戏、虚拟助手）中具有广泛的应用价值。已有大量工作关注人体运动合成，但对于**面部**的 3D 生成研究相对滞后。现有音频驱动的 3D 面部动画方法大多基于 **3DMM（3D Morphable Model）**（如 FLAME、VOCA 等），其采用固定拓扑的线性混合形状（linear blendshapes）表征面部运动。
- **核心局限**：3DMM 表征能力有限，无法精细建模**头发、耳朵、皱纹、皮肤褶皱等高频几何细节**，也无法表达微妙的眼部运动（如眨眼）和复杂表情。
- **核心问题**：如何从输入音频信号生成**高保真、时序连贯、富有表现力**的 3D 说话头部运动序列，同时兼顾面部细节（头发、耳朵、皮肤皱褶）与多样化的表情风格？
- **论文立场**：本文提出将语音信号与**神经参数化头部模型（NPHM, Neural Parametric Head Models）** 的潜在空间耦合，利用扩散模型在 NPHM 的**表情潜在空间**中合成高保真且时序连贯的头部运动，弥补了 3DMM 表达力不足与 2D 方法缺乏几何信息的空白。据作者所述，这是**第一个**针对体积化人体头部的音频驱动生成式方法。

## 2. 论文提出的方法论：核心思想、关键技术细节与算法流程

### 2.1 核心思想
- 使用 **NPHM**（而非传统的 3DMM）作为头部表征，利用其体积化 SDF 表达，捕捉头发、耳朵、皱纹等细节。
- 将扩散模型构建在 **NPHM 的表情潜在空间（expression latent space）** 中，而不是直接生成网格或 SDF，从而兼顾表达力与计算效率。
- 音频特征使用预训练的 **Wave2Vec 2.0** 提取，并通过交叉注意力机制与表情序列对齐。

### 2.2 关键技术细节

1. **音频编码（Audio Encoding）**：
   - 使用冻结的 Wave2Vec 2.0 提取音频特征，经 TCN 层 + 频率插值层将 16kHz 音频对齐到 24Hz 的帧率，再由 Transformer 编码器处理，得到对齐后的音频特征序列$$A_{1:N}$$。
   - 通过前馈层将音频特征投影到表情解码器的潜在空间中。

2. **表情编码与扩散训练（Expression Encoding & Diffusion）**：
   - 训练数据为优化得到的 NPHM 表情序列$$\theta^{exp}_{1:N}$$（在 §5 中描述）。
   - 采用标准的前向扩散过程，对随机采样的时间戳$$t \sim \text{Uniform}(0, T)$$加入噪声。
   - 表情解码器为**堆叠的多头 Transformer 解码器**，包含：
     - **自注意力层**：使用 look-ahead 二进制掩码矩阵$$T_{ij}$$，防止模型窥探未来帧；
     - **交叉注意力层**：通过**表达式-音频对齐掩码**$$M = \delta_{ij}$$（克罗内克δ函数），确保第$$i$$帧音频特征只与第$$i$$帧表情特征对齐，从而保证唇形同步；
     - **FiLM（Feature-wise Linear Modulation）层**：在自注意力、交叉注意力和前馈网络之间插入，用于融合扩散时间戳嵌入，对生成质量非常关键。
   - 训练损失为标准的条件扩散损失：
     $$L_\theta = E_{x,t}[\|x - G_\theta(x_t, t, c)\|_2^2]$$

3. **表情增强（Expression Augmentation）**：
   - 为缓解语音驱动面部动画容易过拟合的问题，提出随机放大/抑制表情幅度的增强策略：随机采样调制因子$$r \sim \text{Uniform}(a, b)$$，将表情编码缩放为$$r \times \theta^{exp}$$。
   - 该方法在保持唇音同步的前提下有效地增加了生成表情的多样性。

4. **采样（Sampling）**：
   - 使用**无分类器引导（Classifier-Free Guidance）**，训练时以 25% 概率随机将音频替换为空条件。
   - 推理时，对条件生成与无条件生成结果进行加权组合，引导强度$$w > 1$$可增强音频条件的影响。

5. **序列后处理（Sequence Generation）**：
   - 预测出的表情编码送入冻结的 NPHM 表情 MLP 得到表达式形变（deformations）。
   - 使用**基于高斯核的面部平滑**（以嘴部为中心，3D 高斯核加权），抑制头部和颈部区域的抖动与闪烁伪影。
   - 最终通过 Marching Cubes 从 SDF 中提取网格序列。

### 2.3 数据集构建策略

- 由于不存在现成的「音频-NPHM 表情」配对数据，作者基于 **NeRSemble 数据集**（16 相机多视角录制）优化得到对应的 NPHM 表情序列。
- 流程：COLMAP 提取点云 → 在固定身份编码$$\theta_{id}$$的条件下，以滑动窗口（n=10 帧、重叠 2 帧）方式优化表情编码$$\theta^{exp}_{i}$$。
- 优化损失函数：
  $$L_{total} = \lambda_{sdf} L_{sdf} + \lambda_{temp} L_{temp} + \lambda_{reg} L_{reg}$$
  其中$$L_{sdf}$$为 SDF 损失，$$L_{temp}$$为时序平滑损失（Huber），$$L_{reg}$$为表情编码的 L2 正则化，以避免偏离 NPHM 先验分布。
- 最终构建了包含 **1000 个序列**的 FaceTalk 数据集。

## 3. 实验设计：数据集、基准与对比方法

- **数据集**：
  - **NeRSemble**：16 相机多视角录制的人脸说话视频，用于优化 NPHM 表情序列作为训练数据。
  - **VOCA 数据集**（用于构造混合测试集的参考数据）、**LJSpeech**（用于长音频测试）。
  - 测试集构成为：100 条混合音频序列（25 条来自 VOCA + 25 条来自 FaceTalk + 50 条来自 LJSpeech），测试音频均来自所有方法训练时未见过的身份。

- **对比方法**：
  - **VOCA** [14]、**MeshTalk** [51]、**FaceFormer** [21]、**CodeTalker** [75]、**Imitator** [65]、**EmoTalk** [44]、**EMOTE** [15]。

- **评价指标**：
  - **LSE-D**（Lip Sync Error Distance）：唇音同步误差（越低越好）。
  - **FID** / **KID**：生成多样性/分布距离（仅评估嘴部区域裁剪，避免其余面部几何偏差）。
  - **FIQA**（Face Image Quality Assessment）：面部图像质量（越高越好）。
  - **VQA**（Video Quality Assessment）：视频整体质量（越高越好）。
  - **Diversity Score**：生成多样性。
  - **用户研究**：40 名参与者，15 条未见过的音频，分别从整体质量、唇音同步、面部真实感三个维度进行偏好比较。

## 4. 资源与算力

- **论文未明确报告**所使用的 GPU 型号、数量、训练时长等算力信息。仅在实现细节中提到使用 Adam 优化器、学习率 0.0001、扩散时间戳 1000 步、训练序列裁剪为 2 秒（48 帧）进行小批量训练，未交代具体硬件配置与训练成本。

## 5. 实验数量与充分性

本文共进行了以下几组实验，**整体充分性较高，但存在一定偏差风险**：

1. **主实验（定量对比）**：在混合测试集上与 7 种 SOTA 方法对比 5 项指标，FaceTalk 在 LSE-D、FID、KID、FIQA、VQA 上均取得最优。
2. **用户研究**：40 名参与者进行三方面偏好测试，FaceTalk 在整体质量（75.56%）、唇音同步（71.11%）、面部真实感（73.89%）上大幅胜出。
3. **定性可视化对比**：对真实音频片段渲染网格动画进行视觉比较。
4. **消融实验**（Table 2）：
   - 移除表达式增强（w/o expr. aug.）→ 多样性大幅下降；
   - 移除面部平滑（w/o facial smoothing）→ 出现帧间抖动；
   - 移除 FiLM 层（w/o FiLM layer）→ 唇音同步误差显著增大；
   - 移除表达式-音频对齐（w/o expr.-audio align.）→ 模型完全忽略音频，生成恒定表情；
   - 移除扩散（w/o diffusion）→ 仅能产生单一确定性结果（多样性几乎为 0）。
5. **泛化性展示**：将生成的表情编码迁移到不同身份（不同发型、耳形）上的效果，以及同一身份多样表情风格展示。

**充分性评估**：实验设计较全面，涵盖定量、定性、消融与用户研究，能较好地支撑各模块设计的有效性。但存在两个偏差风险：
- 测试集数量较少（100 条混合序列），且音频来源包含跨数据集组合，分布一致性存疑；
- 消融实验展示的是单一指标数值，未给出方差或显著性检验（如置信区间、p 值）。

## 6. 论文的主要结论与发现

- FaceTalk 首次实现了**音频驱动的体积化头部运动扩散生成**，能够合成包含头发、耳朵、复杂皱纹和精细眼部运动的 3D 头部动画序列。
- 在唇音同步、感知质量和生成多样性方面**全面优于现有 3DMM 模板方法**：LSE-D 达到 11.2737（最优），FID 仅 40.692（相比次优方法 201.311 大幅降低），用户研究中以约 72-75% 的偏好率胜出。
- **FiLM 条件调制**和**表达式-音频对齐掩码**是保证唇音同步和高质量表情的关键模块。
- **表达幅度增强**在保持音频一致性的前提下有效增加了生成多样性。
- **高斯面部平滑**能够显著抑制扩散生成中的帧间抖动与闪烁伪影。
- FaceTalk 生成的表达式编码与身份解耦，可无缝迁移到不同身份/形态的 NPHM 模型上。

## 7. 优点

- **表征创新**：首次将 NPHM（体积化 SDF 表征）与扩散生成模型结合，突破了 3DMM 在表达力上的瓶颈，提升了面部细节的真实感。
- **方法完备性**：从数据构建（基于点云优化的表情序列）、音频特征对齐、扩散模型设计到后处理平滑，形成了完整可复现的 pipeline。
- **时序一致性设计**：通过 look-ahead 掩码、表达式-音频对齐掩码以及高斯平滑多重机制保障了时序连贯性，避免了 3D 生成中常见的抖动问题。
- **多样性控制**：在音频约束较强的场景下，提出简单有效的表达式增强策略并配合无分类器引导，实现了可控的风格多样性。
- **高效的序列级生成**：相比逐帧回归或自回归方式，FaceTalk 一次生成整个序列，采样效率更高。
- **身份泛化能力**：表达式编码与身份解耦，可自由迁移到不同头部形状/风格，实用性较强。

## 8. 不足与局限

- **推理速度受限**：扩散模型需要多步（1000 步）去噪采样，难以满足实时应用需求；论文虽提到未来可用高效采样技术，但未在本文验证。
- **无法生成身份（identity）**：当前方法仅合成表情编码，头部形状和身份仍需由用户提供/预设，不是完整的"声音→完整头像"生成方案。
- **数据集偏差与规模**：
  - 训练完全基于 NeRSemble 单一的采集设置，面部身份多样性有限，可能造成对不同人口特征（如性别、年龄、种族）的表现偏差；
  - 优化得到的 NPHM 表情序列质量依赖 COLMAP 点云质量与 NPHM 身份空间覆盖程度。
- **无方差/显著性报告**：定量指标仅给出单一均值，未提供多次运行的标准差和统计显著性检验，削弱了结果可信度的论证。
- **缺乏对比组间的计算开销与模型参数报告**：无法评估其在实际部署中的相对成本。
- **未涉及表情-情感耦合**：对情感表达（如生气、悲伤）的建模能力未作充分探索，与 EmoTalk、EMOTE 等情感导向方法的对比也主要局限于定量分数。

（完）
