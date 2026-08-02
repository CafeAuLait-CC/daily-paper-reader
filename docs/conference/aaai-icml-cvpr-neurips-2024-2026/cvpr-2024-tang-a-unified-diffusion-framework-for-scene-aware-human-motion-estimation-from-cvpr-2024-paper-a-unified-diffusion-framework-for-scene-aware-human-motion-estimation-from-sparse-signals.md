---
title: A Unified Diffusion Framework for Scene-aware Human Motion Estimation from Sparse Signals
title_zh: 一种用于场景感知人体动作估计的统一扩散框架
authors: "Tang, Jiangnan, Wang, Jingya, Ji, Kaiyang, Xu, Lan, Yu, Jingyi, Shi, Ye"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Tang_A_Unified_Diffusion_Framework_for_Scene-aware_Human_Motion_Estimation_from_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 8.0
evidence: 基于条件扩散模型从稀疏信号估计三维场景中的全身人体动作
tldr: 从稀疏跟踪信号估计全身动作存在严重的不确定性。S2Fusion提出统一条件扩散框架，将三维场景上下文与头显、手柄等稀疏信号融合，并在扩散去噪过程中生成合理的全身动作。结合场景信息有效缓解了一对多映射问题，提升了动作估计的合理性。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 866, \"height\": 444, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1705, \"height\": 937, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 862, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1731, \"height\": 613, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 852, \"height\": 972, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1713, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1468, \"height\": 292, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 865, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 865, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 865, \"height\": 295, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-tang-a-unified-diffusion-framework-for-scene-aware-human-motion-estimation-from-cvpr-2024-paper/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 864, \"height\": 292, \"label\": \"Table\"}]"
motivation: 基于稀疏信号的全身动作估计存在固有的病态歧义，需要场景上下文帮助消解。
method: 将场景特征与稀疏信号作为条件，输入条件扩散模型进行全身动作生成。
result: 在稀疏信号下估计出更合理且场景一致的三维人体动作。
conclusion: 场景信息与扩散生成相结合能显著提升动作估计质量。
---

## Abstract
Estimating full-body human motion via sparse tracking signals from head-mounted displays and hand controllers in 3D scenes is crucial to applications in AR/VR. One of the biggest challenges to this task is the one-to-many mapping from sparse observations to dense full-body motions which endowed inherent ambiguities. To help resolve this ambiguous problem we introduce a new framework to combine rich contextual information provided by scenes to benefit full-body motion tracking from sparse observations. To estimate plausible human motions given sparse tracking signals and 3D scenes we develop \text S ^2Fusion a unified framework fusing \underline S cene and sparse \underline S ignals with a conditional dif\underline Fusion model. \text S ^2Fusion first extracts the spatial-temporal relations residing in the sparse signals via a periodic autoencoder and then produces time-alignment feature embedding as additional inputs. Subsequently by drawing initial noisy motion from a pre-trained prior \text S ^2Fusion utilizes conditional diffusion to fuse scene geometry and sparse tracking signals to generate full-body scene-aware motions. The sampling procedure of \text S ^2Fusion is further guided by a specially designed scene-penetration loss and phase-matching loss which effectively regularizes the motion of the lower body even in the absence of any tracking signals making the generated motion much more plausible and coherent. Extensive experimental results have demonstrated that our \text S ^2Fusion outperforms the state-of-the-art in terms of estimation quality and smoothness.

---

## 论文详细总结（自动生成）

### 1. 核心问题与整体含义（研究动机和背景）

- **任务定义**：论文聚焦于AR/VR场景中，从HMD（头戴显示器）和左右手控制器提供的**稀疏跟踪信号**（仅3个6D跟踪器）估计**全身人体动作**的问题。
- **核心挑战**：稀疏观测到稠密全身动作的映射是一个**典型的一对多问题**，存在固有的歧义性。特别是**下半身（腿、脚）完全没有可直接观测的信号**，导致生成的动作常常出现不自然、穿模（贯穿场景几何体）以及上下半身运动不协调的问题。
- **研究动机**：人体运动通常与周围环境密切相关，因此将**3D场景信息**引入模型，利用场景提供的丰富上下文约束，来缩小可能的动作分布空间，从而消解一对多映射带来的歧义。
- **整体含义**：论文提出了一个统一框架S²Fusion，它通过条件扩散模型，将稀疏跟踪信号、场景几何信息以及提取的周期运动特征融合起来，以生成物理上更合理、场景感知的全身动作，显著提升了稀疏信号驱动的动作估计质量与平滑性。

