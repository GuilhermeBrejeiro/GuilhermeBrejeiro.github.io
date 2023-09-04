---
layout: essay
type: essay
title:  MLOps - Orquestração de Pipelines
# All dates must be YYYY-MM-DD format!
date: 2023-09-18
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Um dos principais componentes do MLOps é a orquestração de pipelines, permitindo criar, gerenciar e automatizar fluxos de trabalho complexos de treinamento, avaliação, implantação e monitoramento de modelos de ML.

## O Papel da Orquestração de Pipelines de Machine Learning

Um projeto de machine learning envolve diversas etapas, como por exemplo, coletar dados, pré-processá-los, treinar múltiplos modelos com diferentes hiperparâmetros, avaliar o desempenho de cada modelo, selecionar o melhor dentre eles, implantá-lo em produção e monitorá-lo continuamente. Cada uma dessas etapas é um componente crítico do ciclo do modelo, e a orquestração de pipelines é o que mantém todas essas peças funcionando em harmonia.

## Os principais benefícios da orquestração de pipelines

* **Automatização:** Permite a execução automatizada de tarefas complexas, seguindo uma sequência específica.
* **Reprodutibilidade:** Torna possível reproduzir exatamente o mesmo fluxo de trabalho em diferentes momentos.
* **Rastreabilidade:** Facilita o acompanhamento de cada etapa e a identificação de desvios ou melhorias.
* **Eficiência:** Economiza tempo e recursos ao eliminar processos manuais repetitivos.

## Boas práticas ao orquestrar a sua pipeline de Machine Learning

Orquestrar um modelo tem diversos desafios técnicos mas seguindo algumas recomentações esse processo pode ser bem mais fluido e eficaz:

1. **Defina Claramente os Objetivos do Pipeline**
   Tenha uma compreensão solida dos objetivos da criação dessa pipeline. Quais tarefas específicas devem ser automatizadas? Qual é a prioridades de cada uma delas? Ter uma visão clara dos resultados desejados é o primeiro passo em uma orquestração bem sucedida.
2. **Escolha a Ferramenta Certa**
   Existem diversas ferramentas de orquestração de pipelines disponíveis, como Apache Airflow, Kubeflow Pipelines e Prefect. Escolha a que melhor se adapta às necessidades e ao ambiente.
3. **Separe as Etapas do Pipeline**
   Divida o pipeline em etapas (tasks) menores e mais gerenciáveis. Isso facilita a solução de problemas e o paralelismos, se necessário.
4. **Utilize Controle de Versão**
   Mantenha o código do pipeline sob controle de versão, permitindo o rastreio de alterações ao longo do tempo e a possibilidade de revertar para uma versão anterior, caso necessário.
5. **Integre Testes**
   Incorpore testes automatizados em seu pipeline que garantam que cada etapa funcione conforme o esperado.
6. **Monitore e Registre**
   Monitoramenteo e registro do pipeline torna possivel acompanhar o progresso e identificar problemas rapidamente.

## Das Ferramentas citadas acima

Existem várias ferramentas poderosas para orquestração e acompanhar a evolução e lançamentos de ferramentas esta cada vez mais complicado. Dentre elas:

* **Apache Airflow:** Novamente cito o Airflow por ser a ferramenta que tenho mais proximidade, é uma plataforma de código aberto amplamente utilizada para agendar, monitorar e orquestrar fluxos de trabalho. Além disso, é altamente configurável e oferece uma ampla gama de conectores.
* **Kubeflow Pipelines:** Projetado especificamente para Kubernetes, facilita a criação de pipelines de ML nativos da nuvem.
* **Prefect:** Uma estrutura de orquestração de pipelines de código aberto que se integra bem com várias bibliotecas de Machine Learning.

## Conclusão

A orquestração de pipelines ajuda a garantir uma entrega bem-sucedida de projetos de Machine Learning em larga escala. Ela permite que equipes colaborem de maneira eficiente, automatizem tarefas complexas e garantam a reprodutibilidade e a rastreabilidade em todo o ciclo de vida do modelo.

## Links:  
https://towardsdatascience.com/machine-learning-orchestration-vs-mlops-d4cfe3b7bec  
https://www.astronomer.io/blog/machine-learning-pipeline-orchestration/  
https://medium.com/@ekawade1394/ml-orchestration-kubeflow-d95e547b3af  
https://www.kubeflow.org/  
https://www.prefect.io/  
