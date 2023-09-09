---
layout: essay
type: essay
title:  MLOps - Testes Unitários em Projetos de Machine Learning
# All dates must be YYYY-MM-DD format!
date: 2023-03-10
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Anteriormente, falei sobre o conceito dos testes unitários e sua importância no desenvolvimento de projetos de Machine Learning. Agora, vamos aprofundar ainda mais nesse tópico fundamental, desde a sua criação até a execução de testes unitários especificos para tarefas comuns de pré-processamento e engenharia de recursos (feature engineering). Para isso, será utilizado a biblioteca de testes do Python chamada pytest.

## Importância dos Testes Unitários

Como dito anteriormente, os testes unitários focam na verificação dos componentes individuais do código, visando garantir que cada parte do sistema funcione conforme o esperado quando isolada das outras partes do sistema. Alguns dos motivos de serem essenciais em projeto de MLOps:

* **Qualidade do Código:** Testes unitários ajudam a garantir que seu código funcione corretamente e produza resultados consistentes.
* **Manutenção Simplificada:** Eles facilitam a identificação de erros e problemas à medida que o código evolui
* **Confiança no Modelo:** Testar partes cruciais do pipeline de Machine Learning aumenta a confiabilidade do modelo em produção.

## Testes Unitários em Pré-Processamento

Vamos começar com exemplos de testes unitários para tarefas de pré-processamento de dados. Supondo que tenha sido criado anteriormente a classe **'DataPreprocessing'** que realiza operações como substituir valores ausentes e normalizar dados. Para testar essa classe, podemos criar um caso de teste com o pytest.

```python
import pytest
import pandas as pd
from data_preprocessing import DataPreprocessing

def test_replace_question_marks():
  """
  Testa a substituição do '?' por NaN.
  """
  # Caso de teste: Substituicao de '?' por NaN
  data = pd.DataFrame({'col1': ['?', 'x', 'y']})
  dp = DataPreprocessing()

  # Executa a função de pré-processamento
  result = dp.replace_question_marks(data)

  # Resultado esperado após o pré-processamento
  expected = pd.DataFrame({'col1': [np.nan, 'x', 'y']})

  # Verifica se o resultado é igual ao esperado
  assert result.equals(expected), "Falha no teste test_replace_question_marks"

def test_normalize_data():
  """
  Testa a normalização de dados.
  """
  # Caso de teste: Normalização de dados
  data = pd.DataFrame({'col1': [1,2,3,4,5]})
  dp = DataPreprocessing()

  # Executa a função de normalização
  result = dp.normalize_data(data)

  # Resultado esperado após a normalização
  expected = pd.DataFrame({'col1': [0.0, 0.25, 0.5, 0.75, 1.0]})

# Verifica se o resultado é igual ao esperado
  assert result.equals(expected), "Falha no teste test_normalize_data"
```


## Testes Unitários em Engenharia de Recursos

Agora, vamos explorar testes para engenharia de recursos (feature engineering). Supondo a classe **'FeatureEngineering'** que realiza a codificação de recursos categóricos e escalonamento de recursos numéricos. Os testes ficariam dessa maneira:

```python
import pytest
import pandas as pd
from feature_engineering import FeatureEngineering

def test_encode_categorical_features():
  """
  Testa a codificação de recursos categóricos
  """
  # Caso de teste: Codificação de recursos categóricos
  data = pd.DataFrame({'col1': ['A', 'B', 'A', 'C']})
  fe = FeatureEngineering()

  # Executa a função de codificação categorica
  result = fe.encode_categorical_features(data)

  # Resultado esperado após a codificação
  expected = pd.DataFrame({'col1': [0, 1, 0, 2]})

  # Verifica se o resultado é igual ao esperado
  assert result.equals(expected), "Falha no teste test_encode_categorical_features"

def test_scale_numeric_features():
  """
  Testa o escalonamento
  """
  # Caso de teste: Escalonamento de recursos numéricos
  data = pd.DataFrame({'col1': [1, 2, 3, 4, 5]})
  fe = FeatureEngineering()

  # Executa o escalonamento 
  result = fe.scale_numeric_features(data)

  # Resultado esperado após o escalonamento
  expected = pd.DataFrame({'col1': [0.0, 0.25, 0.5, 0.75, 1.0]})

  # Verifica se o resultado é igual ao esperado
  assert result.equals(expected), "Falha no teste test_scale_numeric_features"
```

