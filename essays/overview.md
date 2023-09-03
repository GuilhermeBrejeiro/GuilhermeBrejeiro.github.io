---
layout: essay
type: essay
title:  "ML: Classificação, Regressão Linear e Clusterização"
# All dates must be YYYY-MM-DD format!
date: 2019-08-10
labels:
  - Machine Learning
  - Modelos
  - Aprender ensinando
---



## Processo de Classificação

<p> O processo de classificação tem como objetivo identificar a categoria à qual uma nova entrada de dados pertence, com base em um conjunto de dados históricos.</p> 
<p>Um exemplo comum é o classificador de spam, que, com base em registros anteriores contendo palavras-chave frequentemente usadas em e-mails de spam, categoriza novos e-mails como spam ou não spam.</p>

<img class="ui fluid rounded image" src="../images/email_spam.jpg">



## Processo de Regressão

<p> Ao contrário da classificação, no processo de regressão, o objetivo é prever comportamentos futuros com base em critérios conhecidos. Um exemplo seria prever a demanda por guarda-chuvas com base na quantidade de chuva, permitindo uma melhor organização do estoque e pedidos.</p>
<br>
<img class="ui fluid rounded image" src="../images/guardachuva_nivel.png">
<br>
<p>No exemplo acima, abordamos um modelo de Regressão Linear Simples, mas existem modelos mais complexos, como Regressão Linear Múltipla e Regressão Logística, que exploraremos em futuras postagens.</p>
  
## Correlação entre Variáveis

<p>Para determinar se duas variáveis estão correlacionadas, basta plotar um gráfico e, de forma intuitiva, é possível identificar padrões.</p>

Na imagem a seguir, da direita para a esquerda, apresentamos exemplos de: 
  * Forte correlação positiva
  * Forte correlação negativa
  * Correlação positiva moderada
  * Correlação negativa moderada 
  * Ausência de correlação
  
 
<img class="ui fluid rounded image" src="../images/correlacoes.png">
  
  
  
## Correlação não Implica Causalidade

<p> Uma máxima na estatística é que "Correlação não implica causalidade", o que significa que não podemos tirar conclusões definitivas com base apenas em correlações. É aqui que o conhecimento de domínio desempenha um papel crucial.</p>
<p>Um exemplo clássico é a relação entre o consumo de chocolate e o número de prêmios Nobel por país.</p>

<p>O que não foi considerado e passou despercebido foram outras variáveis importantes. Por exemplo, o fato de que existe uma correlação entre a quantidade de chocolate consumida e o número de prêmios Nobel pode ser influenciado por outros fatores, como o nível de renda, o grau de educação e o poder aquisitivo das pessoas para comprar chocolate. Além disso, o tamanho do país desempenha um papel significativo, uma vez que os EUA têm uma produção científica muito alta, mas também uma população muito maior em comparação com a Noruega. Isso exemplifica a importância de compreender o contexto e as nuances do cenário em que os dados são analisados.</p>
<br>
<img class="ui fluid rounded image" src="../images/grafico_choco.jpg">
<br>

<p> Outro exemplo bizarro é a aparente relação entre o número de filmes de Nicolas Cage e as mortes por afogamento em piscinas.</p>
<br>
<img class="ui fluid rounded image" src="../images/nicolascage.jpeg">
<br>

## Processo de Clusterização

<p> Na aprendizagem não supervisionada, temos o processo de clusterização. Nesse caso, os algoritmos procuram características semelhantes e agrupam os dados em pequenos grupos, sendo o número de grupos um parâmetro que precisa ser especificado manualmente.</p>

<p>Para ilustrar, considere a organização de produtos em um supermercado, que pode ser feita com base em diferentes critérios, como preço, marca, uso, data de validade, cor, etc.</p>

Alguns métodos comuns de clusterização incluem:

* Baseado no centróide
* Baseado na conectividade
* Baseado na densidade
* Baseado em métodos probabilísticos

	
<img class="ui fluid rounded image" src="../images/clustering_example.png">


  
  
  	


