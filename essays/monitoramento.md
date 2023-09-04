---
layout: essay
type: essay
title:  MLOps - Gerenciamento de Experimentos
# All dates must be YYYY-MM-DD format!
date: 2023-09-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

A criação de um modelo de Machine Learning envolve várias etapas, como:

1. **Coleta de Dados:** Aquisição de dados relevantes ao problema que deve ser resolvido.
2. **Pré-processamento de Dados:** Limpeza, transformação e preparação dos dados para o treinamento.
3. **Treinamento de Modelo:** Utilização dos dados para treinar o modelo, ajustando os paramêtros necessários.
4. **Validação e Testes:** Avaliação do desempenho do modelo para garantir que ele funcione bem com novos dados.
5. **Implantação:** Colocar o modelo em produção, para que comece a fazer previsões.
6. **Monitoramento:** Acompanhamento continuou de desempenho e comportamento no ambiente de produção.

## Importância do Monitoramento

O monitoramente desempenha um papel fundamental no ciclo de vida do modelo. Aqui estão algumas das principais razões:

1. **Mudanças nos Dados de Entrada**
   Os modelos de Machine Learning, diferentes de um software convencional, dependem de dados para fazer previsões. No entanto, os dados do mundo real estão em constante evolução, inclusive em casos que o usuario aprende os padrões das previsões e começa a burlar as regras. Novos padrões podem surgir, distribuições podem mudar e valores ausentes podem ocorrer. O monitoramente permite detectar esses mudanças nos dados de entrada e avaliar o quanto elas estão afetando o desempenho do modelo.
