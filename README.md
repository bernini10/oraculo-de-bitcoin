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

## 🗺️ Roadmap do Projeto

-   [ ] **Fase 1: Coleta e Engenharia de Dados**
    -   [ ] Script para download de dados históricos via Freqtrade.
    -   [ ] Notebook de exploração de dados (`notebooks/01-data-exploration.ipynb`).
    -   [ ] Implementação da engenharia de features (`src/feature_engineering.py`).
    -   [ ] Implementação do Método Triple-Barrier (`src/labeling.py`).
-   [ ] **Fase 2: Treinamento do Modelo**
    -   [ ] Notebook de prototipagem do modelo LSTM (`notebooks/02-model-prototyping.ipynb`).
    -   [ ] Script de treino e validação do modelo (`scripts/train_model.py`).
-   [ ] **Fase 3: Integração com Freqtrade**
    -   [ ] Configuração do Freqtrade e FreqAI.
    -   [ ] Criação da estratégia `OracleStrategy.py` em `freqtrade/user_data/strategies/`.
-   [ ] **Fase 4: Backtesting e Otimização**
    -   [ ] Execução de backtests e análise de resultados.
    -   [ ] Otimização da estratégia com Hyperopt.
-   [ ] **Documentação**
    -   [ ] Criar diagrama da arquitetura.
    -   [ ] Detalhar o processo de re-treino do modelo.

---

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

