---
title: "CoMA: Compositional Human Motion Generation with Multi-modal Agents"
title_zh: CoMA：基于多模态智能体的组合式人体运动生成
authors: "Shanlin Sun, Jiaqi Xu, Gabriel de Araujo, Shenghan Zhou, Hanwen Zhang, Ziheng Huang, Chenyu You, Xiaohui Xie"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37878/41840"
tags: ["query:dmg"]
score: 8.0
evidence: 使用多模态智能体与掩码Transformer生成三维人体运动，未涉及扩散/流匹配
tldr: 三维人体运动生成仍难以处理训练数据中未见的复杂细节动作，主要受限于数据集稀缺。CoMA借助多个大语言模型和视觉模型智能体协同工作，结合基于掩码Transformer的生成器（包含身体部件编码器和码本），实现精细控制和组合式生成。框架支持短长序列生成、编辑和理解。在多个数据集上的实验表明，CoMA能生成更复杂、更可控的动作，并缓解了数据稀缺带来的生成瓶颈。虽然没有使用扩散/流匹配，但为运动生成提供了另一种多模态生成范式。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法难以生成训练数据中未见的复杂细节动作，数据集稀缺且生成新样本成本高。
method: 将大语言模型和视觉模型作为多智能体协作，配合掩码Transformer生成器与身体部件编码器/码本实现细粒度运动生成。
result: 实验证明在复杂动作生成、编辑和理解任务上表现优越，支持长短序列。
conclusion: CoMA通过多模态智能体与部件级生成器推动复杂三维人体运动生成的进展。
---

## Abstract
3D human motion generation has seen substantial advancement in recent years. While state-of-the-art approaches have improved performance significantly, they still struggle with complex and detailed motions unseen in training data, largely due to the scarcity of motion datasets and the prohibitive cost of generating new training examples. To address these challenges, we introduce CoMA, an agent-based solution for complex human motion generation, editing, and comprehension. CoMA leverages multiple collaborative agents powered by large language and vision models, alongside a mask transformer-based motion generator featuring body part-specific encoders and codebooks for fine-grained control. Our framework enables generation of both short and long motion sequences with detailed instructions, text-guided motion editing, and self-correction for improved quality. Evaluations on the HumanML3D dataset demonstrate competitive performance against state-of-the-art methods. Additionally, we create a set of context-rich, compositional, and long text prompts, where user studies show our method significantly outperforms existing approaches.

---

## 论文详细总结（自动生成）

# CoMA 论文中文总结

## 1. 论文的核心问题与整体含义

- **研究动机**：三维人体运动生成近年来取得显著进展，但现有方法在生成训练数据中未出现过的复杂、细节丰富的动作时仍表现不佳。
- **根本原因**：① 文本到动作的映射本身具有高度歧义性；② 人体运动数据采集成本高昂，导致空间和时间上复杂的数据稀缺。
- **现有方法局限**：
  - 扩散/自回归等生成模型难以处理“上下文丰富”的文本描述，尤其是训练集之外的提示。
  - 已有方法（如 FineMoGen、CoMo）虽引入 LLM 解析提示，但缺乏组合式生成、自校正与细粒度身体部件编辑的能力。
  - 单一模型难以同时完成复杂动作生成、时序组合、空间组合、编辑和理解。
- **论文含义**：提出 CoMA，一个基于多模态智能体协作的组合式人体运动生成框架，将 LLM、VLM 与空间感知掩码生成模型结合，试图突破数据稀缺和复杂动作的生成瓶颈，同时支持生成、编辑、理解与自我修正。

## 2. 论文提出的方法论

