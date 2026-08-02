---
title: "Shape My Moves: Text-Driven Shape-Aware Synthesis of Human Motions"
title_zh: Shape My Moves：文本驱动的体型感知人体动作合成
authors: "Liao, Ting-Hsuan, Zhou, Yi, Shen, Yu, Huang, Chun-Hao Paul, Mitra, Saayan, Huang, Jia-Bin, Bhattacharya, Uttaran"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Liao_Shape_My_Moves_Text-Driven_Shape-Aware_Synthesis_of_Human_Motions_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 文本驱动的体型感知三维人体动作合成
tldr: 现有文本到动作生成通常默认同质化体型，忽略体型对动作的影响。本文提出体型感知的动作生成方法，利用有限标量量化变分自编码器将动作离散化，并利用连续体型信息去量化得到精细动作，同时借助预训练语言模型预测动作标记。实验表明，该方法能生成更贴合不同体型的自然动作。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1821, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1565, \"height\": 897, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1788, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1786, \"height\": 266, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1807, \"height\": 346, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1804, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 865, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-liao-shape-my-moves-text-driven-shape-aware-synthesis-of-human-motions-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 859, \"height\": 129, \"label\": \"Table\"}]"
motivation: 主流方法学习同质化标准体型，导致动作与真实体型不匹配。
method: 使用FSQ-VAE将动作量化，并结合体型信息解码，用预训练语言模型生成动作标记。
result: 生成的体型相关动作更自然、多样。
conclusion: 在动作生成中引入体型条件可提升真实感与个性化。
---

## Abstract
We explore how body shapes influence human motion synthesis, an aspect often overlooked in existing text-to-motion generation methods due to the ease of learning a homogenized, canonical body shape. However, this homogenization can distort the natural correlations between different body shapes and their motion dynamics. Our method addresses this gap by generating body-shape-aware human motions from natural language prompts. We utilize a finite scalar quantization-based variational autoencoder (FSQ-VAE) to quantize motion into discrete tokens and then leverage continuous body shape information to de-quantize these tokens back into continuous, detailed motion. Additionally, we harness the capabilities of a pretrained language model to predict both continuous shape parameters and motion tokens, facilitating the synthesis of text-aligned motions and decoding them into shape-aware motions. We evaluate our method quantitatively and qualitatively, and also conduct a comprehensive perceptual study to demonstrate its efficacy in generating shape-aware motions.

---

## 论文详细总结（自动生成）

# Shape My Moves：文本驱动的体型感知人体动作合成——论文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **背景**：近年来文本到动作生成（text-to-motion）取得了显著进展，但现有方法大多将人体动作映射到一个**同质化的标准体型（canonical body shape）** 上进行学习与生成，忽略了真实世界中不同体型对动作动力学的影响。
- **核心问题**：同一动作由不同体型的人执行时，在生理表现上存在显著差异（如步幅、肢体协调、重心变化等）。现有方法将动作“标准化”到统一骨架后，会导致：
  - 生成的动作与真实体型不匹配；
  - 在动作重定向（motion retargeting）时产生伪影（如自相交、脚部滑步、姿态不自然）；
  - 无法泛化到多样化的身体形态。
- **整体含义**：论文主张将**体型信息（body shape）显式地引入动作生成过程**，实现从自然语言描述同时生成“体型参数”和“符合该体型的动作”，从而提升动作的真实感、个性化和物理合理性。

## 2. 论文提出的方法论

### 核心思想
- 采用**两阶段框架**：
  1. **SA-VAE（Shape-Aware FSQ-VAE）**：将形状归一化动作（shape-normalized motion）量化为离散 token，并在解码时注入连续体型信息，重建出体型感知动作（shape-aware motion）。
  2. **ShapeMove**：基于预训练语言模型（T5），从文本输入同时预测体型参数和动作 token 序列，最终通过 SA-VAE 解码器生成动作。

### 关键技术细节

