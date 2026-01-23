<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="Chinês">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="Inglês">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Espanhol">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Português">
  
  <h1>📚 Notas de Leitura: Diagnóstico de falhas explicável baseado em simulação termodinâmica assistida por Random Forest</h1>
  <p>Paper: Thermodynamic simulation-assisted random forest for marine diesel engine fault diagnosis</p>
  
  <div style="margin: 10px 0;">
    <a href="./" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">简体中文</a> | 
    <a href="README_en.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">English</a> | 
    <a href="README_es.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Español</a> | 
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">Português</a>
  </div>
</div>

> Título do artigo: Thermodynamic simulation-assisted random forest: Towards explainable fault diagnosis of combustion chamber components of marine diesel engines  
> Publicado em: Measurement (2025, Vol.251)  
> Método principal: TSRF (Thermodynamic Simulation-assisted Random Forest)  
> Métrica chave: Precisão média de diagnóstico 99.07%  

## 🔍 Problemas Centrais
O diagnóstico de falhas em câmaras de combustão de motores diesel marítimos enfrenta dois desafios principais:
- Métodos baseados em dados: Dependem de grandes volumes de dados rotulados (escarços em cenários industriais) e são "caixas pretas" com resultados de diagnóstico inexplicáveis.
- Métodos baseados em modelos: Possuem significado físico claro, mas a modelagem é complexa e têm pouca flexibilidade para sistemas não lineares.
- Métodos híbridos: Melhoram a precisão e a interpretabilidade, mas os modelos são complexos e o custo computacional é alto.

> 📈 *Comparação de Vantagens e Desvantagens dos Três Métodos*
> 
| Tipo de Método | Vantagens | Limitações |
|----------------|-----------|------------|
| Baseado em Modelos | 1. Significado físico claro<br>2. Adequado para sistemas com mecanismos claros | 1. Flexibilidade e adaptabilidade insuficientes<br>2. Difícil de lidar com sistemas não lineares complexos |
| Baseado em Dados | 1. Forte adaptabilidade<br>2. Adequado para cenários de Big Data | 1. Alta dependência da qualidade e quantidade de dados<br>2. Baixa interpretabilidade |
| Híbrido | 1. Precisão relativamente alta<br>2. Melhor interpretabilidade | 1. Alta complexidade do modelo<br>2. Alto custo computacional |

## 💡 Solução Inovadora: Método TSRF
O método TSRF (Random Forest assistido por simulação termodinâmica) proposto no artigo foca na fusão de "mecanismo + dados + interpretabilidade":

1. Modelagem Termodinâmica de Falhas: Reprodução rápida de falhas via ajuste fino de parâmetros:
- Primeiro, constrói-se um modelo termodinâmico 1D incluindo turbocompressor, intercooler e 6 cilindros, definindo 6 pontos de monitoramento principais.
- Sem depender de micro-simulações complexas, simulam-se 5 tipos de falhas típicas + estado normal ajustando os parâmetros centrais.

> 📊 Diagrama Estrutural do Modelo Termodinâmico 1D
![Diagrama Estrutural](assets/fig1.jpg)
*Esta figura mostra o modelo de simulação 1D do motor diesel marítimo construído no artigo, incluindo turbocompressor (TC1), intercooler (CO1), 6 cilindros (C1-C6) e coletores de admissão/escape (PL1/PL2). O modelo controla o fluxo através de válvulas (MP1-MP6), simulando o processo real de admissão-combustão-escape, servindo como base para o ajuste de parâmetros de falha e coleta de características.*

2. Seleção de 8 parâmetros de diagnóstico principais usando valores SHAP:
A simulação gera 14 parâmetros termodinâmicos (pressão do cilindro, temperatura, fluxo de calor, etc.). O método Tree SHAP é usado para calcular a importância dos parâmetros e selecionar 8 principais:
- Temperatura de escape após o turbocompressor (P14)
- Fluxo de calor na parede da camisa do cilindro (P05)
- Fluxo de calor por fuga de gás (Blow-by) (P06)
- Vazão mássica de fuga de gás (P07)
- Pressão de escape antes do turbocompressor (P11)
- Temperatura de escape antes do turbocompressor (P12)
- Fluxo de calor na parede do pistão (P03)
- Fluxo de calor na parede do cabeçote (P04)

