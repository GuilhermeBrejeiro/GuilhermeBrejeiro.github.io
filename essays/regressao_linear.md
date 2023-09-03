---
layout: essay
type: essay
title:  Regressão Linear
# All dates must be YYYY-MM-DD format!
date: 2019-08-19
labels:
  - Regressão Linear
  - Classificação
  - Aprender ensinando
---



## Regressão Linear Simples

<p>Quando precisamos analisar a relação entre duas variáveis, a regressão linear simples é o tipo de modelo apropriado. Neste modelo, uma variável independente e uma variável dependente são plotadas para identificar sua relação e gerar uma linha que pode ser usada para prever dados futuros, como o preço de uma casa em relação ao seu tamanho, conforme ilustrado na figura abaixo:</p>

<img class="ui medium fluid image" src="../images/Lin_reg_simples.png">

<p>A partir desse gráfico, podemos derivar a equação da linha e a correspondente medida de erro, que representa a distância entre os pontos reais e a linha ajustada:</p>
<img class="ui small fluid image" src="../images/eq_reta.png">

## Regressão Linear Múltipla

<p>A regressão linear múltipla é bastante semelhante à regressão linear simples, mas busca aumentar a precisão do modelo ao incorporar várias variáveis que afetam a variável de saída. No exemplo anterior, é improvável que o tamanho da casa seja o único fator a influenciar o preço. Para melhorar a precisão, podemos incluir variáveis como o número de cômodos, a localização, a área externa, entre outras.</p>

<p>A fórmula é semelhante à da regressão linear simples, mas agora incorpora várias variáveis que afetam a variável de saída:</p>
<img class="ui medium fluid image" src="../images/eq_reta_mult.png">

<p>OBS: É importante observar que é possível usar várias variáveis para prever o modelo, mas não é aconselhável incluir variáveis colineares, pois isso pode prejudicar a qualidade do modelo final.</p>
	

	