#### 数据预处理
- 使用 SMPL 模型的形状参数 β 提取六项体型属性：身高、臂长、腿长、胸围、腰围、臀围，构成体型描述。
- 利用 Shapy 的 A2S 模型生成额外合成体型，进行数据增强（替换 10% 的 ground-truth 形状参数）。
- 动作表示沿用 HumanML3D 的预处理流程（D=263 维），但**跳过体型归一化步骤**，保留体型差异，记为 XR；对应的归一化版本记为 XN。

#### SA-VAE 结构
- **编码器 E** 输入形状归一化动作 XN，输出下采样后的动作特征 Z（τ 帧，512 维）。
- 使用 **FSQ（Finite Scalar Quantization）** 作为量化器（码本大小为 1000，维度配置 ℓ=[8,5,5,5]），避免传统 VQ 的码本坍塌问题，无需额外正则化。
- 通过两个 MLP（θm 和 φm）将特征变换到目标码本维度。
- **解码器 D** 接收离散动作特征 ˆZ 与体型特征 ˜β（由投影器 Pθs 从 β 映射到 32 维）的拼接，重建体型感知动作 ˆX。
- **损失函数**：
  - 重建损失：平滑 L1 损失，包含整体动作和旋转信息的加权项（λrot）。
  - 物理损失：浮动损失（Lfloat）、脚滑损失（Lslide）、骨长损失（Lbone），约束生成动作的物理合理性。
  - 总损失：Lvq = Lr + λf Lfloat + λs Lslide + λb Lbone。

#### ShapeMove 框架
- 在语言模型词表中增加 k+2 个动作 token（k=1000 个码本索引 + 起始/结束符）以及 1 个形状 token `[BETA]`。
- 训练时，文本输入被编码，目标输出为 `[BETA]` 后接动作 token 序列；`[BETA]` 对应的嵌入经过投影器 Pθe 回归连续体型参数 ˆβ。
- 损失函数：
  - 交叉熵损失（Ltoken）用于动作 token 预测；
  - L1 损失（Lshape）用于体型参数回归，加权系数 λβ。
- 推理时，模型输出动作 token 与体型参数，经 FSQ 反量化、与体型特征拼接后由解码器生成最终动作。

## 3. 实验设计

### 数据集与场景
- **HumanML3D**：最大规模文本-动作数据集，包含 14,616 个动作序列和 44,970 条文本描述，动作来自 AMASS 和 HumanAct12 的 449 个不同受试者。
- 预处理沿用 HumanML3D 标准流程，但**保留体型差异**，不使用标准骨架归一化。

### 对比方法
- 与七种主流方法对比：T2M、TM2T、MLD、MotionDiffuse、MDM、T2M-GPT、MotionGPT。
- 所有基线均使用相同的体型感知训练数据重新训练；T2M 和 TM2T 因文本编码器词汇限制无法输入体型描述，仅输入动作描述作为参考。
- 评估指标包括：
  - **物理合理性**：Penetrate（地面穿透）、Float（漂浮）、Skate（脚滑）、Bone Length Variances（骨长方差，本文新提出）；
  - **文本-动作对齐与动作质量**：R-Precision、FID、MM-Dist、Diversity。

### 额外实验
- **量化器重建对比**：将 SA-VAE 与 TM2T、T2M-GPT、MotionGPT 的量化器对比，指标包括 FID、骨长差异、抖动差异。
- **消融实验**：逐一移除体型条件、骨长损失、浮动损失、脚滑损失，观察各组件贡献。
- **体型属性预测**：报告六项属性预测值与 ground truth 的平均差异（由于尚无并发预测体型参数的工作，仅评估本文方法）。
- **人类感知评估**：在 Amazon Mechanical Turk 上招募 45 名受试者，对 34 个随机文本描述生成样本进行两两比较，评估“形状-文本匹配”、“动作-文本匹配”、“动作-体型合理性”三个维度。

## 4. 资源与算力

- **SA-VAE 训练**：单张 A100 GPU 上训练约 **12 小时**（200K 迭代，学习率 2e−4；再 100K 迭代，学习率 1e−5，batch size 256）。
- **ShapeMove 训练**：
  - 第一阶段（文本↔动作双任务）：**8 张 A100 GPU，训练 120K 迭代，约 1 天**；
  - 第二阶段（仅文本到动作）：**8 张 A100 GPU，额外 30K 步，约 10 小时**。
