# Relatório
## Introdução
    Este relatório tem como objetivo explorar e analisar o conjunto de dados relacionado ao Spotify© focando nas características das músicas disponíveis na plataforma. O objetivo principal é identificar padrões e insights relevantes sobre os atributos musicais, como energia, "dançabilidade", popularidade, entre outros, que possam auxiliar na compreensão dos fatores que influenciam o sucesso técnico de uma música na plataforma para que assim, futuras músicas a serem lançadas poderão ter uma pequena provisão técnica de seu possível desempenho (lembrando que, além do fator técnico o marketing também influencia diretamente o sucesso do lançamento de uma música).
    
    Os dados foram extraidos do site kaggle no endereço: https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset. E incluem informações detalhadas sobre faixas, como suas propriedades acústicas, métricas de popularidade e características técnicas.
    
    A análise será estruturada em etapas, começando pela exploração inicial dos dados para entender sua composição e qualidade. Em seguida, serão realizados tratamentos de inconsistências, análise de valores ausentes, possíveis estudos para melhor entendimento do conteúdo trabalhado e identificação de outliers. Por fim, será conduzida uma análise exploratória mais profunda, buscando relações entre os atributos e insights sobre padrões gerais de consumo e características de músicas populares.
    
# Objetivos específicos:

* Avaliar a integridade e qualidade do dataset.
* Identificar características predominantes entre músicas populares.
* Explorar relações entre atributos musicais e o nível de popularidade.
* Propor insights e recomendações baseados nos padrões encontrados.
* Este relatório servirá como base para compreender como os atributos musicais influenciam o consumo de músicas no Spotify, fornecendo subsídios para projetos futuros relacionados à análise e recomendação musical.
* Prever quão popular uma música se tornará com base em seus dados técnicos.
* Organizar caso necessário uma lista de melhores músicas para usuários com base em seu gênero.


# Relatório de tarefas dos membros

## Features Criadas : Rafaela

* A Criação das features envolveu calcular a intensidade das músicas, classificando a velocidade (baseada em BPM). Criando as novas features.

* A função calcular_intensidade calcula um valor de intensidade para cada música, com base em duas variáveis: energia(energy) e loudness.

### Ajuste de loudness:
Quando o valor de loudness é menor ou igual a 0, é ajustado o valor para 1. Pois não é possível aplicar o logaritmo de números menores ou iguais a zero, por isso, ajustando para 1, é assegurado que o cálculo funcione para qualquer valor de loudness.

### Cálculo da intensidade:
* Calculei a intensidade multiplicando o valor de energy pelo logaritmo de loudness + 1. Capturando o efeito combinado de quão energéticas e de quão alto são as músicas.
* Usei logaritmo pois ele ajuda a diminuir o impacto de variações muito grandes no valor de loudness, já que a escala logarítmica diminui as diferenças entre números elevados. Isso faz sentido porque o volume percebido (loudness) segue uma escala logarítmica, um aumento de 10 dB no volume percebido não é linear, mas sim uma multiplicação.

* Multiplicação por 100: Após calcular a intensidade, multipliquei o resultado por 100 para escalá-la e torná-la mais legível. Transformando a métrica de intensidade em números maiores e mais fáceis de interpretar.

* Limitação da intensidade A função np.clip(intensidade, 0, 200) fui usada para garantir que os valores de intensidade não ultrapassem os limites de 0 e 200, impedindo que valores extremos ou erros no cálculo de intensidade causem problemas de interpretação..

* Arredondamento: A função round(intensidade) foi utilizada para arredondar a intensidade calculada, deixando o valor final em números inteiros, Torna os valores mais fáceis de ler e interpreta-los,  e evitando valores decimais que não são necessários para esse tipo de métrica.

### Aplicação da função calcular_intensidade ao DataFrame: 
Utilizei o método apply do Pandas para aplicar a função calcular_intensidade em cada linha do DataFrame.  Isso permitiu calcular a intensidade para cada música de forma independente, utilizando os valores de energy e loudness de cada linha (ou música) do seu DataFrame.

### Função classificar_velocidade: 
Essa função classifica o tempo de uma música (em BPM - batidas por minuto) em categorias como "Lento", "Moderado" ou "Rápido". Essa classificação ajudou a categorizar as músicas de acordo com o seu ritmo.
* Lógica de classificação:
    * bpm <= 90: A música é classificada como "Lento".
    * bpm <= 150: A música é classificada como "Moderado".
    * bpm <= 200: A música é classificada como "Rápido".
    * Qualquer valor superior a 200 é classificado como "Desconhecido".
    *    
