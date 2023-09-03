---
layout: essay
type: essay
title: K Nearest Neighbours (KNN)
# All dates must be YYYY-MM-DD format!
date: 2019-09-20
labels:
  - KNN
  - k vizinhos
  - Aprender ensinando
---



## K vizinhos mais próximos

<p>Este algoritmo é usado para encontrar rapidamente o caminho mais curto entre dois pontos, embora nem sempre seja o caminho ideal. Ele utiliza a base de dados de treinamento e a quantidade de vizinhos que o modelo deve considerar para dividir os dados em regiões. Quando fornecemos um novo dado de entrada, ele será atribuído à região mais próxima com base em suas características.</p>
<p>Aqui, podemos ver uma ilustração de como o algoritmo divide os dados em regiões, representadas por quadrados vermelhos e bolinhas azuis. Ao usar esse modelo para prever a categoria do triângulo, com base na quantidade de k vizinhos especificada, o algoritmo mede a distância para k elementos mais próximos e decide em qual categoria o novo elemento se encaixa. Neste caso, ele será atribuído à categoria das bolinhas azuis.</p>
<img class="ui medium fluid image" src="../images/knn_exemplo.png">
<p>Agora, no segundo caso, qual categoria o triângulo pertence?</p>
<p>Bem, isso dependerá da quantidade k que especificarmos. Se escolhermos 1, ele será classificado como uma bolinha azul porque é o elemento mais próximo. Se escolhermos 4, ele será classificado como um quadrado vermelho, pois entre os quatro elementos mais próximos do triângulo, três são quadrados vermelhos.</p>
<img class="ui medium fluid image" src="../images/knn_exemplo2.png">

<p>OBS: A definição do valor de k é arbitrária. Valores baixos podem tornar o modelo mais suscetível a outliers, enquanto valores muito altos podem criar tantas categorias que reduzirão a precisão do modelo. Portanto, a escolha de k deve ser feita com cuidado, considerando a natureza dos dados e o objetivo da análise.
