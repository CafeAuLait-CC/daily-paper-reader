<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-06-12
- 运行时间：2026-06-12 21:58:53 UTC
- 运行状态：成功
- 本次总论文数：17
- 精读区：6
- 速读区：11

### 今日简报（AI）
1) 今日聚焦文本到运动生成，精读《MoGeFlow》与《KV-Control》高分突破，速读涵盖文本到视频生成及扩散模型优化。  
2) 最值得看《MoGeFlow》的运动码本几何流生成与《KV-Control》的参数高效轨迹控制，两者均达8.0/10以上。  
3) 建议优先精读这两篇论文，深入理解运动生成中的离散编码与可控性设计，为后续构建高保真运动模型打基础。
- 详情：[/202606/12/README](/202606/12/README)

### 精读区论文标签
1. [MoGeFlow: Flowing Through Motion Codebook Geometry for Text-to-Motion Generation](/202606/12/2606.11656v1-mogeflow-flowing-through-motion-codebook-geometry-for-text-to-motion-generation)  
   标签：评分：9.0/10、query:3d-motion-generation
   evidence：基于流的文本到动作生成，利用运动码本几何
2. [KV-Control: Parameter-Efficient K/V Injection for Trajectory-Controlled Text-to-Motion](/202606/12/2606.05624v1-kv-control-parameter-efficient-kv-injection-for-trajectory-controlled-text-to-motion)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：提出KV-Control实现轨迹可控的文本到三维人体动作生成
3. [SynthICL: Scalable In-context Imitation Learning with Synthetic Data](/202606/12/2606.08154v1-synthicl-scalable-in-context-imitation-learning-with-synthetic-data)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：使用流匹配变压器策略进行模仿学习
4. [EgoPriMo: Egocentric Motion Generation for Interactive Humanoid Control](/202606/12/2606.08495v1-egoprimo-egocentric-motion-generation-for-interactive-humanoid-control)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：使用扩散Transformer从自我中心视角生成3D人体运动（SMPL）
5. [Latent Diffusion Policy: Shaping Latent Spaces for Diffusion-Based Robotic Manipulation](/202606/12/2606.08657v1-latent-diffusion-policy-shaping-latent-spaces-for-diffusion-based-robotic-manipulation)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：在潜在空间中使用流匹配进行轨迹生成
6. [Self-Consistent Generative Paths via Admissible Random Variational Transport](/202606/12/2606.08953v1-self-consistent-generative-paths-via-admissible-random-variational-transport)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：统一扩散和流匹配生成路径的理论框架

### 速读区论文标签
1. [SpecLoR: Spectral Lookahead Rectification for Motion-Coherent Text-to-Video Generation](/202606/12/2606.11969v1-speclor-spectral-lookahead-rectification-for-motion-coherent-text-to-video-generation)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：提出SpecLoR方法，基于Flow Matching实现运动连贯的文本到视频生成
2. [Complexity-Balanced Diffusion Splitting](/202606/12/2606.06477v1-complexity-balanced-diffusion-splitting)  
   标签：评分：7.0/10、query:3d-motion-generation
   evidence：通过时间容量分配提升扩散模型效率
3. [Exploring the Design Space of Reward Backpropagation for Flow Matching](/202606/12/2606.11075v1-exploring-the-design-space-of-reward-backpropagation-for-flow-matching)  
   标签：评分：7.0/10、query:3d-motion-generation
   evidence：研究流匹配模型中的奖励反向传播
4. [Mean Flow Distillation: Robust and Stable Distillation for Flow Matching Models](/202606/12/2606.11155v1-mean-flow-distillation-robust-and-stable-distillation-for-flow-matching-models)  
   标签：评分：7.0/10、query:3d-motion-generation
   evidence：流匹配模型蒸馏方法
5. [TopoCap: Learning Topology-Agnostic Motion Priors for Monocular Video-to-Animation](/202606/12/2606.12153v1-topocap-learning-topology-agnostic-motion-priors-for-monocular-video-to-animation)  
   标签：评分：7.0/10、query:3d-motion-generation
   evidence：从视频生成3D人体运动序列并重定向到任意骨架
6. [DRIFT: A Residual Flow Adapter for Decoding Continuous Outputs in Vision-Language Models](/202606/12/2606.05758v1-drift-a-residual-flow-adapter-for-decoding-continuous-outputs-in-vision-language-models)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：使用流匹配进行连续输出细化
7. [Learning to Solve Generative ODEs Beyond the Linear Span](/202606/12/2606.08672v1-learning-to-solve-generative-odes-beyond-the-linear-span)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：通过学习空间残差改进流/扩散模型的ODE求解器
8. [Guided Discovery of New Behaviors using Diffusion Policies](/202606/12/2606.08743v1-guided-discovery-of-new-behaviors-using-diffusion-policies)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：应用扩散策略发现新机器人行为
9. [MaskAlign: Token-Subset Representation Alignment for Efficient Diffusion Training](/202606/12/2606.08788v1-maskalign-token-subset-representation-alignment-for-efficient-diffusion-training)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：提出表示对齐方法加速扩散训练
10. [CSFlow: Aligning Flow Matching with Human Contrast Sensitivity](/202606/12/2606.08833v1-csflow-aligning-flow-matching-with-human-contrast-sensitivity)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：利用人类对比敏感度改进流匹配训练
11. [Compositional Generative Modeling from Decentralized Data](/202606/12/2606.10153v1-compositional-generative-modeling-from-decentralized-data)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：流匹配方法用于组合生成建模


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
