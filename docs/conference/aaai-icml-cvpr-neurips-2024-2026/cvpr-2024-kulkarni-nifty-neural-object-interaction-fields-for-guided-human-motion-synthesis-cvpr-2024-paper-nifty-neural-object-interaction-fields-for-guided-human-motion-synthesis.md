---
title: "NIFTY: Neural Object Interaction Fields for Guided Human Motion Synthesis"
title_zh: NIFTY：神经对象交互场引导的人体运动合成
authors: "Kulkarni, Nilesh, Rempe, Davis, Genova, Kyle, Kundu, Abhijit, Johnson, Justin, Fouhey, David, Guibas, Leonidas"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Kulkarni_NIFTY_Neural_Object_Interaction_Fields_for_Guided_Human_Motion_Synthesis_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 使用带交互场的扩散模型合成逼真的3D人体运动
tldr: 针对人与物体交互的3D运动生成问题，本文提出NIFTY方法：为物体建立神经交互场，输出人体姿态到有效交互流形的距离，并以此为引导约束物体条件的人体运动扩散模型采样。同时设计了自动合成数据管线，利用预训练运动模型和锚点姿态补充稀缺交互数据。实验证明该方法能生成物理合理、接触自然的交互式3D人体运动。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 854, \"height\": 434, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1704, \"height\": 698, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 824, \"height\": 594, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1717, \"height\": 610, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 746, \"height\": 356, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1602, \"height\": 1049, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 875, \"height\": 459, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-kulkarni-nifty-neural-object-interaction-fields-for-guided-human-motion-synthesis-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 877, \"height\": 380, \"label\": \"Table\"}]"
motivation: 生成与物体自然交互的3D人体运动很难，且交互数据稀缺。
method: 构造物体特定的神经交互场，以距离函数引导扩散模型采样，并结合合成数据管线增加交互样本。
result: 引导扩散模型生成的交互运动在接触和语义上更合理，显著优于基准方法。
conclusion: 为物体条件的人体运动合成提供了可泛化的交互场引导机制。
---

## Abstract
We address the problem of generating realistic 3D motions of humans interacting with objects in a scene. Our key idea is to create a neural interaction field attached to a specific object which outputs the distance to the valid interaction manifold given a human pose as input. This interaction field guides the sampling of an object-conditioned human motion diffusion model so as to encourage plausible contacts and affordance semantics. To support interactions with scarcely available data we propose an automated synthetic data pipeline. For this we seed a pre-trained motion model which has priors for the basics of human movement with interaction-specific anchor poses extracted from limited motion capture data. Using our guided diffusion model trained on generated synthetic data we synthesize realistic motions for sitting and lifting with several objects outperforming alternative approaches in terms of motion quality and successful action completion. We call our framework NIFTY: Neural Interaction Fields for Trajectory sYnthesis.

---

## 论文详细总结（自动生成）

# NIFTY：神经对象交互场引导的人体运动合成（CVPR 2024）——论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：生成逼真的、人与场景中物体交互的 3D 人体运动，具体聚焦于交互的“最后一英里”——即人接近物体、发起并完成接触（如坐椅子、举起箱子）这一关键阶段。论文明确指出，与整个场景导航（主要是碰撞避免）不同，解决“最后一英里”必须考虑物体的可供性（affordance）和接触变化对人体运动的影响。
- **主要挑战**：
  - **建模难题**：现有生成式人体运动模型（如 MDM、MoGlow）能生成逼真运动，但对场景上下文无感知；基于场景条件的方法存在多阶段、依赖后处理优化或手工设计约束等缺陷，容易产生穿模、脚滑等物理伪影。
  - **数据稀缺**：高质量的人-物交互动作捕捉数据（如 BEHAVE）规模小、范围有限；全场景数据质量参差；扩展采集新物体和动作的成本高昂。
- **论文贡献**（三方面）：
  1. 提出 **物体交互场**（Object Interaction Field），以数据驱动方式引导物体条件的人体运动扩散模型在采样阶段生成合理交互。
  2. 提出 **自动合成数据管线**，仅需少量交互锚点姿态（anchor poses）即可生成大规模多样的交互运动数据。
  3. 在坐（sitting）和举（lifting）两类交互、多种物体上实现高质量运动合成，优于现有方法。

