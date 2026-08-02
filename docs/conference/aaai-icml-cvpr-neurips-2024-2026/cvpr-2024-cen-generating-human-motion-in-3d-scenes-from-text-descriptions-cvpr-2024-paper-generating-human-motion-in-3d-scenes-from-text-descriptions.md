---
title: Generating Human Motion in 3D Scenes from Text Descriptions
title_zh: 从文本描述生成三维场景中的人体运动
authors: "Cen, Zhi, Pi, Huaijin, Peng, Sida, Shen, Zehong, Yang, Minghui, Zhu, Shuai, Bao, Hujun, Zhou, Xiaowei"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Cen_Generating_Human_Motion_in_3D_Scenes_from_Text_Descriptions_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 6.0
evidence: 从文本生成三维场景中的人体运动，分解为语言定位与物体中心生成
tldr: 从文本生成三维场景中的人体运动任务涉及多模态和空间推理。作者将问题分解为两个子问题：目标物体的语言定位和以物体为中心的运动生成。语言定位确定交互对象，物体中心生成则结合场景几何和文本条件合成运动。该解耦方法降低复杂度，并提升交互的视觉与物理真实性。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1785, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1612, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 444, \"height\": 227, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 698, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 740, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1790, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 786, \"height\": 636, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1531, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-cen-generating-human-motion-in-3d-scenes-from-text-descriptions-cvpr-2024-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 863, \"height\": 423, \"label\": \"Table\"}]"
motivation: 现有工作较少同时考虑文本条件与人体-场景交互，影响生成真实感。
method: 分解为语言定位和物体中心的运动生成两个子问题。
result: 有效提升了三维场景中文本驱动人体运动的真实性和物理合理性。
conclusion: 为文本驱动的场景人体运动生成提供了一种可分解的解决思路。
---

## Abstract
Generating human motions from textual descriptions has gained growing research interest due to its wide range of applications. However only a few works consider human-scene interactions together with text conditions which is crucial for visual and physical realism. This paper focuses on the task of generating human motions in 3D indoor scenes given text descriptions of the human-scene interactions. This task presents challenges due to the multimodality nature of text scene and motion as well as the need for spatial reasoning. To address these challenges we propose a new approach that decomposes the complex problem into two more manageable sub-problems: (1) language grounding of the target object and (2) object-centric motion generation. For language grounding of the target object we leverage the power of large language models. For motion generation we design an object-centric scene representation for the generative model to focus on the target object thereby reducing the scene complexity and facilitating the modeling of the relationship between human motions and the object. Experiments demonstrate the better motion quality of our approach compared to baselines and validate our design choices. Code will be available at https://zju3dv.github.io/text_scene_motion.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **研究动机**：文本驱动的人体运动生成已有较多研究，但大多数方法仅关注人体自身动作，忽略了人体与三维场景的交互。然而在真实室内环境中，动作往往与场景中的物体密切相关（如“坐在沙发旁的桌子上”），场景上下文和物理约束对生成动作的真实感至关重要。
- **核心问题**：给定一个三维室内场景点云和一段描述人-场景交互的文本，生成与文本和场景都一致的自然人体运动。该任务面临三大挑战：
  - 多模态性（文本、场景、运动三种模态的融合）；
  - 空间推理能力（需要将文本中的空间关系映射到场景中的具体物体）；
  - 场景的复杂性和噪声（全场景点云中大量无关点干扰生成）。
- **整体含义**：该论文是首个（在CVPR 2024）系统地解决“文本+3D场景+人体运动”三者联合生成问题的方法，通过将复杂问题分解为两个子问题，有效提升了生成动作的物理真实性和语义一致性，是该方向的重要探索。

## 2. 论文提出的方法论

论文提出**两阶段解耦式生成框架**（Two-stage pipeline）：

### 阶段一：目标物体的语言定位（Language Grounding）

- **核心思想**：不直接学习文本到物体的映射，而是借助大语言模型（LLM）以“问答”方式完成视觉定位。
- **技术流程**：
  1. **构建空间场景图（Spatial Scene Graph）**：使用预训练3D检测模型（Group-Free 3D检测器）获取物体包围盒，根据包围盒推断物体间的空间关系（水平邻近、垂直邻近、支撑、中间等），生成场景图的文本描述。
  2. **两轮ChatGPT提示（Two-stage Prompting）**：
     - 第一轮：让ChatGPT根据输入文本判断目标物体类别和锚定物体类别，从而缩小场景图范围。
     - 第二轮：将简化后的场景图关系（如“chair 0 is near the end table”）提供给ChatGPT，要求其推断出具体目标物体实例。
