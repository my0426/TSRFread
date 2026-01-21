<div align="center">
  <!-- 语言徽章（可选，提升视觉效果） -->
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="中文">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="English">
  
  <h1>📚 读书笔记：基于热力学仿真辅助随机森林的可解释故障诊断</h1>
  <p>论文：Thermodynamic simulation-assisted random forest for marine diesel engine fault diagnosis</p>
  
  <!-- 核心语言切换导航（仿Ultralytics风格） -->
  <div style="margin: 10px 0;">
    <a href="#readme" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px;">简体中文</a> | 
    <a href="./README_en.md" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px;">English</a>
  </div>
</div>

> 论文标题：Thermodynamic simulation-assisted random forest: Towards explainable fault diagnosis of combustion chamber components of marine diesel engines  
> 发表期刊：Measurement (2025, Vol.251)  
> 核心方法：TSRF (Thermodynamic Simulation-assisted Random Forest)  
> 关键指标：平均诊断准确率 99.07%  

## 🔍 核心问题
船舶柴油机燃烧室故障诊断面临两大核心问题：
- 数据驱动方法：依赖海量标注数据，工业场景样本稀缺，且是「黑箱模型」，诊断结果无法解释；
- 模型驱动方法：物理意义清晰，但建模复杂，面对非线性系统灵活性差；
- 混合方法：精度和可解释性有提升，但模型复杂、计算成本高

> 📈
| 方法类型       | 优势                                     | 局限性                                     |
|----------------|------------------------------------------|--------------------------------------------|
| 模型驱动方法   | 1. 物理意义清晰<br>2. 适用于机理明确的系统 | 1. 灵活性与适应性不足<br>2. 难以应对复杂非线性系统 |
| 数据驱动方法   | 1. 适应性强<br>2. 适用于大数据场景       | 1. 高度依赖数据质量与数量<br>2. 可解释性差       |
| 混合方法       | 1. 准确率相对较高<br>2. 可解释性更好     | 1. 模型复杂度高<br>2. 计算成本高                 |
> *三种故障诊断方法优缺点对比*

## 💡 创新方案：TSRF方法
论文提出的TSRF（热力学仿真辅助随机森林）方法，核心是「机理+数据+可解释性」融合：
1. 热力学故障建模：用参数微调快速复现故障：
- 先搭建包含涡轮增压器、中冷器、6 个气缸的一维热力学模型，设置 6 个关键监测点
- 不依赖复杂微观仿真，通过调整核心参数模拟 5 类典型故障 + 正常状态

> 📊 
![柴油机一维热力学模型结构图](assets/table2.png)
*柴油机一维热力学模型结构图*

2. 用SHAP值筛选8个核心诊断参数：
仿真输出 14 个热力学参数（缸压、缸温、热流量等），用 Tree SHAP 方法计算参数重要性，筛选出 8 个核心参数：
- 涡轮增压器后排气温度（P14）
- 缸套壁热流量（P05）
- 窜气热流量（P06）
- 窜气质量流量（P07）
- 涡轮增压器前排气压力（P11）
- 涡轮增压器前排气温度（P12）
- 活塞壁热流量（P03）
- 缸盖壁热流量（P04）

> 📊 
![基于 SHAP 值的参数重要性分析图](assets/table3.png)
*基于 SHAP 值的参数重要性分析图*

3. 随机森林分类+双视角（局部/全局）解释结果：
- 用筛选后的核心参数训练随机森林模型，解决多分类问题
- 局部解释：用水滴图（Waterfall plot）分析单个样本的诊断逻辑
- 全局解释：用蜂群图（Beeswarm plot）展示参数整体贡献，用交互图揭示参数关联

> 📊 
![基于 SHAP 值的活塞环磨损故障分析图](assets/fig4.png)
*基于 SHAP 值的活塞环磨损故障分析图*

## 📈 实验结果
论文用真实船舶柴油机传感器数据校准模型（仿真值与实验值误差 < 5%），构建 6 种状态的数据集（每种 120 个样本），对比 KNN、SVM 和 RF 三种模型：
| 模型 | 原始数据集准确率 | 最优参数子集准确率 |
|------|------------------|--------------------|
| KNN  | 89.81%±3.73      | 94.44%±3.24        |
| SVM  | 92.13%±2.72      | 94.44%±1.85        |
| RF   | 99.07%±0.46      | 99.07%±0.46        |
> 📊 
![混淆矩阵图](assets/fig4.png)
*混淆矩阵图*
![精确率 - 召回率曲线](assets/fig4.png)
*精确率 - 召回率曲线*

## 🌟 核心亮点
1. 参数微调建模：快速复现故障特征，解决样本稀缺问题；
2. SHAP全维度筛选：不仅选参数，还能揭示参数交互作用；
3. 双视角解释框架：结合热力学机理，实现可解释故障诊断；
4. 99.07%高准确率：兼顾精度与可解释性，适合工业部署。

## 📚 参考资料
- 参考文献：[1] C. Luo, M. Zhao*, X. Fu, S. Zhong, S. Fu, K. Zhang, X. Yu. Thermodynamic simulation-assisted random forest: Towards explainable fault diagnosis of combustion chamber components of marine diesel engines[J]. Measurement, 2025, 251: 117252.
- 论文链接：https://doi.org/10.1016/j.measurement.2025.117252
- 原作者的代码及数据：https://ts-rf.github.io/zh-CN/
- 核心代码思路：基于 Tree SHAP 的特征选择 + 随机森林分类（可参考 scikit-learn+shap 库实现）

## 🔖 笔记说明
本文是对 2025 年《Measurement》期刊论文的核心解读，重点提炼了 TSRF 方法的创新点、实验设计和关键结果。适合从事工业故障诊断、船舶工程、机器学习应用的开发者参考。

<br>

<!-- 底部再次添加语言切换，提升易用性 -->
<div align="center">
  <p>© 2025 技术博客笔记 | 论文链接：<a href="https://doi.org/10.1016/j.measurement.2025.117252">Measurement 2025</a></p>
  <br>
  <a href="#readme">简体中文</a> | 
  <a href="./README_en.md">English</a>
</div>
