# Modelismo Pratico

Este projeto aborda o processo de modelagem de regressão para estimar os preços de imóveis na california/USA.
Serão utilizadas técnicas de machine learning para treinar modelos preditivos e avaliar seu desempenho.

O objetivo é fornecer um material detalhado sobre as etapas envolvidas na construção, treinamento, avaliação e otimização de modelos de regressão.

# Conjunto de Dados

O conjunto de dados usado foi California housing dataset.
O banco de dados original está disponível em StatLib

http://lib.stat.cmu.edu/datasets/

Os dados contêm 20.640 observações em 9 variáveis.

Este conjunto de dados contém o valor médio da casa como variável-alvo
e as seguintes variáveis ​​de entrada (características): renda média,
idade média da habitação, quartos médios, quartos médios, população,
ocupação média, latitude e longitude nessa ordem.

Referências
----------

Pace, R. Kelley e Ronald Barry, Sparse Spatial Autoregressions,
Statistics and Probability Letters, 33 (1997) 291-297.

# Seleção das Técnicas de Modelagem

As técnicas de modelagem selecionadas para treinar os modelos de regressão foram:


1. Regressão Linear: modelo linear simples do Scikit-Learn
2. Support Vector Regression (SVR): modelo de regressão baseado em Support Vector Machines
3. Decision Tree Regression: modelo de árvore de decisão para regressão do XGBoost

# Pressupostos dos Modelos

Alguns pressupostos e limitações das técnicas selecionadas:


Aceitam apenas variáveis numéricas como entrada
Não trabalham nativamente com dados categóricos
Podem ter problemas com outliers 

# Separação entre Conjuntos de Treino e Teste

Foi utilizada uma separação padrão entre conjuntos de treino e teste, com 20% da massa de dados destinada ao conjunto de teste.

A separação foi feita de forma aleatória utilizando a função traintestsplit do Scikit-Learn, passando uma semente aleatória (random state) para garantir a reprodutibilidade do resultado.

Dessa forma, temos:


Xtrain, Ytrain: conjuntos de treino
Xtest, Ytest: conjuntos de teste

O modelo será treinado no conjunto de treino e depois avaliado no conjunto de teste. Isso evita overfitting e permite avaliar se o modelo se generaliza bem para dados nunca vistos antes.


# Métricas de Avaliação

Para avaliar o desempenho dos modelos, serão utilizadas as métricas:


Mean Squared Error (MSE): mede a média do quadrado das diferenças entre os valores previstos e os valores reais. Penaliza mais erros grandes de previsão.

Root Mean Squared Error (RMSE): raiz quadrada do MSE. Facilita a interpretação dos erros em unidades da variável alvo.


O objetivo é minimizar o MSE e RMSE, buscando modelos com erros de previsão menores possíveis.

# Treinamento do Modelo Linear

O primeiro modelo implementado foi uma Regressão Linear simples utilizando a biblioteca scikit-learn. O modelo foi instanciado com os parâmetros padrão e treinado nos dados de treino com o método .fit().

Em seguida, o modelo treinado foi utilizado para fazer previsões nos dados de teste com o método .predict(). As previsões foram comparadas aos valores reais de preço das casas no conjunto de teste para avaliar a performance.

O MSE obtido pela Regressão Linear foi de 0.5558915986952422 e o RMSE de 0.7455813830127749.

# Treinamento do Modelo SVR

O segundo modelo implementado foi um Support Vector Regressor (SVR) também da biblioteca scikit-learn. Foi realizado o mesmo processo: instanciação padrão, treinamento com .fit() e previsões no conjunto de teste com .predict().

O MSE do SVR foi maior: 1.3320115421348744. Consequentemente, o RMSE também foi pior: 1.1541280440812771.

# Treinamento do Modelo XGBoost

Por fim, foi implementado um modelo de Regressão por Árvores de Decisão usando o algoritmo XGBoost. Novamente o mesmo processo de treino e previsões.

O XGBoost obteve o melhor desempenho dentre os modelos, com MSE de 0.2225899267544737 e RMSE de 0.4717943691423984. Significativamente menor que os demais.

# Conclusão

Após avaliação das métricas de erro MSE e RMSE nos dados de teste, o modelo XGBoost Regressor obteve o melhor desempenho para a tarefa de previsão dos preços dos imóveis em Boston.

O XGBoost será otimizado em próximos passos ajustando seus hiperparâmetros para tentar reduzir ainda mais o erro das previsões e melhorar a performance. O modelo final será implementado em produção.

As etapas realizadas incluíram:


Seleção das técnicas de modelagem
Separação dos dados em treino e teste
Definição das métricas de avaliação
Treinamento dos três modelos candidatos
Previsões no conjunto de teste
Cálculo de MSE e RMSE
Comparação do erro médio de cada modelo
Seleção do melhor modelo (XGBoost)

# Hiperparametros 

Apos a escolha do modelo decidi fazer alguns testes de parametro para otimizar a modelagem
os melhores paramentor foram:
{'booster': 'gbtree',
 'gamma': 0,
 'learning_rate': 0.2,
 'max_delta_step': 1,
 'max_depth': 7,
 'min_child_weight': 1,
 'n_jobs': 5,
 'objective': 'reg:squarederror',
 'subsample': 1}

com estes paramentros alcancei MSE de 0.21638147438949515 e um RMSE de 0.4651682216032122, um desempenho significativo em relação ao defaut 
