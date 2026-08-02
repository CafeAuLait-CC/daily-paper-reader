---
title: "DiffPerformer: Iterative Learning of Consistent Latent Guidance for Diffusion-based Human Video Generation"
title_zh: DiffPerformer：面向基于扩散的人体视频生成的一致性潜在引导迭代学习
authors: "Wang, Chenyang, Zheng, Zerong, Yu, Tao, Lv, Xiaoqian, Zhong, Bineng, Zhang, Shengping, Nie, Liqiang"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Wang_DiffPerformer_Iterative_Learning_of_Consistent_Latent_Guidance_for_Diffusion-based_Human_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 4.0
evidence: 基于扩散的人体视频生成，关注时间一致性；不涉及3D动作序列
tldr: 基于扩散的姿势引导人体视频生成常出现时间不一致。DiffPerformer通过对目标角色的单段视频微调预训练扩散模型，并引入隐式视频表示作为代理，学习时间一致的潜在引导。引导被编码到VAE潜空间，构建迭代优化循环。该方法无需复杂架构改动即可合成高保真、时间一致的人体视频。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1748, \"height\": 612, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1760, \"height\": 831, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 845, \"height\": 471, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 699, \"height\": 528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1701, \"height\": 1040, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 845, \"height\": 1065, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 837, \"height\": 635, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 863, \"height\": 374, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 824, \"height\": 327, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-wang-diffperformer-iterative-learning-of-consistent-latent-guidance-for-diffusion-based-human-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 897, \"height\": 301, \"label\": \"Table\"}]"
motivation: 现有扩散模型生成的人体视频在姿态和外观上存在时间不一致问题。
method: 微调单视频上的预训练扩散模型，学习隐式视频表示作为一致潜在引导。
result: 在无需复杂架构修改的情况下提升了视频保真度和时间一致性。
conclusion: 提供了一种轻量级、可微调的扩散视频生成方案，适合目标角色定制。
---

## Abstract
Existing diffusion models for pose-guided human video generation mostly suffer from temporal inconsistency in the generated appearance and poses due to the inherent randomization nature of the generation process. In this paper we propose a novel framework DiffPerformer to synthesize high-fidelity and temporally consistent human video. Without complex architecture modification or costly training DiffPerformer finetunes a pretrained diffusion model on a single video of the target character and introduces an implicit video representation as a proxy to learn temporally consistent guidance for the diffusion model. The guidance is encoded into VAE latent space and an iterative optimization loop is constructed between the implicit video representation and the diffusion model allowing to harness the smooth property of the implicit video representation and the generative capabilities of the diffusion model in a mutually beneficial way. Moreover we propose 3D-aware human flow as a temporal constraint during the optimization to explicitly model the correspondence between driving poses and human appearance. This alleviates the misalignment between guided poses and target performer and therefore maintains the appearance coherence under various motions. Extensive experiments demonstrate that our method outperforms the state-of-the-art methods.

---

## 论文详细总结（自动生成）

## 1. 论文核心问题与整体含义

- **研究背景**：基于扩散模型（Diffusion Model）的姿态引导人体视频生成（Pose-guided Human Video Generation）在人体计算机交互、运动分析、VR 等领域有广泛应用。
- **核心问题**：现有扩散模型在生成人体视频时，由于去噪过程的**固有随机性**，导致生成视频在**时间维度上出现严重不一致**——具体表现为外观闪烁（flickering）、姿态抖动（jittering）、身份漂移等问题；即使采用时空注意力（如 DreamPose）或针对特定人物微调（如 DisCo），也难以从根本解决。
- **整体含义**：论文主张不依赖复杂架构改造或大规模训练，而是从**表示学习的角度**引入隐式视频表示作为"时间代理"，从而在扩散模型的生成过程中注入时间一致性先验，实现高保真、时间一致、姿态对齐的人体视频合成。

---

## 2. 方法论

### 核心思想
- 借鉴 text-to-3D 生成中通过 **3D 代理表示（NeRF）** 优化 2D 扩散模型以实现视图一致性的思路，**将隐式视频表示视为时间域上的代理**，通过迭代优化让扩散模型与视频表示互惠互利。

