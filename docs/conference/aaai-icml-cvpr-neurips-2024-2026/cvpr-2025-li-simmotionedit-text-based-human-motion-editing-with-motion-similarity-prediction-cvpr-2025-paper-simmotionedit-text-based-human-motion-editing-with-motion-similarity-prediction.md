---
title: "SimMotionEdit: Text-Based Human Motion Editing with Motion Similarity Prediction"
title_zh: SimMotionEdit：基于运动相似度预测的文本驱动人体运动编辑
authors: "Li, Zhengyuan, Cheng, Kai, Ghosh, Anindita, Bhattacharya, Uttaran, Gui, Liangyan, Bera, Aniket"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Li_SimMotionEdit_Text-Based_Human_Motion_Editing_with_Motion_Similarity_Prediction_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 4.0
evidence: 文本驱动的3D人体运动编辑；未使用流匹配或扩散方法
tldr: 该论文针对文本驱动的3D人体运动编辑任务，提出联合训练运动相似度预测以学习语义表示，并贡献了相关数据集。但方法并未涉及流匹配或扩散模型，属于3D运动生成相关领域的周边工作。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-simmotionedit-text-based-human-motion-editing-with-motion-similarity-prediction-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 723, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-simmotionedit-text-based-human-motion-editing-with-motion-similarity-prediction-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1659, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-simmotionedit-text-based-human-motion-editing-with-motion-similarity-prediction-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 871, \"height\": 1010, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-li-simmotionedit-text-based-human-motion-editing-with-motion-similarity-prediction-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1714, \"height\": 2277, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-simmotionedit-text-based-human-motion-editing-with-motion-similarity-prediction-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1689, \"height\": 509, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-simmotionedit-text-based-human-motion-editing-with-motion-similarity-prediction-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-li-simmotionedit-text-based-human-motion-editing-with-motion-similarity-prediction-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 316, \"label\": \"Table\"}]"
motivation: 现有文本驱动运动编辑难以精确控制，语义和语言指令易错位。
method: 引入运动相似度预测任务，与编辑任务多任务联合训练学习语义表示。
result: 提升了运动编辑的语义对齐效果，并发布了配套数据。
conclusion: 为运动编辑提供了一个有效的多任务学习范式。
---

## Abstract
Text-based 3D human motion editing is a critical yet challenging task in computer vision and graphics. While training-free approaches have been explored, the recent release of the MotionFix dataset, which includes source-text-motion triplets, has opened new avenues for training, yielding promising results. However, existing methods struggle with precise control, often leading to misalignment between motion semantics and language instructions. In this paper, we introduce a related task --- motion similarity prediction --- and propose a multi-task training paradigm, where we train the model jointly on motion editing and motion similarity prediction to foster the learning of semantically meaningful representations. To complement this task, we design an advanced Diffusion-Transformer-based architecture that separately handles motion similarity prediction and motion editing. Extensive experiments demonstrate the state-of-the-art performance of our approach in both editing alignment and fidelity.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

文本驱动的3D人体运动编辑是计算机视觉与图形学中的一个关键且具有挑战性的任务。该任务的目标是：给定一段源运动序列和一条文本编辑指令，生成符合文本语义且与源运动保持合理一致性的编辑后运动序列。

- **研究背景**：随着文本驱动运动生成技术的进步（如MDM、MotionDiffuse等），对现有运动序列进行精细编辑成为动画制作等工作流中的迫切需求。MotionFix数据集的发布提供了“源运动-文本指令-编辑后运动”三元组，使得有监督训练成为可能。
- **现存问题**：尽管已有方法（如训练免方法、基于注意力操作的方法）取得了一定效果，但现有方法普遍存在精细控制不足的问题，常导致运动语义与语言指令之间的错位（misalignment）。
- **核心动机**：作者提出，动画师在编辑运动时，通常不会直接开始编辑，而是先识别需要修改的关键帧。由此引出核心思想——**运动相似度预测**（Motion Similarity Prediction）作为辅助任务，帮助模型学习“哪些帧需要被编辑”这一语义信息，从而提升编辑对齐效果。
- **整体贡献**：提出了SimMotionEdit框架，通过多任务联合训练（运动编辑 + 运动相似度预测），使模型学习更具语义意义的表征，在编辑对齐性和保真度上均达到最先进水平。

