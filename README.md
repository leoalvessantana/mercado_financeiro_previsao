# Previsão de Mercado Financeiro com Abordagens de Machine Learning e Séries Temporais

Este projeto visa prever o preço de fechamento das ações da **Petrobras (PETR4.SA)** usando diferentes abordagens de Machine Learning e séries temporais.  
O objetivo principal é comparar o desempenho de modelos mais tradicionais, como a **Regressão Linear**, com técnicas mais avançadas, como **ARIMA** e **LSTM**.

---

## Descrição do Projeto
O projeto utiliza dados históricos de cotações da PETR4.SA, obtidos através da biblioteca **yfinance**, para treinar e avaliar modelos preditivos.  
O notebook Jupyter **`project.ipynb`** detalha todas as etapas do processo, desde a importação e tratamento dos dados até a conclusão.

---

## Principais Etapas

### 1. Importação e Tratamento de Dados
- Período: **01/08/2018 a 31/08/2025**  
- Exclusão de colunas irrelevantes e ajuste dos tipos de dados.  

### 2. Engenharia de Features
Criação de variáveis técnicas comumente usadas em análise de mercado financeiro:  
- Retorno diário  
- Médias móveis de 5, 14 e 21 dias (`mm5d`, `mm14d`, `mm21d`)  
- Volatilidade de 14 dias (`volatilidade14`)  
- Momentum de 5 e 14 dias (`momentum5`, `momentum14`)  
- Índice de Força Relativa (`RSI14`)  
- MACD e linha de sinal (`MACD`, `MACD_signal`)  

### 3. Análise Exploratória de Dados (EDA)
- Histogramas e gráficos de séries temporais revelaram forte relação linear entre preços (Abertura, Máximo, Mínimo) e Fechamento.  
- Matriz de correlação confirmou alta correlação.  

### 4. Seleção de Features
- Técnica **SelectKBest** usada para ranquear importância das variáveis.  
- Features mais relevantes: preços e médias móveis.  
- Features menos relevantes (Retorno, momentum5, Volume) foram descartadas.  

### 5. Modelagem de Regressão Linear
- Modelos testados: Linear, Ridge, Lasso, Random Forest, Gradient Boosting e MLP.  
- Melhor desempenho: **Regressão Linear** com **R² = 0,9978**.  

### 6. Otimização de Hiperparâmetros
- **GridSearchCV + KFold** usados para ajustar parâmetros.  
- Resultou em desempenho ainda melhor no conjunto de validação.  

### 7. Avaliação Final
- R² = **0,9942**  
- MAE = **0,1072**  
- RMSE = **0,1377**  
- Excelente capacidade de generalização.  

---

## Modelagem de Séries Temporais

### ARIMA
- Teste ADF mostrou série não estacionária → aplicada diferenciação (d=1).  
- Melhor modelo: **(0, 1, 0)** via `auto_arima`.  
- Desempenho: **R² = -8,8004** (muito ruim).  
- MAE = 9,4956 → mostrou que ARIMA não se adapta à complexidade da série.  

### LSTM
- Dados normalizados e divididos em sequências temporais.  
- Hiperparâmetros otimizados via **Keras Tuner (RandomSearch)**.  
- Resultados:  
  - R² = **0,8743**  
  - MAE = 0,5277  
  - RMSE = 0,7107  
- Superou ARIMA, mas não bateu a Regressão Linear.  

---

## Conclusão Final
- **Melhor modelo:** Regressão Linear com features técnicas derivadas.  
- **LSTM**: bom desempenho, mostrou potencial para séries complexas.  
- **ARIMA**: inadequado para esse caso devido à volatilidade do ativo.  

---

## Como Executar o Projeto

1. Clone o repositório:
   ```bash
   git clone <url_do_seu_repositorio>

2. Instale as dependências:
```bash
   pip install -r requirements.txt