- **目的**：避免直接输入全场景图导致LLM“困惑”，提升定位准确率。

### 阶段二：以目标物体为中心的运动生成（Object-centric Motion Generation）

- **核心思想**：将全场景点云转换为围绕目标物体的体积化传感器（Volumetric Sensors），使生成模型聚焦于目标物体及其周边环境，降低场景复杂度。
- **场景表示**：
  - **环境传感器（Environment Sensor）**：以目标物体中心为中心，4×4×4 m³立方体，8×8×8体素，记录占据率、中心位置和法线方向，提供目标物体周围粗略几何。
  - **目标传感器（Target Sensor）**：裁剪目标物体包围盒内的点云，构造8×8×8体素，提供目标物体的精细几何。
  - **轨迹传感器（Trajectory Sensor）**：在每帧人物根位置处构建的以自我为中心的传感器，用于推理人体与场景的动态交互。
- **生成模型**：
  - **轨迹生成（Diffusion-based Trajectory Generation）**：使用条件扩散模型（Transformer解码器），条件为 `Ct = {文本特征L, 环境传感器E, 目标传感器T}`，生成整个人体轨迹（平移和朝向）。
  - **运动补全（Diffusion-based Motion Completion）**：第二个扩散模型沿着生成轨迹合成局部关节姿态，条件为 `Cm = {L, E, T, O1...ON}`（O为每帧轨迹传感器）。
- **训练细节**：
  - 扩散模型采用简单的目标函数（公式2）：`L = E[‖x0 - G(xt, t, C)‖]`。
  - 先在AMASS数据集上预训练200 epochs，再在HUMANISE数据集上微调200 epochs。
  - 使用Transformer解码器，条件均投影到512维。
  - 文本编码使用CLIP文本编码器。

## 3. 实验设计

### 数据集与Benchmark

- **HUMANISE数据集**：论文主要实验和训练测试基准。该数据集包含3D场景、文本描述和人体运动数据。
  - 训练集：543个场景中的16.5k个运动序列。
  - 测试集：100个场景中的3.1k个运动序列。
- **PROX数据集**：用于泛化测试，不进行任何微调，直接测试方法在未见场景上的表现。

### 对比方法

1. **MDM\***：基于扩散的运动生成器，用点Transformer提供场景特征。
2. **GMD\***：增强控制的MDM变体，同样使用点Transformer场景特征。
3. **GMD_HC**：用HUMANISE预测的物体中心作为引导，加入邻近损失。
4. **HUMANISE**：最相关的先前工作，使用Transformer VAE + 辅助目标中心回归任务。

### 评估指标

- **场景条件质量**：body-to-goal distance（目标距离）+ 人工感知评分（scene score）。
- **动作条件质量**：动作识别准确率（accuracy）、多样性（diversity）、多模态性（multimodality）。
- **纯运动质量**：FID + 人工感知评分（quality score）。

## 4. 资源与算力

- **论文明确提到的算力信息**：训练使用单个Nvidia RTX 3090 GPU，AdamW优化器，学习率0.0001，批量大小128。
- **未明确说明的信息**：训练的具体时长（epoch数有说明：AMASS预训练200 epochs + HUMANISE微调200 epochs，但没有给出总训练时间）；不同对比实验各自消耗的总算力；推理阶段的耗时也没有具体数值。
- **总结**：论文给出了基本硬件配置和训练轮数，但缺少精确的GPU训练小时数等细节，属于“部分明确”。

## 5. 实验数量与充分性

### 实验组数

- **主对比实验**：4个基线方法 + 真实数据，共5组结果（表1），覆盖场景条件、动作条件、纯运动质量共7个指标。
- **主组件消融实验**：5个变体（w/o localization、w/o object-centric、w/o two-stage、w/o diffusion、w/o pretrain），涉及3大类指标（表2）。
- **定位方法设计消融**：2个外部基线 + 5个自身变体（w/o two-stage、w/o few-shot、text matching、LLaMA 2、Mistral 7B），在两种检测设置（预测检测、GT检测）下对比（表3）。
- **泛化实验**：在PROX数据集上的定性结果（图6），无定量指标。

