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

Fase 1: Coleta e Engenharia de Dados (Concluída)
1. Download de 5 anos de dados para 5 ativos principais em múltiplos timeframes.
2. Versionamento dos dados com Git LFS.
3. Análise Exploratória de Dados (EDA) para entender as características do mercado.
4. Criação de um pipeline de engenharia de features (SMA, EMA, RSI, MACD, Bollinger, ATR, features de tempo).
5. Implementação do "Triple-Barrier Method" para rotulagem dos dados.

Fase 2: Treinamento do Modelo de Deep Learning (Concluída)
1. Construção de um modelo LSTM base.
2. Implementação de um pipeline de treino e teste, incluindo normalização de dados.
3. Otimização do modelo para hardware Apple Silicon (M3).
4. Implementação de "Early Stopping" para combater o overfitting.
5. Avaliação do modelo em dados de teste, atingindo ~66% de acurácia.

Fase 3: Criação do Indicador "Oráculo" (Concluída)
1. Criação de um script de previsão que carrega o modelo treinado e gera probabilidades para dados novos.

Fase 4: Backtesting e Otimização (Concluída)
1. Implementação de um script de backtesting para simular a estratégia de trading.
2. Otimização dos parâmetros do Triple-Barrier (alvo/stop) e limiares de confiança.
3. **Conclusão:** A estratégia, baseada apenas em indicadores técnicos tradicionais, não se mostrou lucrativa nos timeframes diário e de 15 minutos. O modelo não atinge confiança suficiente para operar.

Fase 5: Engenharia de Features Avançada (Concluída)
1. Foco na Hipótese 1 (Dados de Mercado): Construção de um pipeline de dados para processar o fluxo de ordens (trades individuais) da Binance.
2. Criação de Features de Fluxo: Desenvolvimento de um novo conjunto de features, incluindo `buy_ratio`, `trade_count_accel` e `volume_dominance`, para capturar a microestrutura do mercado.
3. Criação do Dataset Enriquecido: Junção das novas features com os dados de preço (OHLCV) e criação de uma variável alvo (`target`) para o próximo ciclo de treino.

Fase 6: Re-treinamento e Avaliação do Modelo (Próximo Passo)
1. Preparação dos Dados: Escalonamento das features e divisão em conjuntos de treino/validação/teste.
2. Treinamento do Modelo: Treinar a arquitetura de Deep Learning com o novo dataset enriquecido.
3. Avaliação Offline: Analisar as métricas de performance do modelo (Acurácia, Precisão, Recall, F1-Score, Matriz de Confusão).
4. Integração e Backtesting: Integrar o novo modelo no Freqtrade e realizar um backtest financeiro para avaliar a performance em condições de mercado simuladas.

---

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
