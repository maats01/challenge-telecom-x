# challenge-telecom-x
<a href="https://colab.research.google.com/github/maats01/challenge-telecom-x/blob/main/TelecomX_BR.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a>

### 1. Introdução

A empresa Telecom X está sofrendo com uma alta evasão de clientes (*Churn*), por conta disso foi realizada essa análise para tentar descobrir as possíveis razões disso, para resolver esse problema.

### 2. Limpeza e tratamento de dados

Os dados foram importados via *API* e processados utilizando a biblioteca `pandas` do **Python**.
- Os dados estavam originalmente em formato `json`, portanto foi utilizado o método `read_json` para importar a base de dados para o *notebook*.
- A estrutura da base de dados era composta por chaves e valores aninhados, portanto foi utilizado o método `json_normalize` para normalizar essas colunas que tinham valores aninhados e transformá-las em colunas únicas.
- Foi realizada a checagem de valores vazios, nulos, duplicados e de valores únicos nas colunas categóricas.
  - Com essa checagem, foi identificado que a coluna `Churn` possuia alguns registros vazios e que a coluna `Charges.Total` não estava com o tipo `float64`, que seria o tipo de dado adequado para ela, pois se trata de uma coluna numérica.
  - Os registros onde a coluna `Churn` era vazia foram eliminados do *dataset* pois eram pouquíssimos valores.
  - Na coluna `Charges.Total`, foi identificado que quando ela era vazia, era por causa da coluna `tenure` zerada (o que implica que aquele cliente ainda estava no primeiro mês de contrato). Portanto, os valores vazios foram substituidos por zero e a coluna foi convertida para `float64`.
- As colunas e os dados categóricos foram traduzidas para o português, para padronizar o *dataframe* e ajudar na visualização dos gráficos na etapa de análise exploratória de dados.

### 3. Análise exploratória de dados

Durante a análise exploratória de dados, foram gerados certos tipos de gráficos, para ajudar melhor na visualização do problema e gerar insights, como:
- Gráfico de linha
- Histograma
- Gráfico de barras
- Boxplot

Alguns exemplos:

<img src="https://github.com/maats01/challenge-telecom-x/blob/main/assets/distribuicao_evasao_clientes.png?raw=true" width="50%">

<img src="https://github.com/maats01/challenge-telecom-x/blob/main/assets/histograma_evasao_clientes.png?raw=true" width="90%">

<img src="https://github.com/maats01/challenge-telecom-x/blob/main/assets/evasoes_por_tipo_contrato.png?raw=true" width="45%">

<img src="https://github.com/maats01/challenge-telecom-x/blob/main/assets/taxa_churn_por_tempo.png?raw=true" width="60%">

<img src="https://github.com/maats01/challenge-telecom-x/blob/main/assets/boxplot_gasto_diario.png?raw=true" width="60%">

### 4. Conclusões e insights

- A Telecom X está com um problema em manter novos clientes:
  - **61.99%** dos novos clientes cancelaram o contrato com a Telecom X, no seu primeiro mês. No sexto mês de contrato, a taxa foi consideravelmente menor, porém ainda elevada, de **36.36%**.
  - A tendência da taxa é diminuir conforme o tempo, atingindo valores como **1.66%** em clientes com 72 meses de contrato. Entretanto, na maior parte do tempo, a taxa é superior a **10%**.
- O gasto diário diário dos clientes que cancelaram é consideravelmente maior do que o gasto dos clientes que permaneceram, implicando que talvez o serviço esteja muito custoso para esses clientes.
- A maioria das evasões ocorreram em clientes com o tipo de contrato mensal:
  - Dos 1869 clientes que cancelaram o contrato, 1655 deles possuiam um contrato mensal com a Telecom X, o que corresponde a **88.5%** de todos os cancelamentos.
  - Combinando isso com o fato do gasto diário superior dos clientes que cancelaram, é possível que um dos motivos de cancelamento seja o custo mensal elevado do contrato dos serviços da Telecom X no modelo de contrato mensal.
 
### 5. Recomendações

**Curto prazo:**
- Solicitar um *feedback* dos clientes que cancelaram, para tentar entender com mais precisão o motivo do cancelamento.
- Considerar reavaliar o contrato mensal, pois **88.5%** dos cancelamentos ocorreram com clientes que estavam sob esse formato de contrato.
- Considerar adicionar novas formas contratuais, como trimestrais e semestrais.

**Médio prazo:**
- Solicitar com frequência um *feedback* dos clientes atuais, para obter mais informações referente a qualidade dos serviços prestados, pois a taxa de cancelamento referente aos serviços de fibra óptica e serviços telefônicos no geral é alta.
