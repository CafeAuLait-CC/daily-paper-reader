---
title: "MultiMotion: Multi Subject Video Motion Transfer via Video Diffusion Transformer"
title_zh: MultiMotion：基于视频扩散Transformer的多主体视频运动迁移
authors: "Penghui Liu, Jiangshan Wang, Yutong Shen, Shanhui Mo, Chenyang Qi, Jack Ma"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/37660/41622"
tags: ["query:dmg"]
score: 4.0
evidence: 基于扩散Transformer的多物体视频运动迁移
tldr: 现有扩散Transformer在视频运动迁移中面临多物体运动纠缠和缺乏物体级控制的问题。本文提出MultiMotion框架，利用SAM 2掩码实现注意力运动流的显式解耦，并提出RectPC预测-校正采样器以加速生成。还构建了首个面向DiT多物体运动迁移的基准数据集。实验表明该方法能有效控制多物体运动，提升生成效率。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 多物体视频运动迁移中存在运动纠缠和缺乏物体级控制，DiT架构难以处理。
method: 引入掩码感知注意力运动流（AMF）显式解耦多物体运动，并设计高阶预测-校正求解器RectPC提高采样效率。
result: 在构建的多物体基准上实现更准确的运动控制和更高效的采样，验证了AMF与RectPC的有效性。
conclusion: 为基于DiT的多物体视频运动迁移提供了新的解耦控制与高效采样方案。
---

## Abstract
Multi-object video motion transfer poses significant challenges for Diffusion Transformer (DiT) architectures due to inherent motion entanglement and lack of object-level control. We present MultiMotion, a novel unified framework that overcomes these limitations. Our core innovation is Mask-aware Attention Motion Flow (AMF), which utilizes SAM 2 masks to explicitly disentangle and control motion features for multiple objects within the DiT pipeline. Furthermore, we introduce RectPC, a high-order predictor-corrector solver for efficient and accurate sampling, particularly beneficial for multi-entity generation. To facilitate rigorous evaluation, we construct the first benchmark dataset specifically for DiT-based multi-object motion transfer. MultiMotion demonstrably achieves precise, semantically aligned, and temporally coherent motion transfer for multiple distinct objects, maintaining DiT's high quality and scalability.The code is in the supp.

---

## 论文详细总结（自动生成）

## 1. 核心问题与研究动机

- **问题背景**：多物体视频运动迁移旨在将参考视频中多个独立对象的运动模式迁移到目标视频中，应用场景涵盖虚拟角色控制、多角色动画、影视特效等。相比成熟的单物体运动迁移，多物体场景面临**运动纠缠**（多个对象的运动在潜空间中相互干扰）、**语义对齐困难**以及**交互行为建模复杂**等挑战。
- **DiT 架构的固有局限**：Diffusion Transformer（DiT）凭借其统一的时空注意力机制和可扩展性成为主流架构，但其**全局注意力设计缺乏对独立实例的感知**，导致不同对象的运动在潜空间中不可避免地相互干涉，造成语义漂移、对象可控性下降和视觉输出混乱。
- **现有求解器的不足**：主流扩散反演求解器（DDIM、DPM-Solver、UniPC 等）主要针对单图像或短时无约束视频生成而设计，在多物体视频编辑中表现出**高重建误差、收敛缓慢和明显的不稳定性**，尤其在动态遮挡和复杂交互场景下问题更为突出。
- **现有方法的空白**：虽然已有研究尝试通过 token 掩码或姿态条件为 DiT 注入实例感知能力，但大多局限于低分辨率生成或单物体动画，缺乏**可扩展、高保真的多物体运动控制能力**。

## 2. 方法论

### 2.1 整体框架

MultiMotion 由三个关键阶段组成：**多物体运动分解** → **掩码感知注意力运动流（Mask-aware AMF）提取** → **多物体运动重组与生成**，并配以 **RectPC 求解器** 提升采样效率与稳定性。

### 2.2 多物体运动分解

- **实例级语义分割**：利用 SAM 2 对参考视频 Vref 中的每个对象 sk 生成跨帧的精确二值掩码序列 Msk = {M¹sk, M²sk, ..., MFsk}。
- **运动区域解耦**：为避免对象间运动干扰，定义对象 sk 从帧 i 到帧 j 的独立运动区域为：

  **Mⁱ|ʲsk = Mⁱsk \ ⋃ₘ≠ₖ (Mⁱsk ∩ Mʲsm)**

  即从对象自身掩码中扣除与其他对象掩码的交集，确保其运动特征不被其他对象的运动污染。

### 2.3 掩码感知注意力运动流（Mask-aware AMF）

