---
layout: essay
type: essay
title:  MLOps - Fundamentos de APIs em projetos de Machine LEarning
# All dates must be YYYY-MM-DD format!
date: 2023-05-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

As APIs (Application Programming Interfaces) são pontes que conectam os modelos de Machine Learning com outrs aplicativos ou serviços que os utilizam. Aqui, tentarei explorar um pouco dos fundamentos, incluindo o que são APIs, por que são importantes em projetos de Machine Learning e falarei um pouco sobre uma ferramenta bastante conhecida para esse tipo de aplicação, o FastAPI.

## O que é uma API?

Em termos simples, uma API é a conexão que permite que diferentes softwares se comuniquem entre si. Elas definem como as solicitações e respostas devem ser estruturadas, permitindo que aplicativos interajam uns coms os outros.

As APIs podem ser encontradas em todos os lugares no mundo da tecnologia. Quando usamos um aplicativo de previsão do tempo para verificar o clima, ele está fazendo uma solicitação para uma API que fornece os dados meteorológicos em tempo real. Quando postamos uma foto no instagram por meio de um aplicativo de terceiros, esse aplicativo está se comunicando com a API do instagram para enviar a foto com a legenda e por ai vai.

## Uma explicação um pouco fora do ambiente da técnologia

Pensando no mundo real, imagine que você é um excelente chef de cozinha, mas em um restaurante desconhecido, onde você não tem conhecimento dos ingredientes necessários para uma receita especial. A única maneira de saborear esse prato é indo até o restaurante. Lá, você faz o seu pedido ao garçom, que por sua vez, repassa o pedido ao chef. O pedido é preparado e, finalmente, o garçom serve a refeição. Nessa interação, o garçom desempenhou o papel de uma API. Você fez a solicitação a ele, ele transmitiu o seu pedido ao chef, que preparou a refeição e, em seguida, o garçom trouxe o prato até você. Assim como no mundo da tecnologia, você não tem conhecimento sobre como o prato foi preparado (assim como os clientes geralmente não conhecem os códigos e dados usados para gerar as respostas das solicitações). Você apenas fez o pedido e recebeu o prato, pagando por ele. Da mesma forma, as empresas não revelam seus segredos comerciais, apenas atendem às necessidades do cliente, entregando os dados processados.

## APIs em Projetos de Machine Learning

Em projetos de Machine Learning, as APIs muitas vezes desempenham papéis críticos em várias etapas do ciclo de vida do modelo. Dependendo do modelo e da empresa, elas podem ser inseridas em diversos contextos:

1. **Ingestão de Dados:** Existem muitos casos aonde os dados necessários para treinar o modelo estão armazenados em sistemas diferentes, vindos até mesmo de empresas diferentes. As APIs podem ser usadas para extrair esses dados e prepará-los para o treinamento do modelo.
2. **Implantação do Modelo:** Após o treinamento do modelo, precisamos implementa-lo em produção para que ele possa fazer as previsões. As APIs são a interface pela qual os aplicativos solicitam essas previsões ao modelo.
3. **Monitoramente de Modelos:** Para garantir que os modelos estejam funcionando corretamente, precisamos monitorá-los continuamente. As APIs podem ser usadas para enviar dados de monitoramente e para receber alertas quando algo estiver errado.
4. **Integração com Aplicativos:** OS modelos de ML geralmente são usados em conjunto com outros aplicativos, sites ou serviços. As APIs permitem que esses aplicativos se comuniquem com os modelos e usem suas previsões.

## Introdução ao FastAPI

FastAPI é um framework Python moderno e de alto desempenho para construir APIs de maneira rápida e eficiente. Alguns dos seus principais recursos são:


1. **Fortemente inspirado no Flask:** Ele tem uma microestrutura leve e com suporte a decorators de rotas, semelhantes ao Flask
2. **Geração Automática de Documentação:** Uma das características mais notáveis do FastAPI é a capacidade de gerar automaticamente documentação interativa para a API com base nas anotações de tipo. ISso simplifica a criação e manutenção da documentação da API.
3. **Desempenho:** O FastAPI é conhecido por seu desempenho excepcional. Ele utiliza o mecanismo de execução assíncrona do Python para lidar com muitas solicitações simultânes com eficiência.
4. **Integração com Pydantic:** O FastAPI se integra perfeitamente com o Pydantic, uma biblioteca para validação de dados e análises de tipos. Isso torna mais fácil validar as entradas e saídas da API.

## Exemplo Prático: Criando uma API 

Suponha que você já possui um modelo de Machine Learning treinado em formato pkl. Todas as etapas anteriores, desde a ingestão dos dados de treinamento até o treinamento do modelo, foram concluídas. Este modelo tem o objetivo de prever os preços das casas com base em suas características, seguindo um modelo básico do Kaggle.

```python
from fastapi import FastAPI
from pydantic import BaseModel
import pickle
import numpy as np

# Instanciando o fastapi
app = FastAPI()

# Carregando o modelo treinado e salvo em formato pkl
with open("modelo_previsao.pkl", "rb") as model_file:
  modelo = pickle.load(model_file)

class HouseFeatures(BaseModel):
  square_feet: float
  num_bedrooms: int
  num_bathrooms: int

@app.post("/prever_precos/")
async def prever_precos(features: HouseFeatures):

  recursos = np.array([[features.square_feet, features.num_bedrooms, features.num_bathrooms]])

  resultado = modelo.predict(recursos)

  return {"previsao": resultado.tolist()}

```

Com este código em execução localmente, por meio de um cliente HTTP, você pode acessá-lo a partir da sua própria máquina através do endereço http://localhost:8000/prever_precos. Além disso, é possível explorar a documentação interativa da API diretamente em seu navegador, por meio do endereço http://localhost:8000/docs.

Alguns pontos desse exemplo:

1. O FastAPI precisa ser instanciado  para em seguida pode ser usado
2. O modelo de previsão foi carregado como se estivesse no mesmo diretório que o código do FastAPI
3. O uso do Pydantic permitiu definir a class **HouseFeatures** para validar os dados de entrada
4. Para fazer as previsões, nesse exemplo, os dados foram convertidos para uma matriz NumPy, passados para o modelo e em seguida o modelo fez as previsões.
5. A resposta HTTP retorna um JSON com as previsões

## Conclusão

As APIs são peças fundamentas em projetos de Machine Learning, permitindo a integração e implantação eficaz de modelos. O FastAPI é uma ferramente poderosa que simplifica a criação de APIs robustas e bem documentadas. Ao combinar o FastAPI com as melhores práticas de MLOps, é possível criar sistemas de Machine Learning altamente eficientes e escaláveis.
