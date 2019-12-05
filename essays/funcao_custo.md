---
layout: essay
type: essay
title:  "Função custo: Linear e Logística"
# All dates must be YYYY-MM-DD format!
date: 2019-11-04
labels:
  - Machine Learning
  - Cost Function
  - Aprender ensinando
---



## Função custo

<p> Em um gráfico correlacionando duas variaveis, a reta não cortará todos os pontos. Portanto, o objetivo será acertar o máximo possivel com a reta escolhida.</p>
<p> Conforme a ilustração a seguir, podemos ver a distância entre a reta utilizada para prever o valor e o ponto que de fato era o valor, essa diferença entre o valor real e o valor previsto é utilizada para o cálculo de uma função de custo.</p>

<img class="ui fluid image" src="../images/exe_func_cust.png">

<p>Mas como saber se essa reta é a ideal? Talvez um pouco mais pra baixo ela me desse um valor mais próximo do real para todas as medições, talvez um pouco mais pra cima, como descobrir? É ai que entra o gradiente descendente</p>

<p> O gradiente descendente é formado por cada possível linha que se encaixaria no modelo, todas as inumeras possibilidades. Cada uma das linhas gera um custo e com todos esses valores plotamos um novo gráfico.</p>

<p>Exemplo de inúmeras possibilidades</p>
<img class="ui fluid image" src="../images/exe_func_cust2.png">

<p>Os valores de erro de inúmeras possibilidades, no seu ponto mais baixo está o valor que representa a reta da função com o melhor acerto do modelo, portanto utilizamos o gradiente descendente para encontrar esse ponto</p>

<img class="ui fluid image" src="../images/exe_func_cust3.png">