- **DiT 注意力分析**：在去噪步 t=0，利用 DiT 第 n 层的自注意力提取查询矩阵 Q 与键矩阵 K。
- **掩码引导的跨帧注意力**：传统 AMF 计算全局跨帧注意力，容易造成多物体运动混淆。MultiMotion 提出掩码约束的注意力计算：

  **A⊗ⁱ,ʲsk = σ(τ(Qⁱsk (Kʲsk)ᵀ / √dk)) ⊙ Mⁱ,ʲ_cross**

  其中 Mⁱ,ʲ_cross 为精心构造的跨帧掩码约束矩阵，确保注意力仅在有效且解耦的对象区域内计算。
- **对象特定运动流构建**：对掩码引导的注意力图取 argmax 得到最强对应关系，进而构建逐 patch 的位移矩阵 Δⁱ,ʲsk，最终定义对象 sk 的注意力运动流：**AMF_sk(zref) = {Δⁱ,ʲsk}_{i,j∈[1,F]}**。

### 2.4 多物体运动重组

- **对象级运动引导**：在目标视频生成过程中，每个对象利用提取的 AMF 作为精确引导信号，计算当前软运动流：

  **Δ̃ⁱ,ʲsk(t) = Σₚ A⊗ⁱ,ʲsk(p) · pos(p)**

- **多物体运动损失**：

  **Lobj = Σₖ λₖ ‖AMF_sk(zref) − AMF_sk(zt)‖²₂**（对象运动保真）

  **Lbg = λc ‖AMF_bg(zref) − AMF_bg(zt)‖²₂**（背景一致性）

  总损失 **Lmulti = Lobj + Lbg**。

- **自适应权重调整**：当某个对象被其他对象严重遮挡时，通过 **λadaptive_k = λk · exp(−α · IoU(Mⁱsk, ⋃ₘ≠ₖ Mʲsm))** 动态降低其损失权重，避免歧义区域中错误的引导信号。

### 2.5 RectPC 求解器

- **λ-空间重参数化**：采用 λt = log αt − log σt 的重新参数化，为数值积分提供更稳定、更线性的路径。
- **高阶外推估计器**：利用历史噪声预测 {ε̂s₀, ..., ε̂s_{K−1}} 进行高阶外推预测：

  **x_pred = Ax_{λt−1} − B·ϕ₁(h)·ε̂s₀ − B·Σᵢ ρᵢDᵢ**

  其中 Dᵢ = ε̂sᵢ − ε̂sᵢ₋₁ 为历史噪声估计的差分，ρᵢ 通过 Vandermonde 系统求解以保证高阶精度。
- **中点校正**：可选的中点校正步骤通过模型在中点处的预测动态修正轨迹：

  **x_corr = x_pred + (h²/2)·(vθ(x_mid, t) − vθ(x_pred, t))/h**

  有效减小累积误差，提升轨迹精度和稳定性。
- **推理流程**：RectPC 的完整推理流程如算法伪代码所示（初始高斯噪声 → 逐步高阶预测 → 可选校正 → 迭代直至得到最终样本）。

## 3. 实验设计

### 3.1 数据集与基准（MultiMotionEval）

- **首个专为 DiT 多物体运动迁移构建的基准数据集**，共 **103 个高质量视频**，每个视频包含 **41 帧**（约 2 秒），分辨率 **832×480**。
- 涵盖**321 个不同对象**，超过 80% 的场景包含两个或以上对象。
- 涉及**追逐、遮挡、同步协作、分离**等多种具有挑战性的交互模式。
- 所有视频均提供**实例级掩码和轨迹标注**；视频来自公开授权的视频平台，文字描述由 GPT4o 自动生成。

### 3.2 对比方法

与 **MOFT、MotionInversion、MotionClone、SMM、MotionDirector、DiTFlow** 六种主流视频运动迁移方法进行对比。Motionshop 和 MotionCrafter 因缺乏公开版本被排除。

### 3.3 评估指标

- **文本相似度（Text Sim.）**：生成内容与文本描述的对齐程度。
- **运动保真度（Motion Fid.）**：参考视频与生成视频中对象轨迹的相似性。
- **时间一致性（Temp. Cons.）**：相邻帧之间 CLIP 特征的相似性。

### 3.4 实现细节

- 统一使用 70 步去噪过程；前 20 步使用 Adam 优化器进行 5 步微调，学习率从 0.008 线性衰减至 0.002。
- AMF 损失在 WAN2.1-1.3B 模型的第 15 个 Transformer 块上进行特征对齐。

## 4. 资源与算力

**论文正文中未明确说明所使用的 GPU 型号、数量、训练时长等算力信息**，也未提及模型的训练成本或推理时间开销。仅能从实现细节推断使用了 WAN2.1-1.3B 作为基础 DiT 模型，但具体硬件配置不可考。

