---
layout: essay
type: essay
title:  MLOps - Servindo Modelos de Machine Learning
# All dates must be YYYY-MM-DD format!
date: 2023-06-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

O processo de coleta de dados, treinamento do modelos e à preparação para a implantação em uma API, é apenas uma das grandes etapas envolvidas na entrega de um modelo de Machine Learning pronto para se tornar um dos pilares de uma empresa voltada para dados. Aqui vou explorar os principais aspectos de servir um modelo, baseados em informações coletadas em diversas fontes de estudos e na minha experiência pessoal nesta área.

## Como será o carregamento do modelo?

Ao servir um modelo de Machine Learning, uma das primeiras decisões a serem tomadas é onde e como esse modelo será carregado. Isso pode variar desde hospedar o modelo em servidores locais até implantá-lo na nuvem ou em dispotivos de borda. Essa escolha depende das necessidades especificas do projeto.

* **Servidores Locais:** Modelos podem ser executados em servidores locais dedicados. Isso pode ser adequado para cenários em que existem questões específicas de privacidade ou segurança e também pode ser uma boa opção em situações onde a latência é uma preocupação crítica ou se for necessário hardware especializado para executar o modelo.
* **Nuvem:** É uma opção que oferece flexibilidade e escalabilidade. Modelos podem ser hospedados em servidores virtuais ou serviços gerenciados, permitindo escalonamento automático conforme a demanda.
* **Dispositivos de Borda:** Para aplicativos que requerem respostas em tempo real, podendo ser armazenados em celulares, smartwatches, assistentes digitais e afins. Essa alternativa tem suas restrições, como tamanho do modelo e até a quantidade de energia que pode ser consumida por esse modelo, apesar disso é uma boa opção para diminuir a latência das predições.

## Qual será a latência do modelo?

A latência do modelo é um fator crítico a ser considerado. Ela basicamente se refere ao tempo que leva para o modelo fornecer uma respostas após receber uma solicitação. Aplicações que exigem respostas instantâneas, como assistentes virtuais, demandam uma baixa latência. Em contrapartida, tarefas que podem tolerar maior latência, como análise de dados científicos, tem requisitos diferentes.

Para otimizar a latência, estratégias como a replicação do modelo em várias maquinas e o uso de hardware acelerador, como GPUs, podem ser empregadas. A escolha vai depender das necessidades específicas do aplicativo.

## Onde o modelo irá ficar?

A localização física do modelo também é uma consideração essencial. Ela pode impactar a latência, a escalabilidade e a segurança do sistema. Além disso, preocupações de privacidade podem influenciar essa decisão.

* **Servidores Locais:** Pode ser vantajoso em cenários em que privacidade e a segurança são cruciais. No entanto, isso pode limitar a escalabilidade.
* **Nuvem:** Oferece escalabilidade e flexibilidade, mas os custos e a latência podem variar com base na localização dos data centers.
* **Dispositivos de Borda:** Oferece uma baixa latência e autonomia, porém tem limitaçòes devido ao próprio dispositivo aonde o modelo precisará ficar.

## Como o modelo será armazenado, carregado, versionado e atualizado?

Gerenciar modelos em produção requer um sistema eficiente para armazenar, carregar, versionar e atualizar modelos. Isso envolve garantir que as atualizações possam ser aplicadas sem interromper o serviço e rastrear versões anteriores do modelo.

Estrátegias como o carregamento gradual de novas versões, o monitoramento de desempenho e a verificação de qualidade do modelo desempenham um papel fundamental na manutenção de sistemas de Machine Learning em produção.

## Arquiteturas para servir modelos

Existem várias arquiteturas para servir modelos de Machine Learning, cada uma adequada a diferentes cenários:

* **Offline:** Modelos são atualizados periodicamente, e as previsões são geradas em lotes. É adequado para aplicativos com requisitos de latência flexíveis.
* **Online:** Modelos respondem em tempo real às solicitações, sendo ideais para aplicativos que exigem baixa latência.
* **Model as a Service:** Modelos são armazenados em um cluster dedicado e os resultados são fornecidos por meio de APIs, permitindo sua integração em aplicativos de terceiros de maneira simples
* **Serving at the Edge:** Modelos são implantados diretamente em dispositivos de borda, como câmeras e sensores, para aplicaçãos de IoT e automação.


## Conclusão

Servir modelos de Machine Learning é uma parte crítica da jornada de implementação de IA em produção. Compreender e planejar cuidadosamente o carregamento, a latência, a localização, o hardware, o gerenciamento e a arquitetura são passos essenciais para o sucesso de qualquer projeto de Machine Learning
