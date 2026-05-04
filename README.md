# Análise de Dados: Qualidade de Vinhos Tintos 🍷

Este repositório contém uma análise exploratória detalhada sobre o conjunto de dados **Red Wine Quality** (Cortez et al., 2009). O objetivo principal é entender como as propriedades físico-químicas, como teor alcoólico, acidez e pH, interagem para determinar a qualidade do vinho.

## Visão Geral
A análise foi desenvolvida originalmente em um ambiente Kaggle Notebook, focando na transformação de dados brutos em informações acionáveis através de:
- **Agregações Estatísticas:** Médias e desvios padrão por nível de qualidade.
- **Tabelas Dinâmicas (Pivot Tables):** Resumo de grandes volumes de dados para facilitar a comparação.
- **Normalização (Z-Score):** Ajuste de variáveis para análise comparativa dentro de grupos específicos.
- **Visualização de Dados:** Uso de Boxplots para identificar dispersão e outliers.

## Principais Insights
- **Teor Alcoólico:** Observou-se uma correlação positiva onde vinhos de maior qualidade tendem a apresentar maior teor alcoólico médio.
- **Acidez Cítrica:** Vinhos classificados como "bons" frequentemente apresentam níveis baixos de ácido cítrico.
- **pH e Densidade:** A análise via tabelas dinâmicas permitiu segmentar o pH por faixas de álcool, revelando padrões de estabilidade química.

## Tecnologias Utilizadas
- **Python 3.12**
- **Pandas:** Manipulação e tabelas dinâmicas.
- **Numpy:** Operações matemáticas.
- **Matplotlib / Seaborn:** Visualização de dados.

## Estrutura do Projeto
- `notebooks/`: Contém o arquivo `.ipynb` com o código completo.
- `data/`: Link ou diretório para o dataset original.
- `scripts/`: Funções auxiliares para limpeza e normalização.
