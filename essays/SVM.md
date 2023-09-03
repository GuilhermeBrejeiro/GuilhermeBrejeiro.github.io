---
layout: essay
type: essay
title: Máquina de Vetores de Suporte
# All dates must be YYYY-MM-DD format!
date: 2019-10-15
labels:
  - Support Vector Machine
  - SVM
  - Aprender ensinando
---



## O que é?

<p>O SVM (Support Vector Machine) é um modelo de aprendizado supervisionado que separa dados por meio da identificação de padrões, sendo amplamente utilizado para problemas de classificação.</p> 
<img class="ui medium image" src="../images/SVM1.png">
<p>Quando os dados podem ser bem separados, como mostrado no exemplo acima, é relativamente simples classificá-los. No entanto, em casos mais complexos, como aqueles que envolvem a dosagem de um medicamento, a situação fica mais desafiadora. A dosagem não pode ser nem muito alta nem muito baixa; é necessário encontrar a quantidade ideal.</p>
<img class="ui medium image" src="../images/SVM2.png">
<p>Nessas situações, a utilização do SVM com Kernel (que age como uma função para aumentar a dimensionalidade dos dados) pode solucionar o problema. Por exemplo, ele eleva todos os termos ao quadrado, o que resulta em uma melhor separação dos dados:</p>
<img class="ui medium image" src="../images/SVM3.png">
<p>O SVM nos permite criar hiperplanos para a separação dos dados, margens que são menos afetadas por outliers e, com o truque do Kernel, ainda preservamos o poder computacional.</p>
