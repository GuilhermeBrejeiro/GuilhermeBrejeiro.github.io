---
layout: essay
type: essay
title:  "Função custo: Linear e Logística"
# All dates must be YYYY-MM-DD format!
date: 2019-08-26
labels:
  - Machine Learning
  - Cost Function
  - Aprender ensinando
---



## Função custo

<p> Quando traçamos um gráfico relacionando duas variáveis, geralmente não é possível que uma reta passe por todos os pontos. Portanto, nosso objetivo é encontrar a reta que melhor se ajusta aos dados disponíveis.</p>
<p> Como ilustrado abaixo, podemos observar a distância entre a reta usada para prever um valor e o ponto real correspondente. Essa diferença entre o valor real e o valor previsto é essencial para calcular uma função de custo.</p>

<img class="ui fluid image" src="../images/exe_func_cust.png">

<p>Mas como saber se essa reta é a melhor escolha? Talvez uma ligeira inclinação para baixo resultaria em previsões mais precisas, ou talvez um leve aumento. É aí que entra o conceito do gradiente descendente.</p>

<p> O gradiente descendente representa todas as possíveis retas que poderiam se ajustar ao modelo, uma infinidade delas. Cada uma dessas retas gera um valor de custo, e todos esses valores são usados para criar um novo gráfico.</p>

<p>Exemplo das muitas possibilidades:</p>
<img class="ui fluid image" src="../images/exe_func_cust2.png">

<p>Cada ponto no gráfico resulta da função de custo aplicada a cada reta possível. No ponto mais baixo do gráfico, encontramos a reta que melhor se ajusta ao modelo, representando o mínimo da função de custo. Portanto, usamos o gradiente descendente para encontrar esse ponto.</p>

<img class="ui fluid image" src="../images/exe_func_cust3.png">

<p>A função de custo é usada tanto em regressão linear quanto em regressão logística, seguindo o mesmo conceito, embora com fórmulas diferentes, como mostrado abaixo:</p>

Função de custo para regressão linear
<img class="ui fluid image" src="../images/linear_costfunc.png">
	
Função de custo para regressão logística
<img class="ui fluid image" src="../images/log_costfunc.png">

<p>A diferença entre essas funções ocorre porque, no caso da regressão logística, nossas variáveis de saída são binárias. Se usássemos a função de custo da regressão linear, o gráfico do gradiente descendente seria não convexo, o que resultaria em vários mínimos locais, ocultando o mínimo global desejado.</p>

	




