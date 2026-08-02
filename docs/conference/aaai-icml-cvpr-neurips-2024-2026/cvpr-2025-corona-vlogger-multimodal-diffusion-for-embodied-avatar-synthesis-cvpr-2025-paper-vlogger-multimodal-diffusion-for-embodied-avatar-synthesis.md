---
title: "VLOGGER: Multimodal Diffusion for Embodied Avatar Synthesis"
title_zh: VLOGGER：用于具身虚拟人生成的多模态扩散模型
authors: "Corona, Enric, Zanfir, Andrei, Bazavan, Eduard Gabriel, Kolotouros, Nikos, Alldieck, Thiemo, Sminchisescu, Cristian"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Corona_VLOGGER_Multimodal_Diffusion_for_Embodied_Avatar_Synthesis_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 10.0
evidence: 基于扩散的三维人体运动模型用于音频驱动的虚拟人生成
tldr: 从单张人物图像生成音频驱动的高质量视频仍是难点。VLOGGER提出包含两个组件的框架：一是随机的人体到三维运动扩散模型，二是带有空间和时间控制的新型扩散架构，可支持文本或语音控制的可变长度视频生成。该方法无需针对个人训练，不依赖人脸检测和裁剪，能生成完整图像。实验证明在人物视频合成任务上显著优于现有方法，为具身虚拟人的生成提供了一种统一的多模态扩散方案。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1447, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 916, \"height\": 390, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1699, \"height\": 660, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1803, \"height\": 402, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1811, \"height\": 1138, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 813, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 869, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-corona-vlogger-multimodal-diffusion-for-embodied-avatar-synthesis-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1789, \"height\": 956, \"label\": \"Table\"}]"
motivation: 现有方法依赖每人的训练或人脸裁剪，无法生成完整图像，且难以控制。
method: 结合三维运动扩散模型与时空控制扩散架构，从单图生成可控的高质量人物视频。
result: 实验在音频驱动人物视频生成上性能领先，支持可变长度和文本/语音控制。
conclusion: VLOGGER提供了一种无需针对个人训练的通用多模态扩散框架，用于逼真的具身虚拟人合成。
---

## Abstract
We propose VLOGGER, a method for audio-driven human video generation from a single input image of a person, which builds on the success of recent generative diffusion models. Our method consists of 1) a stochastic human-to-3d-motion diffusion model, and 2) a novel diffusion-based architecture that augments text-to-image models with both spatial and temporal controls. This supports the generation of high quality video of variable length, easily controllable through text or speech via high-level representations of human faces and bodies. In contrast to previous work, our method does not require training for each person, does not rely on face detection and cropping, generates the complete image (not just the face or the lips), and considers a broad spectrum of scenarios (e.g. visible torso or diverse subject identities) that are critical to correctly synthesize humans who communicate. We also curate MENTOR, a new and diverse dataset with 3d pose and expression anno- tations, one order of magnitude larger than previous ones (800,000 identities) and with dynamic gestures, where we train and ablate our main technical contributions. VLOGGER outperforms state-of-the-art methods in three public benchmarks, considering image quality, identity preservation and temporal consistency while also generating upperbody gestures. We analyze the performance of VLOGGER with respect to multiple diversity metrics, showing that our architectural choices and the use of MENTOR benefit training a fair and unbiased model at scale. Finally we show applications in video editing and personalization.

---

## 论文详细总结（自动生成）

# VLOGGER：用于具身虚拟人生成的多模态扩散模型 — 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **核心问题**：如何仅凭**一张人物图像**和**一段音频**，生成该人物说话时的高质量、长时间、逼真的视频？这需要同时协调头部运动、面部表情、唇部运动、视线、眨眼，以及更具挑战性的**上半身肢体动作和手势**。
- **研究动机**：
  - 音频驱动的虚拟人合成在内容创作、娱乐、在线教育、低带宽通信、个性化虚拟助手等领域有巨大需求。
  - 现有方法存在明显局限：① 许多方法需要为每个目标人物单独训练；② 严重依赖人脸检测与裁剪，无法处理可见躯干或手部的图像；③ 多数方法只生成面部或嘴唇区域，忽略身体动态；④ 人际交流不仅依赖语音+唇动，还依赖手势、视线、身体姿态等非语言线索，而现有方法普遍缺乏对这些要素的建模。
- **整体意义**：VLOGGER 提出了一个**通用（person-agnostic）、免逐人训练、无需人脸裁剪、能生成完整图像（含上半身和手势）**的音频驱动虚拟人合成框架，旨在弥合“可控图像生成”与“动态视频生成”之间的差距。

## 2. 论文提出的方法论：核心思想与技术细节

