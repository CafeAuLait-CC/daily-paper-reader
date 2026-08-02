---
title: "RealisMotion: Decomposed Human Motion Control and Video Generation in the World Space"
title_zh: RealisMotion：世界空间中解耦的人类运动控制与视频生成
authors: "Jingyun Liang, Jingkai Zhou, Shikai Li, Chenjie Cao, Lei Sun, Yichen Qian, Weihua Chen, Fan Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/4390e29da1bd04e2a2c6241f44e910191ae4ab94.pdf"
tags: ["query:dmg"]
score: 8.0
evidence: 在三维世界空间中生成可控运动的人类视频
tldr: 针对现有方法无法独立控制前景、背景、轨迹和动作等关键视频元素的问题，本文提出 RealisMotion，在三维世界坐标系中显式解耦运动与外观、主体与背景、动作与轨迹，支持灵活组合。通过将 2D 轨迹反投影到 3D 空间实现轨迹控制，并执行三维空间中的运动编辑，最终生成可控且逼真的人类视频。方法在不同交互场景下展示了良好的可控性和生成质量。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有方法无法对人类视频中的前景、背景、轨迹和动作进行独立控制，限制了对生成结果的灵活编辑。
method: 建立地面感知的 3D 世界坐标系，显式解耦运动与外观、主体与背景、动作与轨迹，并将 2D 轨迹反投影到 3D 空间实现控制。
result: 实现了可组合的人类运动控制和高质量视频生成，验证了分解式控制在真实场景中的有效性。
conclusion: 该框架为灵活可控的人类视频生成提供了解耦式解决方案，具有广泛的应用前景。
---

## Abstract
Generating human videos with realistic and controllable motions is a challenging task. While existing methods can generate visually compelling videos, they lack separate control over four key video elements: foreground subject, background video, human trajectory, and action patterns. In this paper, we propose a decomposed human motion control and video generation framework that explicitly decouples motion from appearance, subject from background, and action from trajectory, enabling flexible mix-and-match composition of these elements. Concretely, we first build a ground-aware 3D world coordinate system and perform motion editing directly in the 3D space. Trajectory control is implemented by unprojecting edited 2D trajectories into 3D with focal-length calibration and coordinate transformation, followed by speed alignment and orientation adjustment; actions are supplied by a motion bank or generated via text-to-motion methods. Then, based on modern text-to-video diffusion transformer models, we inject the subject as tokens for full attention, concatenate the background along the channel dimension, and add motion (trajectory and action) control signals by addition. Such a design opens up the possibility for us to generate realistic videos of anyone doing anything anywhere. Extensive experiments on benchmark datasets and real-world cases demonstrate that our method achieves state-of-the-art performance on both element-wise controllability and overall video quality.

---

## 论文详细总结（自动生成）

# 论文总结：RealisMotion

## 1. 核心问题与整体含义
- **研究背景**：生成具有真实且可控运动的人类视频是一项挑战性任务。现有方法虽然能生成视觉上吸引人的视频，但无法对视频中的四个关键元素进行**独立控制**：前景主体、背景视频、人类轨迹和动作模式。
- **研究动机**：需要一种能分别控制这些元素并支持灵活组合的方法，从而实现更加精细和自由的视频编辑与生成。
- **整体含义**：本文提出一种解耦式的人类运动控制与视频生成框架，显式分离“运动”与“外观”、“主体”与“背景”、“动作”与“轨迹”，使得用户可以独立控制每个元素，并任意组合，最终实现“任何人做任何事在任何地方”的视频生成。

## 2. 方法论
- **核心思想**：在三维世界坐标系中建立地面感知（ground-aware）的 3D 空间，直接在该空间内进行运动编辑，从而将 2D 视频生成问题提升到 3D 世界空间，实现更符合物理规律的控制。
- **关键技术细节**：
  - **轨迹控制**：将编辑后的 2D 轨迹反投影到 3D 空间，过程包括焦距校准（focal-length calibration）和坐标变换（coordinate transformation），随后进行速度对齐（speed alignment）和方向调整（orientation adjustment）。
  - **动作控制**：动作可以由预定义的动作库提供，也可以通过文本到动作（text-to-motion）方法生成，增加了动作来源的灵活性。
  - **视频生成**：基于现代文本到视频扩散 Transformer 模型，具体注入方式为：
    - 将主体（subject）作为 token 注入，参与全注意力机制；
    - 将背景沿通道维度拼接（concatenation）；
    - 将运动信号（包括轨迹和动作）通过加法方式注入。
- **整体流程**：建立 3D 坐标系 → 在 3D 空间编辑运动 → 轨迹反投影与调整 → 动作生成/选择 → 将主体、背景、运动信号注入扩散 Transformer → 生成视频。文中未给出具体公式。

## 3. 实验设计
- **数据集 / 场景**：摘要中提及了“基准数据集”和“真实世界案例”，但**未给出具体数据集名称**。
- **Benchmark**：未明确说明采用了什么样的评估基准。
- **对比方法**：摘要仅称“现有方法”，但**未列出任何具体对比方法**的名称。
- **评估指标**：未说明使用了哪些定量或定性指标。

## 4. 资源与算力
- 提供的文本中**完全没有提及** GPU 型号、数量、训练时长、参数量等任何算力信息，因此无法总结。

## 5. 实验数量与充分性
- 文中仅笼统地表述为“大量实验”（Extensive experiments），但**没有提供实验组数、消融研究、对比实验的详细列表**。
- 由于信息不足，无法客观判断实验的充分性和公平性；需要查阅完整论文以评估实验设计的严谨程度。

## 6. 主要结论与发现
- 所提出的方法在**元素级可控性**（对主体、背景、轨迹、动作的独立控制）和**整体视频质量**上均达到了当前最优性能（state-of-the-art）。
- 验证了分解式控制方法在真实场景中的有效性，表明将运动与外观、主体与背景、动作与轨迹解耦是可行且高效的。

## 7. 优点
- **解耦设计**：首次明确提出将四个关键视频元素完全解耦，并支持“mix-and-match”的灵活组合，极大提升了可控性。
- **3D 世界空间控制**：将轨迹控制从 2D 提升到 3D，通过焦距校准和坐标变换实现更符合几何规律的轨迹编辑，理论上能适应不同相机参数。
- **动作来源多样**：动作既可由动作库提供，也可由文本生成，增加了使用的灵活性。
- **架构兼容性**：基于现代文本到视频扩散 Transformer 模型，通过 token 注入、通道拼接和加法注入三种轻量级方式融合控制信号，无需修改模型主干，具有较好的可扩展性。

## 8. 不足与局限
- **实验细节缺失**：提供的文本中未给出具体数据集、对比方法、评估指标和消融实验，无法判断实验的全面性和公平性。
- **轨迹控制敏感性**：反投影过程依赖焦距校准，可能对相机参数估计误差较为敏感，在无标定真实场景中可能影响精度。
- **动作覆盖限制**：动作库的规模和质量以及文本到动作模型的生成能力会直接影响生成动作的多样性，可能无法覆盖所有真实人类动作。
- **依赖扩散模型性能**：整体视频质量高度依赖于底层文本到视频扩散模型，若基础模型对主体和背景的融合不佳，可能影响最终合成效果。
- **未讨论失败案例**：文中没有提及方法可能失效的场景（如遮挡、多人物交互、复杂几何变形的世界空间等）。

（完）
