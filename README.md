# Priorização de Hipóteses e Análise de Teste A/B para Loja Online

Este repositório contém um projeto completo de análise de dados para uma grande loja online, com o objetivo de aumentar a receita. A análise é dividida em duas partes principais: a priorização de um conjunto de hipóteses de marketing e a análise aprofundada dos resultados de um teste A/B.

## 📄 Contexto do Projeto

Em colaboração com o departamento de marketing, foi compilada uma lista de hipóteses para otimizar o desempenho da loja. Este projeto utiliza frameworks de priorização para selecionar as hipóteses mais promissoras e, em seguida, analisa os resultados de um teste A/B para validar o impacto de uma das mudanças implementadas, com o objetivo final de tomar uma decisão de negócio baseada em dados.

## 🗂️ Conjuntos de Dados

A análise utiliza três conjuntos de dados distintos:

1.  **/datasets/hypotheses_us.csv**: Contém 9 hipóteses com suas respectivas pontuações para:
    -   `Reach`: Alcance do usuário (escala de 1 a 10).
    -   `Impact`: Impacto nos usuários (escala de 1 a 10).
    -   `Confidence`: Confiança na hipótese (escala de 1 a 10).
    -   `Effort`: Recursos necessários para o teste (escala de 1 a 10).

2.  **/datasets/orders_us.csv**: Registros de pedidos realizados durante o teste A/B.
    -   `transactionId`, `visitorId`, `date`, `revenue`, `group`.

3.  **/datasets/visits_us.csv**: Registros de visitas diárias ao site durante o teste A/B.
    -   `date`, `group`, `visits`.

## 🛠️ Metodologia e Etapas da Análise

O projeto foi estruturado nas seguintes etapas:

### Parte 1: Priorização de Hipóteses
1.  **Framework ICE (Impact, Confidence, Effort)**: As hipóteses foram pontuadas e classificadas com base no seu impacto potencial, confiança na avaliação e esforço de implementação.
2.  **Framework RICE (Reach, Impact, Confidence, Effort)**: Uma segunda priorização foi realizada, adicionando o fator de "Alcance" (Reach) para avaliar quantas pessoas seriam impactadas pela mudança.
3.  **Comparação**: As classificações dos dois frameworks foram comparadas para entender como o alcance do usuário altera a prioridade das hipóteses.

### Parte 2: Análise de Teste A/B
1.  **Pré-processamento de Dados**: Verificação e limpeza dos dados, incluindo a remoção de usuários que foram incorretamente atribuídos a ambos os grupos do teste (A e B).
2.  **Análise de Métricas Cumulativas**: Visualização da performance dos grupos ao longo do tempo através de gráficos de:
    -   Receita acumulada.
    -   Tamanho médio do pedido (Ticket Médio) acumulado.
    -   Diferença relativa no ticket médio acumulado entre os grupos.
    -   Taxa de conversão diária e acumulada.
    -   Diferença relativa na conversão acumulada entre os grupos.
3.  **Análise de Anomalias (Outliers)**: Identificação de valores atípicos através de gráficos de dispersão e cálculo dos percentis 95 e 99 para o número de pedidos por usuário e para os preços dos pedidos.
4.  **Significância Estatística (Dados Brutos)**:
    -   Teste de hipótese (teste Z para proporções) para verificar se a diferença na **conversão** era estatisticamente significativa.
    -   Teste de hipótese não paramétrico (Mann-Whitney U) para verificar a significância na diferença do **tamanho médio do pedido**.
5.  **Significância Estatística (Dados Filtrados)**: Repetição dos testes de significância após a remoção dos usuários e pedidos anômalos para confirmar os resultados sem a influência de outliers.
6.  **Tomada de Decisão**: Com base nos resultados gráficos e estatísticos, foi tomada uma decisão final sobre o teste.

## 📈 Principais Conclusões e Decisão Final

### Priorização de Hipóteses
-   O framework **ICE** priorizou a hipótese 8 ("Lançar uma promoção de aniversário"), que tinha alto impacto e confiança, mas baixo esforço.
-   O framework **RICE** alterou drasticamente a prioridade, com a hipótese 7 ("Adicionar um formulário de assinatura") subindo para o primeiro lugar. Isso ocorreu porque, apesar de um esforço maior, seu **alcance** (Reach) era máximo (10), impactando todos os usuários do site.

### Análise do Teste A/B
-   **Dados Brutos**: Os gráficos de receita e ticket médio acumulado mostraram uma aparente superioridade do Grupo B, mas essa métrica foi fortemente influenciada por pedidos de valores muito altos (outliers).
-   **Dados Filtrados**: Após a remoção de anomalias:
    -   Não houve diferença estatisticamente significativa no **tamanho médio do pedido** entre os grupos A e B (p-value de 0.730).
    -   Houve uma diferença estatisticamente significativa na **taxa de conversão**, com o Grupo B superando o Grupo A em aproximadamente **17.23%** (p-value de 0.0106).

### Decisão Final
-   **Pare o teste, considere o Grupo B o líder.**

**Justificativa**: Embora o tamanho médio do pedido não tenha apresentado uma melhora estatisticamente significativa após a filtragem dos dados, a **taxa de conversão do Grupo B mostrou uma melhora clara, estável e estatisticamente comprovada**. Os gráficos se estabilizaram, indicando que o teste já coletou dados suficientes para uma conclusão confiável. Portanto, a mudança testada no Grupo B foi bem-sucedida em seu objetivo principal de aumentar a conversão.

## 💻 Tecnologias Utilizadas
-   Python 3
-   Pandas
-   NumPy
-   Matplotlib
-   SciPy (stats)
-   Jupyter Notebook

## 🚀 Como Executar o Projeto
1.  Clone este repositório.
2.  Instale as bibliotecas necessárias:
    ```bash
    pip install pandas numpy matplotlib scipy
    ```
3.  Certifique-se de que os arquivos `.csv` estão no diretório `/datasets/` ou ajuste os caminhos no notebook.
4.  Execute o Jupyter Notebook para visualizar a análise completa.