## 2. 论文提出的方法论

### 2.1 整体架构：Motion Diffusion Transformer

模型由两大部分组成（如图2所示）：

- **Condition Transformer（条件Transformer）**：负责处理源运动序列X和文本指令L（经CLIP编码），执行辅助任务——运动相似度预测，并输出增强后的文本特征和运动特征。这两路特征通过辅助损失（auxiliary loss）进行交互融合。
- **Diffusion Transformer（扩散Transformer）**：接收增强后的运动特征与噪声化编辑运动的拼接序列，并通过AdaLN-Zero层注入增强文本特征和扩散时间步t，最终预测去噪后的编辑运动。

### 2.2 扩散模型公式化

采用标准的DDPM扩散范式，前向过程为：

- Mt = √ᾱt·M0 + √(1−ᾱt)·ε（迭代添加高斯噪声）
- 训练时直接预测原始运动信号M0，编辑损失为：
- Le = E[‖M0 − E(Mt, t, L, X)‖²₂]

### 2.3 运动相似度预测（辅助任务）

**（1）可预测的运动相似度曲线构建：**

- 基于关节旋转空间定义帧级相似度SRʳᵢ，使用滑动窗口（窗口大小为W）计算源运动每帧到编辑运动对应窗口内最近帧的距离（取负值作为相似度），以解决帧偏移问题。
- 对称地在关节位置空间计算SRˡᵢ，加权融合得到SRᵢ。
- 进行min-max归一化到[0,1]，以消除不同编辑指令造成的尺度差异（如“轻微动作”与“大幅动作”的相似度尺度不同）。
- 利用**MotionSNR**（运动信噪比）过滤低质量样本：基于top-κ和bottom-κ帧的相似度比值，过滤掉信噪比低于经验阈值的序列，因为这些序列的相似度曲线难以预测，会引入噪声。

**（2）辅助损失函数：**

- 将归一化相似度值SNᵢ量化（quantize）为K个类别（实验中取K=3最优）。
- 对每帧输出K维logits，通过softmax转换为概率，使用交叉熵损失作为辅助损失：
- Laux = −(1/F)·Σ log pᵢ,ₛᵢ

**量化而非回归的理由**：给定源运动和文本指令，可行的编辑运动有多个；回归会限制模型只能看到数据集中的特定编辑结果，而量化允许模型关注粗粒度的相似度层级，增强泛化能力。

### 2.4 总损失

总训练损失为：L = Laux + Le（辅助损失 + 编辑损失联合训练）。

## 3. 实验设计

### 3.1 数据集

- **MotionFix数据集**：文本驱动的3D运动编辑数据集，包含6,730个注释三元组（源运动、编辑后运动、文本指令），划分为训练集、验证集和测试集。

### 3.2 评估指标

- **对齐性（Alignment）**：基于预训练TMR模型提取特征，计算运动到运动检索的Top-1、Top-2、Top-3准确率（R@1/R@2/R@3），分别在batch size为32和完整测试集两种设置下报告，并报告平均排名（AvgR）。
- **保真度（Fidelity）**：使用**MotionCritic分数（M-score）**评估运动真实感。

### 3.3 对比基线

- **MDM**（Human Motion Diffusion Model）：仅以文本指令为输入的预训练扩散模型，不了解源运动信息。
- **MDM-BP**：在MDM基础上引入GPT辅助的身体部位检测，对未提及的身体部位遮罩保留源运动特征。
- **TMED**：专门在MotionFix上训练的条件扩散模型，同时利用源运动和文本指令进行编辑。

### 3.4 实现细节

- DDPM扩散步数300，使用余弦噪声调度器；文本编码采用预训练CLIP（ViT-B/32）；条件/扩散Transformer分别为4层和8层编码器层，8个注意力头，隐层维度512；batch size=128，AdamW优化器，学习率10⁻⁴，训练1,500个epoch；采用双向条件引导（guidance scale=2）。

## 4. 资源与算力

- **论文中明确提到**：模型在**单个A100 GPU**上训练约**1天**时间（1,500 epochs，batch size=128）。
- 对于数据预处理、消融实验等其他计算资源的使用情况，论文未作详细披露。

## 5. 实验数量与充分性

### 5.1 实验组数统计

论文共进行了以下实验：