### 框架组成
论文框架包含三个核心组件，形成闭环：

**(a) 姿态引导扩散模型（Pose-guided Diffusion Model）**
- 以 VideoComposer 预训练视频扩散模型为基础，将 2D UNet 扩展为含时间层的 3D UNet。
- 输入：参考图 CLIP 嵌入（保身份）+ 姿态序列特征（如 OpenPose 关键点或 DensePose）。
- 在**单段目标人物视频**上微调 UNet 和 VAE 解码器，使模型具备特定人物的外观先验，无需大规模数据集。

**(b) 隐式视频表示（Implicit Video Representation, IVR）**
- 采用 CoDef 的范式，由**规范空间 MLP C** 和**时间变形场 D** 组成：\( (r,g,b) = C(D(H(x,y,n))) \)，其中 H 为 3D 多分辨率哈希编码（InstantNGP），用于捕捉高频动态细节。
- 训练目标：重建损失 \( \mathcal{L}_{rec} = \sum_n \|I_n - C(D(H(x,y,n)))\|_1 \)。
- 提出 **3D 感知人体光流（3D-aware Human Flow）** 作为时域约束：
  - 用 PyMAF-X 从驱动视频估计 3D 人体网格 \( \Theta_n = \{\theta_n, \beta_n, \pi_n\} \)。
  - 将驱动姿态中的形状参数替换为参考人物的形状参数：\( \Theta_t = \{\theta_n, \beta_r, \pi_n\} \)，解决了参考人物与驱动信号之间的**体型不匹配**问题。
  - 渲染 2D 深度图并建立逐点对应，计算相邻帧位置偏移作为光流，构成损失 \( \mathcal{L}_{flow} \)。
  - 总损失：\( \mathcal{L}_{ivr} = \mathcal{L}_{rec} + \lambda \mathcal{L}_{flow} \)。
- IVR 对扩散模型生成的视频进行**蒸馏**，输出平滑且外观一致的视频 \( V_s \)。

**(c) 潜在引导与迭代联合优化（Latent Guidance & Iterative Joint Optimization）**
- 将平滑视频 \( V_s \) 编码到 VAE 潜空间后**添加噪声**，作为扩散模型的去噪初始化——相比于图像域加噪，潜空间加噪更能保留原始视频的时间一致性（论文用 T-SNE 可视化证明）。
- 扩散模型细化 \( V_s \) 得到新的 \( V_p \)，\( V_p \) 再作为 IVR 的优化目标，形成**闭环迭代**；每 2000 步更新一次 \( V_p \)。
- 优化初期用参考图像 \( I_{ref} \) 初始化 IVR，加速收敛。
- 随着 \( V_s \) 收敛，逐步减少加噪强度，降低随机性干扰。

---

## 3. 实验设计

### 数据集与场景
- **日常拍摄视频（casually captured videos）**：验证一般场景下方法有效性。
- **TikTok 数据集**：包含真实舞蹈视频，覆盖复杂姿态和大幅度运动，用于进一步验证。

### 对比方法
- **Fast-Vid2Vid**（GAN 方法的代表）
- **DreamPose**（基于扩散，含时空注意力）
- **DisCo**（基于扩散，解耦控制）

### 评估指标
- 图像质量：PSNR、SSIM、LPIPS、FID、L1
- 视频质量：FID-VID、FVD（衡量时间一致性）

### 消融实验设计（共三组）
1. **隐式视频表示（IVR）的有效性**：三档设置——① 仅扩散模型输出（w/o Opt.）；② 以扩散模型原始输出作为"平滑视频"再经扩散模型细化（Image Opt.）；③ 完整框架（IVR Opt.）。
2. **3D 感知人体光流（3DHF）的有效性**：对比有无 3DHF 约束下的姿态对齐效果，重点观察大幅度肢体运动。
3. **VAE 解码器微调的有效性**：对比冻结 VAE 解码器的效果，观察面部细节恢复情况。

---

## 4. 资源与算力

- 论文明确说明实验环境为 **单块 NVIDIA RTX 3090 GPU**，生成分辨率 **512×512**，PyTorch 框架。
- 关键超参数：
  - 姿态引导扩散模型微调：10 epochs，学习率 \( 5\times10^{-6} \)。
  - VAE 解码器微调：2000 步，学习率 \( 5\times10^{-5} \)。
  - 隐式视频表示：优化 10000 步，学习率 \( 1\times10^{-3} \)。
  - 扩散采样：DDIM，50 步。