## 2. 论文提出的方法论：核心思想、关键技术细节

### 整体框架
NIFTY 由三大核心组件构成：
- **物体条件的运动扩散模型** Mθ（负责生成候选运动）
- **物体交互场** Fφ（以引导目标 G 的形式在采样时校正运动）
- **自动合成数据生成管线**（解决训练数据不足的问题）

### 2.1 运动扩散模型（Motion Generation through Diffusion）
- **运动表示**：每一帧姿态 Xi 由 SMPL 模型的 22 个关节的关节位置 jp、6D 旋转 jr、速度 jv、角速度 jω，以及全局平移 tp 和速度 tv 组成；一段运动为 N 帧姿态序列 τ。
- **模型结构**：采用仅编码器的 Transformer 架构（类似 MDM）。去噪过程以噪声轨迹 τk、扩散步数 k、条件 C 为输入，直接预测最终干净信号 τ̂0，训练目标为 ∥τ̂0 − τ0∥²₂。
- **条件 C**：{Po（物体点云，经 PointNet 编码）, Ro（刚体姿态）, b（SMPL 形状参数）, X0（起始姿态）}。
- **采样与引导**：采用类似 Video Diffusion 的引导公式，在每个去噪步骤中用引导目标的梯度扰动干净轨迹输出：
  τ̃0 = τ̂0 − α∇τk G(τ̂0)。共采样 10 个样本，取引导目标最优者输出。

### 2.2 物体交互场（Human-Object Interaction Field）
- **定义**：以物体局部坐标系定义的神经场 Fφ，输入简化人体姿态 X̃ = {jp, tp}，输出一个偏移向量 ∆X̃，将输入姿态投影到该物体的有效交互姿态流形（valid interaction manifold）上，使 X̃ + ∆X̃ 成为合理的交互姿态。该场可用于可视化：查询远离物体的姿态时，输出的校正向量指向物体（见论文 Fig. 3）。
- **引导目标**：若运动序列的最后姿态（交互锚点帧）应满足有效交互，则定义 G(τ) = ∥Fφ(X̃i)∥²₂ 作为引导目标，在去噪过程中推动姿态靠近有效交互流形。
- **训练方式**：利用扩散模型自身生成难例。将加噪后的真实交互运动输入扩散模型，预测的 τ̂0 视为无效交互运动，对应的真实 τ0 为有效运动，取各自最后帧构成训练对；另加随机刚体变换增强。损失函数为 L1 距离：∥Fφ(X̃N) − (ỸN − X̃N)∥₁。
- **架构**：仅编码器 Transformer，以姿态为 token，物体点云为条件 token；单一模型可处理多种物体。
- **关键优势**：与仅给标量距离的场（如 Pose-NDF）不同，偏移向量同时提供方向和距离，学习信号更强。

### 2.3 自动合成数据生成管线（Synthetic Data Generation）
- **锚点姿态选择**：从 BEHAVE 数据集手工挑选关键交互帧（如坐定瞬间、举物初始接触瞬间），作为合成运动的最后一帧。
- **时间反转的 HuMoR**：将预训练的场景无关运动模型 HuMoR 重新训练为时间反转模型（给定当前姿态预测过去而非未来），从锚点姿态出发反向生成整段运动，保证运动在构造上以目标姿态结束。
- **树状展开与过滤**：从锚点姿态开始，每次采样 30 帧后分支并行展开，形成指数增长的“运动树”；通过启发式过滤（碰撞物体、浮空、姿态不自然、静止不动）裁剪分支。树深度为 7，并过滤掉起点距物体 1 米以内的序列。
- **生成结果**：坐姿 174 个锚点 → 200K 序列（椅子、凳子、桌子、瑜伽球）；举物 72 个锚点 → 110K 序列。

## 3. 实验设计：数据集、场景与基准对比

