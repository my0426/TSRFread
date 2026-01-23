<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="Chinese">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="English">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Spanish">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Portuguese">
  
  <h1>📚 Reading Notes: Thermodynamic simulation-assisted random forest...</h1>
  <p>Paper: Thermodynamic simulation-assisted random forest for marine diesel engine fault diagnosis</p>
  
  <div style="margin: 10px 0;">
    <a href="./" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Simplified Chinese</a> | 
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">English</a> | 
    <a href="README_es.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Español</a> | 
    <a href="README_pt.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Português</a>
  </div>
</div>

> Paper Title: Thermodynamic simulation-assisted random forest: Towards explainable fault diagnosis of combustion chamber components of marine diesel engines  
> Published in: Measurement (2025, Vol.251)  
> Core Method: TSRF (Thermodynamic Simulation-assisted Random Forest)  
> Key Metric: Average diagnostic accuracy 99.07%  

## 🔍 Core Problems
Fault diagnosis of marine diesel engine combustion chambers faces two core challenges:
- Data-driven methods: Rely on massive labeled data (scarce in industrial scenarios) and are "black-box models" with unexplainable diagnostic results;
- Model-driven methods: Clear physical meaning but complex modeling and poor flexibility for nonlinear systems;
- Hybrid methods: Improved accuracy and interpretability but complex models with high computational costs

> 📈 *Comparison of Advantages and Disadvantages of Three Fault Diagnosis Methods*
> 
| Method Type     | Advantages                                     | Limitations                                     |
|-----------------|------------------------------------------------|------------------------------------------------|
| Model-driven    | 1. Clear physical meaning<br>2. Suitable for systems with clear mechanisms | 1. Insufficient flexibility and adaptability<br>2. Difficult to handle complex nonlinear systems |
| Data-driven     | 1. Strong adaptability<br>2. Suitable for big data scenarios | 1. Highly dependent on data quality and quantity<br>2. Poor interpretability |
| Hybrid          | 1. Relatively high accuracy<br>2. Better interpretability | 1. High model complexity<br>2. High computational cost |

## 💡 Innovative Solution: TSRF Method
The TSRF (Thermodynamic Simulation-assisted Random Forest) method proposed in the paper is centered on the integration of "mechanism + data + interpretability":
1. Thermodynamic Fault Modeling: Rapidly reproduce faults via parameter fine-tuning:
- First, build a 1D thermodynamic model including turbocharger, intercooler, 6 cylinders, with 6 key monitoring points set
- Without relying on complex micro-simulation, simulate 5 typical fault types + normal state by adjusting core parameters

> 📊 Structure Diagram of 1D Thermodynamic Model for Diesel Engine
![Structure Diagram of 1D Thermodynamic Model for Diesel Engine](assets/fig1.jpg)
*This figure shows the 1D simulation model of marine diesel engine built in the paper, including turbocharger (TC1), intercooler (CO1), 6 cylinders (C1-C6), and intake/exhaust manifolds (PL1/PL2). The model controls the flow path through valves (MP1-MP6), which can simulate the intake-combustion-exhaust process of real diesel engines, serving as the core carrier for subsequent fault parameter fine-tuning and feature collection.*

2. Screening 8 core diagnostic parameters using SHAP values:
The simulation outputs 14 thermodynamic parameters (cylinder pressure, cylinder temperature, heat flux, etc.). The Tree SHAP method is used to calculate parameter importance and screen out 8 core parameters:
- Exhaust temperature after turbocharger (P14)
- Cylinder liner wall heat flux (P05)
- Blow-by gas heat flux (P06)
- Blow-by gas mass flow rate (P07)
- Exhaust pressure before turbocharger (P11)
- Exhaust temperature before turbocharger (P12)
- Piston wall heat flux (P03)
- Cylinder head wall heat flux (P04)

> 📊 Parameter Importance Analysis Chart Based on SHAP Values
![Parameter Importance Analysis Chart Based on SHAP Values](assets/fig2.jpg)
*This set of figures analyzes the contribution of parameters to fault diagnosis from 3 perspectives: 1. Heatmap (a): Shows the SHAP values (contribution) of different parameters under various faults, with P14 and P05 having high contributions in most faults; 2. Average SHAP value chart (b): Sorts parameters by contribution, confirming P14, P05, and P06 as core diagnostic parameters; 3. Proportion chart (c): Reflects the correlation distribution between parameters and fault types, providing a basis for subsequent feature screening.*

