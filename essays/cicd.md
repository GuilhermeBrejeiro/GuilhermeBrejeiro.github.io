---
layout: essay
type: essay
title:  MLOps - CI/CD para Modelos de Machine Learning
# All dates must be YYYY-MM-DD format!
date: 2023-09-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

Agora vamos explorar o papel fundamental da CI/CD em um pipeline de Machine Learning e como essa abordagem pode melhorar significativamente o ciclo de vida de desenvolvimento de modelos.

Os modelos de ML são diferentes do software tradicional. Eles dependem de dados para treinamento e operação e podem evoluir com o tempo à medida que novos dados são disponibilizados. Gerenciar modelos de Machine Learning de forma efetiva envolve lidar com várias considerações complexas:

1. **Treinamento Iterativo:** Os modelos de ML são frequentemente treinados de forma iterativa, com experimentos visando ajustar os hiperparâmetros e a arquitetura. Isso requer um controle rigoroso das versões do modelo e dos dados.
2. **Dados em Evolução:** Os dados usados para treinar e alimentar os modelos podem mudar ao longo do tempo, exigindo uma maneira de rastrear e gerenciar essas mudanças
3. **Colaboração Multidisciplinar:** Equipes de ML geralmente incluem cientistas de dados, engenheiros de software e especialistas em domínio. Coordenar o trabalho de diferentes disciplinas é fundamental.
4. **Implantação e Monitoramento Contínuos:** Modelos de Machine Learning precisam ser implantados em produção e continuamente monitorados para garantir que mantenham o desempenho desejado.

## A importância da Integração Contínua (Continuous Integration - CI)

A CI é uma prática que envolve a integração frequente de alteraçòes de código em um repositório compartilhado. Para modelos de Machine Learning, isso significa integrar não apenas o código, mas também os dados, hiperparâmetros e metadados relevantes. A CI permite:

* **Validação Rápida:** Alterações são validadas automaticamente por meio de testes, reduzindo a probabilidade de erros.
* **Rastreamento de Versões:** Todas as mudanças no código, dados e configurações são salvas, permitindo a reprodução exata de experimentos anteriores.
* **Colaboração Eficiente:** Equipes podem trabalhar de forma colaborativa, sabendo que as alterações serão integradas e testadas de forma consistente.

## A Entrega Contínua ( Continuous Delivery - CD)
A CD é o próximo passo após a CI e envolve a implantação automatizada de código em produção. Para modelos de ML, a CD inclui a implantação de modelos treinados e validados em ambientes de produção, juntamente com processos contínuos de monitoramento e validação. A CD oferece benefícios significativos:

* **Implantações Confiáveis:** A implantação automatizada reduz o risco de erros humanos ao colocar o modelo em produção
* **Monitoramento Contínuo:** Modelos em produção são monitorados continuamente para detectar degradação de desempenho ou mudanças nos dados
* **Reversão Segura:** Se problemas forem detectados, a CD permite reverter rapidamente para uma versão anterior do modelo

A medida que o campo de MLOps evolui, podemos esperar novas ferramentas cada vez mais sofisticadas para apoiar esse ciclo de vida do modelo. Algumas ferramentas bastante populares não só para modelos de Machine Learning mas para o processo de CI/CD em geral incluem Jenkins, Travis CI, GitLab CI/CD, CircleCI e o GitHub Actions.

## GitHub Actions

O GitHub Actions é a ferramenta que tenho mais familiaridade, juntamente com o GitLAb CI e é uma ferramenta que pode ser usada tanto para CI quanto para CD. É uma plataforma de automação que permite criar diversos fluxos de trabalho personalizados, que automatizam as etapas de desenvolvimento de software, incluindo compilação, testes, implantação e muito mais.

No contexto da CI, podemos configurar fluxos de trabalho que automatizam a compilação e os testes do código sempre que ocorre um push no repositório. Essa automação pode ser condicionada à branch na qual o push foi efetuado, permitindo um controle refinado sobre quando a CI é acionada. Essa abordagem é altamente benéfica, pois ajuda a identificar problemas de código precocemente, melhorando a qualidade e a eficiência na entrega do software.

Na CD, o GitHub Actions permite automatizar a implantação do código em ambientes de produção após a conclusão bem-sucedida dos testes e validações necessários. É possível configurar segredos (secrets) que fornecem acesso seguro a plataformas como a AWS. Dessa forma, o GitHub Actions pode implantar as alterações automaticamente, atualizando o modelo em produção. Isso proporciona uma entrega rápida e confiável do modelo aos usuários finais.

Aqui está um exemplo de um arquivo de configuração que deve ser incluído no repositório do projeto, na pasta .github/workflows/arquivo_ci_cd.yaml. Esse arquivo descreve os passos executados pelo fluxo de trabalho:

* O fluxo de trabalho é acionado quando ocorre um push na branch 'main'.
* O processo é executado em uma máquina virtual Ubuntu.
* As credenciais da AWS devem ser configuradas como secrets no GitHub, com nomes como 'AWS_ACCESS_KEY_ID' e 'AWS_SECRET_ACCESS_KEY'. Isso implica em registrar um usuário e senha no GitHub para que ele possa acessar a conta da AWS, garantindo que esses dados sensíveis não fiquem expostos no repositório.
* A etapa final utiliza o comando 'aws s3 sync' para sincronizar o conteúdo do diretório 'your-static-website-folder' com um bucket S3 na AWS. 

Dessa forma, o GitHub Actions possibilita a integração contínua e a entrega contínua de maneira segura, eficiente e confiável.
