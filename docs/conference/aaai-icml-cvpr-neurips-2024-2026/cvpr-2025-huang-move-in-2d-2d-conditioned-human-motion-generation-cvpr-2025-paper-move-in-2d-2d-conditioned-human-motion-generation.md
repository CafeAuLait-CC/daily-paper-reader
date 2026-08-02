---
title: "Move-in-2D: 2D-Conditioned Human Motion Generation"
title_zh: 在二维中移动：二维条件的人体运动生成
authors: "Huang, Hsin-Ping, Zhou, Yang, Wang, Jui-Hsien, Liu, Difan, Liu, Feng, Yang, Ming-Hsuan, Xu, Zhan"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Huang_Move-in-2D_2D-Conditioned_Human_Motion_Generation_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 10.0
evidence: 基于扩散模型的场景与文本条件三维人体运动生成
tldr: 现有的高质量人体视频生成依赖已有动作序列，限制了场景适配。Move-in-2D提出以场景图像和文本为条件，利用扩散模型直接生成匹配场景的人体运动序列，无需从已有视频中提取动作。为了训练，作者构建了大规模单人活动视频数据集并对动作进行标注。实验显示该方法在多样性和场景匹配度上有显著优势，为二维条件驱动的动作生成提供了一种通用框架。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1802, \"height\": 698, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1425, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1797, \"height\": 500, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1797, \"height\": 846, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1800, \"height\": 527, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1802, \"height\": 733, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 858, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 849, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-huang-move-in-2d-2d-conditioned-human-motion-generation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 792, \"height\": 205, \"label\": \"Table\"}]"
motivation: 现有动作生成方法依赖从视频中提取的已有动作，难以适配不同场景，限制了生成多样性。
method: 利用扩散模型，以场景图像和文本提示为条件生成人体运动序列，并收集大规模单人活动视频数据集进行训练。
result: 实验证明该方法能生成与场景匹配且多样化的人体动作，显著提升泛化能力。
conclusion: Move-in-2D为二维图像条件的人体运动生成提供了有效且通用的方案，可扩展至多种场景。
---

## Abstract
Generating realistic human videos remains a challenging task, with the most effective methods currently relying on a human motion sequence as a control signal. Existing approaches often use existing motion extracted from other videos, which restricts applications to specific motion types and global scene matching. We propose Move-in-2D, a novel approach to generate human motion sequences conditioned on a scene image, allowing for diverse motion that adapts to different scenes. Our approach utilizes a diffusion model that accepts both a scene image and text prompt as inputs, producing a motion sequence tailored to the scene. To train this model, we collect a large-scale video dataset featuring single-human activities, annotating each video with the corresponding human motion as the target output. Experiments demonstrate that our method effectively predicts human motion that aligns with the scene image after projection. Furthermore, we show that the generated motion sequence improves human motion quality in video synthesis tasks.

---

## 论文详细总结（自动生成）

好的，我将根据提供的论文内容，为您生成一份详细的中文总结。

## 论文总结：Move-in-2D：2D条件下的自然人体运动生成

### 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：现有高质量人体视频生成方法高度依赖于预先存在的**驱动运动序列**（如从其他视频中提取的舞蹈或动作序列），这些序列通常受限于特定动作类型和全局场景匹配，难以适配多样化的新场景和文本描述。
- **研究空白**：文本驱动的运动生成方法缺乏场景感知，生成的 motion 难以无缝集成到特定环境中；而3D场景感知运动生成受限于3D数据获取成本高、重建耗时费力，且多局限于室内场景和简单动作（如行走、坐下）。
- **核心贡献（本文提出的新任务）**：正式定义并解决「**2D条件下的自然运动生成**」任务，即给定一张代表目标场景的2D图像和一段描述期望运动的文本提示，生成一个既符合文本描述、又能在投影到场景图像上时显得自然合理的运动序列。
- **意义**：该任务为人体运动生成引入了一种新模态（2D场景图像），通过输入图像即可实现场景兼容性，无需3D重建，极大地扩展了可应用的场景范围（如户外场景），并为下游的视频生成任务（two-pass pipeline）提供更可控且场景匹配的运动引导信号。

