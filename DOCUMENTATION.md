# Documentação do Projeto: Detecção de Anomalias em Criptomoedas

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

| Atributo | Valor |
|----------|-------|
| **Origem** | Yahoo Finance API (yfinance) |
| **Período** | 1 ano (dados recentes) |
| **Intervalo** | 1 hora |
| **Registros** | ~8.760 (365 dias × 24 horas) |
| **Complexidade** | Média-alta |

### TrumpCoin (TRUMP-USD)

| Atributo | Valor |
|----------|-------|
| **Origem** | Yahoo Finance API (yfinance) |
| **Período** | Máximo disponível |
| **Intervalo** | 1 hora |
| **Tipo** | Memecoin política |
| **Complexidade** | Alta (volatilidade extrema) |

### Variáveis Utilizadas

| Variável | Descrição |
|----------|-----------|
| `Open` | Preço de abertura |
| `High` | Preço máximo |
| `Low` | Preço mínimo |
| `Close` | Preço de fechamento |
| `Volume` | Volume negociado |
| `RSI` | Relative Strength Index (indicador de momentum) |
| `MACD` | Moving Average Convergence Divergence |
| `BB_upper` | Banda superior de Bollinger |
| `Volume_Change` | Variação percentual do volume |
| `Price_Change` | Variação percentual do preço |
| `Volatility` | Volatilidade (desvio padrão móvel) |
| `Hour` | Hora do dia (feature temporal) |
| `DayOfWeek` | Dia da semana (feature temporal) |

## 🔧 Metodologia

### 1. Coleta de Dados

Os dados são coletados automaticamente via API do Yahoo Finance utilizando a biblioteca `yfinance`:

```python
import yfinance as yf

# Bitcoin
btc_raw = yf.download('BTC-USD', period='1y', interval='1h')

# TrumpCoin
trump_raw = yf.download('TRUMP-USD', period='max', interval='1h')
```

### 2. Engenharia de Features

#### Indicadores Técnicos Calculados

| Indicador | Fórmula/Descrição |
|-----------|-------------------|
| **RSI** | Índice de Força Relativa (período=14) |
| **MACD** | EMA(12) - EMA(26) |
| **Bollinger Upper** | Média móvel + 2 × Desvio padrão |
| **Volatility** | Desvio padrão móvel (janela=24h) |

### 3. Pré-processamento

1. **Remoção de infinitos**: Valores infinitos substituídos por NaN
2. **Preenchimento de NaN**: Valores ausentes preenchidos com 0
3. **Clipping de extremos**: Valores limitados aos percentis 1% e 99%
4. **Normalização**: RobustScaler (resistente a outliers)

### 4. Criação de Labels Sintéticos

Labels de anomalia criados usando regras estatísticas:

```python
Anomaly_Label = (
    (|Price_Change| > percentil_99) |
    (RSI > 85) | (RSI < 15) |
    (Volume_Change > percentil_98)
)
```

## 🤖 Algoritmos de Detecção

### Modelos Utilizados

| Algoritmo | Descrição | Parâmetros |
|-----------|-----------|------------|
| **Isolation Forest** | Isola anomalias usando árvores de decisão aleatórias | `contamination=0.015` |
| **Local Outlier Factor (LOF)** | Compara densidade local entre vizinhos | `n_neighbors=25`, `contamination=0.015` |
| **One-Class SVM** | Aprende fronteira ao redor dos dados normais | `nu=0.015`, `kernel='rbf'` |
| **Isolation Forest (Deep)** | Variante com maior diversidade | `max_samples=0.8` |

### Parâmetro de Contaminação

O valor `contamination=0.015` indica que esperamos aproximadamente **1.5% de anomalias** no dataset.

## 📈 Métricas de Avaliação

| Métrica | Descrição |
|---------|-----------|
| **Precision** | Das anomalias detectadas, quantas são realmente anomalias? |
| **Recall** | Das anomalias reais, quantas foram detectadas? |
| **F1-Score** | Média harmônica entre Precision e Recall |

> **Nota**: Como utilizamos labels sintéticos (aproximação estatística), as métricas servem como referência comparativa entre os modelos, não como verdade absoluta.

## 📊 Visualizações Geradas

### Bitcoin
1. **Série Temporal com Anomalias**: Preço + anomalias detectadas
2. **Volume de Negociação**: Identificação de picos de volume
3. **RSI**: Zonas de sobrecompra/sobrevenda
4. **Comparação de Algoritmos**: Quantidade de anomalias por modelo
5. **Distribuição**: Proporção anomalias vs normal

### TrumpCoin
1. **Série Temporal com Anomalias**: Preço + anomalias (Isolation Forest)
2. **Comparação de Algoritmos**: Quantidade de anomalias por modelo
3. **Distribuição**: Proporção anomalias vs normal

## 📁 Estrutura do Projeto

```
bitcoin-and-trumpcoin_anomaly-detection_final-project_ia/
│
├── bitcoin_trumpcoin_anomaly_detection.ipynb   # Notebook principal
├── DOCUMENTATION.md                             # Esta documentação
│
├── grafico1_preco_anomalias.png                # Visualização Bitcoin
├── grafico2_volume.png                          # Volume Bitcoin
├── grafico3_rsi.png                             # RSI Bitcoin
├── grafico4_comparacao.png                      # Comparação Bitcoin
├── grafico5_distribuicao_anomalias.png         # Distribuição Bitcoin
│
├── trump_grafico1_serie_temporal.png           # Visualização TrumpCoin
├── trump_grafico2_comparacao.png               # Comparação TrumpCoin
└── trump_grafico3_distribuicao.png             # Distribuição TrumpCoin
```

## 🛠️ Dependências

```python
# Manipulação de dados
pandas
numpy

# Visualização
matplotlib
seaborn

# Machine Learning
scikit-learn

# Dados financeiros
yfinance

# Avisos
warnings
```

### Instalação

```bash
pip install pandas numpy matplotlib seaborn scikit-learn yfinance
```

## 🚀 Como Executar

1. **Clone o repositório** ou baixe os arquivos
2. **Abra o notebook** `bitcoin_trumpcoin_anomaly_detection.ipynb`
3. **Execute as células sequencialmente** (Shift + Enter)
4. **Aguarde o download dos dados** via Yahoo Finance
5. **Visualize os resultados** e gráficos gerados

## 📝 Observações Importantes

1. **Labels Sintéticos**: Os rótulos de anomalia são criados algoritmicamente, não representam eventos reais confirmados
2. **Dados em Tempo Real**: Os dados são baixados na execução, podendo variar entre execuções
3. **Interpretação**: Os resultados devem ser interpretados como indicativos, não como verdade absoluta
4. **Memecoin**: O TrumpCoin apresenta volatilidade extrema por ser uma memecoin política