- **总体框架**：CoMA 由四个协作智能体组成，将复杂任务分解为多个简单子任务，分阶段执行（生成、编辑、审阅、轨迹控制）。
  - **任务规划器（Task Planner）**：
    - 使用 LLM（GPT-4o）对输入文本进行重写/改述，去除数据集中不存在的抽象描述。
    - 采用检索增强生成（RAG），将改写词汇限制在训练集词汇内，减少幻觉。
    - 自动将长文本拆分为时间上连续的动作片段。
    - 将任务分解为“基础动作生成 + 局部身体部件编辑”两个子任务。
  - **运动生成器（Motion Generator，SPAM）**：
    - 提出“空间感知掩码生成运动模型”（Spatially-Aware Masked Generative Motion Model）。
    - 核心思想：将人体运动分解为四个身体部位（左上、右上、左下、右下），每个部位使用独立的编码器和码本进行离散化，共享解码器重建全身动作。
    - 基于残差向量量化（RVQ），每层残差量化公式为：\(\tilde{b}^v = Q(r^v),\ r^{v+1}=r^v-\tilde{b}^v\)。
    - 训练损失：\(L_{rvq} = \|m-\tilde{m}\|_1 + \beta \sum_v\|R^v - sg[B^v]\|_2^2\)。
    - 使用因子化空间-时间自注意力：先在同一时间步的四个身体部位间做空间注意力，再在每个空间位置跨时间步做时间注意力。
    - 支持三种无需额外训练的编辑方式：
      - 帧间插值编辑（In-between Editing）
      - 身体部件编辑（Body Part Editing）
      - 序列混合编辑（Blend Editing）
  - **运动评审器（Motion Reviewer）**：
    - 渲染生成的动作序列，使用 VLM（VideoChat2）生成动作描述。
    - 将描述与原始文本提示对比，评估一致性，并通过 LLM 生成修正指令，反馈给运动生成器。
  - **轨迹编辑器（Trajectory Editor）**：
    - 可选模块，根据轨迹文本描述生成 2D B 样条曲线函数，映射到骨盆轨迹上。
    - 使用思维链（CoT）调用 LLM 的空间推理能力，支持直线、绕障碍等轨迹控制。

## 3. 实验设计

- **标准数据集与基准**：
  - **HumanML3D**：包含 14,616 个动作，44,970 条文本描述；标准划分：23,384 训练 / 1,460 验证 / 4,384 测试。
  - 评估指标：FID（分布距离）、R-Precision（Top-1/2/3）、Multimodal Distance、Multimodality。
- **对比方法**：
  - 扩散类：MDM、FineMoGen、CoMo、ReMoDiffuse
  - 掩码生成类：MMM、MoMask
  - 自回归类：T2M-GPT、MotionGPT
  - 大运动语言模型类：MotionChain、Motion-Agent、Motion-R1
- **运动编辑实验**：定性对比 CoMA vs. MMM vs. Motion-Agent，测试“左手挥舞同时右手举向头部”这类空间组合动作。
- **运动描述生成实验**：在 HumanML3D 上对比 TM2T、MotionGPT、MotionChain、MotionLLM，使用 BLEU、ROUGE、CIDEr、BERTScore。
- **用户研究**：
  - 设计 42 个挑战性提示（长文本、上下文丰富、空间组合式）。
  - 96 名参与者对 CoMA、MoMask、ReMoDiffuse、MMM、MotionGPT、FineMoGen 生成序列评分。
  - 提出运动对齐分数（MAS），用 InternVideo2 计算视频-文本嵌入相似度。
  - 另有 18 名参与者完成智能体消融的用户偏好测试。
- **智能体消融**：在 MTT 复杂运动数据集上，对比 STMC（MotionDiffuse）、EnergyMoGen（E-MOGEN）和 SPAM，逐步加入 Task Planner、Motion Reviewer、时间分段、任务分解，评估 FID、R@1、R@3、M2T、M2M。

## 4. 资源与算力

- **论文正文未明确披露训练所用的 GPU 型号、数量、训练时长等算力信息**。
- 仅提到使用 GPT-4o 作为 LLM、VideoChat2 作为 VLM；部分训练与实现细节在附录中，但提取文本未包含具体资源数据。
- 因此，无法从正文评估其训练成本和可复现性所需的硬件资源。