### 2. 论文提出的方法论

- **核心思想**：将三维场景信息作为额外的条件输入，结合条件扩散模型从稀疏信号中生成全身动作，以解决稀疏输入引起的固有歧义。
- **整体框架**：S²Fusion由四个主要模块组成：运动先验初始化、条件获取模块、条件去噪器以及损失引导的采样过程。
- **关键技术细节**：
  1. **运动先验初始化（Motion Prior）**：为了克服场景-动作数据集数据量有限的不足，模型基于大规模数据集AMASS预训练了一个条件VAE。训练完成后，在反向扩散过程的起点，从该先验中采样初始“噪声”运动，而不是直接使用高斯噪声。这既提升了样本质量，也加速了推理过程（减少了所需去噪步数）。
  2. **条件获取模块**：
     - **场景条件**：以HMD测量的全局位置为中心裁剪（2m×2m×2m）局部点云，馈入PointNet++场景编码器，提取场景特征向量Eₛ，捕捉人体周围的局部上下文。
     - **周期运动特征**：使用周期自编码器（PAE，结合1D卷积和快速傅里叶变换）从稀疏信号中提取频域参数（频率F、振幅A、偏移B、相位偏移S），重建出多分辨率的正弦函数形式的时间对齐特征，用来表示身体各部位运动的节奏和时间对齐关系。
     - **稀疏跟踪信号**：采用头/手部位的位置和旋转，以及额外计算得到的角速度和线速度作为输入。
  3. **条件去噪器**：采用条件扩散模型，在训练时直接预测干净的信号x₀，而非预测噪声ϵ。损失函数包含简单目标L_simple和正则化生成动作的几何损失L_geometric（通过前向运动学FK比较关节位置）。
  4. **损失引导采样过程**：
     - 设计了两种不需要下半身真实观测的损失函数：
       - **场景穿透损失**：约束膝盖和脚踝关节与场景点云之间不发生穿透（通过KNN查询点云并惩罚半径内的接近）。
       - **相位匹配损失**：基于观测到的上半身（头、左手、右手）运动的相位特征与生成的下半身（骨盆、左右脚踝）的相位特征进行匹配，迫使上下半身运动在时间上保持协调一致。
     - 在采样过程中，利用这两个损失函数的梯度引导采样轨迹，对最初生成的干净样本进行更新，从而对上/下半身协同性和场景几何一致性进行正则化。

### 3. 实验设计

- **数据集与Benchmark**：在两个全身运动-场景交互数据集上进行训练和评估：
  - **CIRCLE**：包含10小时的全身动作，涉及9个多样化场景，按7:3比例划分训练/测试。
  - **GIMO**：包含由Hololens和IMU动捕服采集的人体动作序列、场景扫描和视线信息。
- **对比方法**：与三个最先进（SOTA）的纯传感器驱动方法进行比较：
  - AvatarPoser (2022)
  - AGRoL (2023)（基于扩散模型）
  - AvatarJLM (2023)
- **评估指标**：采用多个常用指标，涵盖运动估计精度、平滑度和场景感知合理性：
  - MPJRE（平均关节旋转误差）、MPJPE（平均关节位置误差）、MPJVE（平均关节速度误差）、Jitter（抖动程度）、FS（脚部滑动漂移），以及分身体部位评估的Hand PE、Upper PE、Lower PE。

### 4. 资源与算力

- **算力说明**：**论文正文中未明确提及**使用的GPU型号、数量、训练时长或任何算力基础设施信息。因此无法从论文中总结其具体的实验算力消耗。

### 5. 实验数量与充分性