- 论文明确给出了上述算力信息，但对整体能耗、显存占用等未做进一步说明。

## 5. 实验数量与充分性

### 实验数量
- 定量对比实验（表 1）：包含 7 种基线方法的物理与文本对齐指标；
- 量化器重建对比（表 2）：与 3 种基于量化的方法对比；
- 消融实验（表 3）：5 组配置逐步加入组件；
- 体型属性预测（表 4）：6 项属性误差报告；
- 定性可视化：多组动作序列对比；
- 人类感知研究：3 个评估维度 × 4 种对比对象（3 种基线 + ground truth）。

### 充分性与客观性评估
- **优点**：覆盖了定量、定性、消融、感知多个层面，对比方法与自身框架一致，评估维度较全面；物理指标上还排除了攀爬等非地面动作，保证指标有效性；消融实验证明了各损失组件的贡献。
- **潜在不足**：
  - 基线方法在重新训练时，部分方法（T2M、TM2T）无法输入体型描述，公平性受限；
  - 感知研究仅 45 名受试者、34 个文本描述，样本量不算大；
  - 消融实验中某些指标（如 FID）在添加部分损失后出现波动，模型选择的解释可更充分；
  - 所有实验基于单一数据集（HumanML3D），跨数据集泛化未验证。

## 6. 论文的主要结论与发现

- 提出的 **SA-VAE 能有效量化形状归一化动作，并在体型条件下重建出更准确的体型感知动作**，相比现有量化方法，骨长误差降低约一半。
- **ShapeMove 框架能从文本联合预测体型参数和动作 token**，生成的动作在物理合理性（穿透、漂浮、脚滑、骨长稳定）和文本对齐指标上优于大多数同设置基线，甚至在某些指标上超过需要 ground-truth 长度的扩散方法。
- 人类感知研究表明，**本方法生成的动作在形状匹配、动作匹配和整体合理性上接近 ground truth，并显著优于基线**（偏好率高出约 12%–38%）。
- 体型参数预测误差约 1 cm，说明模型能够准确理解文本中的体型描述。

## 7. 优点

- **问题新颖且重要**：首次系统性地在文本到动作生成中显式建模体型与动作的关联，填补了现有方法的空白。
- **方法设计巧妙**：将连续体型信息与离散动作 token 结合，通过 FSQ-VAE 解耦“动作内容”与“体型风格”，既利用了语言模型强大的序列建模能力，又避免了纯离散编码对连续体型信息的损失。
- **物理约束完善**：引入多种物理损失（穿透、漂浮、脚滑、骨长）显著提升生成动作的物理合理性。
- **实验全面**：包含定量、定性、消融、感知研究，结果可信度高；同时提出新的“骨长方差”指标，用于衡量动作形态稳定性。
- **工程细节扎实**：提供了数据增强（合成体型）策略，缓解了现有数据集体型多样性不足的问题。

## 8. 不足与局限

- **形状描述模板受限**：预处理要求体型描述遵循特定模板（如“身高 175 cm，腿长 70 cm”），对自由形式的自然语言描述鲁棒性不足。作者建议未来可用大语言模型标准化描述或引入更丰富的描述风格数据。
- **数据集单一**：仅在 HumanML3D 上验证，未在 KIT-ML 等其他文本-动作数据集上测试，跨数据集泛化能力未知。
- **体型多样性依赖合成数据**：真实数据中体型分布仍有限，合成体型的真实性和多样性可能影响模型效果。
- **基线对比公平性局限**：部分基线无法接受体型描述输入，只能采用简化设置；另有一些需要 ground-truth 长度的方法在表中作为参考，不完全可比。
- **感知研究规模有限**：受试者数量和文本样本数相对较小，统计效力有限。
- **计算资源需求较高**：ShapeMove 训练需要 8×A100 GPU，且分两个阶段训练，对一般研究者复现成本较高。
- **实时性未讨论**：论文未提及推理速度，对于游戏、交互式应用等实时场景的适用性尚不清楚。

（完）
