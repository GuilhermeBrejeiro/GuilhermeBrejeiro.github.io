---
layout: essay
type: essay
title: K Means
# All dates must be YYYY-MM-DD format!
date: 2019-10-04
labels:
  - Kmeans
  - Agrupamento
  - Aprender ensinando
---



## Agrupamento não supervisionado

<p>Este é um algoritmo não supervisionado, o que significa que fornecemos a base de dados sem rótulos e o algoritmo se organiza automaticamente, levando em consideração as similaridades entre os dados e a quantidade de k especificada.</p>
<p>Na imagem abaixo, o valor escolhido para k é igual a 3. Inicialmente, três pontos são escolhidos aleatoriamente e, em seguida, os pontos mais próximos vão sendo assimilados por esses pontos iniciais (centros dos clusters), ao mesmo tempo em que o centro de cada cluster se move. No final, os itens do conjunto de dados são agrupados em categorias com base em sua proximidade com esses centros de cluster, e os centros se estabilizam, prontos para lidar com novos dados de entrada.</p>
<img class="ui large image" src="../images/kmeans.png">
