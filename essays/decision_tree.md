---
layout: essay
type: essay
title: Árvore de decisão e Floresta aleatória
# All dates must be YYYY-MM-DD format!
date: 2019-11-04
labels:
  - Decision Tree
  - Random Tree
  - Aprender ensinando
---



## Árvore de decisão, o que é?

<p>Árvore de decisão possue um principio bastante simples, dado certas regras e condições, ela vai por um certo caminho, partindo de sua raíz até chegar em suas folhas. Podem ser usadas tanto para classificação quanto regressão</p>

<p>Na figura abaixo podemos ver um exemplo de seu funcionamento, partindo da raíz do problema até suas folhas, pois a arvore de fato fica de cabeça para baixo</p> 
<img class="ui fluid image" src="../images/decision_tree.png">

<p>Uma arvore de decisão pode ter infinitos ramos, dependendo do problema em questão. Por isso, tambem é necessario limitar essa quantidade  de complexidade, para evitar que o modelo fique sobreajustado (overfitting), isto é, que aprenda tanto com a base de dados e suas peculiariedades ao ponto de não conseguir prever novos dados de entrada (é como decorar as respostas de uma prova e não ter aprendido a matéria, de fato). </p> 

## Floresta aleatória

<p>Árvores de decisão são faceis de criar, faceis de usar e faceis de interpretar, o grande problema é que elas possuem uma acuracia ruim, isto é, elas não trabalham bem com novos dados e trabalhar bem com dados já existentes não é algo realmente útil. É ai que entra a floresta aleatória, que como o nome indica, é formada por diversas árvores de decisão. </p>
	

<p> A floresta aleatória combina a simplicidade da árvore de decisão com um grande aumento de acuracia proporcionada pela floresta de árvores. Para sua construção, cada árvore é formada por variaveis escolhidas de forma aleatória e combinadas umas com as outras.</p>
<p>Imagine que, agora, com uma grande quantidade de árvores prevendo novas entradas de valores, mesmo que algumas errem a predição, o resultado final terá um numero de acertos muito maior.</p>

<img class="ui fluid image" src="../images/random_forest.png">


	
	

