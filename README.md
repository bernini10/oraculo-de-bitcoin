# oraculo-de-bitcoin
"Um sistema de IA para gerar indicadores preditivos nativos para Bitcoin usando Deep Learning e Freqtrade."
# O Oráculo de Bitcoin 🔮

**Um sistema de IA para gerar indicadores preditivos nativos para Bitcoin usando Deep Learning e Freqtrade.**

Este projeto visa substituir indicadores técnicos tradicionais por um modelo de Deep Learning (LSTM) que aprende os padrões únicos do mercado de Bitcoin 24/7, gerando probabilidades de negociação em tempo real.

---

## 🎯 Visão e Objetivo

O mercado de criptomoedas opera de forma contínua e possui uma dinâmica fundamentalmente diferente dos mercados tradicionais. Este projeto abandona a aplicação de indicadores clássicos (RSI, MACD) e, em vez disso, constrói um "Oráculo" que gera os seus próprios indicadores preditivos, otimizados especificamente para o Bitcoin.

O objetivo final é criar um indicador baseado em probabilidades que, quando integrado numa estratégia de trading no Freqtrade, demonstre uma vantagem estatística superior em comparação com estratégias baseadas em indicadores clássicos.

---

## 🏗️ Arquitetura do Sistema

O projeto está dividido em 4 fases principais:

1.  **Coleta e Engenharia de Dados:** Obtenção de 5 anos de dados multi-timeframe (1D, 4h, 1h, 30m, 15m, 5m) e enriquecimento com dezenas de features (preço, momentum, tempo, ciclo). O alvo da previsão é definido usando o **Método Triple-Barrier**.
2.  **Treinamento do Modelo de Deep Learning:** Uma Rede Neural Recorrente (LSTM) é treinada para classificar o futuro próximo em três classes: **Comprar**, **Vender** ou **Neutro**, com base nas features de uma sequência de velas.
3.  **Criação do Indicador "Oráculo":** O modelo treinado é integrado numa estratégia Freqtrade através do **FreqAI**. A cada nova vela, o modelo gera um "Painel de Probabilidades" (ex: Alta: 75%, Baixa: 15%, Neutra: 10%).
4.  **Backtesting e Otimização:** A estratégia é rigorosamente testada e comparada com benchmarks. Os limiares de probabilidade e a lógica de saída são otimizados usando o Hyperopt do Freqtrade.

![Diagrama da Arquitetura](docs/architecture_diagram.png)  <!-- Criaremos este diagrama depois -->

---

## 🛠️ Tecnologias e Ferramentas

*   **Plataforma de Trading:** [Freqtrade](https://www.freqtrade.io/en/stable/ )
*   **Linguagem:** Python 3.9+
*   **Bibliotecas de ML:** TensorFlow, Keras, Scikit-learn
*   **Manipulação de Dados:** Pandas, NumPy
*   **Engenharia de Features:** tsfresh (a explorar)
*   **Hardware (Recomendado):** GPU NVIDIA com CUDA para aceleração do treino.

---

## 🚀 Como Começar

### Pré-requisitos

*   Python 3.9+
*   Git
*   Docker (Recomendado para Freqtrade)

### Instalação

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/[SEU_USERNAME]/oraculo-de-bitcoin.git
    cd oraculo-de-bitcoin
    ```

2.  **Crie e ative um ambiente virtual:**
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # No Windows: .venv\Scripts\activate
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```
    *(Nota: O ficheiro `requirements.txt` será criado no próximo passo ).*

---
## 🗺️ Roadmap do Projeto (Atualizado)

O projeto está dividido em fases claras, construindo progressivamente a nossa solução.

- [x] **✅ Fase 1: Coleta e Engenharia de Dados**
  - [x] Coleta de 5 anos de dados para 5 ativos principais (BTC, ETH, BNB, SOL, XRP) em 7 timeframes.
  - [x] Análise Exploratória de Dados (EDA) no notebook `01-Data-Exploration.ipynb`.
  - [x] Criação de features técnicas (SMA, EMA, RSI, Bollinger, MACD).
  - [x] Criação de features de tempo.
  - [x] Implementação do "Triple-Barrier Method" para criar os labels (Comprar/Vender/Neutro).
  - [x] Geração do dataframe final de features (`final_btc_features.feather`).

- [x] **✅ Fase 2: Treinamento do Modelo de Deep Learning**
  - [x] Configuração do ambiente TensorFlow para GPU em Apple Silicon (M3).
  - [x] Construção da arquitetura do modelo LSTM no notebook `02-Model-Training.ipynb`.
  - [x] Treino do modelo V1 com uma acurácia de **~66%** no conjunto de teste.
  - [x] Implementação de "Early Stopping" para evitar overfitting.
  - [x] O modelo treinado (`oracle_lstm_v1.h5`) e o scaler (`scaler_v1.pkl`) foram guardados.

- [x] **✅ Fase 3: Criação do Indicador "Oráculo" (Prova de Conceito)**
  - [x] Criação do script de previsão no notebook `03-Prediction-Script.ipynb`.
  - [x] Demonstração de como carregar o modelo e fazer uma previsão para o próximo dia.

- [ ] **⏳ Fase 4: Backtesting e Otimização (Próximo Passo)**
  - [ ] Criar um script de backtesting para avaliar o desempenho do modelo ao longo do tempo.
  - [ ] Calcular métricas de trading (Profit Factor, Sharpe Ratio, Drawdown).
  - [ ] Comparar os resultados com uma estratégia de base.
  - [ ] (Opcional) Otimizar os limiares de probabilidade para entrada de trades.

- [ ] **Fase 5: Integração e Produção**
  - [ ] Adaptar o script de previsão para uma estratégia de inferência no FreqAI.
  - [ ] Implementar a lógica de sinais no Freqtrade.
  - [ ] Executar o modelo em "dry-run" ou "live-run".


---

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