VLOGGER 采用**两阶段扩散模型流水线**：

### 2.1 阶段一：音频驱动的 3D 运动生成网络（M）

- **输入**：音频波形（梅尔频谱图），可选文本经 TTS 转换。
- **架构**：基于 Transformer，含 4 个多头时序注意力层，带有位置编码、因果掩码（只关注过去帧），以及音频和扩散步的嵌入 MLP。
- **输出**：逐帧的 3D 面部表情参数 $\theta_e^i$ 和身体姿态残差 $\Delta\theta_b^i$（身体姿态 = 参考姿态 + 残差，以保留输入图像的姿态）。
- **3D 人体模型**：使用参数化统计 3D 人体模型（如 GHUM），拟合输入图像得到身份形状码，渲染得到三类 2D 控制信号：
  - **密集图** $C_d$：将姿态化人体顶点栅格化为稠密 RGB 表示；
  - **语义图** $C_m$：不同语义区域的分割掩码；
  - **局部扭曲参考图** $C_w$：将参考图像像素颜色附着到可见顶点并随姿态重渲染。
- **损失函数**：
  - 扩散损失：$L_{diff} = \mathbb{E}\left[\|x_0 - x_0^\phi(x_t, t, a)\|_2^2\right]$（直接预测去噪后的真实分布）；
  - 时序平滑损失：$L_{temp} = \|x_0^\phi(x_t,t,a)_{i+1} - x_0^\phi(x_t,t,a)_i\|_2^2$，对表情和身体姿态使用不同权重。

### 2.2 阶段二：时空控制的图像扩散生成网络

- **基础架构**：基于 Imagen 文本-图像扩散模型，借鉴 ControlNet 思路——冻结原模型，新增零初始化的可训练编码器副本，接收时序控制信号 $C$。
- **时空扩展**：在编码器每个下采样块的第一个卷积层后、第二个 GroupNorm 前，插入**时间维 1D 卷积层**，实现跨帧时序建模。
- **训练策略**：两阶段训练——先在单帧上训练新控制层以快速学习人脸重演任务，再在视频序列上微调时间模块。基于视频的模型在 MENTOR 上训练，参考帧选择与目标片段距离较远的帧以增强泛化。
- **超分辨率**：基础模型生成 128×128 视频，级联两个超分辨率扩散模型提升至 256×256 和 512×512。
- **变长视频生成——时间外扩（temporal outpainting）**：先生成 N 帧，然后基于前 N−N′ 帧迭代外扩生成后续视频，相邻片段有 50% 重叠，可扩展到数千帧。
- **损失函数**：标准扩散噪声预测损失 $L_{diff} = \mathbb{E}\left[\|\epsilon_I - \epsilon_I^\phi(x_t, C, t)\|_2^2\right]$。

## 3. 实验设计：数据集、评测基准与对比方法

### 3.1 数据集

- **MENTOR（新提出）**：从大规模单说话人视频库中构建，包含 **800K 个身份、2200 小时（8M 秒）训练数据、120 小时测试数据**，带 3D 姿态和表情标注，含动态手势，规模比此前数据集大一个数量级。
- **HDTF**、**TalkingHead-1KH**：公开音频驱动说话头生成基准测试集。

### 3.2 对比方法

与 MakeItTalk、Audio2Head、Wang et al.、SadTalker、StyleTalk 共 5 种 SOTA 方法对比。（注意：所有基线均需裁剪人脸区域，无法处理全身可见的图像。）

### 3.3 评估指标

- **图像质量**：FID、CPBD（清晰度）、NIQE（自然度）
- **唇音同步**：LME（唇部关键点误差）、LSE-D
- **身份保持**：ArcFace 距离
- **时间一致性**：Jitter / jerk 误差（顶点抖动）
- **多样性**：生成视频中表情参数的标注标准差；另报告多次生成（Best of 3/5/8）时的平均指标
- **公平性/偏差**：按可见身体部位、肤色、年龄、感知性别分组分析

## 4. 资源与算力

- **论文未明确披露** GPU 型号、GPU 数量、总训练时长等具体算力信息。
- 仅提及训练设置：基础图像分辨率 128×128（级联 256/512），学习率 5e-5，训练 400K 步，batch size 128，两阶段训练（先单帧后视频）。
- 推理时使用 DDIM 采样，具体推理耗时未报告。

## 5. 实验数量与充分性评估

