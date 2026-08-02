---
title: "Generative Rendering: Controllable 4D-Guided Video Generation with 2D Diffusion Models"
title_zh: 生成式渲染：基于二维扩散模型的可控四维引导视频生成
authors: "Cai, Shengqu, Ceylan, Duygu, Gadelha, Matheus, Huang, Chun-Hao Paul, Wang, Tuanfeng Yang, Wetzstein, Gordon"
date: 2024-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2024/papers/Cai_Generative_Rendering_Controllable_4D-Guided_Video_Generation_with_2D_Diffusion_Models_CVPR_2024_paper.pdf"
tags: ["query:dmg"]
score: 7.0
evidence: 利用二维扩散模型进行可控四维引导视频生成
tldr: 视频扩散模型虽能生成逼真视频，但难以精确控制。该方法将动态三维网格与二维扩散模型结合，通过注入低保真渲染网格的几何与运动信息，实现对视频内容的可控生成。实验表明该方法能同时保留三维可控性与扩散模型的表达能力，为视频生成提供了一种新的控制范式。
source: CVPR-2024-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cai-generative-rendering-controllable-4d-guided-video-generation-with-2d-diffusion-models-cvpr-2024-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1800, \"height\": 412, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cai-generative-rendering-controllable-4d-guided-video-generation-with-2d-diffusion-models-cvpr-2024-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1783, \"height\": 688, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cai-generative-rendering-controllable-4d-guided-video-generation-with-2d-diffusion-models-cvpr-2024-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1788, \"height\": 1104, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cai-generative-rendering-controllable-4d-guided-video-generation-with-2d-diffusion-models-cvpr-2024-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1788, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cai-generative-rendering-controllable-4d-guided-video-generation-with-2d-diffusion-models-cvpr-2024-paper/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1792, \"height\": 1771, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2024-accepted/cvpr-2024-cai-generative-rendering-controllable-4d-guided-video-generation-with-2d-diffusion-models-cvpr-2024-paper/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1784, \"height\": 440, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2024-accepted/cvpr-2024-cai-generative-rendering-controllable-4d-guided-video-generation-with-2d-diffusion-models-cvpr-2024-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 886, \"height\": 323, \"label\": \"Table\"}]"
motivation: 视频扩散模型难以精确控制生成内容，传统三维工具又缺乏自动化。
method: 以动态三维网格为条件，将低保真渲染结果注入二维扩散模型的生成过程。
result: 实现了具有三维可控性的高质量视频生成，支持后续编辑。
conclusion: 结合三维网格和扩散模型可有效提升视频生成的可用性与可控性。
---

## Abstract
Traditional 3D content creation tools empower users to bring their imagination to life by giving them direct control over a scene's geometry appearance motion and camera path. Creating computer-generated videos however is a tedious manual process which can be automated by emerging text-to-video diffusion models. Despite great promise video diffusion models are difficult to control hindering users to apply their creativity rather than amplifying it. To address this challenge we present a novel approach that combines the controllability of dynamic 3D meshes with the expressivity and editability of emerging diffusion models. For this purpose our approach takes an animated low-fidelity rendered mesh as input and injects the ground truth correspondence information obtained from the dynamic mesh into various stages of a pre-trained text-to-image generation model to output high-quality and temporally consistent frames. We demonstrate our approach on various examples where motion can be obtained by animating rigged assets or changing the camera path.

---

## 论文详细总结（自动生成）

# 论文总结

## 1. 核心问题与整体含义

- **研究动机**：传统 3D 内容创作工具能够对场景几何、外观、运动与相机路径进行精确控制，但流程繁琐、耗时且高度依赖专业技能。新兴的文本到视频（T2V）扩散模型可以自动生成视频，但用户难以对生成内容的布局、运动进行精细且时序一致的控制。现有方法如 ControlNet 只能对单帧提供结构控制，视频结果易闪烁；视频到视频编辑方法则依赖高质量输入视频，而这类视频往往不易获得。
- **核心问题**：如何将 3D 工作流的可控性与 2D 扩散模型的表达能力和可编辑性结合，实现“由用户定义的粗糙动态 3D 场景”直接生成“高质量、风格可控、时序一致的视频动画”。
- **整体含义**：论文提出 **Generative Rendering** 框架，将带运动信息的低保真 3D 网格作为输入，利用动态网格提供的**真实 4D 时空对应关系**，引导预训练的文本到图像（T2I）扩散模型进行多帧一致生成，从而在保留用户对 3D 场景控制能力的同时，利用扩散模型“渲染”出最终风格化动画。

