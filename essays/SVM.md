---
layout: essay
type: essay
title: Máquina de Vetores de Suporte
# All dates must be YYYY-MM-DD format!
date: 2019-11-04
labels:
  - Support Vector Machine
  - SVM
  - Aprender ensinando
---



## O que é?

<p>São modelos de aprendizagem supervisionada que separa os dados por meio da identificação de padrões, utilizado principalmente para casos de classificação.</p> 
  
<img class="ui medium floated right image" src="../images/SVM1.png">

<p> Quando se tem uma boa divisão dos dados, fica muito mais simples separa-los e classifica-los, como mostra o exemplo acima. Mas e se tivessemos um problema que envolvesse a dosagem de um remédio? Não pode ser uma dosagem nem muito alta e nem muito baixa, precisamos da quantidade ideal</p>

<img class="ui medium floated right image" src="../images/SVM2.png">

<p>Nesse tipo de caso, a utilização do SVM com Kernel (que serve como uma equação para aumentar as dimensões dos dados) consegue solucionar o problema, elevando todos os termos ao quadrado, por exemplo, e teriamos uma maneira melhor de separar os dados:</p>


<img class="ui medium floated right image" src="../images/SVM3.png">

<p>Com a utilização do SVM conseguimos criar hiperplanos para separação dos dados, margens que não sofrem influência por outliers e com o truque de Kernel, ainda preservamos poder computacional.</p> 
