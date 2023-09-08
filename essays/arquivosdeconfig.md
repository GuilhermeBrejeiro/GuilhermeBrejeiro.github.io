---
layout: essay
type: essay
title:  MLOps - A importância dos arquivos de configuração
# All dates must be YYYY-MM-DD format!
date: 2023-09-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Nos meus exemplos anteriores ao escrever algumas coisas 'hard-coded' eu percebi que é importânte falar sobre esse assunto. Desenvolver um software eficiente e de fácil manutenção não se trata apenas de escrever código limpo e organizado. Uma parte fundamental é a capacidade de gerenciar as configurações e os parâmetros de forma eficaz. É ai que entram os arquivos de configuração, uma prática que pode tornar o desenvolvimento e a administração do sistema muito mais simples.

## O desafio das Variáveis no Código

Quando começamos o desenvolvimento de um novo projeto, muitas vezes nos deparamos com variáveis que armazenam informações cruciais para o funcionamento do software. Isso inclui informações como URLs de banco de dados, chaves de API, configurações de servidores, entre outras configurações. No entanto, é uma má prática codificar esses valores diretamente no código. Dentro os motivos, posso citar alguns:

1. **Dificuldade de Manutenção:** Quando as configurações estão codificadas diretamente, qualquer alteração requer a modificação do código fonte. Isso não apenas aumenta o risco de erros, mas também torna a manutenção bem mais complicada
2.  **Risco de Vazamento de Informações Sensíveis:** Codificar informações sensíveis, como senhas, diretamente no código, pode levar a riscos de segurança. Se o código for compartilhado ou armazenado em repositórios públicos, essas informações podem ser expostas.
3.  **Adaptação a Ambientes Diferentes:** Em ambientes de desenvolvimento, teste e produção, as configurações frequentemente variam. Codificar esses configurações diretamente no código dificulta a adaptação a diferentes ambientes.

## A Solução: Arquivos de Configuração

Arquivos de configuração são projetados para armazenar variáveis e configurações em um formato que pode ser facilmente lido e modificado sem a necessidade de modificar o código. Algumas vantagens:

1. **Separação de Dados e Lógica:** Os arquivos de configuração permitem separar os dados das lógicas do programa. Isso torna o código mais limpo e facilita a manutenção.
2. **Flexibilidade:** Com arquivos de configuração, você pode facilmente adaptar seu software a diferentes ambientes, como desenvolvimento, teste e produção, simplesmente ajustando os valores nos arquivos de configuração correspondentes.
3. **Segurança:** Informações sensíveis, como senhas e chaves de API, podem ser armazenadas com segurança em arquivos de configuração fora do código fonte, reduzindo o risco de vazamentos.

## Organização com 'config.yaml'

Para melhorar ainda mais o gerenciamento de configurações, é uma prática comum criar um arquivo 'config.yaml' dedicado para armazenar variáveis importantes. Essas variáveis são frequentemente escritas em letras maiúsculas para indicar que são constantes e não devem ser alteradas diretamente no código.

```yaml
  # Configurações de Path
  data_directory: /caminho/para/dados
  data_filename: dataset.csv
  target_name: coluna10
  columns_to_drop: [coluna1, coluna4, coluna7]
  test_size: 0.2

  # Configurações de modeloagem
  model_directory: /caminho/para/modelo
  model_filename: modelo.pkl
  hyperparameters:
  learning_rate: 0.01
  n_estimators: 100
  max_depth: 10
```

## Como Implementar Arquivos de Configuração

A implementação de arquivos de configuração envolve os seguintes passos:

1. **Crie um Arquivo de Configuração:** Crie um arquivo específico para armazenar as configurações. O formato YAML utilizado acima é uma escolha bastante comum mas é possível ser feito até como um arquivo python.
2. **Defina Variáveis:** No arquivo de configuração, defina variáveis e atribua os valores apropriados, seguindo as convençòes de nomemclatura.
3. **Leia o Arquivo de Configuração:** No código, crie um mecanismo para ler o arquivo de configuração e carregas as variáveis.
4. **Utilize as Configurações:** Use as variáveis carregadas a partir do arquivo de configuração em seu código, evitando digitar manualmente qualquer uma delas.

```python
  import yaml

  # Carregue o arquivo de configurações
  with open('config.yaml') as file:
    config = yaml.safe_load(file)

  # Acesse as variáveis do arquivo

  data_directory = config['data_directory']
  data_filename = config['data_filename']
  target_name = config['target_name']
  ...
  learning_rate = config['learning_rate']
  n_estimators = config['n_estimators']
  max_depth = config['max_depth']

  # Agora é possivel utilizar essas variaveis no codigo

  print(f"Data directory: {data_directory})
  print(f"Learning Rate: {learning_rate})
  print(f"Max Depth: {max_depth})
```
Dessa forma, é possível acessar as variáveis do arquivo YAML e usa-las no código Python conforme necessário. No caso acima o confi.yaml estava no mesmo diretório do arquivo python, caso contrário é preciso apontar corretamente para o seu diretório local.

## Conclusão

A utilização de arquivos de configuração, como o **'config.yaml'**, é uma prática recomendade no desenvolvimento do seu software de ML. Ela simplifica o gerenciamento de configurações, torna o código mais seguro e facilita a adaptação a diferentes ambientes. Ao implementar essa prática nos projetos, você aumenta a organização e a eficiência no desenvolvimento e mantenabilidade do modelo.

