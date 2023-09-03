---
layout: essay
type: essay
title:  Naive Bayes
# All dates must be YYYY-MM-DD format!
date: 2019-09-08
labels:
  - Naive Bayes
  - Classificação
  - Aprender ensinando
---

## Conceito

<p>O algoritmo Naive Bayes, como o próprio nome sugere, é baseado no teorema de Bayes. Ele é amplamente utilizado para classificar texto com base na ocorrência de palavras ou para prever um fenômeno com base em outros fatores.</p>
<p>O Naive Bayes nos fornece a probabilidade de um fenômeno ocorrer, dado que outro fenômeno já ocorreu, como, por exemplo, a probabilidade de haver trânsito dado que está chovendo, ou dado que está ensolarado, e assim por diante.</p>
<p>Aqui está a fórmula do teorema:</p> 
<img class="ui medium fluid image" src="../images/Naive_formula.png">
Ela nos dá a probabilidade de ocorrer o evento B, dado que ocorreu o evento A.

<p>Para calcular isso, multiplicamos a probabilidade de ocorrer o evento A dado o evento B pela probabilidade de ocorrer o evento A e, em seguida, dividimos essa multiplicação pela probabilidade de ocorrer o evento B.</p>
<p>Vamos usar um exemplo com o tempo e o trânsito para calcular a probabilidade de ter trânsito quando está chovendo.</p>
<img class="ui medium fluid image" src="../images/tab_freq.png">
<p>Nesta tabela, temos a frequência de ocorrências de trânsito quando choveu e quando fez sol. Para responder à pergunta, primeiro calculamos a probabilidade de chover quando há trânsito, em seguida a probabilidade de chover e, por fim, a probabilidade de ter trânsito.</p>
Aqui estão os valores calculados:
* Total de frequências medidas: 27
* P(B|A): 8/14 = 0.571
* P(A): 11/27 = 0.407
* P(B): 14/27 = 0.518

<p>Portanto, a probabilidade de haver trânsito quando está chovendo (P(A|B)) é (0.571 * 0.407) / 0.518 = 0.449 ou 44,9%.</p>
<p>Este é um exemplo fictício, mas para quem mora em São Paulo, o trânsito é uma realidade constante.</p>

