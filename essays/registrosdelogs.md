---
layout: essay
type: essay
title:  MLOps - Garantindo a Robustez com Try e Except e Registros de Logs
# All dates must be YYYY-MM-DD format!
date: 2023-03-01
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Durante o desenvolvimento de modelos de Machine Learning, deparar-se com excessões e erros acaba sendo inevitável. Garantir a robustez da implementação em produção é crucial. Vamos falar um pouco sobre a combinação de blocos **try** e **except** e o registros de logs no sistema.

## Evitando que Mudanças Passem Despercebidas

O ambiente de produção possui uma variedade de interações que podem fugir do nosso controle e da forma como o modelo de Machine Learning está preparado para atuar. Dados de entrada podem mudar ou um serviço externo pode interromper o funcionamento de forma repentina. O código precisa ser resiliente o suficiente para lidar com essas situações.

## try...except: Capturando as Exceções

Uma maneira de tornar o código mais robusto é usando blocos **try** e **except**. Esses blocos "tentam" executar o trecho do código dentro deles e, em caso de falha, executam o código dentro da excessão. Isso impede que o código simplesmente quebre e fornece a oportunidade de lidar com esse erro de forma adequada.

```python
try:
  # Codigo que, inicialmente, deveria sempre funcionar
  resultado = funcao_x()
except Exception as e:
  # Tratamento dado devido a funcao_x ter falhado
  logger.error(f"Erro inesperado: {str(e)})
  # Ação tomada em caso de erro da funcao_x, como gerar alguma notificacao ou registrar o erro em um arquivo de logs
```

## Registros de Logs

Capturar exceções e impedir que o código quebre é extremamente importante, mas saber o que aconteceu também é necessário. É aí que entra a necessidade de registrar os logs que ocasionaram essas exceções. Um sistema de registro eficiente registra eventos e informações úteis sobre o comportamento do código.

Para tornar essa tarefa mais simples, existe uma biblioteca de registro em Python conhecida como **'logging'**, a qual você pode configurar diferentes níveis de registro (como INFO, WARNING, ERROR,...) e direcionar saídas para locais apropriados, como arquivos ou sistemas de monitoramento.

```python
import logging

# Configuração básica de registro
logging.basicConfig(level=logging.INFO)

# Registra uma mensagem
logging.info('Aplicação iniciada com sucesso')

# Registr um erro
try:
  resultado = funcao_x()
except Exception as e:
  logging.error(f"Erro inesperado: {str(e)}")
```

## Registros personalizados

O código acima pode se tornar bem mais robusto com a adição de direcionadores de saída e formatação personalizada.

```python
import logging
import os
from datetime import datetime

# Composição do arquivo .log utilizando a data e a hora, tornando cada arquivo único
LOG_FILE=f"{datetime.now().strftime('%m_%d_%Y_%H_%M_%S')}.log"

# Criação do diretório logs, caso ele não exista, para salvar os logs gerados
logs_path=os.path.join(os.getcwd(),"logs",LOG_FILE)
os.makedirs(logs_path,exist_ok=True)

# Variável com o caminho completo onde o log será salvo
LOG_FILE_PATH=os.path.join(logs_path,LOG_FILE)

# Registro do log com formato personalizado, as mensagens incluirão data, hora, nome do logger e nível de registro
logging.basicConfig(
    filename=LOG_FILE_PATH,
    format="[ %(asctime)s ] %(lineno)d %(name)s - %(levelname)s - %(message)s",
    level=logging.INFO)
```

## Gerenciando Erros
Com o uso inteligente do **try** e **except** e registros de **logs**, você permite que sua aplicação lide com exceções de forma muito mais robusta. Em vez de falhar silenciosamente, sua aplicação pode:

* Registrar detalhes sobre o erro para diagnóstico posterior.
* Executar ações, como notificações automáticas
* Continuar a funcionar em um estado degradado
* Garantir que você esteja ciente de problemas imediatamente

# Conclusão

Em um projeto de Machine Learning com práticas de MLOps, onde a confiabilidade é fundamental, a combinação **try** e **except** e registros de **logs** desempenha um papel vital. Eles ajudam a manter as aplicações robustas e resilientes, mesmo quando confrontadas com situações adversas. Usar essa combinação de forma efetiva é extremamente importante.

