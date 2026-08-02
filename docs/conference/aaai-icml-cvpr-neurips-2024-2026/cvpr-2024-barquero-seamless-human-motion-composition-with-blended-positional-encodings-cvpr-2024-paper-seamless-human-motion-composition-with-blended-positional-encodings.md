---
title: Seamless Human Motion Composition with Blended Positional Encodings
title_zh: 基于混合位置编码的无缝人体动作组合
authors: "Barquero, German, Escalera, Sergio, Palmero, Cristina"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Barquero_Seamless_Human_Motion_Composition_with_Blended_Positional_Encodings_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 基于扩散的FlowMDM实现文本驱动的无缝长时人体动作组合
tldr: 人类动作生成常局限于短时片段，难以生成长序列。本文提出FlowMDM，一种基于扩散的模型，通过混合绝对与相对位置编码，在去噪链中保持全局一致性与局部连贯性，无需后处理即可生成长而连续的文本引导动作序列。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 940, \"height\": 397, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 851, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 870, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 871, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1797, \"height\": 414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 874, \"height\": 452, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1805, \"height\": 765, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1632, \"height\": 388, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1630, \"height\": 319, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1825, \"height\": 422, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-barquero-seamless-human-motion-composition-with-blended-positional-encodings-cvpr-2024-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1822, \"height\": 416, \"label\": \"Table\"}]"
motivation: 现有动作生成方法只能产出短时孤立片段，难以处理长序列文本引导。
method: 在扩散模型中使用混合绝对/相对位置编码，实现长动作序列的平滑组合。
result: 不需要后处理即可生成无缝长动作序列。
conclusion: 为长时条件动作生成提供了一种高效且流畅的扩散模型方案。
---

## Abstract
Conditional human motion generation is an important topic with many applications in virtual reality gaming and robotics. While prior works have focused on generating motion guided by text music or scenes these typically result in isolated motions confined to short durations. Instead we address the generation of long continuous sequences guided by a series of varying textual descriptions. In this context we introduce FlowMDM the first diffusion-based model that generates seamless Human Motion Compositions (HMC) without any postprocessing or redundant denoising steps. For this we introduce the Blended Positional Encodings a technique that leverages both absolute and relative positional encodings in the denoising chain. More specifically global motion coherence is recovered at the absolute stage whereas smooth and realistic transitions are built at the relative stage. As a result we achieve state-of-the-art results in terms of accuracy realism and smoothness on the Babel and HumanML3D datasets. FlowMDM excels when trained with only a single description per motion sequence thanks to its Pose-Centric Cross-ATtention which makes it robust against varying text descriptions at inference time. Finally to address the limitations of existing HMC metrics we propose two new metrics: the Peak Jerk and the Area Under the Jerk to detect abrupt transitions.

---

## 论文详细总结（自动生成）

# 基于混合位置编码的无缝人体动作组合（FlowMDM）论文总结

## 1. 论文的核心问题与整体含义

### 研究动机与背景
- **现有局限**：当前条件式人体动作生成方法（如基于文本、音乐、场景引导的生成）通常只能生成**短时、孤立**的动作片段，难以满足虚拟现实、游戏、机器人等应用对**长序列、多控制信号连续驱动**的需求。
- **核心任务**：论文聚焦于生成式**人体动作组合（Human Motion Composition, HMC）**——即在一段长动作序列中，不同时间段由不同的文本描述（控制信号）分别驱动，且动作之间需要**平滑、真实地过渡**。
- **关键挑战**：
  - 现有数据集缺乏长序列、多文本标注的样本；
  - 自回归方法存在误差累积、依赖单向前序动作而无法"预判"后续动作的问题；
  - 已有的扩散式组合方法（如DoubleTake、DiffCollage、MultiDiffusion）需要对不同子序列分别生成并执行**冗余去噪步骤**或后处理来融合过渡，计算开销大且依赖预定义的过渡长度。

### 论文定位
论文提出 **FlowMDM**——**首个无需任何后处理或冗余去噪步骤、直接同时生成完整无缝人体动作组合的扩散模型**，在Babel和HumanML3D数据集上达到SOTA水平。

---

## 2. 论文提出的方法论

### 整体框架
- FlowMDM 基于**双向（encoder-only）Transformer**作为扩散模型的去噪网络，类似MDM（Motion Diffusion Model），但进行了多项面向HMC的关键创新。
- 核心思想：利用扩散模型的迭代去噪特性，在**不同去噪阶段采用不同的位置编码策略**，并引入**姿态中心的交叉注意力**来应对条件信号在训练与推理之间的不一致问题。

