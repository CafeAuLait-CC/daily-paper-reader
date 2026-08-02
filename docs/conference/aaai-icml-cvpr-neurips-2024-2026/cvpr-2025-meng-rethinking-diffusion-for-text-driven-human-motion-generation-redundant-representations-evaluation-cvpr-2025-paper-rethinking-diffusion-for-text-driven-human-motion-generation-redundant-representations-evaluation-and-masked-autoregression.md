---
title: "Rethinking Diffusion for Text-Driven Human Motion Generation: Redundant Representations, Evaluation, and Masked Autoregression"
title_zh: 重新思考用于文本驱动人体运动生成的扩散模型：冗余表示、评估与掩码自回归
authors: "Meng, Zichong, Xie, Yiming, Peng, Xiaogang, Han, Zeyu, Jiang, Huaizu"
date: 2025-06-01
pdf: "https://openaccess.thecvf.com/content/CVPR2025/papers/Meng_Rethinking_Diffusion_for_Text-Driven_Human_Motion_Generation_Redundant_Representations_Evaluation_CVPR_2025_paper.pdf"
tags: ["query:dmg"]
score: 9.0
evidence: 面向文本驱动人体运动生成的扩散连续生成方法，针对VQ方法的局限性展开研究
tldr: 当前基于向量量化的离散生成方法虽然在标准指标上占优，但存在信息损失和多样性不足。本文重新审视扩散模型的连续空间生成特性，认为其更适合人体运动生成。作者提出掩码自回归改进去噪过程，并完善评估协议。实验表明该方案在生成质量和多样性上具有竞争力，推动了扩散模型在该方向的发展。
source: CVPR-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 588, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 858, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1619, \"height\": 445, \"label\": \"Figure\"}, {\"url\": \"assets/figures/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1510, \"height\": 336, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 706, \"height\": 203, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 705, \"height\": 263, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 707, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1622, \"height\": 683, \"label\": \"Table\"}, {\"url\": \"assets/tables/cvpr-2025-accepted/cvpr-2025-meng-rethinking-diffusion-for-text-driven-human-motion-generation-redundant-representations-evaluation-cvpr-2025-paper/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 837, \"height\": 240, \"label\": \"Table\"}]"
motivation: VQ类离散方法存在信息损失和多样性受限，扩散连续生成具备更强潜力。
method: 提出掩码自回归扩散改进和新的评估协议，重估扩散方法在文本驱动人体运动生成中的表现。
result: 实验表明该方案在生成质量与多样性上具有竞争力，挑战了VQ方法的绝对优势。
conclusion: 扩散模型仍可凭借连续生成特性成为人体运动生成的有力方案，为后续研究提供新基线。
---

## Abstract
Since 2023, Vector Quantization (VQ)-based discrete generation methods have rapidly dominated human motion generation, primarily surpassing diffusion-based continuous generation methods in standard performance metrics. However, VQ-based methods have inherent limitations. Representing continuous motion data as limited discrete tokens leads to inevitable information loss, reduces the diversity of generated motions, and restricts their ability to function effectively as motion priors or generation guidance. In contrast, the continuous space generation nature of diffusion-based methods makes them well-suited to address these limitations and with even potential for model scalability. In this work, we systematically investigate why current VQ-based methods perform well and explore the limitations of existing diffusion-based methods from the perspective of motion data representation and distribution. Drawing on these insights, we preserve the inherent strengths of a diffusion-based human motion generation model and gradually optimize it with inspiration from VQ-based approaches. Our approach introduces a human motion diffusion model enabled to perform masked autoregression, optimized with a reformed data representation and distribution. Additionally, we propose a more robust evaluation method to assess different approaches. Extensive experiments on various datasets demonstrate our method outperforms previous methods and achieves state-of-the-art performances.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
面向文本驱动人体运动生成的扩散连续生成方法，针对VQ方法的局限性展开研究。

### 2. 核心内容
当前基于向量量化的离散生成方法虽然在标准指标上占优，但存在信息损失和多样性不足。本文重新审视扩散模型的连续空间生成特性，认为其更适合人体运动生成。作者提出掩码自回归改进去噪过程，并完善评估协议。实验表明该方案在生成质量和多样性上具有竞争力，推动了扩散模型在该方向的发展。

### 3. 对应检索需求
Generative modeling of 3D human motions using flow matching or diffusion。

### 4. 来源与原文
- Source：CVPR-2025-Accepted
- OpenReview：[https://openaccess.thecvf.com/content/CVPR2025/html/Meng_Rethinking_Diffusion_for_Text-Driven_Human_Motion_Generation_Redundant_Representations_Evaluation_CVPR_2025_paper.html](https://openaccess.thecvf.com/content/CVPR2025/html/Meng_Rethinking_Diffusion_for_Text-Driven_Human_Motion_Generation_Redundant_Representations_Evaluation_CVPR_2025_paper.html)
