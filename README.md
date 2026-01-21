<div align="center">
  <!-- 语言徽章（可选，提升视觉效果） -->
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="中文">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="English">
  
  <h1>📚 读书笔记：热力学仿真+随机森林赋能船舶柴油机燃烧室可解释故障诊断</h1>
  <p>论文：Thermodynamic simulation-assisted random forest for marine diesel engine fault diagnosis</p>
  
  <!-- 核心语言切换导航（仿Ultralytics风格） -->
  <div style="margin: 10px 0;">
    <a href="#readme" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px;">简体中文</a> | 
    <a href="./README_en.md" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px;">English</a>
  </div>
</div>

## 🔍 核心痛点
船舶柴油机燃烧室故障诊断面临两大核心问题：
- 数据驱动方法：依赖海量标注数据，工业场景样本稀缺，且是「黑箱模型」，诊断结果无法解释；
- 模型驱动方法：物理意义清晰，但建模复杂，面对非线性系统灵活性差。

> 📊 此处插入论文原图：
![三种故障诊断方法对比](assets/table1.png)
*Table 1：三种故障诊断方法优缺点对比*

## 💡 创新方案：TSRF方法
论文提出的TSRF（热力学仿真辅助随机森林）方法，核心是「机理+数据+可解释性」融合：
1. 搭建一维热力学模型，通过参数微调模拟5类典型故障；
2. 用SHAP值筛选8个核心诊断参数；
3. 随机森林分类+双视角（局部/全局）解释结果。

> 📈 此处插入论文原图：
![柴油机热力学模型结构](assets/fig2.png)
*Fig. 2：柴油机一维热力学模型结构图*

## 📊 实验结果
| 模型 | 原始数据集准确率 | 最优参数子集准确率 |
|------|------------------|--------------------|
| KNN  | 89.81%±3.73      | 94.44%±3.24        |
| SVM  | 92.13%±2.72      | 94.44%±1.85        |
| RF   | 99.07%±0.46      | 99.07%±0.46        |

## 🌟 核心亮点
1. 参数微调建模：快速复现故障特征，解决样本稀缺问题；
2. SHAP全维度筛选：不仅选参数，还能揭示参数交互作用；
3. 99.07%高准确率：兼顾精度与可解释性，适合工业部署。

<br>

<!-- 底部再次添加语言切换，提升易用性 -->
<div align="center">
  <p>© 2025 技术博客笔记 | 论文链接：<a href="https://doi.org/10.1016/j.measurement.2025.117252">Measurement 2025</a></p>
  <br>
  <a href="#readme">简体中文</a> | 
  <a href="./README_en.md">English</a>
</div>
