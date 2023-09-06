---
layout: essay
type: essay
title:  MLOps - Criando Sua Própria Estrutura de Projetos de ML com Cookiecutter
# All dates must be YYYY-MM-DD format!
date: 2023-01-24
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Anteriormente exploramos a importância de uma estrutura bem organizada para projetos de Machine Learning. Uma estrutura bem definida facilita o desenvolvimento, a colaboração e a manutenção dos projetos ao longo do tempo. Agora, como tudo em MLOps, vamos dar uma olhada em como automatizar a criação dessa estrutura de forma personalizada com a ajuda do Cookiecutter.

O Cookiecutter é uma ferramenta de geração de projetos que permite criar estruturas de diretórios personalizadas de forma bastante eficiente. Com ele, você pode personalizar a estrutura de acordo com as necessidades especificas dos projetos.

## Instalando o Cookiecutter

Para começar a criar sua própria estrutura de projeto personalizada, você precisará instalar a ferramenta Cookiecutter em seu ambiente de desenvolvimento. A instalação é simples e pode ser feita usando o seguinte comando pip:

```bash
pip install cookiecutter
```

## Escolhendo o Modelo de Cookiecutter

O Cookiecutter oferece uma variedade de modelos prontos para uso. Você pode encontrar modelos específicos para projetos de Machine Learning, como o Cookiecutter Data Science, que já inclui uma estrutura de diretórios e arquivos de configuração bem definidos.

Você pode descobrir modelos específicos pesquisando no repositório oficial do Cookiecutter no GitHub ou em outros repositórios públicos. Além disso, você tem a opção de criar seu próprio modelo personalizado.

## Criando um Modelo Personalizado

Se você deseja personalizar a estrutura do projeto de acordo com as necessidades do seu projeto de Machine Learning, siga estas etapas:

1. Crie um novo diretório para o seu modelo de Cookiecutter:

   ```bash
   mkdir cookiecutter-mlops
   cd cookiecutter-mlops
   ```
   
2. Dentro do diretório, crie um arquivo chamado cookiecutter.json. Este arquivo conterá as perguntas interativas que o Cookiecutter fará ao criar um novo projeto e que serão usadas para preencher automaticamente os itens especificados. Aqui está um exemplo:

   ```json
   {
   "project_name": "Nome-do-Projeto",
   "author_name": "Seu-nome",
   "description": "Uma breve descricao do projeto",
   "repo_name": "nome_do_repositorio"
   }
   ```
3. Crie a estrutura de diretórios desejada dentro do seu modelo do Cookiecutter. Por exemplo:

   ```css
   cookiecutter-mlops
   ├── cookiecutter.json
   ├── {{cookiecutter.repo_name}}
   │   ├── data
   │   │   ├── 01_raw
   │   │   ├── 02_train
   │   │   ├── 03_eval
   │   │   ├── 04_test
   │   │   └── ingestion
   │   ├── models
   │   ├── notebooks
   │   ├── README.md
   │   ├── requirements.txt
   │   └── src
   │       ├── 01_data_preprocessing
   │       ├── 02_feature_engineering
   │       ├── 03_model_training
   │       ├── 04_model_evaluation
   │       ├── 05_api
   │       └── utils
   └── README.md
   ```
4. Disponibilize a estrutura personalizada

  Com a criação da estrutura e do arquivo **cookiecutter.json** agora você deve criar um novo repositório, no GitHub por exemplo, e a partir desse momento, com a URL desse repositório o seu time poderá copiar esse template com o comando **'cookiecutter + URL do repositorio'**:
  
  ```bash
    cookiecutter /caminho/para/o/modelo/cookiecutter-mlops
  ```

5. Utilize a estrutura personalizada
   
No exemplo acima é possivel visualizar que a pasta principal do repositório se chama **{{cookiecutter.repo_name}}**, isso significa que ao clonar esse repositório e responder a pergunta inicial **repo_name** o cookiecutter fará com que essa pasta assuma o nome o qual você informou. Todos os diretórios ou arquivos que contenham chaves duplas **'{{ }}´** com uma das variaveis preenchidas no **cookiecutter.json** irão assumir essas variáveis.


Supondo que, ao iniciar o cookiecuter, você responda a pergunta **'repo_name'** com o valor de **'meu_primeiro_repositorio'**, a estrutura do repositório acima ficaria assim:

   ```css
   ├── cookiecutter.json
   ├── meu_primeiro_repositorio
   │   ├── data
   │   │   ├── 01_raw
   │   │   ├── 02_train
   │   │   ├── 03_eval
   │   │   ├── 04_test
   │   │   └── ingestion
   │   ├── models
   │   ├── notebooks
   │   ├── README.md
   │   ├── requirements.txt
   │   └── src
   │       ├── 01_data_preprocessing
   │       ├── 02_feature_engineering
   │       ├── 03_model_training
   │       ├── 04_model_evaluation
   │       ├── 05_api
   │       └── utils
   └── README.md
   ```

Com essa abordagem, você pode não apenas personalizar a estrutura de pastas, mas também definir nomes personalizados para essas pastas e o conteúdo dos arquivos com base nas respostas fornecidas durante o processo de criação do projeto com o Cookiecutter.

## Conclusão

Como visto anteriormente, criar uma estrutura de projeto de Machine Learning torna evidente para todos os membros da equipe onde cada elemento do projeto deve ser alocado, resultando em uma colaboração mais fluida e simplificando manutenções futuras. Com o Cookiecutter você tem flexibilidade e eficiência, podendo adaptar a estrutura de diretórios às necessidades específicas do projeto e economizar tempo na configuração inicial. Ele é mais um passo na automação de todo o processo de engenharia de Machine Learning.