- **实验组数量**：
  - **主实验**：在两个数据集（CIRCLE, GIMO）上与三个SOTA方法进行了全面对比，且提供了多组评价指标（主表1和附加指标表2）。
  - **模块消融**：进行了5组消融，分别验证Motion Prior（MP）、Scene、PAE三个核心组件的贡献（表3、表4）。
  - **损失引导消融**：进行了4组实验，以验证场景穿透损失（L_penetration）和相位匹配损失（L_phase）的单独及组合效果（表5、表6）。
  - **定性实验**：提供了多个场景下的轨迹可视化对比（图4）。
- **充分性评估**：
  - **优点**：实验覆盖了两类不同的数据集，既包含丰富的室内场景交互，也包含真实场景扫描，保证了数据多样性；消融实验系统地验证了三个主要模块和两个损失函数的作用；定量与定性结合，结果具有较强的说服力。
  - **客观与公平性**：论文提及“为了公平比较，我们在CIRCLE和GIMO上重新训练了对比方法直至收敛”，这增加了对比的公平性。但值得注意的是，与模型直接相关的一些核心细节（如训练具体参数）放在了补充材料中，而算力开销也并未在正文中披露，可能在完全复现时面临一定障碍。

### 6. 论文的主要结论与发现

- 提出S²Fusion框架，成功将场景模态融入稀疏信号到全身动作的扩散生成过程，显著解决了稀疏信号引发的一对多映射歧义。
- 在CIRCLE和GIMO数据集上，S²Fusion在**MPJPE、MPJVE、Jitter、FS**等核心指标上全面优于SOTA方法，其中下半身动作误差（Lower PE）的改善效果**尤为显著**。
- 验证了“场景信息能作为有价值的上下文线索，帮助在缺乏直接观测的情况下推断下半身动作”的核心假设。
- 验证了预训练运动先验对生成多样性和平滑度的提升作用，以及周期自动编码器能够有效提取跟踪信号中的时间对齐信息，促进上下肢的动作协调性。

### 7. 优点

- **创新性**：首次将3D场景信息与稀疏跟踪信号相结合，统一到一个扩散框架中来解决动作估计中的固有歧义，为AR/VR场景下的动作恢复提供了新思路。
- **方法设计合理且系统**：将预处理（运动先验）、特征提取（PAE）、条件编码（场景）与扩散采样有机整合，形成了完整的工业化流程；利用频域特征直观且优雅地解决上下半身协调问题。
- **可解释性与可控制性**：两种损失函数（场景穿透和相位匹配）分别针对物理合理性和动作协调性设计，在采样阶段能够以可控制的方式精细地调整输出，非常直观。
- **实验表现**：在两个数据集上与三个最新的SOTA方法比较，在大多数指标上获得明显优势，尤其是显著改善了原本无人监督的下半身动作质量。

### 8. 不足与局限

- **计算资源不透明**：论文未提及训练和推理的算力开销（GPU型号/数量/时长等），不利于复现和比较实用成本；扩散模型的迭代采样过程相对较重，推理效率可能仍是落地瓶颈。
- **数据集规模与局限性**：实验仅在CIRCLE和GIMO两个数据集上进行，这两个数据集虽然包含丰富的交互，但在动作类型和场景多样性上有限（例如主要涵盖行走、坐、站等日常场景），无法完全反映复杂和动态的真实世界环境。
- **物理合理性有限**：场景穿透损失是对膝盖/脚踝等关节的局部约束，并未考虑全局的物理接触与作用力（例如无法完全避免人体其他部位如臀部/手部与场景的穿透），也未涉及全身的动力学一致性。
- **对场景的强依赖**：模型严重依赖HMD提供的全局位置来裁剪场景；如果全局定位误差较大，场景编码质量就会下降，进而影响整个动作生成的精度。
- **对上半身动作的依赖**：相位匹配损失依赖于上半身（头/手）的观测信号。如果上半身运动微弱或存在噪声干扰，阶段特征提取可能不稳定，从而影响对下半身的约束效果。

（完）
