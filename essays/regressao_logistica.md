---
layout: essay
type: essay
title:  Classificação
# All dates must be YYYY-MM-DD format!
date: 2019-11-04
labels:
  - Regressão Logística
  - Classificação
  - Aprender ensinando
---


## Regressão Logística

<p>É um modelo usado para problemas de classificação, como explicado anteriormente, nesse tipo de problema nós tentamos
prever uma resposta binária, como um sim ou não, certo ou errado e etc.</p>

<p>E qual o motivo de usar um modelo de regressão logistica ao invés de um modelo de regressão linear?</p>

<p>Variáveis binarias violam as regras da linearidade pois não temos uma resposta explicativa contínua e a regressão linear lida com valores que podem ser superiores a 1 e inferior a 0.</p>

<p>Aplicando uma regressão linear em um conjunto de dados binários, nosso modelo simplesmente não conseguiria prever novas entradas e, se essas entradas fossem baixas, teriamos valores caminhando para o negativo, o que não pode ocorrer.</p>

<img class="ui fluid image" src="../images/reg_lin_fake.png">

<p>Devido a esse problema na utilização de modelos lineares, se faz necessário a utilização de modelos de regressão logística.</p>
<p>Para utiliza-la, será necessário efetuar algumas alterações no modelo linear, como a utilização do sigmoid, uma equação matemática que irá manter todos os valores dentro do range (0,1) e uma função de custo, que irá penalizar o algoritmo dependendo do valor de entrada.</P>

<p>Feita as alterações, o nosso modelo agora consegue prever uma resposta binária, sem ser prejudicado por valores extremamente altos ou baixos que possam vir a aparecer.</p>

<img class="ui fluid image" src="../images/reg_lin_fake2.png">



  
 