## 2. 方法论

### 核心思想

- 将预训练 T2I 扩散模型（StableDiffusion + 深度条件 ControlNet）当作一个**多帧渲染器**。
- 输入来自动态 3D 场景的深度图序列 `D` 和 UV 坐标图序列 `UV`，其中 UV 图提供逐像素的跨帧对应关系。
- 通过对扩散模型自注意力模块的**输入特征（pre-attention）**和**输出特征（post-attention）**进行对应感知的注入与融合，并结合 **UV 空间的噪声初始化**，实现时序一致的高质量生成。

### 关键技术细节

1. **Pre-attention 特征注入（Keyframe 扩展注意力）**
   - 传统 self-attention 中，Q/K/V 均由当前帧特征投影得到。
   - 论文为减少计算量，不对所有帧做扩展注意力，而是每步随机选取 `m` 个关键帧（keyframes），对这些关键帧进行联合扩展注意力，并将关键帧的 pre-attention 特征与当前帧特征拼接，组成新的 K、V：
     - `K(i,l) = WK [ f(i,l), f_KF(l) ]`
     - `V(i,l) = WV [ f(i,l), f_KF(l) ]`
   - 这样所有帧都能参考关键帧的全局结构信息，提升一致性。

2. **Post-attention 特征注入（UV 空间特征融合）**
   - 利用 UV 图将多个帧的 post-attention 特征投影到规范的 UV 空间，进行混合（blending）。
   - 为避免直接平均导致模糊，采用“顺序填充 + 平均”的组合策略：每个 texel 优先使用未填充帧的特征，最后对填充结果与平均结果取均值，得到统一 UV 特征图 `T^l`。
   - 将该统一特征投影回当前帧，与当前帧注意力输出加权融合：
     - `F_out = α · F_bar + (1 − α) · F_hat`

3. **UV 空间噪声初始化**
   - 已有视频编辑方法依赖 DDIM inversion 得到一致噪声，但本任务输入是无纹理的 3D 渲染，inversion 不可行；固定噪声又会导致纹理粘连。
   - 论文改为在 UV 空间采样高斯噪声纹理，再通过帧与 UV 的对应关系投影到每一帧，从而获得具有时序相关性的初始噪声。

4. **潜在空间归一化（Latent Normalization）**
   - 为缓解颜色闪烁，对预测的 latent 做 AdaIN 操作，使其整体分布接近第一帧。
   - 为避免运动影响全局统计，仅基于背景像素计算分布（背景在 3D 设置中易于分割）。

### 算法流程（简略）

1. 在 UV 空间采样噪声，并投影到各帧得到初始 latent。
2. 对每个扩散步：
   - 随机采样一组关键帧；
   - 对关键帧执行扩展注意力，提取 pre/post 特征；
   - 将 post-attention 特征投影到 UV 空间并融合得到统一特征图；
   - 对所有帧依次执行扩散步：用关键帧 pre-attention 特征扩展自注意力，并用投影回的 UV 融合特征对输出做加权混合。
3. 输出最终生成帧。

## 3. 实验设计

### 数据集 / 场景类型

论文构建了多种动画序列进行评估：

- **相机旋转**：单个静态物体，绕物体 360° 旋转的相机路径。
- **物理模拟**：例如弹跳球的刚体碰撞动画。
- **角色动画**：从 Mixamo 获取的绑定角色，渲染多种舞蹈动作。

### 对比方法

由于没有完全同任务的已发表工作，作者将两种现有方法适配到本任务作为基线：

- **Pix2Video\***：使用其 pre-attention 特征传播机制（每帧关注锚点帧和上一帧），并加上深度条件控制。
- **TokenFlow\***：使用其扩展注意力和 token 传播机制，但将原本基于 DDIM inversion 的最近邻匹配替换为论文提供的 3D 真实对应关系。
- **Per-Frame**：逐帧独立生成（作为下界参考）。
- **Gen1**：一个专有的文本到视频（T2V）扩散模型，作为参考上限。

注意：由于本任务没有真实输入视频，Pix2Video 和 TokenFlow 均无法使用 inversion 初始化，统一改用固定噪声。

### 评估指标

- **帧一致性（Frame Consistency）**：计算输出视频相邻帧 CLIP 图像嵌入的平均余弦相似度。
- **提示保真度（Prompt Fidelity）**：计算每帧 CLIP 嵌入与输入文本提示的平均相似度。

## 4. 资源与算力