### 充分性评价

- **优点**：实验覆盖较全面，从主性能、消融、定位模块设计到泛化均有涉及；感知研究（人工评分）增强了结论的可信度；定位模块的详细消融验证了LLM选择的合理性。
- **不足**：
  - PROX泛化仅提供定性结果，缺乏定量评估。
  - 传感器密度相关实验被放在补充材料，正文中没有给出详细数据。
  - 部分指标（如多样性、多模态性）与真实数据差异较大，论文解释不够深入。
  - 人工评分实验的具体设置（评分标准、评分者一致性等）未详细说明。
- **公平性**：对比方法均使用同样的HUMANISE设置，且为基线提供了场景特征的公平输入，总体公平性较好。但GMD_HC中使用了HUMANISE预测的物体中心，可能会带来不公平优势，不过论文没有过度依赖这一优势，因为其还是不如本文方法。

## 6. 论文的主要结论与发现

1. **两阶段分解是有效的**：先定位目标物体再生成运动，显著优于直接端到端生成。
2. **LLM用于3D视觉定位效果良好**：ChatGPT（以及可替换的开源Mistral 7B）在文本-场景关系推理上明显优于纯CLIP文本匹配方法和专门的3D视觉接地模型，说明LLM的常识推理能力可以弥补传统方法在空间理解上的不足。
3. **以物体为中心的表示优于全场景表示**：使用目标传感器+环境传感器代替全场景点云，大幅降低了场景复杂度，提高了运动质量（FID从3.14降到0.12）。
4. **扩散模型优于cVAE**：在本任务中，扩散模型比cVAE生成的运动更真实（FID 0.12 vs 3.61）。
5. **预训练很重要**：在AMASS上的预训练显著提升了生成质量（FID从2.50降到0.12）。
6. **方法具有泛化能力**：无需微调即可在PROX场景中合理生成动作。

## 7. 优点

- **问题分解合理**：将“文本+场景+运动”这一复杂问题拆解为“定位”和“生成”两个相对独立的子问题，降低了整体难度，且每个子问题都能复用现有成熟技术（LLM、扩散模型）。
- **创新的定位方法**：利用LLM做3D视觉接地，不是训练一个专用网络，而是通过场景图文本化和提问式推理，无需额外训练数据，且容易更换LLM。
- **以物体为中心的表示设计巧妙**：
  - 使用三种体积化传感器（目标、环境、轨迹），既提供了目标物体的精细几何，又保留了场景上下文，还考虑了人体移动过程中的动态环境。
  - 相比原始点云，该表示对尺度更鲁棒，且与扩散模型兼容性好。
- **两阶段生成（轨迹+姿态）**：先全局后局部，符合人体运动的空间逻辑，提升运动连贯性。
- **实验设计较全面**：主对比、消融、定位模块消融、泛化测试都有，且包含人工评估和多种指标。
- **对LLM的局限有讨论**：指出了LLM可能因检测缺失失效、行为受提示影响，并实验验证了开源Mistral 7B可以替代ChatGPT，提高了可复现性。

## 8. 不足与局限

- **数据集限制**：
  - HUMANISE数据集由模板生成，文本描述较简单（多为固定句式），缺少自然语言多样性。
  - 运动序列较短（60%约1-3秒），不能很好体现长时动作和复杂交互。
  - 动作类别有限（仅walk, sit, stand up, lie）。
- **场景限制**：
  - 仅处理静态场景，无法处理动态物体（如移动的椅子、其他人）。
  - 场景图依赖3D检测器的质量，若检测器漏检物体，LLM定位可能失败。
- **方法局限**：
  - 使用LLM进行推理比传统解析方法更慢成本更高，且行为可能受提示语影响，稳定性不足。
  - 虽然验证了Mistral可替代ChatGPT，但整体框架仍依赖LLM的推理能力，存在不可控风险。
- **实验不足**：
  - PROX泛化仅定性；传感器密度实验放在补充材料；缺少对失败案例的深入分析。
  - 对多模态性指标的解释不够充分（生成多样性虽接近真实，但没有说明其分布特点）。
- **伦理与安全**：未讨论生成动作可能被用于不当用途的风险。

（完）