- **主实验**：在MotionFix测试集上，与MDM、MDM-BP、TMED三个基线进行对比（Tab.1）。
- **消融实验一**：Motion Diffusion Transformer架构的消融——变化文本特征和运动特征的不同组合（增强/原始/缺失），共6种设置（Tab.2）。
- **消融实验二**：辅助损失函数的消融——对比回归损失vs分类损失，以及不同类别数（3/5/9类）的影响（Tab.3）。
- **消融实验三**：是否使用MotionSNR过滤（w/o filtering设置，Tab.1最后一行）。

### 5.2 充分性与客观性评估

- **优点**：消融设计较为全面，覆盖了主要设计决策（条件特征组合、损失形式、类别数、数据过滤），能够清楚验证各组件贡献；在batch和全测试集两种设置下报告结果，降低偶然性；与多个基线的对比具有足够区分度。
- **不足之处**：
  - 仅在**单一数据集（MotionFix）**上验证，缺乏跨数据集的泛化验证；
  - 未报告多次运行的标准差，无法判断结果的稳定性；
  - 主体指标（R@K）是基于TMR检索的间接评估，可能不完全等同于编辑语义的精确对齐；
  - M-score仅对TMED和Ours报告了数值，MDM和MDM-BP的M-score缺失，对比不够完整。

## 6. 论文的主要结论与发现

- SimMotionEdit在编辑对齐性（R@1/R@2/R@3、AvgR）和保真度（M-score）方面均全面超越现有基线，达到最先进水平。
- 运动相似度预测作为辅助任务能有效促进文本特征与源运动特征的交互融合，从而提升编辑性能。
- 运动相似度值采用**分类（量化）**损失优于**回归**损失，且类别数不宜过多（3类最优），说明辅助任务应保持简单以避免干扰主任务。
- 使用增强后的文本和运动特征比使用原始特征效果更好，且两者的联合增强在“对齐性”和“真实感”之间取得更好平衡。
- 过滤低MotionSNR（即相似度曲线难以预测）的训练样本有助于提升模型表现。

## 7. 优点

- **新颖的辅助任务设计**：将“识别需要编辑的帧”这一直观直觉形式化为运动相似度预测任务，思路清晰且具有可解释性，是该领域首次探索。
- **架构设计合理**：将条件Transformer（辅助任务）与扩散Transformer（生成任务）解耦，使两个模块各自专精，既避免了噪声化编辑运动对辅助任务学习的干扰，又加速和稳定了训练收敛。
- **工程细节扎实**：针对运动相似度曲线的可预测性问题，提出了滑动窗口匹配、min-max归一化、MotionSNR过滤等一系列工程化处理，展现了较强的分析能力。
- **量化损失的设计考量**：从“同一条件下多个可行编辑结果”的角度论证了分类损失优于回归损失的理论依据，设计具有洞察力。
- **高质量实验验证**：通过多层消融实验逐步验证了每个设计组件的必要性，结论可信度较高。

## 8. 不足与局限

- **单数据集验证**：实验仅在MotionFix上完成，缺乏在其他运动编辑数据上的泛化验证。由于MotionFix本身可能存在数据收集偏差（如特定动作类型、特定标注风格），模型的跨域泛化能力未知。
- **无大规模用户研究**：虽然M-score与人类感知有较好相关性，但本质仍是自动评估。论文未提供主观用户研究来进一步验证编辑质量的真实可用性，在动画制作等实际应用场景中的效果证据有限。
- **MotionSNR阈值的经验性**：过滤阈值为经验设定，缺乏对其影响的分析（如不同阈值下性能如何变化），可能存在数据选择偏差。
- **辅助任务在推理阶段的利用有限**：虽然辅助任务在训练阶段帮助学习了更好的特征，但推理时模型仅使用增强特征进行编辑，运动相似度预测本身的输出（作为显式信号）并未在推理时被使用，其潜力可能未被完全发挥。
- **基线对比可扩展性**：与更新、更强的基线（如基于大语言模型的两阶段方法或更近期的扩散编辑模型）的对比缺乏，可能削弱SOTA结论的时效性。
- **计算资源限制**：训练长达1,500个epoch在单卡上需1天，对于更大规模数据集或更高分辨率运动的可扩展性未作讨论。

（完）
