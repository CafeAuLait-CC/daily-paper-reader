---
title: "DiffSHEG: A Diffusion-Based Approach for Real-Time Speech-driven Holistic 3D Expression and Gesture Generation"
title_zh: DiffSHEG：基于扩散的实时语音驱动全身3D表情与手势生成
authors: "Chen, Junming, Liu, Yunfei, Wang, Jianan, Zeng, Ailing, Li, Yu, Chen, Qifeng"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Chen_DiffSHEG_A_Diffusion-Based_Approach_for_Real-Time_Speech-driven_Holistic_3D_Expression_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 10.0
evidence: 基于扩散的Transformer从语音联合生成同步的3D表情和手势
tldr: 针对语音驱动表情和手势联合生成尚未充分探索的问题，本文提出DiffSHEG，一种基于扩散的方法。其扩散式共生运动生成Transformer支持从表情到手势的单向信息流，实现同步表情-手势分布匹配。还提出基于外绘制的采样策略，支持任意长度序列的实时生成，为该任务提供了高效实用的解决方案。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 870, \"height\": 419, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1800, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 839, \"height\": 187, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1672, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1640, \"height\": 316, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 862, \"height\": 309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1769, \"height\": 458, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-chen-diffsheg-a-diffusion-based-approach-for-real-time-speech-driven-holistic-3d-expression-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1813, \"height\": 868, \"label\": \"Table\"}]"
motivation: 现有工作分别生成表情或手势，缺乏联合同步生成模型。
method: 用扩散式Transformer实现从表情到手势的信息单向流，并采用外绘制采样生成任意长度序列。
result: 可实时生成同步的3D表情和手势，质量和效率均优。
conclusion: 提供了一种实用的联合生成方案，推动语音驱动3D动作生成方向。
---

## Abstract
We propose DiffSHEG a Diffusion-based approach for Speech-driven Holistic 3D Expression and Gesture generation. While previous works focused on co-speech gesture or expression generation individually the joint generation of synchronized expressions and gestures remains barely explored. To address this our diffusion-based co-speech motion generation Transformer enables uni-directional information flow from expression to gesture facilitating improved matching of joint expression-gesture distributions. Furthermore we introduce an outpainting-based sampling strategy for arbitrary long sequence generation in diffusion models offering flexibility and computational efficiency. Our method provides a practical solution that produces high-quality synchronized expression and gesture generation driven by speech. Evaluated on two public datasets our approach achieves state-of-the-art performance both quantitatively and qualitatively. Additionally a user study confirms the superiority of our method over prior approaches. By enabling the real-time generation of expressive and synchronized motions our method showcases its potential for various applications in the development of digital humans and embodied agents.

---

## 论文详细总结（自动生成）

# DiffSHEG 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机与背景）

- **研究问题**：语音驱动的 3D 面部表情与身体手势的**联合同步生成**问题。以往工作通常只单独生成"共语手势"或"表情"，而同时生成两者并保证其自然同步的研究非常少。
- **现有方法缺陷**：
  - 部分工作将独立的表情生成模型与手势生成模型简单拼接（如 TalkSHOW），忽略了表情与手势之间的潜在关联；
  - 部分工作采用多任务学习框架（如 LS3DCG），但共享语音编码器后**分别解码**，仍未显式建模二者联合分布；
  - 确定性 CNN 模型难以刻画语音到动作的"多对多"映射，生成结果缺乏多样性与灵活性。
- **整体意义**：论文提出首个基于扩散模型的**统一联合生成框架** DiffSHEG，显式建模表情-手势联合分布，并可在单张 RTX 3090 上实现**实时（>30 FPS）任意长度序列**生成，为数字人、具身智能体等应用提供了实用解决方案。

## 2. 论文提出的方法论

### 2.1 核心思想
- 采用**扩散模型**（DDPM 框架）作为生成基础，通过一个统一的"表情-手势去噪网络"同时生成表情与手势；
- 提出**单向信息流（Uni-directional Expression-to-Gesture, UniEG）**：信息从表情流向手势，而非相反或双向；
- 提出 **FOPPAS（Fast Out-Painting-based Partial Autoregressive Sampling）**，基于"外绘制（outpainting）"实现任意长度序列的实时采样。

### 2.2 关键技术细节

**（1）语音编码器**
- 提取两类语音特征：**Mel-spectrogram**（低层特征）与 **HuBERT** 特征（高层特征，训练时冻结）；
- Mel 特征送入共享的 Transformer 编码器得到中层语音表示，供表情和手势两个分支共用。

