---
title: Programmable Motion Generation for Open-Set Motion Control Tasks
title_zh: 面向开放集运动控制任务的可编程运动生成
authors: "Liu, Hanchao, Zhan, Xiaohang, Huang, Shaoli, Mu, Tai-Jiang, Shan, Ying"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Liu_Programmable_Motion_Generation_for_Open-Set_Motion_Control_Tasks_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 5.0
evidence: 可编程开放集运动控制生成；并非特指3D人体运动或扩散/流匹配
tldr: 真实场景角色动画需要轨迹、关键帧、交互等多种约束，现有方法只能处理有限任务。本文提出开放集运动控制问题并引入可编程运动生成范式，将任意运动控制任务转化为可执行程序，从而灵活组合和扩展约束。该范式允许用户通过程序化描述定制运动控制，大幅提升运动生成的通用性和可扩展性。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1794, \"height\": 897, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1698, \"height\": 544, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 842, \"height\": 440, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1791, \"height\": 1146, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 860, \"height\": 501, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1812, \"height\": 339, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1800, \"height\": 770, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-liu-programmable-motion-generation-for-open-set-motion-control-tasks-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 854, \"height\": 227, \"label\": \"Table\"}]"
motivation: 现有运动控制方法只能处理单一或有限约束，难以扩展和定制。
method: 提出可编程运动生成范式，将任意运动控制任务表达为程序并进行生成。
result: 支持开放集、可定制的运动控制任务，扩展了传统方法。
conclusion: 可编程范式为复杂运动控制提供了统一且可扩展的解决方案。
---

## Abstract
Character animation in real-world scenarios necessitates a variety of constraints such as trajectories key-frames interactions etc. Existing methodologies typically treat single or a finite set of these constraint(s) as separate control tasks. These methods are often specialized and the tasks they address are rarely extendable or customizable. We categorize these as solutions to the close-set motion control problem. In response to the complexity of practical motion control we propose and attempt to solve the open-set motion control problem. This problem is characterized by an open and fully customizable set of motion control tasks. To address this we introduce a new paradigm programmable motion generation. In this paradigm any given motion control task is broken down into a combination of atomic constraints. These constraints are then programmed into an error function that quantifies the degree to which a motion sequence adheres to them. We utilize a pre-trained motion generation model and optimize its latent code to minimize the error function of the generated motion. Consequently the generated motion not only inherits the prior of the generative model but also satisfies the requirements of the compounded constraints. Our experiments demonstrate that our approach can generate high-quality motions when addressing a wide range of unseen tasks. These tasks encompass motion control by motion dynamics geometric constraints physical laws interactions with scenes objects or the character's own body parts etc. All of these are achieved in a unified approach without the need for ad-hoc paired training data collection or specialized network designs. During the programming of novel tasks we observed the emergence of new skills beyond those of the prior model. With the assistance of large language models we also achieved automatic programming. We hope that this work will pave the way for the motion control of general AI agents.

---

## 论文详细总结（自动生成）

# 论文总结：可编程运动生成（Programmable Motion Generation）

## 1. 核心问题与整体含义

- **研究动机**：现实世界中的角色动画需要同时满足多种运动约束（如轨迹、关键帧、物体交互、物理规律等），而现有 AI 方法通常将单一或有限个约束视为独立任务来设计专门的网络和数据集，这类方法本质上属于**闭集运动控制**，难以扩展和定制。
- **核心问题**：本文提出并定义了**开放集运动控制问题**——即运动控制任务的集合是开放、任意可定制的，且无需为每个新任务采集配对训练数据或重新设计网络结构。
- **整体含义**：该工作希望为通用 AI 智能体的运动控制铺路，让任意新任务可以通过“编程”的方式统一求解，而非逐一训练专用模型。

## 2. 方法论

- **核心思想**：任何复杂的运动控制任务都可以分解为若干**原子约束**的组合；几乎所有约束都可以用误差（Error）来度量，且误差在数学上是可加的。因此，可以将任务“编程”为一个可微的**误差函数**，然后优化预训练运动生成模型的潜码（latent code），使生成的运动在继承生成先验的同时满足约束。
- **关键技术细节**：
  - **原子约束库**：包括绝对位置约束、高阶动力学约束（速度/加速度）、几何约束（点/线/面/体）、相对距离约束、方向约束、关键帧约束、质心约束等，作为构建复杂任务的模块。
  - **运动编程框架**：定义统一输入（motions + parameters）和输出（标量 total_error）；重新设计了逻辑运算，如 `>` 用 `max(margin - E, 0)`、`<` 用 `max(E - margin, 0)`、`AND` 用 `E1 + E2`、`OR` 用 `min(E1, E2)`、`NOT` 用 `-E`；支持 `for`/`if` 等流程控制。
  - **优化方式**：使用预训练的 MDM（Motion Diffusion Model）作为生成先验，并转换为 DDIM 形式使潜码 z 成为单个向量；用 Adam 优化器（学习率 0.005，100 步）最小化误差函数。
  - **约束松弛策略**：利用人体运动在水平面上的平移/旋转不变性，将涉及水平位置或旋转的约束先变换到更易优化的等价形式，优化后再变换回原约束。
- **算法流程**：任务描述 → 分解为原子约束 → 编写/生成误差函数 F(z) → 优化潜码 z 使得 F(Gθ(z, C), p) 最小 → 生成满足约束且高质量的运动序列。

## 3. 实验设计