### 核心技术一：Blended Positional Encodings（BPE，混合位置编码）
- **思想来源**：观察到扩散模型在去噪早期主要恢复**低频全局结构**（帧间全局依赖性强），而后期则关注**高频局部细节**（注意力趋于局部）。对应地：
  - **绝对位置编码（APE）**：提供帧到序列起点/终点的全局位置信息，有助于构建完整动作语义，但无法外推到更长序列；
  - **相对位置编码（RPE）**：只编码帧间相对距离（选用了RoPE旋转位置编码），具备序列平移不变性，可泛化到更长序列，但缺乏全局语义信息。
- **BPE的实现**：在**推理时**通过一个调度器（scheduler）控制去噪过程中位置编码的切换——早期使用APE恢复全局动作连贯性，后期使用RPE平滑子序列间的过渡。**训练时随机交替使用APE和RPE**（各50%概率），使模型同时适应两种编码。
- **推理调度**：使用二元阶跃函数，最初125/60步使用APE（Babel/HumanML3D），随后切换到RPE。
- **注意力范围**：RPE的注意力范围被限制在注意力窗口H内（H=100/150），而APE注意力限于子序列内部；整体复杂度维持与L相关的二次复杂度。

### 核心技术二：Pose-Centric Cross-ATtention（PCCAT，姿态中心交叉注意力）
- **问题**：训练时每个动作序列只对应一个文本条件，但推理时不同子序列有不同条件。若条件与姿态混合进注意力计算，当相邻帧条件不同时，注意力分数对应的输入组合在训练中从未出现，造成训练-推理不一致。
- **PCCAT设计**：将**每帧的姿态与条件拼接作为Query**，而**Keys和Values仅使用纯姿态信息**。这样每个姿态的去噪只依赖其自身条件和相邻姿态，降低了条件与姿态之间的纠缠。
- **效果**：使模型在仅用"每序列单一条件"训练后，即可在推理时处理多条件组合，且无需依赖任何显式过渡标注。

### 与其他方法的关键差异
- 对比DoubleTake/DiffCollage/MultiDiffusion：后者将子序列独立生成后在重叠区域融合并执行额外去噪；FlowMDM则**一次性同时生成整段序列**，无需预定义过渡长度、无需后处理、无需额外去噪，避免冗余计算。

---

## 3. 实验设计

### 数据集
- **Babel**：提供细粒度、原子级别的文本标注（包含过渡动作），使用全局位置/朝向+SMPL关节6D旋转表示。
- **HumanML3D**：每个动作序列有多个文本描述，但**缺乏显式过渡标注**，训练时只有单一条件。使用263维姿态向量（关节坐标、角度、速度、脚部接触）。

### Benchmark与评测指标
- 生成长度为**32对文本描述+时长**的动作序列，分别评估32个子序列和31个过渡段。
- **子序列指标**：Top-3 R-precision（R-prec）、多模态距离（MM-Dist）、FID、多样性（Diversity）。
- **过渡质量指标**：FID、Diversity，以及论文新提出的：
  - **Peak Jerk（PJ）**：过渡段中所有关节的最大急动度（jerk，加速度的时间导数）值，捕捉极端突变；
  - **Area Under the Jerk（AUJ）**：瞬时急动度与数据集平均急动度之差的L1范数累计和，反映整体平滑度偏差。

### 对比方法
- **TEACH**（自回归方法）及其关闭球面线性插值过渡的变体TEACH B；
- **DoubleTake***（原版，基于MDM）与**DoubleTake**（使用PCCAT+APE重实现）；
- **DiffCollage** 和 **MultiDiffusion**（扩散采样组合方法）；
- TEACH/TEACH B因HumanML3D缺乏连续动作对而无法在该数据集上训练。

---

## 4. 资源与算力

- **论文未明确说明**所使用的GPU型号、数量、训练时长等具体算力信息。
- 仅提及所有实验使用**1000步扩散去噪**、分类器自由引导权重1.5/2.5、x0参数化与L2重建损失，以及使用网格搜索进行超参数调优。
- 在效率对比上，FlowMDM相比DoubleTake、DiffCollage、MultiDiffusion分别减少了**47.1%、28.4%、16.5%**的逐姿态去噪步数，从侧面体现了其推理效率优势，但未给出绝对时间数据。

---

## 5. 实验数量与充分性