**（2）Motion-Speech Fusion Residual Block（运动-语音融合残差块）**
- 将运动特征与语音嵌入及其他可选时序条件沿通道维直接拼接（而非交叉注意力），实现自然的音-动时序对齐，避免注意力 mask 的复杂性；
- 使用 LayerNorm + MLP 预测运动特征的残差，以加速收敛、稳定训练。

**（3）Style-aware Transformer Block（风格感知 Transformer 块）**
- 注入全局条件：风格（此处为人物 ID）与扩散步数 t，经 MLP 投影后求和，通过 **AdaIN** 在自注意力和 MLP 之后进行风格调制；
- 使用**线性自注意力（linear self-attention）**替代全自注意力以降低计算量。

**（4）单向表情→手势信息流**
- 在每次去噪迭代中，利用当前步预测噪声计算出预测表情 $\hat{x}^E_{0(t)}$，将其送入手势 Transformer 块作为额外条件；
- 该路径上使用**梯度截断（detach）**，防止手势分支梯度反向影响表情编码器；
- 直觉依据：表情（如嘴唇、眉毛、眼神）与语音强相关，可充当手势的线索；而手势对面部表情（尤其是嘴唇）几乎没有影响，反向信息流会造成干扰。

**（5）训练损失（公式 8）**
- 总损失为三部分加权和：$L = \lambda_t L_t + \lambda_v L_v + \lambda_\delta L_\delta$
- $L_t$：扩散模型噪声预测损失（$\lambda_t = 10$）
- $L_v$：速度损失，对相邻帧差分计算 MSE（$\lambda_v = 1$）
- $L_\delta$：运动重建的 Huber 损失（$\lambda_\delta = 1$）

**（6）FOPPAS 任意长度采样**
- 推理时采用"外绘制"策略：后续片段的前若干帧固定为上一片段末尾帧，其余帧通过扩散采样生成（类似 RePaint）；
- 重叠帧数可灵活调整（训练时无需固定），首个片段可设重叠数为 0 随机生成；
- 利用 Transformer 位置编码可截断的特性，支持比训练片段更短的序列（用于最后一段）；
- 将 1000 步 DDPM 替换为 **25 步 DDIM**，加速约 40 倍；最后两步对重叠区做线性混合（blending）以消除边界不一致。

## 3. 实验设计

### 3.1 数据集
| 数据集 | 内容 | 训练/测试设定 |
|---|---|---|
| **BEAT** | 大规模多模态手势+表情数据集，4 个被试 | 训练/验证片段 34 帧；测试为 64 条约 1 分钟长序列；15 FPS；轴角旋转表示 |
| **SHOW** | 音视频数据集，SMPLX 参数，4 人，30 FPS | 训练/验证片段 88 帧；测试为不同长度长序列 |

### 3.2 对比方法
- **BEAT 上**：CaMN（ECCV'22）、DiffGesture（CVPR'23）、DiffuseStyleGesture（IJCAI'23）、LDA（SIGGRAPH'23）；基线原本仅做手势生成，作者将同一流程套用到表情数据上独立生成表情。
- **SHOW 上**：TalkSHOW（CVPR'23）与 LS3DCG（IVA'21），两者支持表情+手势联合生成。

### 3.3 评测指标
- **FMD / FGD / FED**：Fréchet 距离，衡量生成分布与真实分布差异（FMD 为整体联合分布，FGD 为手势、FED 为表情）；
- **PCM / SRGR**：动作参数正确率及其按语义权重加权版本；
- **Diversity（Div）**：生成动作的多样性；
- **Beat Alignment（BA）**：音频节拍与动作节拍对齐度；
- 额外进行了**用户研究**：22 名被试，对 BEAT 8 段 1 分钟视频、SHOW 12 段 10 秒视频，就整体真实感、表情-语音同步、手势-语音同步、多样性四项进行排序。

### 3.4 消融实验
- **Ours w/o $\hat{x}^E_{0(t)}$**：去掉表情→手势条件流；
- **Ours w/o Detach**：不截断梯度；
- **Ours Naïve Concat**：直接将表情和手势向量拼接后送入单一 Transformer 去噪块（为公平比较扩大隐层维度 1.41 倍）；
- **Ours Reverse Direction**：将条件流反向为手势→表情。

## 4. 资源与算力

