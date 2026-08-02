---
title: "FlowRAM: Grounding Flow Matching Policy with Region-Aware Mamba Framework for Robotic Manipulation"
title_zh: FlowRAM：基于区域感知 Mamba 框架的流匹配策略在机器人操作中的应用
authors: "Wang, Sen, Wang, Le, Zhou, Sanping, Tian, Jingyi, Li, Jiayi, Sun, Haowen, Tang, Wei"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_FlowRAM_Grounding_Flow_Matching_Policy_with_Region-Aware_Mamba_Framework_for_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 6.0
evidence: 用于机器人操作的区域感知 Mamba 流匹配策略
tldr: 针对现有扩散策略学习方法推理时迭代去噪导致效率低的问题，本文提出 FlowRAM，利用流匹配生成模型实现区域感知操作。方法设计动态半径调度进行自适应感知，并借助 Mamba 框架实现高效多模态信息处理，在保持高精度的同时提升推理速度。实验表明该方法在机器人操作任务上具有竞争力。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 855, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 911, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1804, \"height\": 629, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1788, \"height\": 451, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 869, \"height\": 482, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 542, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1801, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 859, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 857, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-wang-flowram-grounding-flow-matching-policy-with-region-aware-mamba-framework-for-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 854, \"height\": 350, \"label\": \"Table\"}]"
motivation: 现有的基于扩散的策略学习方法推理效率低，且未充分利用生成模型在 3D 环境信息探索中的潜力。
method: 提出 FlowRAM 框架，结合流匹配模型与区域感知 Mamba，设计动态半径调度以支持自适感知和多模态信息处理。
result: 在机器人高精度操作任务上实现高效推理和良好性能，验证了流匹配策略的可行性。
conclusion: 为生成式策略学习提供了一种高效的新框架，并展示了流匹配在机器人操作中的价值。
---

## Abstract
Robotic manipulation in high-precision tasks is essential for numerous industrial and real-world applications where accuracy and speed are required. Yet current diffusion-based policy learning methods generally suffer from low computational efficiency due to the iterative denoising process during inference. Moreover, these methods do not fully explore the potential of generative models for enhancing information exploration in 3D environments. In response, we propose FlowRAM, a novel framework that leverages generative models to achieve region-aware perception, enabling efficient multimodal information processing. Specifically, we devise a Dynamic Radius Schedule, which enables adaptive perception, facilitating transitions from global scene comprehension to fine-grained geometric details. Furthermore, we integrate state space models to integrate multimodal information, while preserving linear computational complexity. In addition, we employ conditional flow matching to learn action poses by regressing deterministic vector fields, which simplifies the learning process while maintaining performance. We verify the effectiveness of the FlowRAM in the RLBench, an established manipulation benchmark, and achieve state-of-the-art performance. The results demonstrate that FlowRAM achieves a remarkable improvement, particularly in high-precision tasks, where it outperforms previous methods by 12.0% in average success rate. Additionally, FlowRAM is able to generate physically plausible actions for a variety of real-world tasks in less than 4 time steps, significantly increasing inference speed.

---

## 论文详细总结（自动生成）

# FlowRAM：基于区域感知 Mamba 框架的流匹配策略在机器人操作中的应用——论文总结

## 一、核心问题与研究动机

### 1.1 研究背景
- 高精度机器人操作任务（如插USB、拧螺丝、插充电器）在工业与真实世界中具有重要应用价值，对**精度与速度**同时提出严苛要求。
- 现有机器人操作策略主要分为两类：
  - **确定性策略**：直接预测动作的条件概率分布，但在高维连续动作空间中表现受限。
  - **生成式策略（以扩散模型为主）**：通过迭代去噪过程生成动作，能较好建模多模态动作分布，但**推理速度极慢**，难以满足实时控制需求。

### 1.2 核心问题
1. **感知层面**：现有方法缺乏对任务相关区域的专门感知能力，难以获取足够精细的几何细节，导致高精度任务性能不足。
2. **生成效率**：扩散模型迭代去噪的生成范式天然低效，严重限制了机器人的实时控制能力。

### 1.3 核心思想
FlowRAM 通过**条件流匹配（Conditional Flow Matching, CFM）**替代扩散模型，并引入**区域感知的动态半径调度（Dynamic Radius Schedule, DRS）**，在保证生成质量的同时大幅提升推理效率，实现高精度与高效率的统一。


## 二、方法论