- **数据集**：使用 HumanML3D 数据集预训练的官方 MDM 权重（冻结）。
- **Benchmark 与任务类别**：论文设计了 6 大类开放集子任务，包括：
  - 高阶动力学控制（如指定关键帧速度）
  - 几何约束控制（如手触墙、脚踩平衡木）
  - 人-场景交互（如限高、避障、方形区域内行走、窄缝通行）
  - 人-物体交互（如移动物体、抱球）
  - 人体自接触（如手一直摸头）
  - 物理约束生成（如单脚站立平衡、抱重球保持平衡）
- **对比方法**：
  - Inverse Kinematics（IK，直接优化运动序列）
  - IK + 正则化（IK+Reg.，加帧间平滑项）
  - MDM Edit（MDM 自带轨迹编辑/修复能力）
  - PriorMDM（MDM 微调版控制）
- **评估指标**：非语义质量用 Foot Skate Ratio 和 Max Acc.；语义质量用 FID、Diversity、R-Precision；约束满足程度用 C.Err. 和 Unsuccess Rate（约束误差 > 5cm 视为失败）。

## 4. 资源与算力

- 论文**未明确说明**所使用的 GPU 型号、数量或训练/推理时间。
- 仅提到：MDM 使用 DDIM 形式、100 步去噪；优化使用 Adam、学习率 0.005、100 次优化迭代；除 LLM 自动编程外，所有实验均在推理阶段完成，无需额外训练。
- 由于未给出具体硬件配置，无法量化总算力消耗，但从方法本质看属于“推理时优化”范式，算力成本远低于重新训练专用模型。

## 5. 实验数量与充分性

- **定量实验**：2 张对比表，覆盖已知约束（Table 1，HSI-1）和未知/未见任务（Table 2，HSI-2、HSI-3、GEO-1、HOI-1），共 5 个具体子任务的量化评估。
- **定性实验**：Figure 4 展示了 6 个代表性开放集任务的定性结果（含 GPT 自动编程示例），涵盖各类约束。
- **消融/分析实验**：分析了运动先验的作用（Ours vs IK vs IK+Reg.）以及骨长保持能力（Table 3），验证了方法相比于 inpainting 类方法的优势。
- **总体评价**：实验覆盖了 6 大任务类别、10 个以上具体任务，在“开放集”问题的初期研究中**较为充分**；定量指标设计涵盖运动质量、约束满足和语义质量，与多个基线公平对比，整体具有较强的说服力和客观性。但缺少与 GMD、OmniControl 等更新的轨迹控制方法的直接对比（这些方法不在同一任务设定下）。

## 6. 主要结论与发现

- 提出的**可编程运动生成范式**能够以统一、无需重新训练的方式解决广泛的开放集运动控制任务。
- 生成的运动在继承生成模型先验的同时，能很好地满足复合约束，且运动质量在多个指标上优于既有基线。
- **新技能涌现**：在面对“狭窄通道行走”等未见任务时，模型自发产生了收拢手臂、缩肩等适应行为，体现出一定程度的技能泛化能力。
- **LLM 自动编程可行性**：GPT 能理解“触碰墙壁”“避障”等语义并自动生成正确的误差函数代码，使得任意开放集任务可以实现“文本描述 → 自动编程 → 运动生成”的自动化流程。

## 7. 优点

- **范式创新**：首次系统性地将开放集运动控制问题与“编程”思想结合，提供了一个统一的、可扩展的框架。
- **可定制性与扩展性**：用户只需通过组合原子约束即可构造任意新任务，无需搜集数据或设计网络，模块化程度高。
- **逻辑运算设计巧妙**：将 `>`、`<`、`AND`、`OR`、`NOT` 等重定义为可微形式，为复杂约束组合提供了表达力。
- **运动先验保证质量**：基于冻结的预训练 MDM 优化潜码，从本质上避免了 IK 方法常见的运动失真、骨骼拉伸等问题。
- **兼容 LLM**：支持大语言模型自动生成误差函数，为全自动运动控制铺平道路。
- **约束松弛策略**：利用运动学不变性简化优化问题，提升了优化效率与稳定性。

## 8. 不足与局限

- **实验规模有限**：虽然任务类别多样，但每个类别的具体子任务数量偏少（每个 1~2 个），定量评估仅覆盖 5 个子任务，覆盖面有待扩展。
- **缺少大规模消融**：未系统分析不同原子约束类型、不同优化步数/学习率、不同生成模型（如非扩散模型）对结果的影响。
- **依赖可微性与手工设计**：框架要求误差函数可微，某些真实世界约束（如复杂物理接触、不规则物体形状）可能难以直接编程；尽管 LLM 可以辅助，但复杂任务的编程仍不保证稳定可靠。
- **优化效率问题**：每次生成新任务都需要 100 步潜码优化，实际应用中可能面临实时性/交互性瓶颈。
- **评估指标局限性**：语义相关指标（FID、R-Precision）仅适用于约束来自真实数据分布的任务，对未知约束任务只能评估运动质量，缺乏对“语义合理性”的客观度量。
- **基线可比性**：与 PriorMDM、MDM Edit 的对比中存在为适配任务而添加临时技巧的情况，方法间公平性虽大体成立但仍有潜在争议空间。
- **应用范围**：框架目前基于 HumanML3D 单数据集和 MDM 单一生成模型，对更复杂场景（多人交互、真实物理仿真）的泛化能力未经验证。

（完）
