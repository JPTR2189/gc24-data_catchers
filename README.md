# Análise de Dados do Spotify 🎵

Este projeto utiliza o **Spotify Tracks Dataset** do Kaggle para explorar características de músicas e construir insights relevantes sobre padrões no consumo musical. A análise é feita por meio de ferramentas de ciência de dados e visualizações gráficas para compreender melhor os dados disponíveis.

## 🎯 Objetivo  
O objetivo principal deste projeto é aplicar técnicas de análise de dados para extrair informações relevantes de um dataset do Spotify, além de preparar os dados para possíveis modelos de machine learning no futuro.  

## 📂 Dataset  
O dataset contém características musicais de diversas faixas do Spotify, como duração, energia, acústica, volume, entre outras. Ele está disponível no [Kaggle](https://www.kaggle.com/datasets) e conta com mais de 1000 linhas, sendo perfeito para análises e visualizações.  

### Principais Colunas do Dataset  
- **danceability**: Indica o quão dançante é uma faixa.  
- **energy**: Mede a intensidade e a atividade da faixa.  
- **loudness**: Volume médio da faixa em decibéis.  
- **acousticness**: Probabilidade de a faixa ser acústica.  
- **tempo**: Velocidade da música em batidas por minuto (BPM).  
- **valence**: Indicador de positividade da música.  
- **duration_ms**: Duração da música em milissegundos.  

## 🛠️ Bibliotecas Utilizadas  
Durante o desenvolvimento do projeto, as seguintes bibliotecas foram utilizadas:  
- **pandas**: Para manipulação e análise de dados.  
- **numpy**: Para cálculos matemáticos e estatísticos.  
- **seaborn**: Para visualizações estatísticas elegantes.  
- **matplotlib**: Para criar gráficos personalizados.  
- **plotly.express**: Para visualizações interativas.  

## 🧪 Etapas do Projeto  

### 1. **Carregamento dos Dados**  
Utilizamos o **pandas** para carregar o dataset e verificar as primeiras linhas, colunas e estatísticas descritivas. Isso nos ajudou a entender a estrutura e o conteúdo do dataset.  

### 2. **Análise Exploratória de Dados (EDA)**  
Nesta etapa, criamos visualizações para identificar padrões e relações entre as variáveis. Exemplos de análises realizadas:  
- Gráficos de dispersão para explorar correlações entre características como energia e volume.  
- Histogramas para examinar a distribuição de variáveis como danceability e loudness.  
- Boxplots para detectar possíveis outliers.  

### 3. **Limpeza de Dados**  
Identificamos e tratamos valores ausentes, duplicados e inconsistências no dataset.  

### 4. **Preparação para Modelagem (Futuro)**  
Embora o foco atual seja a análise, preparamos o conjunto de dados para possíveis modelagens no futuro.  

## 📊 Visualizações Criadas  
Aqui estão algumas visualizações feitas durante o projeto:  
- **Gráfico de dispersão (scatter plot)**: Mostra a relação entre energia e volume.  
- **Boxplot**: Ajuda a identificar outliers em variáveis como acousticness.  
- **Histograma**: Examina a distribuição de danceability e valence.  

## 🚀 Próximos Passos  
- Construir um modelo de previsão para identificar padrões em músicas de sucesso.  
- Implementar mais visualizações interativas usando **Plotly**.  
- Explorar a aplicação de técnicas de clustering para segmentação musical.  

## 💡 Conclusão  
Este projeto fornece uma visão inicial sobre as características musicais de faixas do Spotify. Ele demonstra o poder da análise de dados e das visualizações para extrair insights de um dataset complexo, servindo como base para futuros estudos ou modelos preditivos.  

## 📚 Referências  
- Dataset do Spotify: [Kaggle](https://www.kaggle.com/datasets)  
- Documentação das bibliotecas:  
  - [pandas](https://pandas.pydata.org/)  
  - [numpy](https://numpy.org/)  
  - [matplotlib](https://matplotlib.org/)  
  - [seaborn](https://seaborn.pydata.org/)  
  - [plotly](https://plotly.com/python/)  