### 3.1 数据集与测试场景
- **训练数据**：由上述管线合成的坐姿/举物交互数据集（不使用真实 BEHAVE 运动数据作为训练数据，仅取锚点）。
- **测试集**：为避免与训练数据同分布，**不使用**合成分发生成测试集，而是构建 500 个测试场景（每种动作各 500 个）：物体随机摆放、人以 HuMoR 生成的随机姿态为起点。所有方法在同一测试场景上比较。
- **User Study**：通过 hive.ai 进行，5 名用户对每对比较视频给出选择，共 2500 条响应；还有独立 Likert 评分比较合成数据 vs. AMASS 真实 MoCap。

### 3.2 比较的基线方法
- **SAMP**：自回归 VAE（GoalNet + MotionNet），用公开代码在本文合成数据上训练 4.8M 迭代，使用调度采样（scheduled sampling）。
- **cVAE**：HUMANISE 的变体，保留场景条件但移除语言条件，在合成数据上训练 600K 迭代。
- **cMDM**：即本文的物体条件扩散模型，但去掉交互场引导（消融引导机制）。

### 3.3 评估指标
- **用户偏好研究**（主指标）
- **Foot Skating（FS）**：脚接近地面时的平均速度，越低越好
- **D2O（Distance to Object）**：最后一帧人体到物体表面的最小距离，报告 ≤2cm 的百分比和 95 百分位数
- **Penetration（%Pen）**：接触段人体穿透物体表面的距离，报告 ≤2cm 的轨迹百分比
- **Skeleton Distance**：生成末帧姿态与合成数据中最近锚点姿态的距离
- **Contact IoU**：生成姿态与最近邻锚点姿态的接触顶点 IoU

## 4. 资源与算力

论文在实验部分明确报告了以下计算资源信息：
- **GPU**：NVIDIA A40 GPU，单卡训练。
- **训练时长**：扩散模型训练 600K 迭代（batch size 32，AdamW，学习率 1e-4），约 2 天；交互场训练 300K 迭代（学习率 5e-5，one-cycle LR），具体时长未单独说明。
- **推理耗时**：约 34 秒/样本（含 10 个并行样本的采样+引导）。
- **基线资源**：SAMP 训练 4.8M 迭代（未说明具体 GPU 时间），cVAE 训练 600K 迭代。
- **说明**：论文未提及使用的 GPU 数量（但从描述看似乎是单卡），也未报告总 GPU 小时数、数据生成（树状展开）所消耗的算力。

## 5. 实验数量与充分性评估

### 主要实验组
1. **用户研究**：坐姿和举物分别独立进行；NIFTY 与每个基线（SAMP、cVAE、cMDM）以及合成数据做对比。每项比较 5 用户 × 500 场景 = 2500 响应。
2. **定量指标对比**（Tab. 1）：两大动作（Sit/Lift）分别对比 4 种方法的 6 组指标。
3. **消融研究**（Tab. 2）：
   - **Distance OIF**：交互场输出改为标量距离（回归到流形距离）而非偏移向量；
   - **NIFTY (NN)**：非参数化最近邻版本（用训练集中最近锚点的差异做校正），假设测试时可访问全部交互训练姿态；
   - **NIFTY**：完整方法。
4. **数据质量评估**：用户 Likert 评分比较合成数据（4.39）vs. AMASS MoCap（4.87）。

### 实验充分性评估
- **优点**：实验设计整体较充分——两部分交互动作、多个基线的公平对比（同一数据、同一测试集）、多种互补指标（感知+物理+语义）、消融实验验证了交互场两个关键设计决策（偏移向量 vs. 距离；学习式 vs. NN）。用户研究与定量指标互相印证。
- **潜在不足**：
  - 测试场景数量为 500，但未说明这些场景的空间配置多样性程度（是否覆盖不同物体类型、不同初始距离、难度等级）。
  - 合成数据本身用于训练，而评估指标（Skeleton Distance、Contact IoU）中使用了合成数据中的锚点姿态，可能有利于 NIFTY（因为它的交互场就是在修正到该分布上），需注意这一潜在的循环评价偏差。
  - 消融中 Distance OIF 和 NN 实现方式的细节（如最近邻特征空间、检索数量）未在正文中描述完整。
  - 用户研究对象数量、人群构成等信息未详细报告。

