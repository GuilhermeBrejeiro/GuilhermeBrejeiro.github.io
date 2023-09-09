---
layout: essay
type: essay
title:  MLOps - Melhorando Seus Commits
# All dates must be YYYY-MM-DD format!
date: 2023-09-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Em artigos anteriores, falei sobre as melhores práticas de codificação, seguindo diretrizes como o **PEP8**, e explorando ferramentas como **pylint** e **autopep8** que ajudam a manter nosso código limpo e organizado. No entando, há algo que muitas vezes esquecemos: executar essas ferramentas antes de fazer um commit. Será que precisamos mesmo nos lembrar de rodar esses comandos manualmente toda vez que enviamos alterações para o repositório?
Quando se trata de MLOps, a ideia é automatizar o máximo possível, então por que não automatizar esse processo pré-commit? Para isso, podemos usar um framework com um nome bastante sugestivo, o pre-commit.

## O que são Pré-Commits?

De maneira simples, pré-commits são verificações automáticas que ocorrem antes de um código ser incorporado ao repositório. Eles desempenham um papel crucial na manutenção da alta qualidade do código, identificando problemas antes mesmo que eles se tornem parte do código principal. Por meio de um arquivo de configuração, você pode selecionar quais ferramentas deseja utilizar para formatar e analisar o código, como as mencionadas anteriormente ou qualquer outra de sua preferência. Essas ferramentas são conhecidas como "hooks" (ganchos) e podem ser facilmente integradas ao seu fluxo de desenvolvimento, contribuindo para uma codificação mais limpa e eficiente. Você pode encontrar uma lista de "hooks" disponíveis diretamente no repositório do pré-commits no GitHub, além de outras opções personalizadas que podem ser encontradas na internet.

## Configurando Pré-Commits em Seu Projeto

Configurar pré-commits em projetos de Machine Learning é uma forma eficaz de garantir a qualidade do código antes de fazer um commit. Os passos necessários para utilizar essa ferramenta são relativamente simples:

1. Instalando o 'pre-commit'

```bash
pip install pre-commit
```

OBS: Como dito anteriormente, ter todos os seus requisitos em um arquivo é uma boa prática, para o pre-commit não seria diferente. No arquivo requirements.txt é interessante adicionar o **pre-commit** junto com as outras dependências.

2. Adicionando arquivo de configuração

Crie um arquivo chamado '.pre-commit-config.yaml' no diretório raiz do projetoe, ele conterá os "hooks" que você deseja executar no seu pré-commit. Aqui está um exemplo:

```yaml  
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v2.3.0
    hooks:
    - id: check-yaml
    - id: end-of-file-fixer
    - id: trailing-whitespace
  - repo: https://github.com/psf/black
    rev: 22.10.0
    hooks:
    - id: black
  - repo: https://github.com/pre-commit/mirrors-autopep8
    rev: v1.5.6
    hooks:
    - id: autopep8
      args: ['--in-place', '--aggressive', '--agressive', '*.py']
  - repo: local
    hooks:
    - id: pylint
      name: pylint
      entry: pylint
      language: system
```

**Vamos entender por partes o que está acontecendo nesse arquivo:**

* **repos:** Seção principal que lista os repositórios de onde os hooks serão baixados e utilizados
* **repo:** URL do repositório do hook, caso já tenha ele instalado na maquina, pode ser utilizado "local", conforme o ultimo exemplo
* **hooks:** lista os hooks que serão utilizados do repositório escolhido, um mesmo repositório pode conter diversos hooks, cada um com seu id e seus argumentos

3. Execute o comando de instalação do 'pre-commit'

  Com o comando de instalação, todos os hooks necessários para ser executado pelo pré-commit serão instalados na máquina

  ```bash
    pre-commit install
  ```

A partir desse momento, sempre que for feito um commit, os pré-commits serão executados automaticamente. Se algum deles falhar, o commit será bloqueado até que sejam feitas as devidas correções.

## Conclusão

Os pré-commits são uma ferramenta podedrosa para melhorar a qualidade do código. Eles ajudam a evitar problemas antes que eles se tornem parte do código principal, economizando tempo e reduzindo a probabilidade de erros. 
Configurar o pré-commit pode exigir algum esforço inicial, mas os benefícios a longo prazo para a qualidade e manutenção do código fazem valer a pena.