- **主实验**：在 HDTF 和 TalkingHead-1KH 两个公开基准上与 5 种 SOTA 方法进行多指标（9 项指标）定量比较，结果在两个数据集上保持一致趋势。
- **消融实验**：
  - 运动生成部分：去除残差预测（∆）、去除时序损失、去除分类器自由引导（CFG）三组对照；
  - 视频生成部分：去除身体控制、无时间外扩、25% 重叠外扩、完整模型（50% 重叠）等 4 组对照；
  - 2D 控制表示：2D 关键点 vs. 密集控制 vs. +扭曲参考图 vs. +训练调度，共 4 组对照。
- **多样性/公平性分析**：在 MENTOR 测试集上按可见身体部位（紧脸/头+躯干/躯干+手）、肤色（浅/中/深）、年龄、感知性别四个维度分组，对抗性分析模型偏差。
- **定性比较**：多图展示与基线在姿态、表情变化、身体可见性上的对比。

**充分性评价**：实验设计总体较为充分，定量指标覆盖了图像质量、唇音同步、身份保持、时间一致性和多样性五个关键维度，消融实验系统验证了主要设计决策。**但存在一定局限性**（详见第 8 点）。

## 6. 论文的主要结论与发现

- **性能全面领先**：在 HDTF 和 TalkingHead-1KH 上，VLOGGER 获得最低的 FID、最高的 CPBD/NIQE（图像质量更优）、最佳身份保持（ArcFace），时间一致性与真实视频接近（仅 StyleTalk 抖动更低，但 StyleTalk 几乎不产生面部运动）。
- **表达多样性**：生成视频中的表情多样性与真实视频相近，优于所有基线；多次生成的“Best of k”策略可进一步提升所有指标。
- **手势能力**：VLOGGER 是首个在音频驱动合成中支持可见躯干和手部动作的扩散方法（定性验证）。
- **公平性**：得益于大规模多样化数据（MENTOR）和大预训练模型的先验，VLOGGER 在肤色、年龄、性别各分组上性能一致，偏差远小于基线；基线在深肤色、老年人等分组中显著退化，且无法处理含躯干/手部的输入。
- **可控性与扩展性**：可基于文本或音频控制，支持任意长度视频生成，可编辑特定区域（如唇部、面部区域），并适用于视频编辑与个性化任务。

## 7. 优点与亮点

- **无需逐人训练**：单一模型即可泛化到任意新身份。
- **不依赖人脸裁剪**：可处理躯干、手部可见的远景图像，覆盖更广的真实场景。
- **完整的肢体建模**：通过统计 3D 人体模型将面部表情、头部姿态、身体运动和手势统一在一个表示空间中，并配合局部扭曲参考图显著提升身份保持度（消融实验中 PSNR 从 20.1→21.6→22.2 逐步提升）。
- **时间外扩策略**：巧妙解决了扩散模型只能生成长度固定短片的问题，支持可变长度、低抖动的长视频生成。
- **大规模数据集贡献**：MENTOR 数据集规模为此前最大数据集的 10 倍，包含手势和丰富的多样性标注，为社区提供了有价值的训练资源。
- **公平性分析前置**：系统性地从多个人口统计维度评估了模型的偏差表现，这在同类论文中较少见。
- **兼顾随机性和可控性**：扩散模型天然建模语音到姿势的“一对多”映射，同时通过 3D 控制和参考图保持身份和唇音同步。

## 8. 不足与局限

- **算力资源未披露**：未报告 GPU 型号/数量/总训练时长，复现成本难以评估，且论文中未讨论训练和推理的效率问题。
- **手势一致性缺少定量评估**：论文承认“身体/手势运动只用定性方式评估”，未定量衡量手势与语音内容的语义一致性，手势相关性缺乏用户研究支持。
- **对比公平性存疑**：所有基线方法都要求裁剪人脸，而 VLOGGER 处理全图，这是方法定位差异，但并非完全对等的对比条件；此外唇音同步（LME/LSE-D）各方法得分接近，VLOGGER 的优势主要体现在其他维度。
- **头部运动幅度偏小**：Jitter 结果中 StyleTalk 更平滑，但 VLOGGER 的抖动高于真实视频，表明时间一致性仍有提升空间（尽管这是运动丰富性带来的权衡）。
- **数据与伦理风险**：依赖大规模人脸/人体视频数据训练，存在潜在的隐私、肖像权滥用和深度伪造风险；论文未深入讨论生成内容的伦理限制和检测手段。
- **模型依赖 3D 拟合质量**：整个流程依赖统计人体模型拟合输入图像的准确性，极端姿态、遮挡、特殊外形等情况下拟合误差可能直接扩散到生成结果，鲁棒性未充分测试。
- **分辨率限制**：虽然支持 512×512，但相较于当前视频生成领域动辄 1080p 的标准仍有差距，且未分析分辨率提升对细节质量的影响。

（完）