### 2. 方法论：核心思想、关键技术细节

- **总体框架（技术路线）**：基于**条件扩散模型（Conditional Diffusion Model）**。给定文本提示 \( p \) 和背景场景图像 \( s \)，模型旨在生成可自然投影到场景图像上的人体运动序列 \( x \)。

- **运动表示**：生成的 motion 序列包含 \( N = 256 \) 帧，每帧的维度 \( D = 147 \)。每帧由 **SMPL** 身体姿态参数（\( \theta_b \in \mathbb{R}^{23 \times 6} \)，23个关节的6D旋转）和全局方向参数（\( \theta_g \in \mathbb{R}^6 \)）构成。**关键创新点**：模型额外预测一个**相机平移参数** \( \pi \in \mathbb{R}^3 \)，并假设固定的针孔相机内参，以将SMPL空间点投影到2D图像平面，确保生成的 motion 在2D场景中的投影是自然的。

- **多条件Transformer架构**：
    - **条件编码**：扩散时间步 \( t \) 使用位置编码；文本提示 \( p \) 通过 **CLIP** 编码器编码；背景图像 \( s \) 通过 **DINO** 编码器编码以保留空间布局信息。
    - **条件注入机制**：
        - **In-context conditioning**：将文本和场景编码得到的 token 与运动序列 token 拼接，作为额外的上下文 token 输入Transformer，不计算其损失。
        - **Adaptive Layer Normalization (AdaLN)**：用于注入扩散时间步 \( t \)，由线性层预测缩放和偏移参数。
        - **Cross-attention layer**：在自注意力层后插入交叉注意力层以融合条件（消融实验发现比In-context效果差）。
    - **最终配置**：文本和场景条件采用In-context机制，时间步条件采用AdaLN机制。

- **训练策略（两阶段训练）**：
    - **第一阶段**：在全部30万视频数据集上训练60万次迭代，学习场景语义和基于文本的多样运动生成。
    - **第二阶段**：在一个由15万视频（60%大运动 + 40%固定背景）组成的混合数据集上微调60万次迭代，以解耦相机运动（选择一个静态背景帧作为场景条件）并增强大幅度运动动态的生成能力。
    - **条件丢弃**：训练时以10%的概率随机丢弃文本和场景条件，以支持Classifier-free guidance (CFG)采样。

### 3. 实验设计：数据集、Benchmark与对比方法

- **新数据集（HiC-Motion）**：由于没有现成的满足条件的数据集，作者从内部30M开放域网络视频中，通过关键点检测和筛选，构建了**HiC-Motion数据集**。该数据集包含 **300k** 段视频，涵盖室内外场景和超过1k种人类活动类别（从日常活动到体育运动）。使用4D-Humans提取SMPL格式的伪GT运动，并用Mask R-CNN和inpainting技术去除人物以获得背景图像。
- **Benchmark（评估集）**：从HiC-Motion的留出部分构建了 **957** 个测试样本，包含文本提示（100个高频动词短语）、场景图像和对应的GT运动序列。
- **对比方法**：
    - **文本条件模型**：MDM、MLD。
    - **场景条件模型（3D点云）**：SceneDiff、HUMANISE，以及经过数据增强的MDM+（在HiC-Motion上重新训练的MDM）。
    - **模型自身变体**：Ours（文本+场景）、Ours-scene（仅场景）。
- **评估任务**：
    - **量化评估**：使用基于STGCN的预训练运动分类器，计算FID、准确性（Accuracy）、多样性和多模态性指标。
    - **自动化VLM评估**：使用ChatGPT-4o对生成的运动（渲染中间帧）进行0-5分的打分，评估指标包括场景对齐度、文本对齐度和运动质量。
    - **下游任务评估**：将生成的运动作为控制信号，输入到Champ和商业模型进行人体视频生成，与Stable Video Diffusion (SVD)进行定性比较。

### 4. 资源与算力

