---
layout: essay
type: essay
title:  Biblioteca Numpy
# All dates must be YYYY-MM-DD format!
date: 2019-12-02
labels:
  - Numpy
  - Bibliotecas ML
  - Aprender ensinando
---


## O que é NumPy?

<p>Quando os modelos matemáticos começaram a demandar um poder computacional muito grande, viu-se a necessidade de uma biblioteca que permitisse trabalhar com arranjos, vetores e matrizes de N dimensões, assim nasceu o NumPy, a principal biblioteca científica do Python e que se equipada com o software proprietário Matlab. NumPy foi implementado em C, por isso sua grande velocidade na realizações das operaçÕes matemáticas.</p>

<p>Para a utilização dessa biblioteca, há a necessidade de instalação. No windows, já com o Python instalado, abra o prompt de comando em modo administrador e digite: </p>

## python -m install numpy

<p>Terminado a instalação, basta fechar o prompt de comando e já é possível utilizar o NumPy junto ao Python, basta utilizar o comando:</p>

## import numpy

<p>Como todas as bibliotecas é possível utilizar um apelido para a mesma, uma boa prática ao utilizar numpy é apelida-lo de np:</p>

## import numpy as np

<p>Com o NumPy importado, já é possível criar arrays, abaixo o exemplo de 1D e 2D:</p>

<p>Nesse exemplo, foi criado uma lista de elementos e em seguida ela foi transformada em um array, com isso ganhamos muitas vantagens para trabalhar com esses números</p>

## baseball = [180, 215, 210, 210, 188, 176, 209, 200]

## np_baseball = np.array(baseball)

<p>Com esse array, trabalhar com elementos matemáticos em cada item se torna muito rápido. No exemplo, é possível ver uma lista multiplicada por um dado número e um array multiplicado por esse número, no segundo caso cada valor é multiplicado</p>

## lista = baseball * 2
## print(lista)
## [180, 215, 210, 210, 188, 176, 209, 200, 180, 215, 210, 210, 188, 176, 209, 200]

## array = np_baseball * 2
## print(array)
## [360 430 420 420 376 352 418 400]






<img class="ui fluid image" src="../images/imagem">