## 5. 实验数量与充分性

- **实验数量**：较为丰富，包含：
  - 1 组标准 benchmark（HumanML3D）定量对比（表 2）
  - 1 组运动编辑定性展示（图 5）
  - 1 组运动描述生成对比（表 3）
  - 1 组用户研究（评分、偏好、MAS，图 6）
  - 1 组在 MTT 上的智能体消融（表 4）
- **充分性分析**：
  - 优点：覆盖了生成、编辑、理解、消融和用户体验多个维度，且消融实验证实了各智能体的贡献。
  - 不足：
    - 标准 benchmark 仅在 HumanML3D 单一数据集上进行，缺少 BABEL、HumanAct12 等其他数据集的验证。
    - SPAM 的 FID 不是最优（0.092 vs MoMask 0.045），Multimodality 明显偏低（0.924），说明多样性不足，但论文未展开讨论。
    - 用户研究的主观性和提示选择可能偏向 CoMA 擅长场景，对比方法（如 Parco）仅在图 7 中定性出现，未纳入正式用户研究。
    - 轨迹编辑器的消融和定量分析缺失，仅在框架描述中提及。

## 6. 论文的主要结论与发现

- CoMA 通过 LLM 任务规划、VLM 自我评审和 SPAM 部件级生成，能够有效处理复杂、上下文丰富、长周期、空间组合式运动生成，优于现有方法。
- SPAM 在标准 HumanML3D 上达到与 SOTA 竞争的精度，尤其在 R-Precision Top-1 上取得第一（0.526），展现出细粒度指令跟随优势。
- MVC 运动描述模型在 BLEU 和 CIDEr 上超过对比方法，说明其生成动作描述的准确性。
- 用户研究显示，CoMA 在复杂动作生成上的评分和偏好显著高于 MoMask、FineMoGen、ReMoDiffuse、MMM、MotionGPT 等。
- 消融实验表明，Task Planner 和 Motion Reviewer 对文本-运动对齐（R@1、M2T）有显著提升，任务分解与时间分段也有正向贡献。

## 7. 优点

- **架构创新**：首次将“多智能体协作”引入人体运动生成，将 LLM 的任务推理、VLM 的视觉反馈与传统生成模型有机结合。
- **细粒度空间控制**：SPAM 的四部件编码器和码本设计，使模型能独立编辑左右上下肢体，支持更精细的动作合成。
- **自校正机制**：Motion Reviewer 通过渲染-描述-对比-修正 的闭环，提高生成结果与文本的一致性。
- **组合式生成**：支持时间分段、空间组合和轨迹控制，能处理长序列和复杂描述。
- **RAG 与 CoT 使用**：在任务规划中采用 RAG 限制词汇和 CoT 增强空间推理，降低 LLM 幻觉风险。
- **良好的可扩展性**：提出将 CoMA 作为数据引擎生成配对数据，训练统一多模态运动模型。

## 8. 不足与局限

- **LLM 可靠性**：依赖 GPT-4o 等外部 LLM，仍可能产生幻觉或错误的任务分解，影响最终生成质量；论文也承认这是主要局限。
- **基准性能不全面**：标准 HumanML3D 上 FID 不是最优，多样性（Multimodality）明显低于其它方法，说明生成动作多样性不足。
- **实验覆盖不足**：仅在 HumanML3D 和 MTT 上验证，缺少更大规模或更多样化的数据集（如 Motion-X、BABEL）的评估；轨迹编辑没有独立量化评价。
- **用户研究偏差**：挑战性提示集由作者设计，可能偏向 CoMA 优势场景；对照方法未全部纳入（如 Parco 仅在定性图中出现）。
- **资源信息缺失**：未报告训练算力、模型参数规模等，复现门槛较高。
- **应用限制**：框架流程较重，多智能体协作推理开销大，实时应用能力未知；生成质量仍受底层 SPAM 模型容量限制。

（完）