## 5. 实验数量与充分性

### 实验数量

- **主对比实验**：在 MultiMotionEval 上与 6 种基线方法进行了系统比较，含定性可视化（图 4）和定量指标（表 1）。
- **消融实验**：设计 4 组变体实验（A：DiT-Flow 基线；B：基线+RectPC；C：基线+Mask-aware AMF；D：完整模型），结合定量表格（表 2）和定性可视化（图 5）验证各模块贡献。
- **反演重建分析**：对比 RectPC 与 DDIM、DPM++、UniPC 在反演-重建过程中的 MSE 曲线（图 2）。

### 充分性与客观性评估

- **优点**：实验覆盖多类运动场景（单物体、多物体、相机运动）；消融设计合理，能够清晰分离每个模块的贡献；定性可视化直观展示了各方法在多物体场景下的表现差异。
- **不足之处**：
  - 所有评估都基于**自建的单一基准** MultiMotionEval，缺乏在已有公开数据集上的验证。
  - 6 个基线方法中大多数为 UNet 架构方法，**与 DiT 架构方法的直接对比不足**。
  - 评估指标主要依赖 CLIP 特征相似性等自动度量，**缺少用户研究（human evaluation）** 来验证主观视觉质量的差异。
  - 未报告定量实验的显著性检验或方差信息，无法判断结果的统计显著性。

## 6. 主要结论

- MultiMotion 是**首个面向 DiT 架构的多物体运动迁移统一框架**，通过 Mask-aware AMF 实现了对象级别的运动解耦和精确控制，有效克服了 DiT 全局注意力导致的多物体运动纠缠问题。
- 提出的 **RectPC 求解器**在反演-重建过程中显著降低 MSE（如图 2 所示），具备更高的采样效率和稳定性，且其核心架构具有良好泛化能力。
- 在 MultiMotionEval 基准上，MultiMotion 在**所有评估指标上均优于现有方法**：文本相似度 0.385（对比最强基线 DiTFlow 0.368）、运动保真度 0.985（对比 SMM 0.920）、时间一致性 0.978（对比 MotionDirector 0.950）。
- 消融实验证明 RectPC 和 Mask-aware AMF **两者并非独立起作用，而是协同增效**，共同实现高质量、高保真、语义准确的多物体运动迁移。

## 7. 方法亮点与贡献

- **针对性强**：直面 DiT 架构中多物体运动迁移的运动纠缠和缺乏物体级控制两大核心痛点，填补了该方向的研究空白。
- **SAM 2 掩码的巧妙运用**：利用 SAM 2 的高质量实例掩码，通过运动区域解耦公式（集合差运算）有效隔离各对象的运动特征，方法简洁而有效。
- **注意力机制的精细控制**：通过掩码约束的跨帧注意力计算，将物体级控制直接嵌入 DiT 的注意力机制中，不改变模型架构即可实现对象级运动引导。
- **自适应遮挡处理**：基于 IoU 的自适应权重调整机制，在遮挡严重时自动降低模糊区域的引导信号权重，增强了对复杂交互场景的鲁棒性。
- **先进的高阶采样器**：RectPC 融合高阶外推、有限差分校正和中点细化，在 λ-空间中实现高效、稳定采样，且具有跨任务的通用潜力。
- **基准建设贡献**：构建了首个专为 DiT 多物体运动迁移设计的标准化基准 MultiMotionEval，为领域内的系统性评估提供了重要资源。

## 8. 不足与局限

- **算力信息缺失**：未报告任何训练/推理的硬件配置和计算开销，削弱了可复现性和实用性参考价值。
- **基准验证范围有限**：仅在自建基准上评估，未在已有公开视频数据集上验证泛化能力；且所有视频均来自单一来源平台，可能存在数据分布偏差。
- **基线对比不够全面**：对比方法以 UNet 架构为主，缺少与其他 DiT 架构运动迁移方法的直接对比；同时排除了 Motionshop 和 MotionCrafter，削弱了对比的完整性。
- **指标维度有限**：评估主要依赖自动度量指标，缺乏用户研究和感知质量评估（如 FVD 等视频质量指标）；也未针对复杂交互场景（重度遮挡、多人协作）进行专门的量化分析。
- **对 SAM 2 的强依赖**：运动解耦质量直接取决于 SAM 2 的分割精度，在极端遮挡、运动模糊或细小对象场景下掩码可能不准确，从而影响整体性能，但论文未讨论该失败模式。
- **模型泛化性未验证**：论文提到 RectPC 具有通用性，但未展示其在其他 DiT 模型或非视频任务上的实验结果。
- **文本描述依赖自动生成**：数据集标注使用 GPT4o 自动生成，可能存在标注噪声，但未报告人工校验的比例或质量评估。

（完）
