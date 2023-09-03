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

Ao começar um projeto de Machine Learning, quase de que imediato precisamos instalar bibliotecas e pacotes necessários na máquina e, conforme o projeto avança, percebemos novas necessidades, talvez um pacote novo de pré-processamento de dados ou uma biblioteca de visualização que nos foi recomentadada. E assim, começamos a instalar mais e mais coisas na máquina. Parece inofensivo de inicio, mas isso pode rapidamente se transformar em uma bola de neve de dependências.

O ambiente de desenvolvimento começa a ficar complicado, e pode ser um pesadelo garantir que todas as bibliotecas estejma atualizadas e funcionando bem juntas. Além disso, compartilhar o projeto ou implantá-lo em outro lugar pode ser extremamente desafiador.

É ai que entra o gerenciamento de dependências. Em vez de instalar tudo diretamente na máquina, criamos um ambiente isolado para todas as dependências do projeto. Isso facilita muito a organização e a manutenção, além de evitar dores de cabeça no futuro (na minha máquina funcionar hahaha)

## Isolando o Ambiente com o Virtual Environments
Uma das abordagens mais comuns para o isolamento do ambiente é o uso de ambientes virtuais.
Essencialmente, você cria um ambiente virtual separado para cada projeto, isolando todas as suas dependências.

Para criar um ambiente virtual, você pode utilizar ferramentas como o [virtualenv](https://virtualenv.pypa.io/en/latest/) ou o [conda](https://docs.conda.io/en/latest/), dependendo de suas preferências. Dentro desses ambientes, você é livre para instalar e gerenciar bibliotecas da maneira que quiser, sem afetar quaisquer outros projetos ou o ambiente do sua máquina local.

## Contêineres Docker
Apesar dos ambientes virtuais serem bastante eficazes, eles ainda podem ser um pouco dificil de gerenciar, especialmente quando o projeto precisa ser compartilhado ou implementado em produção. É nesse momento que o Docker pode ser de grande ajuda.

Contêiners Docker oferecem uma maneira bastante eficaz de empacotar os códigos, suas dependências e até mesmo o sistema operacional que será utilizado. Isso significa que, não importa onde seu código seja executado, ele terá as mesmas dependências e funcionará consistentemente.

Além dessa facilidade, contêiners podem ser orquestrados por ferramentas como o Kubernetes ou o Docker Swarm, facilitando a tarefa de dimensionamento de contêineres em ambientes de produção.

## Conclusão

O gerenciamento de dependências é uma parte crítica do desenvolvimento de projetos (não apenas de Machine Learning). Seja por meio de ambientes virtuais ou contêineres, ter um sistema eficaz de gerenciamento de dependências ajudará a manter os projetos organizados, consistentes e facilmente escaláveis.

Essa é uma das medidas necessárias para começarmos a construir uma esteira robusta de projetos de Machine Learning com práticas de MLOps e é essencial quando trabalhamos em ambientes produtivos. Começar um projeto e já isolar o ambiente só trará ganhos em tempo e performance nos seus desenvolvimentos