## 6. 论文的主要结论与发现

1. **NIFTY 显著优于现有 SOTA 方法**：平均来看，用户偏好 NIFTY 而非 SAMP 的比例为 87.2%，非 cVAE 为 89.4%，非 cMDM 为 86.3%。NIFTY 生成的交互运动在视觉质量上胜出。
2. **交互场引导的引入是关键**：与不加引导的 cMDM 相比，D2O 从 37.9%（坐）/36.3%（举）提升到 99.6%/77.7%，说明通过交互场梯度引导对物体可达性有关键作用。
3. **NIFTY 生成的运动与合成训练数据几乎不可区分**：用户偏好 NIFTY 相对合成数据的比例为 47.2%（≈50%），说明二者质量相当。
4. **合成数据本身质量极高**：用户 Likert 评分中合成数据（4.39/5）接近真实 MoCap（4.87/5），印证了“时间反转运动先验生成数据”这一思路的有效性。
5. **偏移向量设计优于标量距离**：Tab. 2 中 Distance OIF 在 D2O、Skeleton Distance、渗透率等指标上全面劣于完整方法，表明预测带方向的偏移向量是更好的学习信号。
6. **学习式交互场优于最近邻变体**：NIFTY (NN) 在多数指标上被完整方法反超，说明交互场的泛化能力优于需要存储全部训练姿态的非参数化方法。

## 7. 优点：方法与实验设计的亮点

- **方法层面**：
  - 将“神经距离场”思想从手-物抓取/全身姿态流形扩展到**物体中心的全身体交互流形**，并首次将其作为扩散模型的引导信号，而非简单的优化后处理或显式目标姿态输入。
  - 交互场输出**偏移向量**而非标量距离，兼顾方向与幅度，学习难度更低、信息量更大。
  - 交互场直接以扩散模型的失效样本为训练难例（自训练式数据采集），使场在测试时的输入分布上保持有效，这是很巧妙的设计。
  - 扩散模型不预测噪声而是预测干净轨迹，使得物理可解释的引导目标能在姿态空间直接施加。
  - 数据合成的创新点：用场景无关的运动先验（HuMoR）通过**时间反转+树状分支展开**生成大量朝向锚点姿态的运动，绕开了难以获取的人-物配对数据瓶颈，且数据多样性高（起点分布广、路径各异）。
- **实验层面**：
  - 使用用户研究这一感知层面对齐的指标作为主要评价，可信度高。
  - 测试集刻意与训练分布隔离（不采用同一合成管线），增加了评测的公正性。
  - 消融既验证了“学习式 vs 非参数式场”，也验证了“偏移向量 vs 距离”两个正交设计点。

## 8. 不足与局限

- **对预训练运动先验质量的依赖**：合成数据完全来自 HuMoR 的先验质量，作者指出现有更好的模型（如基于 MDM 的生成先验）可能进一步提升数据质量，其自身的限制会传导到最终结果。
- **未处理物体操纵与动作链**：当前方法只到“接触”为止，不移动物体，也不支持将多个交互串联（如坐下后再站起）；物体姿态在交互中保持固定。
- **泛化性有限**：模型仅验证了坐姿和举物两种动作；新物体的泛化可能还需数据增强策略（如 SAMP 中的做法）；较困难的动作（如从椅子背后接近）仍表现不佳。
- **偶发伪影**：数据过滤策略不完美，有时会产生倒着走等不自然运动。
- **推理耗时**：34 秒/样本的推断代价较高（虽然含 10 个并行候选），可能限制在实时应用（VR、游戏）中的使用。
- **指标评价的循环风险**：Skeleton Distance 和 Contact IoU 使用的“真值”来源于合成数据，而 NIFTY 的训练目标是拟合该分布，因此这些指标的评价结论偏向于分布匹配而非物理真实，需结合用户研究来平衡解读。
- **实验覆盖局限**：未提供跨动作的单一统一模型结果（坐和举各训各的），未报告不同物体类型间的性能差距，未详细讨论初始姿态与物体距离对成功率的影响。

（完）
