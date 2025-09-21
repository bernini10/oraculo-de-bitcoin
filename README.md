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

*   **Plataforma de Trading:** [Freqtrade](https://www.freqtrade.io/en/stable/   )
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
    *(Nota: O ficheiro `requirements.txt` será criado no próximo passo   ).*

---
## Roadmap do Projeto
## Roadmap do Projeto

Fase 1: Coleta e Engenharia de Dados (Concluída)
Download de 5 anos de dados para 5 ativos principais em múltiplos timeframes.
Versionamento dos dados com Git LFS.
Análise Exploratória de Dados (EDA) para entender as características do mercado.
Criação de um pipeline de engenharia de features (SMA, EMA, RSI, MACD, Bollinger, ATR, features de tempo).
Implementação do "Triple-Barrier Method" para rotulagem dos dados.

Fase 2: Treinamento do Modelo de Deep Learning (Concluída)
Construção de um modelo LSTM base.
Implementação de um pipeline de treino e teste, incluindo normalização de dados.
Otimização do modelo para hardware Apple Silicon (M3).
Implementação de "Early Stopping" para combater o overfitting.
Avaliação do modelo em dados de teste, atingindo ~66% de acurácia.

Fase 3: Criação do Indicador "Oráculo" (Concluída)
Criação de um script de previsão que carrega o modelo treinado e gera probabilidades para dados novos.

Fase 4: Backtesting e Otimização (Concluída)
Implementação de um script de backtesting para simular a estratégia de trading.
**Conclusão:** A estratégia, baseada apenas em indicadores técnicos tradicionais, não se mostrou lucrativa.

Fase 5: Engenharia de Features Avançada (Concluída)
**Foco na Hipótese 1 (Dados de Mercado):** Construção de um pipeline para processar o fluxo de ordens (trades individuais) da Binance.
**Criação de Features de Fluxo:** Desenvolvimento de um novo conjunto de features (`buy_ratio`, `trade_count_accel`, `volume_dominance`) para capturar a microestrutura do mercado.
**Criação do Dataset Enriquecido:** Junção das novas features com os dados de preço (OHLCV).

Fase 6: Re-treinamento e Avaliação do Modelo v2 (Concluída)
**Modelo Long-Only:** Treino e backtest de um modelo focado apenas em compras, que se mostrou ligeiramente lucrativo mas muito volátil.
**Modelo Long/Short:** Implementação do "Método da Tripla Barreira" para criar um modelo capaz de prever subidas e descidas.
**Otimização de Limiar:** Calibração do modelo para encontrar um limiar de confiança ótimo, resultando num "modelo especialista em shorts" com 50% de precisão estatística.
**Backtest Financeiro Final:** Simulação da estratégia "Short-Only", que se revelou não lucrativa.
**Conclusão Principal:** A vantagem preditiva do fluxo de ordens, por si só, não é suficiente para superar a dinâmica de risco/recompensa do mercado com a arquitetura atual.

Fase 7: Otimização de Estratégia e Filtros de Regime (Próximo Passo)
**Hipótese 1: Filtro de Regime de Mercado.** Adicionar um filtro de tendência de longo prazo (e.g., Média Móvel de 200 períodos) para permitir que o Oráculo opere apenas a favor da "maré" principal do mercado.
**Hipótese 2: Otimização de Parâmetros.** Realizar uma otimização exaustiva dos parâmetros de gestão de risco (Stop-Loss, Take-Profit, Trailing Stop) para encontrar uma combinação lucrativa.
**Hipótese 3: Arquitetura Alternativa.** Pesquisar e testar arquiteturas de modelo mais avançadas (e.g., Transformers) que possam capturar melhor as dependências de longo prazo.


## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
