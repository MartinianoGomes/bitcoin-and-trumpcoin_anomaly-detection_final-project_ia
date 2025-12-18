# Detecção de Anomalias em Criptomoedas: BTC vs TRUMP

## 📋 Informações Gerais

| Campo | Descrição |
|-------|-----------|
| **Projeto** | Detecção de Anomalias em Bitcoin e TrumpCoin |
| **Disciplina** | Inteligência Artificial |
| **Instituição** | UNIFESSPA |
| **Autor** | Martiniano Gomes Barros Cirqueira Neto |
| **Data** | Dezembro de 2025 |

## 🎯 Objetivo

Detectar **pump-and-dump schemes**, **flash crashes** e **manipulações de mercado** em criptomoedas utilizando algoritmos de aprendizado não supervisionado para detecção de anomalias.

## 📊 Datasets

### Bitcoin (BTC-USD)
* **Origem:** Yahoo Finance API (`yfinance`)
* **Período:** 1 ano | **Intervalo:** 1 hora
* **Complexidade:** Média-alta

### TrumpCoin (TRUMP-USD)
* **Origem:** Yahoo Finance API (`yfinance`)
* **Período:** Máximo disponível | **Intervalo:** 1 hora
* **Tipo:** Memecoin política (Volatilidade extrema)

## 🔧 Metodologia

1.  **Coleta:** Automática via `yfinance`.
2.  **Engenharia de Features:** Cálculo de indicadores técnicos (RSI, MACD, Bandas de Bollinger, Volatilidade).
3.  **Pré-processamento:** Tratamento de infinitos/NaN, clipping de outliers e normalização com `RobustScaler`.
4.  **Labels Sintéticos:** Criação de rótulos baseados em regras estatísticas (ex: variação de preço > percentil 99) para validação inicial.

## 🤖 Algoritmos Utilizados

| Algoritmo | Descrição |
|-----------|-----------|
| **Isolation Forest** | Isola anomalias usando árvores de decisão aleatórias. |
| **Local Outlier Factor** | Baseia-se na densidade local dos vizinhos. |
| **One-Class SVM** | Define uma fronteira de decisão para dados "normais". |

---

## 💻 Configuração do Ambiente (VS Code)

Para executar o notebook `.ipynb`, siga os passos abaixo de acordo com seu sistema operacional.

### 1. Requisitos Prévios
* **VS Code** instalado.
* **Python 3.10+** instalado.

### 2. Configuração no Windows
1.  **Instalar Extensões:** No VS Code, instale as extensões **Python** e **Jupyter**.
2.  **Criar Ambiente Virtual:**
    ```powershell
    python -m venv venv
    .\venv\Scripts\activate
    ```

### 3. Configuração no Linux (Ubuntu/Debian)
1.  **Instalar Python/PIP:**
    ```bash
    sudo apt update
    sudo apt install python3 python3-pip python3-venv
    ```
2.  **Criar Ambiente Virtual:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

---

## 🚀 Como Executar

1.  Abra a pasta do projeto no VS Code.
2.  Abra o arquivo `bitcoin_trumpcoin_anomaly_detection.ipynb`.
3.  No canto superior direito, clique em **Select Kernel** -> **Python Environments** e escolha o ambiente `venv` criado.
4.  Clique em **Run All** para processar os dados e gerar os gráficos.

## 📈 Resultados Esperados

O projeto gera visualizações automáticas para:
* Séries temporais com pontos de anomalia marcados.
* Gráficos de dispersão comparando volumes e preços.
* Distribuição estatística das anomalias detectadas por cada modelo.