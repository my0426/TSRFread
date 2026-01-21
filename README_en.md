<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="中文">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="English">
  
  <h1>📚 Reading Notes: Thermodynamic Simulation-assisted Random Forest for Marine Diesel Engine Fault Diagnosis</h1>
  
  <div style="margin: 10px 0;">
    <a href="./README.md" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px;">简体中文</a> | 
    <a href="#readme" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px;">English</a>
  </div>
</div>

## 🔍 Core Challenges
Fault diagnosis of marine diesel engine combustion chambers faces two key challenges:
- Data-driven methods: Rely on massive labeled data (scarce in industrial scenarios) and are "black-box models" with unexplainable results;
- Model-driven methods: Clear physical meaning but complex modeling with poor flexibility for nonlinear systems.

> 📊 Insert original paper figure here:
![Comparison of three fault diagnosis methods](assets/table1.png)
*Table 1: Advantages and disadvantages of three fault diagnosis methods*

## 💡 Innovative Solution: TSRF Method
The TSRF (Thermodynamic Simulation-assisted Random Forest) method proposed in the paper integrates "mechanism + data + interpretability":
1. Build a 1D thermodynamic model and simulate 5 typical faults via parameter fine-tuning;
2. Select 8 core diagnostic parameters using SHAP values;
3. Random Forest classification + dual-perspective (local/global) result interpretation.

> 📈 Insert original paper figure here:
![Diesel engine thermodynamic model structure](assets/fig2.png)
*Fig. 2: Structure of 1D thermodynamic model for diesel engine*

## 📊 Experimental Results
| Model | Accuracy (Original Dataset) | Accuracy (Optimal Parameter Subset) |
|-------|-----------------------------|--------------------------------------|
| KNN   | 89.81%±3.73                 | 94.44%±3.24                          |
| SVM   | 92.13%±2.72                 | 94.44%±1.85                          |
| RF    | 99.07%±0.46                 | 99.07%±0.46                          |

## 🌟 Key Highlights
1. Parameter fine-tuning modeling: Quickly reproduce fault features and solve the problem of scarce samples;
2. SHAP full-dimensional selection: Not only select parameters but also reveal parameter interaction effects;
3. High accuracy (99.07%): Balance precision and interpretability, suitable for industrial deployment.

<br>

<div align="center">
  <p>© 2025 Technical Blog Notes | Paper Link: <a href="https://doi.org/10.1016/j.measurement.2025.117252">Measurement 2025</a></p>
  <br>
  <a href="./README.md">简体中文</a> | 
  <a href="#readme">English</a>
</div>