## Assert

Como é possível visualizar nos códigos e comentários, basicamente é fornecida uma "prova" para a função responder e em seguida nós comparamos o resultado dela com o "gabarito".

## Testes de Unidade

Além dos testes que verificam se a função retornou os valores corretos, existem outros tipos de testes unitários que pode ser úteis, como os testes que verificam a estrutura ou características especificas dos dados, como a quantidade de colunas, tipos de dados, valores padrão, entre outros. 

Por exemplo, se você tem uma função que retorna um DataFrame após realizar um pré-processamento de dados, você pode querer criar testes unitários para verificar se:

1. O DataFrame retornado tem o número correto de colunas
2. As colunas têm os tipos de dados esperados

```python
import pandas as pd

# Função para verificar o número de colunas
def test_check_column_count():
  # Criar um DataFrame de exemplo com 3 colunas
  data = pd.DataFrame({'col1': [1, 2, 3],
                       'col2': ['A', 'B', 'C'],
                       'col3': [0.1, 0.2, 0.3]})
  
  # Verificar se o DataFrame tem o número correto de colunas
  assert len(data.columns) == 3

# Função para verificar os tipos de dados das colunas
def test_check_data_types():
  # Criar um DataFrame de exemplo com tipos de dados especificos
  data = pd.DataFrame({'int_col': [1, 2, 3],
                       'str_col': ['A', 'B', 'C'],
                       'float_col': [0.1, 0.2, 0.3]})

  # Verificar se os tipos de dados das colunas correspondem ao esperado
  assert data['int_col'].dtype == 'int64'
  assert data['str_col'].dtype == 'object'
  assert data['float_col'].dtype == 'float64'
```


## Executando os Testes

Para executar esses testes, podemos utilizar o pytest. Basta navegar até o diretório raiz do projeto e executar o comando **'pytest'**. O pytest é uma ferramenta de teste que utiliza convenções para descobrir e executar testes em projetos Python. Para que o pytest identifique automaticamente seus casos de teste, você precisa seguir algumas convenções simples:

1. **Nome dos arquivos de teste:** OS arquivos de teste devem começar com "test_" ou terminar com "_test.py". Por exemplo, "test_preprocessing.py" ou "preprocessing_test.py".
2. **Nome das funções de teste:** As funções de teste devem começar com "test_". Por exemplo, "test_replace_question_marks" ou "test_normalize_data".
3. **Organização:** É comum organizar seus casos de teste em classes, mas não é obrigatório. Você pode simplesmente usar funções de teste independentes se preferir. Se optar por usar classes, elas também devem seguir as convenções de nomenclaturra e começar com "Test".
4. **Estrutura do diretório:** Os arquivos de teste geralmente estão localizados em um diretório dedicado, como "tests" ou "test_suite". O pytest procurará automaticamente por arquivos de teste nesse diretório.
5. **Invocação:** Você pode executar os testes simplesmente digitando "pytest" no terminal no diretório raiz do projeto. O pytest irá automaticamente encontrar todos os arquivos de teste e executá-los.

Ao seguir essas convenções, o pytest consegue identificar e executar seus testes sem a necessidade de configurações adicionais. Isso torna a criação e execução de testes em Python bastante conveniente e fácil de integrar ao fluxo de desenvolvimento.

## Conclusão

Apronfundamos um pouco mais nos testes unitários, destacando a importância de testar operações e as convenções necessárias. Usamos a biblioteca pytest para criar casos de teste e garantir que o código funcione conforme o esperado. Testes unitários são uma parte fundamental do desenvolvimento de código robusto e confiável em projeto de Machine Learning.

A medida que o projeto evolui, a manutenção desses testes é tão importante quanto escrevê-los inicialmente. Eles ajudam o código a se manter confiável, facilitando a implementação de novos recursos e alterações. Além disso, é importante observar que a execução dos testes unitários é tão simples quanto executar um único comando na linha de comando usando o pytest, o que também pode ser incorporado ao fluxo de CI/CD. Dessa forma, toda vez que você enviar uma alteração ao repositório de código, os testes serão executados automaticamente, fornecendo uma camada adicional de garantia de qualidade no seu projeto.
