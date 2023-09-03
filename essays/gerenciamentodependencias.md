---
layout: essay
type: essay
title: MLOps - Gerenciamento de Dependências
# All dates must be YYYY-MM-DD format!
date: 2023-09-03
labels:
  - Software Engineer
  - MLOps
  - Aprender ensinando
---

Ao começar um projeto de Machine Learning, quase de que imediato precisamos instalar bibliotecas e pacotes necessários na máquina e, à medida que o projeto avança, percebemos novas necessidades, talvez um pacote novo de pré-processamento de dados ou uma biblioteca de visualização que nos foi recomentadada. E assim, começamos a instalar mais e mais coisas na máquina. Parece inofensivo de inicio, mas isso pode rapidamente se transformar em uma bola de neve de dependências.

O ambiente de desenvolvimento começa a ficar complicado, e pode ser um pesadelo garantir que todas as bibliotecas estejma atualizadas e funcionando bem juntas. Além disso, compartilhar o projeto ou implantá-lo em outro lugar pode ser extremamente desafiador.

É ai que entra o gerenciamento de dependências. Em vez de instalar tudo diretamente na máquina, criamos um ambiente isolado para todas as dependências do projeto. Isso facilita muito a organização e a manutenção, além de evitar dores de cabeça no futuro (na minha máquina funcionar hahaha)

## Isolando o Ambiente com o Virtual Environments
Uma das abordagens mais comuns para o isolamento do ambiente é o uso de ambientes virtuais.
Essencialmente, você cria um ambiente virtual separado para cada projeto, isolando todas as suas dependências.

Para criar um ambiente virtual, você pode utilizar ferramentas como o ['virtualenv'](https://virtualenv.pypa.io/en/latest/) ou o ['conda'](https://docs.conda.io/en/latest/), dependendo de suas preferências. Dentro desses ambientes, você é livre para instalar e gerenciar bibliotecas da maneira que quiser, sem afetar quaisquer outros projetos ou o ambiente do sua máquina local.