### 2.1 总体框架
FlowRAM 是一个基于 Mamba 的端到端框架，包含三大核心组件：
1. **区域感知感知模块**（由动态半径调度 DRS 驱动）
2. **多模态 Mamba 融合模块**
3. **条件流匹配策略学习模块**

系统输入多视角 RGB-D 图像、点云、语言指令和机器人本体感知（proprioception），输出下一关键帧的 6-DoF 末端执行器位姿。

### 2.2 条件流匹配（CFM）基础
- 通过常微分方程（ODE）在噪声分布 π₀ 与目标动作分布 π₁ 之间建立传输路径：

  ```
  dx_t = v_θ(x_t, t)dt,  t ∈ [0, 1]
  ```

- 使用线性插值路径 `x_t = t·x₁ + (1-t)·x₀`，优化目标为回归目标速度场：

  ```
  L_CFM = E[||x₁ - x₀ - v_θ(x_t, t, C)||²]
  ```

- 相比扩散模型，CFM 学习**确定性向量场**，推理时仅需少量数值积分步即可生成动作，显著提升速度。

### 2.3 动态半径调度（DRS）——区域感知核心创新

- **核心思想**：利用流匹配生成过程中噪声扰动位置逐渐收敛到真实目标位置这一特性，动态调整感知区域的大小。
- **机制**：生成过程中，以噪声扰动位置 pᵢ 为中心，感知半径 rᵢ 随时间步 i 单调递减：

  ```
  r_min ≤ r_i < r_{i-1} < ... < r₀
  ```

  实现从全局场景理解 → 局部几何细节的渐进式聚焦。
- **优势**：不同于传统全局最远点采样（FPS），DRS 在任务相关区域以更高分辨率采样，兼顾全局语义与局部几何精度，并允许柔性调整几何粒度。
- **灵活性**：半径控制策略可为线性、余弦退火等不同形式，适配不同任务需求。

### 2.4 多模态 Token 序列化与 Mamba 融合

- **点云分支**：DRS 采样后经 Mamba 点云编码器（PointMamba）提取几何特征 F_geo。
- **图像分支**：CLIP 图像编码器 + FPN 提取多视角 RGB 语义特征 F_rgb。
- **语言分支**：CLIP 文本编码器提取指令特征 F_text。
- **位姿分支**：噪声扰动位姿投影为 F_open。
- 所有模态 Token 沿序列维度拼接后输入**多模态 Mamba 模型**完成融合。Mamba 基于选择性状态空间机制，具备 **线性计算复杂度**，相比 Transformer 在融合长序列多模态信息时更高效。

### 2.5 策略学习与推理
- 训练时使用 **Logit-Normal 时间步采样**策略，损失为 CFM 损失与抓取器状态二值交叉熵损失的加权和。
- 推理时从噪声分布采样初始动作，沿学习到的速度场数值积分（通常仅需 2-4 步）：

  ```
  x_{t+Δt} = x_t + v_θ(x_t, t, C)·Δt
  ```


## 三、实验设计

### 3.1 仿真数据集与 Benchmark
- **RLBench**：基于 CoppelaSim 的大规模机器人操作仿真基准，7-DoF Franka Panda 机器人。
- **多任务设定**：10 个任务 × 20 条演示 × 至少 2 个变体，共 166 个变体，采用 4 个 RGB-D 摄像头（前、左肩、右肩、手腕），图像分辨率 128×128。
- **高精度任务设定**：从 RLBench 任务套件中挑选 7 个高精度任务（插USB、拧螺丝、插充电器等），每个任务 100 条演示。

### 3.2 对比方法
- PerAct（体素化 + Perceiver Transformer）
- GNFactor（通用神经特征场）
- ManiGaussian（动态高斯泼溅）
- Act3D（自适应 3D 分辨率采样）
- 3D Diffuser Actor（3D 扩散策略）
- RVT-2（多阶段虚拟视角渲染，SOTA 方法）

### 3.3 真实机器人实验
- 6-DoF UR5 机械臂 + Robotiq 2F-140 二指夹爪 + Azure Kinect RGB-D 相机。
- 6 个语言条件任务、14 个变体、56 条演示轨迹，每个任务评估 10 次。


## 四、资源与算力

- **GPU**：8 × NVIDIA RTX 3090。
- **优化器**：AdamW，学习率 1e⁻⁴。
- **训练步数**：300K 步，batch size 为 320。
- **EMA**：对权重使用指数移动平均。
- **公平性**：为保证对比公平，论文作者复现了 RVT-2 和 3D Diffuser Actor，并使用相同 GPU 类型和数量进行训练。
- **注意**：论文未明确报告训练时长（小时级），仅报告了训练步数与 GPU 配置。