- 论文中**没有明确说明**使用的 GPU 型号、数量、训练时间或推理时间等具体算力资源。
- 仅提及使用 StableDiffusion v1.5、深度条件 ControlNet，输出 512×512 分辨率，Karras scheduler，50 步去噪，但未报告运行成本。
- 模型本身是 **zero-shot** 的，没有对预训练扩散模型进行微调，因此推理资源主要来自预训练模型的单帧生成和帧间特征处理。

## 5. 实验数量与充分性

### 实验数量

- **定性实验**：多个不同场景、不同风格、不同提示的生成结果（如“照片写实篮球弹跳”“水晶蓝狐狸奔跑”“小丑跳舞”“暴风兵游泳”等），涵盖相机旋转、物理模拟、角色动画。
- **定量实验**：一张主表，比较了 Per-Frame、Pix2Video\*、TokenFlow\*、Gen1 和 Ours 的帧一致性与提示保真度。
- **消融实验**：针对三个关键组件进行了逐一消融：
  1. 仅 pre-attention 注入（去掉 post-attention）
  2. 仅 post-attention 注入（去掉 pre-attention）
  3. 固定噪声替代 UV 噪声初始化

### 充分性与客观性评估

- **优点**：消融实验覆盖了方法的主要创新点，定性、定量结合，且对基线做了公平适配（对 TokenFlow 提供真实对应关系）。
- **不足**：
  - 定量指标仅使用 CLIP 相似度，较为单一，缺乏人工评估（user study）或更丰富的指标（如 LPIPS 时序一致性、FVD 等）。
  - 测试场景数量和多样性有限，没有大规模标准数据集或跨领域测试。
  - 与 Gen1 等 T2V 模型的比较不公平（Gen1 为专有模型且只能生成短视频），但作者对此有明确说明。
  - 未报告计算资源、运行时间等，难以评估实际可用性。

## 6. 主要结论与发现

- 将动态 3D 网格的真实对应关系注入预训练 T2I 扩散模型，可以有效生成**高质量、时序一致、风格可控**的动画。
- **UV 空间特征融合**结合 pre-attention 与 post-attention 注入，比单独使用其中任何一种都更好：pre-attention 提供全局结构一致性，post-attention 提供像素级局部约束，两者互补。
- **UV 噪声初始化**优于固定噪声和基于 inversion 的方案，能有效提升跨帧一致性。
- 在 T2I 方法中，论文方法取得了最好的帧一致性，同时提示保真度高于具有合理时序一致性的基线方法（Pix2Video\*、TokenFlow\*），接近并优于 Gen1 的保真度（0.3227 vs 0.3029）。
- 方法还具备一定的 zero-shot 泛化能力，同一 3D 网格配合不同提示可生成不同风格动画，并能产生输入网格未建模的交互效果（如阴影、光照变化、地面变形等）。

## 7. 优点

- **创新性强**：提出“生成式渲染”概念，将传统 3D 渲染管线与 2D 扩散模型有机结合，是一种新的控制范式。
- **可控性高**：用户可以通过 3D 网格、动画、相机路径精确控制生成内容，这是纯 T2V 模型难以做到的。
- **无需微调**：直接利用预训练 T2I 模型，零样本（zero-shot）使用，不需要额外训练数据或大规模算力。
- **方法设计合理**：pre/post attention 注入 + UV 空间统一 + UV 噪声初始化，每个环节都有明确动机，且消融实验验证了各自的有效性。
- **可生成任意长度视频**：由于基于 2D T2I 模型并按帧生成，不受 T2V 模型通常只能生成几秒视频的限制。

## 8. 不足与局限

- **依赖 3D 输入**：需要用户提供带 UV 对应关系的动态 3D 网格，这本身仍需要 3D 建模或动画能力，限制了方法的易用性。
- **特征空间错位问题**：几何对应关系不一定在低维特征空间（64×64）中精确匹配，尤其在物体边缘，直接融合可能产生模糊或伪影。
- **无法建模复杂的物体间交互**：虽然方法能隐式生成阴影、光照等部分效果，但若两个物体在 UV 空间中不对应，则难以生成正确的相互作用（如遮挡、反射）。
- **实验验证有限**：定量指标单一、没有大规模用户研究、测试场景偏少，方法在复杂真实场景中的鲁棒性尚未充分证明。
- **计算效率**：每步需要处理关键帧的扩展注意力并对所有帧进行特征投影和融合，相比单帧生成有额外开销，论文未给出运行时间数据。
- **颜色归一化仅基于背景**：Latent normalization 依赖背景像素统计，在背景复杂或充满前景物体的场景中可能失效。

（完）