- **论文未明确报告总训练/推理时间**，也未提及使用的 GPU 数量、分布式策略或总计算量。仅指出"使用扩散模型比非扩散方法更耗时"。

---

## 5. 实验数量与充分性

- **对比实验**：在两个数据集（日常视频、TikTok 舞蹈视频）上，使用两种姿态信号（关键点、DensePose），与三种代表性方法对比，覆盖了 GAN 和扩散两大技术路线。
- **消融实验**：系统验证三个关键组件的贡献——IVR、3DHF、VAE 微调，且均有定性 + 定量的支撑。
- **客观性评估**：采用 7 个指标，涵盖图像级与视频级；所有对比方法均在相同视频上微调，保证公平性。
- **补充材料**：论文多处提及 Supp.Mat. 包含更多结果与分析。
- **总体评价**：实验维度较全面，但存在一定局限——数据集规模较小，未给出用户研究/主观评价；主要依赖定量指标和可视化比较，未系统评估模型对背景复杂、相机运动剧烈等极端场景的鲁棒性。

---

## 6. 主要结论与发现

1. DiffPerformer 在所有 7 项指标上**全面超越**三种 SOTA 方法（PSNR 30.72、SSIM 0.69、LPIPS 0.22、FID 36.00、FID-VID 22.32、FVD 254.39），证明其在图像质量和时间一致性上的双重优势。
2. **隐式视频表示**能有效消除扩散模型生成过程中的时间不一致性，并可进一步通过扩散模型补充纹理细节。
3. **3D 感知人体光流**显著改善了姿态对齐，尤其对大幅度肢体运动场景（如舞蹈）效果明显；相比学习式光流（如 RAFT），基于固定拓扑的人体网格能提供更准确的运动对应。
4. **VAE 解码器微调**对提升生成结果的面部细节和整体清晰度有直观贡献。
5. 在潜空间加噪引导扩散模型，比在图像域加噪更能保持视频的时间一致性。

---

## 7. 优点

- **方法设计新颖**：首次将隐式视频表示作为"时间代理"引入姿态引导人体视频生成，为缓解扩散模型时间不一致问题提供了全新视角，规避了大规模训练和复杂架构修改的成本。
- **轻量可落地**：在单视频上微调即可完成个性化，符合实际应用中对单个角色定制的需求。
- **迭代优化设计巧妙**：扩散模型与隐式表示互相促进——IVR 利用平滑性消除闪烁，扩散模型利用生成能力补充细节，二者形成良性闭环。
- **3D 感知光流具有物理可解释性**：利用人体网格拓扑一致性的先验来建立姿态-外观对应，比学习式光流更鲁棒。
- **潜空间引导有理论支撑**：用 T-SNE 可视化直观论证了潜空间加噪更利于保持视频一致性，论证扎实。
- **实验较规范**：在多个数据集、多种姿态信号上与代表性方法公平对比，消融实验设计清晰。

---

## 8. 不足与局限

- **场景限制**：由于缺乏背景内容引导，在**相机运动**的视频中效果不佳；对复杂背景和遮挡场景的鲁棒性未充分验证。
- **时间成本高**：扩散模型采样本身耗时，加上隐式表示优化和逐视频微调，整体计算开销较大；论文未提供详细的运行时间对比。
- **单实例定制模式**：每个目标角色都需要独立的微调和优化流程，难以直接扩展到大规模多角色应用。
- **隐私与安全风险**：论文自身指出该方法可能被滥用于制作"深度伪造"（deepfakes）等欺骗性内容，存在社会伦理风险。
- **实验覆盖有限**：仅在自家采集的日常视频和 TikTok 数据集上验证，未在更大规模的公开基准（如 UBC Fashion、iPER、Human3.6M 等）上进行系统评测；缺少与最新视频扩散模型的横向对比（如 Follow Your Pose）。
- **评估主观性缺失**：未包含用户调研（user study）等主观质量评估。

---

（完）
