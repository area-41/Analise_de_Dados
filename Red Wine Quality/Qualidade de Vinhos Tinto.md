# Análise de Dados: Qualidade de Vinhos Tintos 🍷

Este [notebook](https://github.com/area-41/Analise_de_Dados/blob/main/notebooks/red-wine-quality.ipynb) contém uma análise exploratória detalhada sobre o conjunto de dados **Red Wine Quality** (Cortez et al., 2009). O objetivo principal é entender como as propriedades físico-químicas, como teor alcoólico, acidez e pH, interagem para determinar a qualidade do vinho.

### Visão Geral
A análise foi desenvolvida originalmente em um ambiente Kaggle Notebook, focando na transformação de dados brutos em informações acionáveis através de:
- **Agregações Estatísticas:** Médias e desvios padrão por nível de qualidade.
- **Tabelas Dinâmicas (Pivot Tables):** Resumo de grandes volumes de dados para facilitar a comparação.
- **Normalização (Z-Score):** Ajuste de variáveis para análise comparativa dentro de grupos específicos.
- **Visualização de Dados:** Uso de Boxplots para identificar dispersão e outliers.

### Principais Insights
- **Teor Alcoólico:** Observou-se uma correlação positiva onde vinhos de maior qualidade tendem a apresentar maior teor alcoólico médio.
- **Acidez Cítrica:** Vinhos classificados como "bons" frequentemente apresentam níveis baixos de ácido cítrico.
- **pH e Densidade:** A análise via tabelas dinâmicas permitiu segmentar o pH por faixas de álcool, revelando padrões de estabilidade química.

  <img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/56222743-d7be-450a-92d8-1e7ca3c9a073" />


## Tecnologias Utilizadas
- **Python 3.12**
- **Pandas:** Manipulação e tabelas dinâmicas.
- **Numpy:** Operações matemáticas.
- **Matplotlib / Seaborn:** Visualização de dados.

### Estrutura do Projeto
- `notebooks/`: Contém o arquivo `.ipynb` com o código completo.
- `data/`: Link ou diretório para o dataset original.
- `scripts/`: Funções auxiliares para limpeza e normalização.


## Resumo Técnico da Análise Exploratória:

### Transformação Categórica: 
Utilizou-se a função pd.cut() para converter variáveis contínuas (como álcool e acidez) em quatro categorias discretas 
(muito baixo, baixo, médio, alto), facilitando a interpretação em contextos industriais.

    labels_4 = ["muito_baixo", "baixo", "médio", "alto"]

    df2 = pd.DataFrame()
    df2["fixed_acidity"] = pd.cut(df["fixed acidity"], bins=4, labels=labels_4)
    df2["volatile_acidity"] = pd.cut(df["volatile acidity"], bins=4, labels=labels_4)
    df2["citric_acid"] = pd.cut(df["citric acid"], bins=4, labels=labels_4)
    df2["chlorides"] = pd.cut(df["chlorides"], bins=4, labels=labels_4)
    df2["free_sulfur_dioxide"] = pd.cut(df["free sulfur dioxide"], bins=4, labels=labels_4)
    df2["total_sulfur_dioxide"] = pd.cut(df["total sulfur dioxide"], bins=4, labels=labels_4)
    df2["density"] = pd.cut(df["density"], bins=4, labels=labels_4)
    df2["pH"] = pd.cut(df["pH"], bins=4, labels=labels_4)
    df2["sulphates"] = pd.cut(df["sulphates"], bins=4, labels=labels_4)
    df2["alcohol"] = pd.cut(df["alcohol"], bins=4, labels=labels_4)
    

### Tratamento de Assimetria: 
Para a variável residual sugar, aplicou-se pd.qcut() (quantis), garantindo uma divisão estatística mais justa devido à alta assimetria dos dados.

    # dados fortemente assimétricas divide por quantis mais justo estatisticamente
    df2["residual_sugar"] = pd.qcut(df["residual sugar"], q=4, labels=labels_4)
    
    df2["quality"] = pd.cut(
        df["quality"],
        bins=[0, 4, 6, 8, 10],
        labels=["ruim", "regular", "bom", "excelente"],
        include_lowest=True
    )

### Engenharia de Atributos: 
Criou-se a métrica normalized_alcohol utilizando Z-score agrupado por qualidade, permitindo identificar o comportamento do álcool de forma relativa dentro de cada categoria de vinho.

    # Cada valor de `alcohol` é transformado em um z-score mas calculado separadamente para cada grupo de `quality`.
    df["normalized_alcohol"] = (
        df.groupby("quality")["alcohol"].transform(lambda x: (x - x.mean())/x.std())
        # df.groupby("quality")["alcohol"].transform(func_z_score)
    )
    
    df[["quality","alcohol","normalized_alcohol"]].head(10)

### Resumo Multidimensional: 
Através de índices hierárquicos (MultiIndex), foi possível cruzar a qualidade final com a contagem de amostras por nível de ácido cítrico, revelando que a maioria dos vinhos de alta qualidade se concentra em níveis específicos desta substância.

    multi2 = df2.groupby(["quality", "citric_acid"], observed=True).agg(
    contagem=("pH", "count")
    )
    
    display(multi2)

<img width="175" height="331" alt="image" src="https://github.com/user-attachments/assets/397c1459-6fe4-44fe-adc3-3ced9e378275" />

