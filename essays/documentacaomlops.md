---
layout: essay
type: essay
title:  MLOps - Documentação
# All dates must be YYYY-MM-DD format!
date: 2023-09-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Um elemento frequentemente subestimado ou considerado "burocrático" é a documentação técnica do projeto. No entanto, sua verdadeira importância vai muito além da mera formalidade. Ela desemprenha o papel fundamental de servir como um guia essencial tanto para os desenvolvedores quanto para os usuários finais do modelo. Além disso, é uma ferramenta valiosa para o próprio criador do modelo, permitindo que ele mantenha um registro detalhado de modelos desenvolvidos em períodos anteriores, mesmo quando estes foram criados há muito tempo atrás ("Quando escrevi esse código só eu e deus sabia o que ele fazia, agora só deus sabe.")

## Por que a Documentação é Fundamental em MLOps?

Imagine desenvolver um modelo de Machine Learning complexo que envolve várias etapas, desde a coleta e preparação de dados até o treinamento, validação e implantação do modelo em produção. Nesse cenário, a documentação se torna uma ferramenta indispensável por várias razões:

1. **Rastreabilidade e Reprodutibilidade**
   A documentação permite rastrear cada passo do ciclo de vida do modelo, desde a escolha dos dados até os hiperparâmetros usados no treinamento. Isso é fundamental para reprodutibilidade.
2. **Colaboração Eficaz**
   Em projetos de ML, as equipes podem ser multidisciplinares, incluindo cientistas de dados, engenheiros de dados, engenheiros de software, especialistas e muito mais. A documentação serve como um meio de comunicação entre os membros, permitindo que todos compreeendam o que foi feito, como e por quê.
3. **Diagnóstico e Solução de Problemas**
   Os modelos de Machine Learning não são perfeitos e nem tem a pretensão de ser, eventualmente podem apresentar problemas em produção. Quando isso acontece, a documentação pode ser uma fonte valiosa de informações para diagnosticar e resolver problemas. Registros detalhados de versões, configurações e decisões de modelagem podem acelerar o processo de resolução do problema.
4. **Transparência e Auditoria**
   Em muitos casos, é necessário fornecer evidências e garantir a conformidade regulatória. Uma documentação completa e precisa permite transparência em relação ao desenvolvimento e implantação do modelo.

## O Que Documentar em um Projeto de Machine Learning?

Para ter uma documentação eficiente, alguns elementos podem ser essenciais:

1. **Dados**
   * Origem dos dados
   * Como foi feito o pré-processamento
   * Quais foram as transformações aplicadas
   * Como foi dividido o conjunto de treinamento, validação e teste.
2. **Modelo de Machine Learning**
   * Arquitetura usado no modelo
   * Hiperparâmetros selecionados
   * Algoritmo de treinamento utilizado
   * Métricas de avaliação selecionadas
   * Versões anteriores do modelo
3. **Implantação em Produção**
   * Qual o ambiente de implantação
   * Configurações da implantação
   * Monitoramento e métricas em produção
   * Procedimentos de escalabilidade que serão utilizados
   * Arquitetura da implementação
4. **Fluxo de Trabalho e Automação**
   * Fluxo de trabalho de treinamento, validação e implantação
   * Programação de tarefas automatizadas
   * Dependências e pipelines
5. **Manutenção e Atualizações**
   * Registro de atualizações anteriores
   * Motivos das atualizações
   * Resultados dos testes pós atualização
  
## Ferramentas para Gerenciamento de Documentação em MLOps

Para gerenciar eficazmente a documentação, existem ferramentas que podem ajudar:

* **Plataformas MLOps:** Algumas ferramentas comumente usadas em MLOps são o MLflow e o Kubeflow, com recursos integrados de documentação para modelos e fluxos de trabalho.
* **Sistema de Controle de Versão:** um bom exemplo é o GIT, para rastrear e gerenciar a documentação junto com o código.
* **Ferramentas de Geração de Documentação:** Existem ferramentas que podem ajudar a automatizar a geração de documentação a partir de anotações no código
* **Wiki Corporativa:** é uma wiki usada numa empresa ou no contexto organizacional, especialmente para promover o compartilhamento do conhecimento interno.

## Conclusão

A documentação é a espinha dorsal de qualquer projeto, seja ele relacionado a Machine Learning ou a softwares convencionais. Ela não apenas facilita a colaboração e a transparência, mas também desempenha um papel crucial na rastreabilidade, na resolução de problemas e na garantia de conformidade. Cultivar o hábito de investir tempo na criação e manutenção da documentação deve ser uma parte essencial da cultura organizacional. Essa prática não apenas fortalece a qualidade dos projetos, mas também impulsiona a excelência operacional e a inovação.

Links:  

https://medium.com/geekculture/good-documentation-for-machine-learning-a-guide-93ebbb4c4ea  
https://thisisimportant.net/posts/documenting-machine-learning-models/  
https://towardsdatascience.com/document-your-machine-learning-project-in-a-smart-way-35c68aa5fc0e  
https://towardsdatascience.com/automate-your-model-documentation-using-h2o-autodoc-46ce82701a4d
