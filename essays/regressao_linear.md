---
layout: essay
type: essay
title:  Regressão Linear
# All dates must be YYYY-MM-DD format!
date: 2019-11-04
labels:
  - Regressão Linear
  - Classificação
  - Aprender ensinando
---



## Regressão Linear Simples

<p>Quando precisamos estudar duas variáveis, esse é o tipo de regressão que pode ser utilizada. Nesse modelo, uma variável independente e uma variável dependente podem ser plotadas para identificarmos suas relações e gerarmos uma linha que possa vir a explicar dados futuros, como por exemplo o preço de uma casa e o tamanho, conforme a figura.</p>

<img class="ui medium fluid image" src="../images/Lin_reg_simples.png">

<p>Desse plot nós tiramos a equação da reta e o seu devido erro, que é a distância entre onde de fato está o ponto e a reta desenhada:</p>
<img class="ui small fluid image" src="../images/eq_reta.png">

## Regressão Linear Múltipla

<p>Bastante parecida com a anterior, nessa regressão nós tentamos aumentar a precisão do modelo adicionando outras variáveis que influenciam no valor de saída. Como no exemplo anterior, dificilmente podemos afirmar que o tamanho da casa é o único fator que influência no valor, para melhorarmos a precisão utilizamos a quantidade de cômodos, região, área externa, etc.</p>

<p>Parecida com a fórmula anterior, agora temos outras variáveis influenciando no valor de saída</p>
<img class="ui medium fluid image" src="../images/eq_reta_mult.png">

<p>OBS: Como podemos ver, é possível utilizar n variáveis para prever o nosso modelo, porém não é aconselhável utilizar variáveis colineares, pois isso prejudica o modelo final.</p>
	

	