- **论文未明确说明训练所使用的具体GPU型号、数量或总训练时长（小时）**。仅在实现细节中提及，模型训练 **120万次迭代**，batch size为128，使用Adam优化器（学习率0.0002），1000步扩散过程。

### 5. 实验数量与充分性

- **实验数量**：论文进行了较为全面的实验，包括：
    - **一组大规模量化评估**（Tab. 2），对比了7种方法（含变体）的4项指标。
    - **一组VLM自动化评估**（Tab. 3），对比了7种方法的3项指标。
    - **一组消融实验**（Tab. 4），评估了4种不同的条件注入组合。
    - **大量定性实验**，展示了不同场景下的运动生成效果和下游视频生成效果。
- **充分性与公平性分析**：
    - **优点**：评估较为全面。除了标准的量化指标，还引入了VLM评估，并验证了在下游视频生成任务中的有效性。消融实验清晰地验证了AdaLN + In-context 组合的有效性。
    - **可能的偏差与改进空间**：
        - **VLM评估的局限性**：作者选取了20个测试视频进行VLM评估，样本量较小，可能引入偏差。评估仅使用中间帧，无法全面反映一段运动序列的时间一致性和动态质量。
        - **公平性考量**：对比方法（如SceneDiff、HUMANISE）是在其特定的小规模3D场景数据上训练的，与在30万大规模数据上训练的模型进行直接比较，可能存在不公平性。虽然作者通过MDM+来弥补训练数据规模的差异，但场景条件的输入模态（3D点云 vs 2D图像）依然存在根本性不同。
        - **指标鲁棒性**：基于分类器的FID和准确性指标高度依赖于训练该分类器的数据分布，可能无法完全反映真实世界的运动质量。

### 6. 主要结论与发现

- 提出的Move-in-2D方法能够生成**与场景在几何和语义上兼容**、且**与文本描述高度一致**的人体运动序列。
- 模型能够生成**大幅度的运动动态**（如打网球、跳蹦床），这些是现有视频生成模型难以处理的复杂活动。
- 在FID、准确性和多样性等量化指标上，Move-in-2D全面优于所有对比方法（包括文本条件、3D场景条件和多模态条件模型）。
- 通过VLM评估证实了其生成的运动在场景对齐、文本对齐和姿态质量方面具有显著优势。
- 证明了该方法生成的运动序列，可以作为优秀的控制信号，提升下游**运动引导的人体视频生成**的质量（优于无引导的Stable Video Diffusion）。

### 7. 优点：方法与实验设计亮点

- **任务新颖且实用**：提出并解决了2D场景图像条件下的运动生成任务，比依赖3D重建的方法门槛更低、适用场景更广。为两阶段视频生成提供了有效方案。
- **数据集规模大**：构建了目前最大的、包含动作、文本和多样化场景的 **300k** 规模数据集HiC-Motion，极大推动了该方向的研究。
- **方法设计巧妙**：预测相机参数的策略，使得模型生成的运动天生适配2D图像平面；利用in-context learning思想处理多条件输入，优于简单的交叉注意力机制。
- **实验设计紧凑**：涵盖了从量化指标、VLM评估到下游应用的全链路验证，并设计了消融实验来证明各设计组件的有效性。

### 8. 不足与局限

- **相机运动不可控**：框架不控制生成运动中的相机运动，限制了其模拟动态镜头的能力。
- **两阶段流程非端到端优化**：运动生成和视频生成是两个独立的阶段，未实现联合优化，可能无法达到全局最优。
- **依赖数据与注释质量**：训练数据来自网络视频且依赖4D-Humans提供伪GT，运动标注的精度和多样性存在上限。数据过滤流程复杂，可能引入选择偏差。
- **场景兼容性有限**：虽然模型能生成投影后合理的运动，但对复杂的人类-场景物理交互（如坐在特定椅子上）的支持能力未得到深入验证，主要依赖2D图像的语义和布局信息进行推断。
- **手动评估的潜在偏差**：VLM评估的样本量小，且对姿态“质量”的评估主观性强，可能存在评估不全面的风险。

（完）
