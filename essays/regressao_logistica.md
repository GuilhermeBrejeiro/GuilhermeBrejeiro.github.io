---
layout: essay
type: essay
title:  Classificação
# All dates must be YYYY-MM-DD format!
date: 2019-08-11
labels:
  - Regressão Logística
  - Classificação
  - Aprender ensinando
---


## Regressão Logística

<p>Apesar do nome, este é um modelo usado para resolver problemas de classificação. Como mencionado anteriormente, em problemas de classificação, nosso objetivo é prever uma resposta binária, como sim ou não, certo ou errado, e assim por diante.</p>

<p>E por que usar um modelo de regressão logística em vez de um modelo de regressão linear?</p>

<p>As variáveis binárias não se encaixam nas suposições de linearidade, uma vez que não possuem respostas contínuas, ao contrário da regressão linear, que lida com valores que podem ser superiores a 1 e inferiores a 0.</p>

<p>Ao aplicar uma regressão linear a um conjunto de dados binários, nosso modelo simplesmente não conseguiria prever novas entradas de forma eficaz e, se as entradas fossem baixas, teríamos valores que se aproximariam de números negativos, o que não faz sentido nesse contexto.</p>

<img class="ui fluid image" src="../images/reg_lin_fake.png">

<p>Devido a esse desafio na utilização de modelos lineares, torna-se necessário o uso de modelos de regressão logística.</p>

Nesse caso, algumas modificações são necessárias no modelo linear:
 * A utilização da função sigmoid no teste de hipótese, uma equação que manterá todos os valores dentro do intervalo (0,1). Portanto, valores com percentagens inferiores a 0,5 são atribuídos a 0 e valores com percentagens iguais ou superiores a 0,5 são atribuídos a 1. 
 * A aplicação de uma [função de custo](https://guilhermebrejeiro.github.io/essays/funcao_custo.html), diferente da usada em modelos lineares. Isso ocorre devido à natureza das entradas binárias, que requer um modelo matemático logarítmico, conhecido como entropia cruzada.

<p>Com essas modificações, nosso modelo de regressão logística consegue prever com precisão respostas binárias, sem ser afetado por valores extremamente altos ou baixos que possam surgir nos dados.</p>

<img class="ui fluid image" src="../images/reg_lin_fake2.png">



  
 