### 实验数量
| 实验类型 | 数量/说明 |
|---|---|
| 主实验（两个数据集×多个对比方法） | 2组（Babel + HumanML3D），各对比4-5种基线 |
| 消融实验 | 2组（Babel + HumanML3D），共7种配置变体 |
| 外推实验（周期动作重复32次） | 2个数据集均有 |
| 定性分析 | 4组可视化场景 |
| 额外分析 | BPE调度权衡分析、过渡平滑度曲线等，详见补充材料 |

### 实验充分性评价
- **优点**：
  - 消融设计完备——分别验证了**位置编码（A/R/B）× 条件注入方式（PCCAT/SAT/CAT）** 的多种组合，能够清晰分离各组件贡献；
  - 两个数据集的训练设置不同（Babel含连续动作对，HumanML3D无），提供了不同难度和场景的验证；
  - 新指标PJ/AUJ补充了FID对过渡平滑度不敏感的问题，使评估更加全面；
  - 对比方法覆盖了自回归（TEACH）和扩散组合采样（DoubleTake、DiffCollage、MultiDiffusion）两大主流路线，公正性较好。
- **潜在不足**：
  - TEACH在HumanML3D上无法训练，导致该数据集上缺少自回归方法的对照；
  - 补充材料中提到的部分消融细节（如H的设置比较）在正文中未充分展开；
  - 在Babel数据集中，TEACH等方法由于依赖不同训练数据配置，其对比条件不是严格完全一致的。

---

## 6. 论文的主要结论与发现

1. **FlowMDM在HMC任务上达到SOTA**：在Babel和HumanML3D上，子序列的准确率指标（R-prec/MM-Dist）与SOTA相当或更优，FID显著优于所有对比方法。
2. **过渡质量大幅领先**：在过渡段的FID、PJ、AUJ指标上全面领先，生成的过渡最平滑（见图4，FlowMDM的jerk曲线峰值最短；外推任务中几乎无峰值）。
3. **BPE的有效性**：训练时同时暴露于APE和RPE能提升仅用单一编码的性能；推理时BPE调度可在全局一致性与过渡平滑性之间取得最佳平衡（约10%的APE去噪步数效果最佳）。
4. **PCCAT解决多条件推理不一致问题**：在HumanML3D这类单条件训练数据集上，PCCAT生成的过渡在FID和Diversity上明显优于SAT和CAT；在Babel上这种优势不明显，因为其训练数据本身包含多子序列。
5. **新指标的必要性**：FID与AUJ之间缺乏相关性，表明仅依赖FID评估过渡质量可能遗漏平滑度缺陷，PJ和AUJ是有效的补充指标。
6. **外推能力突出**：FlowMDM是唯一能够在静态（如t-pose）和周期动作（如"向右迈步"）的32次重复外推中保持动作连贯性和静态/周期特性的方法。

---

## 7. 优点

- **方法创新性强**：
  - BPE是首个将绝对与相对位置编码在扩散去噪链中动态融合的技术，充分利用了扩散模型"由全局到局部"的去噪特性，思路巧妙且通用性潜力大；
  - PCCAT从注意力机制层面缓解了训练-推理条件不一致问题，简洁有效，避免了对多条件标注数据的需求。
- **端到端、零后处理**：FlowMDM直接同时生成整段长序列，避免了延迟、误差累积和冗余计算，框架简洁高效。
- **评估体系完善**：提出PJ和AUJ两个基于急动度的新指标，填补了现有HMC评估在检测突变过渡方面的盲区，对社区有方法论贡献。
- **实验覆盖面广**：涵盖两大主流数据集、多种基线方法、消融分析、外推任务和定性可视化，分析细致（如jerk曲线图、BPE权衡曲线）。

---

## 8. 不足与局限

- **BPE绝对阶段的局限性**：在APE阶段，模型不建模子序列间的相互关系，导致子序列间的低频全局依赖是独立生成的；论文建议未来引入意图规划模块来建模子序列间的高级语义关系。
- **调度需要调参**：BPE的APE→RPE切换时机（初始步数、调度函数形式）需要针对不同数据集/场景调整，更多是一种超参数而非完全自适应的机制。
- **条件模态的通用性**：论文提到模型可推广到不同控制信号（音乐、场景等）的前提是"都在同一框架下训练"，该假设尚未经实验验证。
- **硬件资源信息缺失**：未报告训练时长、GPU配置等，不利于复现和资源评估。
- **应用限制**：目前只支持单个人体动作生成，未涉及多人交互、物体交互、物理合理性（如脚滑步、穿透）等复杂场景。
- **依赖标准动作表示**：Babel和HumanML3D使用不同的运动表示，FlowMDM需要针对不同表示分别适配，缺少跨数据集的统一表示验证。

---

（完）