- **训练设备**：5 张 NVIDIA RTX 3090 GPU；
- **BEAT**：训练 1000 epochs，batch size 2500；
- **SHOW**：训练 1600 epochs，batch size 950；
- **推理速度**：对 1 分钟音频（900 帧，15 FPS）平均耗时 28.6 秒（含 Mel 与 HuBERT 音频编码时间），约 **31.5 FPS**，达到实时；而原始 DDPM+RePaint 需 2068.1 秒（约 0.44 FPS）。

## 5. 实验数量与充分性

### 5.1 实验数量
- 两个公开数据集上的完整定量对比；
- 两个数据集上的定性可视化对比（含渲染视频）；
- 用户研究（22 人 × 4 项指标）；
- 4 组消融实验（去条件流、去梯度截断、朴素拼接、反向流）；
- 推理速度/实时性分析；
- 不同方面的鲁棒性讨论（如帧率、位置编码截断等）。

### 5.2 充分性与客观性评估
- **优点**：实验覆盖了定量、定性、主观评测和消融，维度较全面；消融对照设计合理（朴素拼接控制计算量、反向流验证方向性假设）；用户研究以真实数据为参照。
- **潜在不足**：
  - BEAT 上的四个基线原本是手势生成方法，作者自行将其适配到表情生成，可能未达到原方法在表情任务上的最优表现；
  - 作者指出 Div 和 BA 指标对抖动/异常运动不鲁棒（抖动会虚高），因此部分数量指标的参考价值有限；
  - TalkSHOW 作者提供的预训练权重生成结果存在失真，需重新训练后才能公平比较，但重训练版本指标与其原文结果略有出入；
  - 定量指标与人类感知并不总是一致的（论文也承认这一点）。

## 6. 论文的主要结论与发现

- DiffSHEG 在两个公开数据集上的 **FMD、FED、FGD 等分布距离指标大幅优于所有基线**，证明联合分布建模的有效性；
- 在 SRGR/PCM、BA、Diversity 等指标上取得最好或可比的结果，且生成动作平滑自然（基线扩散方法普遍存在抖动）；
- 用户研究显示，在真实感、语音-表情同步、语音-手势同步和多样性四项指标上，DiffSHEG 均获得**压倒性的用户偏好**；
- 消融实验验证了"表情→手势单向信息流"设计的必要性：朴素拼接、无梯度截断、反向流均导致性能下降；
- FOPPAS 使得扩散模型能够在单张 3090 上以超实时速度生成任意长度、平滑衔接的运动序列，且支持流式音频输入。

## 7. 方法或实验设计的亮点

1. **问题视角新颖**：首次在扩散模型框架下显式联合建模表情与手势的联合分布，而非简单拼接或分治；
2. **可解释的信息流设计**：基于"表情可提示手势、手势难以影响表情（尤其嘴唇）"的直觉，提出单向条件流，并用消融验证了该假设；
3. **实时任意长度生成**：FOPPAS（外绘制+DDIM+重叠区混合）避免了训练时自回归条件带来的刚性，提供灵活、高效且支持流式的推理方案；
4. **工程细节扎实**：如 Motion-Speech 融合残差块加速收敛、线性自注意力降开销、重叠帧数可动态调整；
5. **评测较全面**：结合分布距离、语义权重指标、节拍对齐、多样性与大规模用户研究，并配套渲染视频直观展示效果。

## 8. 不足与局限

1. **数据集规模与多样性有限**：两个数据集均只有 4 个被试，说话人风格、语言、情绪覆盖有限，跨域泛化能力待验证；
2. **基线公平性风险**：BEAT 上的基线被改造用于表情生成，可能未在最佳设置下比较；TalkSHOW 需重训才能达到可比状态；
3. **指标体系局限**：部分指标（Div、BA）对抖动和离群动作不鲁棒，可能产生误导性高分；Fréchet 距离计算所用特征提取器也影响结果解释性；
4. **应用限制**：实验仅评估上半身动作（跟随基线设置），尽管框架支持下半身；对多人物 ID 的风格多样性仅作为条件输入，未做跨身份迁移的深入分析；
5. **实时性依赖特定硬件**：31.5 FPS 是在单张 RTX 3090 上测得的，在更低端设备上可能无法达到实时；
6. **扩散模型固有代价**：即便加速到 25 步，仍需多步去噪与重叠区多轮重采样，计算冗余客观存在；FOPPAS 的流畅度依赖重叠帧数的选取，极端情况下（如非常短的重叠）仍可能出现边界伪影。

（完）