> 📊 Análise de Importância de Parâmetros baseada em valores SHAP
![Análise SHAP](assets/fig2.jpg)
*Este conjunto de gráficos analisa a contribuição dos parâmetros para o diagnóstico sob 3 perspectivas: 1. Mapa de calor (a): Mostra os valores SHAP (contribuição) em diferentes falhas, com P14 e P05 tendo alta contribuição na maioria; 2. Gráfico de valor médio SHAP (b): Ordena os parâmetros por contribuição, confirmando P14, P05 e P06 como principais; 3. Gráfico de proporção (c): Reflete a distribuição de correlação entre parâmetros e tipos de falha.*

3. Classificação com Random Forest + Interpretação de dupla perspectiva (local/global):
- Treina-se um modelo Random Forest com os parâmetros filtrados para resolver problemas de classificação múltipla.
- Interpretação local: Uso de gráficos de cascata (Waterfall plot) para analisar a lógica de diagnóstico de uma amostra individual.
- Interpretação global: Uso de gráficos de enxame (Beeswarm plot) para mostrar a contribuição geral e gráficos de interação para revelar correlações.

> 📊 Análise da Falha de Desgaste do Anel do Pistão baseada em SHAP
![Análise F4](assets/fig3.jpg)
*Tomando F4 (desgaste do anel do pistão) como exemplo: 1. Gráfico de cascata (a): Analisa a lógica de uma amostra F4 e mostra as contribuições positivas/negativas; 2. Gráfico de enxame (b): Mostra a distribuição de contribuição dos parâmetros para F4 em todas as amostras; 3. Gráfico de interação (c): Reflete a interação entre parâmetros (ex. P11 e P12); 4. Gráfico de dependência (d): Clarifica a relação entre valores de parâmetros e valores SHAP.*

## 📈 Resultados Experimentais
O artigo calibra o modelo com dados reais de sensores de motores diesel marítimos (erro < 5%), constrói um conjunto de dados de 6 estados (120 amostras cada) e compara três modelos: KNN, SVM e RF:

| Modelo | Precisão (Dataset Original) | Precisão (Subconjunto Ótimo) |
|--------|-----------------------------|------------------------------|
| KNN    | 89.81%±3.73                 | 94.44%±3.24                  |
| SVM    | 92.13%±2.72                 | 94.44%±1.85                  |
| RF     | 99.07%±0.46                 | 99.07%±0.46                  |

> 📊 Matriz de Confusão
![Matriz de Confusão](assets/fig4.jpg)
*Comparação do desempenho de classificação. Figuras (a)-(e): Modelos tradicionais (KNN, SVM) com vários erros; Figura (f): Método TSRF (características SHAP + Random Forest), com pouquíssimas amostras mal classificadas, verificando a alta precisão.*

> 📊 Curva de Precisão-Recall
![Curva PR](assets/fig5.jpg)
*Verificação do desempenho por limiares de classificação. O método TSRF (f) mostra um AUC próximo de 1.0 para todas as falhas, demonstrando estabilidade e alto desempenho.*

## 🌟 Pontos de Destaque
1. Modelagem por ajuste fino de parâmetros: Reprodução rápida de características de falha, resolvendo a escassez de amostras.
2. Seleção SHAP multidimensional: Não apenas seleciona parâmetros, mas revela efeitos de interação.
3. Estrutura de interpretação dual: Combina mecanismos termodinâmicos para alcançar um diagnóstico explicável.
4. Alta precisão de 99.07%: Equilíbrio entre precisão e interpretabilidade, adequado para implantação industrial.

## 📚 Referências
- Referência: [1] C. Luo, M. Zhao*, X. Fu, S. Zhong, S. Fu, K. Zhang, X. Yu. Thermodynamic simulation-assisted random forest: Towards explainable fault diagnosis of combustion chamber components of marine diesel engines[J]. Measurement, 2025, 251: 117252.
- Link do artigo: https://doi.org/10.1016/j.measurement.2025.117252
- Código e dados do autor: https://ts-rf.github.io/
- Ideia central do código: Seleção de características baseada em Tree SHAP + Classificação Random Forest.

## 🔖 Nota
Este artigo é uma interpretação central do paper da revista "Measurement" (2025). É adequado para desenvolvedores em diagnóstico de falhas industriais, engenharia naval e aplicações de aprendizado de máquina.

<br>

<div align="center">
  <p>© 2026 Tech Blog Notes | Paper: <a href="https://doi.org/10.1016/j.measurement.2025.117252">Measurement 2025</a></p>
  <br>
  <a href="./">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="README_es.html">Español</a> | 
  <a href="#readme">Português</a>
</div>
