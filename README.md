# <p align="center"> Rossmann Store -  Previsão de Vendas  </p>
![](img/rossmann_logo.png)

## 1. Problema de Negócio:

A Rossmann é uma das maiores redes de drogarias da Europa. Atualmente possui mais de 56000 funcionarios em mais de 4000 lojas.

O CFO possui a necessidade de reformar as lojas da rede de farmácias, para melhorar a estrutura das lojas e atender melhor o público. Para tanto, ele necessita que os gerentes das lojas enviem a previsão de receita das próximas 6 semanas para que ele provisione o valor que será investido ppor cada loja no processo de reforma.

Atualmente, esses valores são calculados de forma individual, sendo que cada gerente realiza a entrega dessa previsão. Como cada loja possui fatores distintos que influenciam em seus resultados, como promoções, competições por clientes, feriados, sazonalidade e etc, e os cálculos são feitos de forma manual, os resultados variam muito.

Dessa forma, a ideia deste projeto é auxiliar o CFO na tomada de decisão, provendo resultados das previsões de cada loja de forma automática, e possibilitando que o CFO consulte as previsões através de um Bot do aplicativo Telegram.

## 2. Descrição dos dados:

Foi disponibilizada pela empresa os dados dentro da plataforma de competições de dados [Kaggle](https://www.kaggle.com/competitions/rossmann-store-sales/overview). Os dados apresentam 1.017.209 registros das vendas realizadas pelas filias da empresa, contendo 18 características únicas para cada venda realizada conforme listado abaixo:

| Atributo                          | Descrição                                                                                                                                             |
| :-------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Store                             | Identificador único de cada loja                                                                                                                      |
| DayOfWeek                         | Variável numérica que representa o dia da semana                                                                                                                  |
| Date                         		| Data em que ocorreu a venda                                                                                                    |
| Sales                             | Valor de vendas do dia                                                                                                                                |
| Customers                         | Quantidade de clientes na loja no dia                                                                                                                 |
| Open                              | Indicador para loja:  1 = Aberta, 0 = Fechada                                                                                                         |
| Promo                             | Indica se a loja está com alguma promoção ativa no dia                                                                                                |
| StateHoliday                      | Indica se o dia é feriado. (a = Feriado público, b = Feriado de páscoa, c = Natal, 0 = Não há feriado)                                        |
| SchoolHoliday                     | Indica se a loja foi ou não fechada durante o feriado escolar                                                                                         |
| StoreType                         | Indica o modelo de lojas. Pode variar entre a, b, c, d                                                                                                |
| Assortment                        | Indica o nível de variedade de produtos: a = básico, b = extra, c = estendido                                                                         |
| CompetitionDistance               | Distância (em metros) para o concorrente mais próximo                                                                                                  |
| CompetitionOpenSince [Month/Year] | Indica o ano e mês em que o concorrente mais próximo abriu                                                                                             |
| Promo2                            | Indica se a loja deu continuidade na promoção: 0 = não está participando, 1 = participando                                                  |
| Promo2Since [Year/Week]           | Indica o ano e semana de quando a loja começa a promoção extendida                                                                                |
| PromoInterval                     | Indica os meses em que a loja iniciou a promo2, ex.: "Jan,Apr,Jul,Oct" significa que a loja iniciou as promoções estendidas em cada um desses meses |

## 3. Estratégia de Solução:

Para desenvolvimento da solução utilizei um processo de modelagem chamado CRISP-DS. Sua natureza cíclica permite não só o refatoramento do código como também a formulação de outras hipóteses e melhora dos modelos ao longo de cada ciclo.

![](img/ciclo_CRISP_DS.png)


## Passos do CRISP-DS:
1. **Questão de Negócio:** Esta etapa tem como objetivo receber o problema de negócio a ser executado.

2. **Entendimento de Negócio:** Esta etapa concentra-se na compreensão dos objetivos e requisitos do projeto. Entender o problema de uma perspectiva de negócio é fundamental para sucesso do projeto.

3. **Coleta de Dados:** Realizar a coleta dos dados. Para esse projeto foi disponibilizado os dados em formato .CSV.

4. **Limpeza dos Dados:** Esta etapa tem como objetivo remover todo e qualquer dado que não seja relevante para o modelo, tomando o cuidado e entender bem o fenômeno que está sendo estudado para que não sejam removidos dados importantes para a modelagem do problema.

5. **Exploração dos Dados:** Esta etapa tem como objetivo entender os dados e qual a relação entre eles. Normalmente, são criadas hipóteses que posteriormente serão validadas utilizando técnicas de análise de dados. É nessa etapa que sera criadas novas *features* que serão utilizadas na etapa de Modelagem de Dados.

6. **Modelagem dos Dados:** Esta etapa tem como objetivo preparar os dados para que eles sejam utilizados pelos algoritmos de Machine Learning. É nesta etapa que são feitos as transformações e *encodign* dos dados, a fim de facilitar o aprendizado do algoritmo utilizado.

7. **Machine Learning:** Esta etapa tem como objetivo selecionar e aplicar algoritmos de Machine Learning nos dados preparados nas etapas anteriores. Aqui tambem são selecionados os algoritmos e feito a comparação de performance enetre eles, para selecionar o algoritmos que melhor performou como algoritmo final.

8. **Avaliação do Algoritimo:** Esta etapa tem como objetivo verificar a performance do algoritmo selecionado na etapa anterior com os resultados atuais. Neste momento é feito a tradução da performance do algoritmo para perfomance de negócio. Ou seja, quanto a solução criada trará de retorno financeiro para a empresa. Caso a performance seja aceitável, o algoritmo é publicado e entra em produção, caso contrário o mesmo retorna para a etapa de entendimento de negócio para um novo ciclo, a fim de melhorar a performance da solução.

9. **Modelo em produção:** Esta etapa tem como objetivo publicar o algoritmo selecionado, deixando publico e acessível para tomada de decisão.

## 4. EDA Insights

## 1: Lojas deveriam vender mais no segundo semestre do ano

**Hipótese Falsa:** Lojas vendem MENOS no segundo semestre do ano

![](img/insight_2nd_semestre.png)

## 2: Lojas deveriam vender mais depois do dia 10 de cada mês.

**Hipótese Verdadeira:** Lojas vendem MAIS depois do dia 10 de cada mês.

![](img/insight_after10.png)

## 3: Lojas deveriam vender MENOS aos finais de semana.

**Hipótese Verdadeira:** Lojas vendem menos no final de semana

![](img/insight_weekend.png)

# 5. Modelos de Machine Learning

## 5.1 Métrica:

A métrica de avaliação escolhida foi a MAPE (Mean Absolute Percentage Error), que representa a porcentagem do erro em relação ao valor médio.

Na primeira parte da etapa foi realizado a avaliação simples do modelo (Single Performance) onde o modelo Random Forest performou melhor.

## 5.2 Resultados:

###Single Performance:

| Model Name | MAE | MAPE | RMSE |
|  --- | --- | --- | --- |
| Random Forest Regressor | 696.477809 | 0.103411 | 1029.574986 |
| Average Model	 | 1354.800353 | 0.206400 | 1835.135542|
| Linear Regression | 1868.313299|0.292392 | 2674.576594 |
| Linear Regression - Lasso | 1891.704881 | 0.289106| 2744.451737 |
| XGBoost Regressor | 6682.604070 | 0.949328 | 7329.887823 |


Mesmo o modelo XGBoost nao performando com um resultado muito bom em primeiro momento, após a etapa de *Hyperparameter fine tuning* onde foram ajustados os parâmetros, o modelo apresentou bons resultados. A escolha deste modelo tambem foi baseada no tempo de processamento do algoritmo, que é muito menor que o Random Forest, significando redução de custos de processamento e cloud.


### Cross Validation Performance:


| Model Name | MAE | MAPE | RMSE |
|  --- | --- | --- | --- |
| XGBoost Regressor | 632.810733 | 0.091442 | 921.441998 |

# 6. Resultado Final

O resultado final foi muito satisfatório, apenas um pequeno grupo destoou na predição em relação aos demais e precisára de ajustes nos proximos ciclos. A maior parte das lojas tiveram o erro MAPE muito próximo do erro performado no modelo que foi de 9%.

![](img/mape_x_store.png)

Com o modelo selecionado e treinado, as 5 melhores lojas apresentaram a performance abaixo:

| ID da Loja |     Previsões |  Pior Cenário | Melhor Cenário |       MAE |   MAPE |
| :--------- | ------------: | ------------: | -------------: | --------: | -----: |
| 258        | \$ 543.536,00 | \$ 543.043,79 |  \$ 544.028,20| \$ 492,20 | 0.0377 |
| 732        | \$ 631.405,37 | \$ 630.688,45 |  \$ 632.122,29 | \$ 716,92 | 0.0487 |
| 561       | \$ 734.331,18 | \$ 733.445,24 |  \$ 735.217,12 | \$ 885,94| 0.0513 |
| 989       | \$ 230.974,42 | \$ 230.645,26 |  \$ 231.303,57 | \$ 329,15 | 0.0518 |
| 1088        | \$ 391.805,59 | \$ 391.252,36 |  \$ 392.358,81 | \$ 553,22 | 0.0542 |

Como resultado final, temos os seguintes cenários:

| Cenários       |    Valores        |
| :------------- | ----------------: |
| Previsão Feita | \$ 283.242.240,00 |
| Pior Cenário   | \$ 282.532.641,95 |
| Melhor Cenário | \$ 283.951.868,44 |

# 7. Deploy