## 五、实验数量与充分性分析

### 5.1 实验组数
论文共包含 5 大组别实验：
1. **多任务对比**（Tab.1）：10 任务 × 25 episodes/任务 × 3 随机种子。
2. **高精度任务对比**（Tab.2）：7 高精度任务 × 3 随机种子。
3. **架构与模块消融**（Tab.3）：Mamba vs. Transformer × DRS 开关 × 点云编码器开关 × CFM vs. DDIM，共 10 种配置。
4. **推理步数分析**（Tab.4）：2/4/8/16/32 步下 CFM vs. DDIM 的性能与推理时间对比。
5. **可视化对比分析**（Fig.4）：DDPM（100步）、DDIM（4步）、CFM（2步）、CFM（4步）在 7 个高精度任务上的表现。

### 5.2 充分性评估
**充分之处：**
- 对比了当前最先进的多种方法，覆盖确定性策略、扩散策略、多阶段策略。
- 消融实验系统性地验证了 DRS、点云编码器、Mamba 架构和 CFM 目标的各自贡献。
- 同时包含仿真与真实实验，增强说服力。

**潜在不足：**
- 真实机器人实验规模相对较小（6 个任务，每任务 10 次评估），统计显著性有限。
- 未报告真实实验的标准差或多重种子重复，结果可能受随机因素影响。
- 未提供实验失败案例分析。


## 六、主要结论与发现

1. **总体性能**：FlowRAM 在 RLBench 10 个多任务上达到 82.3% 平均成功率，超越此前 SOTA 方法 3D Diffuser Actor（78.4%）和 RVT-2（76.2%）。
2. **高精度任务**：在 7 个高精度任务上平均成功率 52.0%，较此前最佳方法提升 **12.0%**，所有任务均取得最佳或持平结果。
3. **推理速度**：CFM 仅需 **2-4 步**即可生成可行动作，而 DDIM 需要 8 步以上、DDPM 需要 100 步。2 步时 CFM 仍保持 29.6% 成功率，DDIM 几乎失败。
4. **消融发现**：
   - DRS 是关键组件：移除后性能下降且推理时间增加。
   - Mamba 与 Transformer 性能相当，但 Mamba 推理更快。
   - 即使不使用点云编码，仅依靠 DRS 语义采样也能获得良好性能，说明任务相关区域感知的重要性。
5. **真实部署**：在 6 个真实任务上总体成功率 49/60（约 81.7%），验证了框架的物理可行性。


## 七、方法优点

1. **创新性**：首次将动态半径调度与流匹配生成过程有机结合，利用流匹配的中间状态（噪声扰动位姿）自适应驱动感知聚焦，设计巧妙。
2. **效率显著**：CFM + Mamba 的组合实现线性复杂度多模态融合 + 极少推理步数，兼顾精度与速度，突破了扩散策略的推理瓶颈。
3. **感知精度高**：动态感知区域的设计很好地平衡了全局语义理解与局部几何细节捕捉，对高精度任务效果显著（如在插入USB任务中优于多阶段方法 RVT-2）。
4. **架构选择合理**：Mamba 序列模型在长序列多模态融合中表现出与 Transformer 相当性能的同时推理更快，验证了 SSM 在机器人操作策略中的可行性。
5. **实验设计较严谨**：在仿真中进行了多组消融和推理步数分析，且对基线方法进行了复现以确保对比公平。


## 八、不足与局限

1. **真实实验规模有限**：仅 6 个任务、每任务 10 次评估，且未报告标准差，统计可靠性不足。
2. **高精度任务绝对性能仍有提升空间**：高精度任务平均成功率仅 52.0%，插入笔帽等任务仅 17.3%，复杂高精度场景仍是显著挑战。
3. **依赖关键帧范式**：方法基于关键帧（keyframe）动作生成，关键帧提取质量直接影响性能，且可能损失细粒度轨迹信息。
4. **动态半径调度的理论依据较浅**：半径变化规律（线性/余弦）的选择缺乏系统性的理论分析或消融，最优调度形式未充分探索。
5. **泛化性验证不足**：仅在 RLBench 单一模拟基准上验证，未在更多样化的模拟环境（如 Robosuite、MetaWorld）中测试，跨基准泛化能力未知。
6. **计算成本未充分披露**：虽报告了 GPU 配置和训练步数，但未给出完整的训练时间，难以评估训练效率的实际改进。


（完）
