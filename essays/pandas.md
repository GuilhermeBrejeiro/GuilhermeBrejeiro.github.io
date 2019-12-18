---
layout: essay
type: essay
title:  Biblioteca Pandas
# All dates must be YYYY-MM-DD format!
date: 2019-12-04
labels:
  - Pandas
  - Bibliotecas ML
  - Aprender ensinando
---


## Trabalhando com Pandas 
<p>Uma importante biblioteca do PYthon é o Pandas, com ele é possível importar, manipular e visualizar dados de forma extremamente prática e muitas vezes intuitiva</p>

<p>Como boa prática, ao importar o pandas daremos um apelido para ele:</p>

<img class="ui fluid medium image" src="../images/pandas1.png">

## Series e DataFrame

<p>Os tipos principais de estrutura de dados no Pandas é uma Series, que é como um arranjo unidimensional e um DataFrame, que é uma estrutura bidimensional de dados, parecido com uma planilha no Excel</p>

<img class="ui fluid medium image" src="../images/pandas2.png">

<p>Podemos observar que a primeira coluna de indice veio preenchida com valores sequenciais automaticamente, mas podemos altera-los acrescentando o campo de index</p>

<img class="ui fluid medium image" src="../images/pandas3.png">

## Stats
<p>O Pandas nos fornece diversas facilidades analiticas dos dados, com facilidade podemos ter estátisticas do nosso DataFrame utilizando .describe()</p>

<img class="ui fluid medium image" src="../images/pandas4.png">

## Localizando valor

<p>Duas maneiras bastante comuns de localizar valores em um DataFrame: .loc e .iloc</p>

loc: referenciado pelos rótulos das linhas e colunas
iloc: referenciado pelos indices

<p>No caso abaixo, aplicando ambos de forma a trazer a o mesmo resultado:</p>

<img class="ui fluid medium image" src="../images/pandas5.png">