### Aplicação da função classificar_velocidade:
Apliquei a função classificar_velocidade à coluna tempo do DataFrame, criando uma nova coluna chamada velocidade que classifica cada música com base no seu BPM.

---------------------

## Tratamento e Limpeza dos Dados: João Pedro

### Estrutura do Código

### 1. Importação de Bibliotecas
- Utilização das bibliotecas:
  - pandas: para manipulação de dados.
  - matplotlib e seaborn: para visualização de dados.
  - numpy: para operações matemáticas.

### 2. Leitura e Pré-processamento de Dados
- O dataset foi carregado utilizando pandas.read_csv para transformar o arquivo CSV em um DataFrame.
- Colunas desnecessárias foram removidas e valores ausentes foram tratados com substituição por valores médios ou médias da coluna.
- Conversão de variáveis de data em formato de timestamp e ajuste dos tipos de dados conforme necessário.

### 3. Cálculos Limiar
- Definição de limiares para características específicas:
  - *Danceability*: limiar para separar músicas mais dançantes (valores > 0.7).
  - *Valence*: músicas mais alegres ou tristes (valores < 0.3 para tristes e > 0.7 para alegres).
  - *Energy* e *Loudness*: análise de correlação entre música de alta energia e volume maior.

### 4. Análises e Agrupamentos
- Agrupamento de dados por *gênero musical* utilizando groupby e cálculo das médias de *danceability, **valence, **energy* e *loudness* para cada grupo.
- Aplicação de correlações e criação de gráficos para visualizar padrões e tendências.

### 5. Visualizações
- Gráficos de Barras e Boxplots: comparação de valores de **danceability* e *valence* entre os gêneros.
- Histogramas: distribuição de características como **energy* e *loudness* nas músicas.
- Heatmaps de Correlação: relações entre variáveis como **energy, **loudness* e *acousticness*.

### 6. Identificação de Tendências
- Identificação de tendências gerais como:
  - Gêneros como *forró* e *salsa* apresentaram altos índices de *valence*, indicando características mais alegres e dançantes.
  - Gêneros como *black-metal* e *ambient* com *valence* baixo, refletindo características mais melancólicas.
  - A correlação entre *danceability* e *valence* mostrou que músicas dançantes tendem a ser mais alegres.

### 7. Resultados Específicos por Gênero
- *Anime* e *K-pop*: Gêneros com grande apelo em comunidades globais, com alta popularidade e engajamento.
- *Brazil*: Músicas que representam aspectos culturais locais, com forte identificação e atratividade nacional.
- *Chill*: Gênero associado a músicas mais suaves, com **low energy* e *high acousticness*, ideal para momentos de foco, estudo ou relaxamento.

### 8. Conclusões
- A análise detalhou como características como *energia* e *danceability* estão diretamente relacionadas a emoções como felicidade ou tristeza.
- Gêneros populares como *K-pop, **anime, **salsa* e *forró* apresentaram características de músicas dançantes e alegres.
- A relação entre *acousticness* e *energy* mostrou que músicas acústicas são mais suaves, enquanto músicas de maior energia, como eletrônicas, são mais intensas.

## Calcular estatísticas descritivas (Moda e Desvio Padrão): Anderson e Jean

* Foram convertidas todas as linhas da coluna 'track_genre' usando o encodador 'OneHotEnconder', para que a coluna estivesse preparada para ser usada no processo de treinamento do modelo.

* Foi criado um novo Dataframe contento os valores de moda e desvio-padrão, calculando as estatísticas para todas as colunas do Dataframe.

* Esta análise de estatísticas do conjunto de dados tem foco em duas métricas importante: Moda e Desvio-padrão.

* Moda:
    *A moda de uma coluna é o valor que aparece com maior frequência. Para cada numero, foi identificado o valor mais comum entre os dados. 
* .Desvio-padrão:
    *O Desvio-padrão indica o quão distante os valores de um conjunto de dados estão em relação à média ou valor central, enquanto valores altos indicam grande variações nos dados, os valores baixos indicam dados mais concentrados.

* Está análise proporciona uma visão rápida e objetiva das colunas numéricas do conjunto de dados, permitindo entender as principais tendências como a "Moda" e a variação do "Desvio-Padão" de cada váriavel.
