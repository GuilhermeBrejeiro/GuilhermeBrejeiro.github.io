---
layout: essay
type: essay
title:  MLOps - Refatorando o Código para Produção
# All dates must be YYYY-MM-DD format!
date: 2023-02-25
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

No mundo de Machine Learning e Data Sciente, é comum iniciarmos os nossos projetos (e os nossos estudos) em Jupyter Notebooks, eles facilitam a maneira como exploramos os dados e experimentamos os algoritmos, além de manter todas as funções auxiliares em um mesmo espaço, isso pode ser util momentaneamente mas pode se tornar uma verdadeira bagunça. Quando o objetivo é implantar modelos em produção, uma refatoração signficativa se torna necessária. Aqui vamos explorar um pouco sobre a prática de transformar o código de notebooks em código de produção, utilizando boas práticas de desenvolvimento e ferramentas que melhoram a manutenção futura desses códigos e a sua eficiência.

# Da Exploração dos Dados à Produção

Vamos começar com um exemplo prático, baseado em um antigo notebook de um dos meus primeiros passos na área de dados. Se tratava de um projeto de aprovação de cartão de credito (o qual dei uma revisão pois bati o olho e vi que tinha data leaking gritando no código antigo hahaha). No notebook, durante a exploração dos dados, os códigos estariam mais ou menos assim:

```python
# Import pandas e numpy
import pandas as pd
import numpy as np

# Carrega os dados
cc_apps_train = pd.read_csv('cc_approvals_train.csv')

# Substitui '?' por NaN
cc_apps_train = cc_apps_train.replace('?', np.NaN)


# Seleciona apenas colunas numericas
numeric_columns = cc_apps_train.select_dtypes(include=['number'])

# Imputa a média nos valores NaN
c_apps_train[numeric_columns.columns].fillna(cc_apps_train[numeric_columns.columns].mean(), inplace=True)
```

## Refatorando para Produção

Agora, vamos transformar esse código do notebook em um código modularizado, pronto para produção. Utilizaremos classes e funções para tornar o código mais organizado e reutilizável. 

```python
import pickle
import numpy as np
import pandas as pd


class DataPreprocessing:
    """
    Preprocessa os dados substituindo os pontos de interrogação por NaNs, seleciona as colunas
    numericas e inputa a média nos valores nulos.
    """

    def __init__(self):
        """
        Inicializando a classe DataPreprocessing.
        """
        self.numeric_imputation_values = None

    def replace_question_marks(self, data):
        """
        Substitui pontos de interrogação por NaNs.
        """
        return data.replace("?", np.NaN)

    def select_numeric_columns(self, data):
        """
        Seleciona as colunas numericas dos dados
        """
        return data.select_dtypes(include=["number"])

    def calculate_imputation_values(self, data):
        """
        Calcula os valores que serao imputados nos dados
        """
        numeric_columns = self.select_numeric_columns(data)
        self.numeric_imputation_values = {
            col: data[col].mean() for col in numeric_columns.columns
        }
    .....

```

## Fluxo de Produção

Acima coloquei apenas um trecho do código a ser modularizado para dar uma ideia de sua utilização. No fluxo de produção, com esse código refatorado, podemos criar uma pipeline como no exemplo abaixo, que também incluiria a classe FeatureEngineering, criada a partir da refatoração dos códigos do notebook:

```python
from data_preprocessing import DataPreprocessing
from feature_engineering import FeatureEngineering
from utils import load_data

data = load_data('cc_approvals_train.csv')
data_preprocessor = DataPreprocessing()

data = data_preprocessor.replace_question_marks(data)
data = data_preprocessor.calculate_imputation_values(data)

feature_engineer = FeatureEngineering()
data = feature_engineer.one_hot_encode(data)
....

```

## Seguindo o Estilo PEP8

Uma vez que seu código está organizado, a formatação é a próxima prioridade. O PEP8 é o guia de estilo oficial do Python, e aderir a ele melhora a legibilidade do código. Ferramentas como **'pep8'**, **'autopep8'** e **'pylint'** podem ajudar nessa tarefa.

* **'pep8'** verifica se seu código segue as diretrizes do PEP8.
* **'autopep8'** pode corrigir automaticamente muitos problemas de formatação.
* **'pylint'** é uma ferramenta de análise estática que verifica seu código em busca de erros, estilo e conformidade com várias convenções, retornando os pontos a serem melhorados a uma "nota" para o seu código.

## Integração Contínua (CI)

Essas ferramentas de formatação e verificação podem ser incorporadas ao seu fluxo de CI/CD (Integração Contínua/Entrega Contínua). Assim, cada vez que você envia uma alteração ao repositório de código, uma série de verificações automáticas será executada. Se o código não estiver em conformidade com as diretrizes, você será notificado imediatamente.

## Integração com a IDE

Além disso, essas ferramentas podem ser integradas à sua IDE favorita, como o Visual Studio (VS Code). Com essa integração, você pode configurar sua IDE para aplicar automaticamente correções PEP8 ao código conforme você digita ou salva. Isso ajuda a manter um estilo de código consistente e economiza tempo na formatação manual. Dessa forma, você pode se concentrar mais na lógica do código e menos na formatação.

## Conclusão

A transformação do código do notebook em um aplicativo de produção envolve mais do que apenas copiar e colar. A modularização, a aderência ao estilo PEP8 e a integração contínua são componentes essenciais desse processo. Além disso, eles são essenciais para garantir que o modelo de Machine Learning seja confiável e escalável quando chegar à produção.