3. Random Forest classification + dual-perspective (local/global) result interpretation:
- Train a random forest model with the filtered core parameters to solve multi-classification problems
- Local interpretation: Use Waterfall plot to analyze the diagnostic logic of a single sample
- Global interpretation: Use Beeswarm plot to show the overall contribution of parameters, and interaction plots to reveal parameter correlations

> 📊 Piston Ring Wear Fault Analysis Chart Based on SHAP Values
![Piston Ring Wear Fault Analysis Chart Based on SHAP Values](assets/fig3.jpg)
*Taking F4 (piston ring wear) as an example, this set of figures realizes the interpretability of the model diagnosis process: 1. Waterfall plot (a): Analyzes the diagnostic logic of a single F4 sample and shows the positive/negative contributions of each parameter; 2. Beeswarm plot (b): Displays the contribution distribution of parameters to F4 across all samples, with P12 and P14 being the core influencing parameters; 3. Interaction plot (c): Reflects the interaction between parameters (e.g., P11 and P12); 4. Dependence plot (d): Clarifies the relationship between parameter values and SHAP values, providing a basis for fault mechanism analysis.*

## 📈 Experimental Results
The paper calibrates the model with real marine diesel engine sensor data (error between simulated and experimental values < 5%), builds a dataset of 6 states (120 samples for each state), and compares three models: KNN, SVM, and RF:
| Model | Accuracy (Original Dataset) | Accuracy (Optimal Parameter Subset) |
|-------|-----------------------------|--------------------------------------|
| KNN   | 89.81%±3.73                 | 94.44%±3.24                          |
| SVM   | 92.13%±2.72                 | 94.44%±1.85                          |
| RF    | 99.07%±0.46                 | 99.07%±0.46                          |

> 📊 Confusion Matrix
![Confusion Matrix](assets/fig4.jpg)
*This set of confusion matrices compares the classification performance of different methods. Figures (a)-(e): Results of traditional models (e.g., KNN, SVM) or original feature sets, with many misclassifications (e.g., F3, F4 samples misjudged); Figure (f): Results of the TSRF method (SHAP-filtered features + random forest), with only a very small number of samples misclassified, verifying the high classification accuracy of the method.*

> 📊 Precision-Recall Curve
![Precision-Recall Curve](assets/fig5.jpg)
*This set of curves verifies performance from the perspective of classification thresholds. Figures (a)-(e): In the curves of traditional models/feature sets, the AUC value of some faults (e.g., F3) is low; Figure (f): In the curve of the TSRF method, the AUC of all faults is close to 1.0, and the overall Micro-average and Roc-AUC reach 1.0, reflecting the stable and high performance of the model.*

## 🌟 Core Highlights
1. Parameter fine-tuning modeling: Rapidly reproduce fault features and solve the problem of sample scarcity;
2. SHAP full-dimensional screening: Not only select parameters but also reveal parameter interaction effects;
3. Dual-perspective interpretation framework: Combine thermodynamic mechanisms to achieve explainable fault diagnosis;
4. High accuracy of 99.07%: Balance precision and interpretability, suitable for industrial deployment.

## 📚 References
- Reference: [1] C. Luo, M. Zhao*, X. Fu, S. Zhong, S. Fu, K. Zhang, X. Yu. Thermodynamic simulation-assisted random forest: Towards explainable fault diagnosis of combustion chamber components of marine diesel engines[J]. Measurement, 2025, 251: 117252.
- Paper Link: https://doi.org/10.1016/j.measurement.2025.117252
- Author's Code and Data: https://ts-rf.github.io/
- Core Code Idea: Feature selection based on Tree SHAP + Random Forest classification (refer to scikit-learn + shap library for implementation)

## 🔖 Note
This article is a core interpretation of the 2025 "Measurement" journal paper, focusing on extracting the innovations, experimental design, and key results of the TSRF method. It is suitable for developers engaged in industrial fault diagnosis, marine engineering, and machine learning applications.

<br>

<!-- Bottom Language Switch for Usability -->
<div align="center">
  <p>© 2026 Tech Blog Notes | Paper: <a href="https://doi.org/10.1016/j.measurement.2025.117252">Measurement 2025</a></p>
  <br>
  <a href="./">Simplified Chinese</a> | 
  <a href="#readme">English</a> | 
  <a href="README_es.html">Español</a> | 
  <a href="README_pt.html">Português</a>
</div>
