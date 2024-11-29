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

### Transformação de Colunas
A coluna duration_ms, que representava a duração das músicas em milissegundos, foi convertida para segundos e minutos para facilitar a interpretação dos dados. A coluna original foi removida, pois se tornou redundante.

### Tratamento de Valores Nulos
Foi feita a verificação de valores nulos no dataset e, como foram encontrados poucos registros ausentes, esses valores foram removidos para manter a integridade dos dados.

### Remoção de Gênero Desnecessário
Gêneros de países como "turkey" e "world", além de "sleep", foram removidos, pois eram irrelevantes para a análise. Optou-se por manter apenas os gêneros relevantes, como os do Brasil, Espanha e países latinos.

### Tratamento de Outliers
* Outliers foram identificados e tratados nas colunas de popularidade e duração:

* Popularidade: Foi verificado que 14% das músicas apresentavam popularidade igual a 0. Como esses registros representavam uma pequena parte do dataset e poderiam distorcer as análises, foram removidos.

* Duração: Para a coluna de duração, foram analisadas músicas com menos de 1 minuto e mais de 15 minutos. Como a maioria das músicas dentro de cada gênero seguiam a média de duração esperada (por exemplo, no gênero rock, a maioria das faixas tem entre 3 a 5 minutos), as faixas fora dessa faixa foram descartadas, pois eram consideradas anômalas para o padrão do dataset.

### Verificação de Duplicados
Foram encontrados duplicados em nomes de artistas e álbuns, algo comum em datasets de música. No entanto, optou-se por não remover esses duplicados, já que um artista ou álbum pode aparecer em várias faixas. O que foi removido foram os nomes duplicados de músicas.

### Verificação de Inconsistências
Foi realizada uma verificação minuciosa para garantir que não houvesse inconsistências nos dados (como valores não numéricos em colunas de texto ou valores de texto em colunas numéricas), e não foram encontradas inconsistências desse tipo.

### Análise Estatística
* Após o tratamento dos dados, foi realizada uma análise estatística descritiva para entender melhor a distribuição das variáveis relevantes, como popularidade, duração, e outras métricas relacionadas.

### Análise de Correlação e Visualizações
* Foram feitas visualizações para examinar as relações entre a popularidade das músicas e variáveis como dançabilidade, energia, instrumentalidade, BPM, e valência emocional.

### Insights realizados ao longo do tratamento:
* Duração e Popularidade: Músicas mais curtas tendem a ser mais populares, um padrão observado em plataformas de streaming, onde faixas mais curtas são mais acessíveis e atraem mais ouvintes.
* Valência e Popularidade: Músicas com valência emocional negativa, ou seja, músicas mais tristes, também podem alcançar alta popularidade, especialmente em gêneros como deep house, que combinam batidas dançantes com letras melancólicas.
* Instrumentalidade e Popularidade: Músicas populares geralmente têm menos instrumentalidade, com ênfase em vocais, o que facilita a conexão emocional com o público.
* Danceabilidade e Popularidade: A popularidade não depende exclusivamente da danceabilidade; muitas músicas populares têm índices de danceabilidade moderados (entre 0.5 e 0.7), o que sugere que o público valoriza uma combinação de elementos emocionais e rítmicos.
  
### Considerações Finais sobre Outliers
* A análise de outliers foi crucial para garantir a qualidade dos dados. Músicas com 0 de popularidade e aquelas com duração abaixo de 1 minuto ou acima de 15 minutos foram removidas, pois não seguiam os padrões esperados para cada gênero musical. Essas decisões foram baseadas em análises detalhadas das distribuições de duração e popularidade, o que ajudou a refinar o dataset e garantir que as análises subsequentes fossem representativas do comportamento real do público nas plataformas de streaming.
