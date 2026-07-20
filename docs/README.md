<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-07-20
- 运行时间：2026-07-20 21:38:26 UTC
- 运行状态：成功
- 本次总论文数：16
- 精读区：6
- 速读区：10

### 今日简报（AI）
今日共扫描16篇论文，精读2篇高分工作：运动预测与流匹配生成。  
最值得关注的是等变潜扩散模型EquiFusion（9.0）和速度调度流匹配（9.0），前者实现运动学无关的人体运动预测，后者优化生成采样效率。  
建议优先精读这两篇高分论文，并关注流匹配在运动生成中的约束优化（ConFlow、SUREFlow）技术。
- 详情：[/202607/20/README](/202607/20/README)

### 精读区论文标签
1. [EquiFusion: Kinematics-Agnostic Human Motion Prediction via Equivariant Latent Diffusion](/202607/20/2607.10984v1-equifusion-kinematics-agnostic-human-motion-prediction-via-equivariant-latent-diffusion)  
   标签：评分：9.0/10、query:3d-motion-generation
   evidence：生成三维人体运动序列
2. [Velocity Scheduled Flow Matching](/202607/20/2607.11442v1-velocity-scheduled-flow-matching)  
   标签：评分：9.0/10、query:3d-motion-generation
   evidence：提出速度调度的流匹配方法，直接改进流匹配生成模型
3. [Physics-Informed Diffusion for Biomechanically Plausible 3D Sign Language Generation](/202607/20/2607.14836v1-physics-informed-diffusion-for-biomechanically-plausible-3d-sign-language-generation)  
   标签：评分：9.0/10、query:3d-motion-generation
   evidence：使用扩散模型进行三维骨骼运动生成
4. [HandFlow: Fully Generative 4D Hand Recovery with Flow Matching](/202607/20/2607.11221v1-handflow-fully-generative-4d-hand-recovery-with-flow-matching)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：使用流匹配进行4D手部重建
5. [Self-Consistent Flow: Unifying Velocity and Endpoint Prediction for Rectified Flow Models](/202607/20/2607.12171v1-self-consistent-flow-unifying-velocity-and-endpoint-prediction-for-rectified-flow-models)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：流匹配方法用于生成建模
6. [Lyapunov Guidance: A Unified Framework for Stabilizing Generative Flows](/202607/20/2607.14272v1-lyapunov-guidance-a-unified-framework-for-stabilizing-generative-flows)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：流匹配指导框架

### 速读区论文标签
1. [ConFlow: Constraints-Guided Learning with Flow Matching for Motion Generation](/202607/20/2607.14424v1-conflow-constraints-guided-learning-with-flow-matching-for-motion-generation)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：流匹配用于带约束的运动生成
2. [Motion Planning with Model-Based Diffusion via Constraint Optimization and Adaptive Scheduling](/202607/20/2607.14455v1-motion-planning-with-model-based-diffusion-via-constraint-optimization-and-adaptive-scheduling)  
   标签：评分：8.0/10、query:3d-motion-generation
   evidence：基于模型的扩散用于运动规划和轨迹优化
3. [SUREFlow: State-space Uncertainty-aware REsidual Flow Matching for Robust Robot Manipulation](/202607/20/2607.10504v1-sureflow-state-space-uncertainty-aware-residual-flow-matching-for-robust-robot-manipulation)  
   标签：评分：7.0/10、query:3d-motion-generation
   evidence：提出带不确定性的流匹配用于机器人操作，方法可迁移
4. [TanGO: Training-Free 3D Editing via Tangent-Space Guidance and Optimization](/202607/20/2607.14927v1-tango-training-free-3d-editing-via-tangent-space-guidance-and-optimization)  
   标签：评分：7.0/10、query:3d-motion-generation
   evidence：流匹配在3D生成与编辑中的应用
5. [LATO.2: Factorized 3D Mesh Generation with Vertex and Topology Flow](/202607/20/2607.10623v1-lato2-factorized-3d-mesh-generation-with-vertex-and-topology-flow)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：流匹配用于3D网格生成
6. [Diversify Diffusion with Temperature Sampling and Variance-Corrective Time Shifting](/202607/20/2607.10853v1-diversify-diffusion-with-temperature-sampling-and-variance-corrective-time-shifting)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：通过温度采样和时间偏移改进扩散采样
7. [SegDiff: Segmented Trajectory Diffusion for Consistent and Adaptive Robot Manipulation](/202607/20/2607.11027v1-segdiff-segmented-trajectory-diffusion-for-consistent-and-adaptive-robot-manipulation)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：扩散模型用于轨迹生成
8. [The Geometry of Memorization: Finite-Time Spectral Sensitivity as a Diagnostic for Flow Matching Models](/202607/20/2607.12616v1-the-geometry-of-memorization-finite-time-spectral-sensitivity-as-a-diagnostic-for-flow-matching-models)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：为流匹配模型提供诊断度量
9. [Integration Matters: Rollout-Based Training for Constrained Diffusion Models](/202607/20/2607.14398v1-integration-matters-rollout-based-training-for-constrained-diffusion-models)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：扩散模型用于约束生成
10. [MeanFlowNFT: Bringing Forward-Process RL to Average-Velocity Generators](/202607/20/2607.15273v1-meanflownft-bringing-forward-process-rl-to-average-velocity-generators)  
   标签：评分：6.0/10、query:3d-motion-generation
   evidence：Flow Matching生成建模方法


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
