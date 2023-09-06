---
layout: essay
type: essay
title:  MLOps - Estruturando Seus Projetos de Machine Learning
# All dates must be YYYY-MM-DD format!
date: 2023-01-08
labels:
  - Machine Learning Engineer
  - MLOps
  - Aprender ensinando
---

No desenvolvimento de projetos de Machine Learning, uma estrutura organizada faz toda a diferença. Uma estrutura bem definida torna evidente para todos os membros da equipe onde cada elemento do projeto deve ser alocado, resultando em uma colaboração mais fluida e simplificando a manutenção a longo prazo.

## A estrutura ideal

Embora diferentes empresas e projetos possam requerer estruturas de diretórios variadas, é possível definir uma estrutura básica que serve como referência. Essa estrutura pode ser modificada e adaptada ao longo do tempo, mas mantém uma organização que facilita a leitura e compreensão do projeto.
  
meu_projeto_ml/  
│  
├── data/                     
│   ├── 01_raw/                 
│   ├── 02_train/  
│   ├── 03_eval/  
│   ├── 04_test/  
│   └── ...  
│  
├── notebooks/               
│  
├── src/                     
│   ├── 01_data_preprocessing/  
│   ├── 02_feature_engineering/  
│   ├── 03_model_training/               
│   ├── 04_model_evaluation/          
│   ├── 05_api/                 
│   ├── utils/               
│   └── ...  
│  
├── models/                  
│  
├── requirements.txt          
│  
├── README.md                
│  
└── ...  

Acima é um exemplo de estrutura e que, conforme dito anteriormente, pode ser adaptado para o cenário da empresa. Os principais componentes da estrutura:

1. **data**
   * **01_raw/:** Armazena os dados brutos.
   * **02_train/:** Armazena o conjunto de dados que foi selecionado para treinar o modelo.
   * **03_eval/:** Armazena o conjunto de dados que foi selecionado para avaliar o modelo após o treino.
   * **04_test/:** Armazena o conjunto de dados que foi selecionado para testar o modelo final.
2. **notebooks**
   * Armazena os notebooks jupyter usados para as análises durante a fase de desenvolvimento do modelo.
3. **src(source code)**
   * **01_data_preprocessing/:** Scripts responsáveis pelo pré-processamento dos dados.
   * **02_feature_engineering/:** Scripts responsáveis pela engenharia de recursos.
   * **03_model_training/:** Scripts responsáveis pelo treinamento do modelo.
   * **04_model_evaluation/:** Scripts responsáveis pela avaliação do modelo treinado.
   * **05_api/:** Scripts responsáveis pela API que vai servir o modelo.
   * **utils/:** Scripts responsáveis por funções e utilitários reutilizáveis em todo o projeto.
4. **models**
   * Armazena os modelos treinados serializados.
5. **requirements.txt**
   * Mantém uma lista com todas as dependências Python para replicar o ambiente.
6. **README.md**
   * Documentação do projeto, incluindo instruções de configuração e uso.

## Importância de uma boa estrutura

1. **Organização**
   * Manter dados, código e modelos organizados torna mais fácil encontrar o que você precisa
3. **Colaboração**
   * Com uma estrutura bem definida, é mais simples para os outros membros da equipe colaborarem no projeto
5. **Reprodutibilidade**
   * A lista de dependências no 'requirements.txt' permite que qualquer pessoa possa replicar o ambiente de desenvolvimento na própria maquina.
7. **Manutenção**
   * A estrutura ajuda na manutenção a longo prazo, permitindo que você retome facilmente o trabalho após um período de inatividade


## Utilizando o Cookiecutter para Criar a Estrutura

No próximo artigo, falarei um pouco sobre como é possível criar toda essa estrutura de diretórios automaticamente utilizando uma ferramenta chamada Cookiecutter. O Cookiecutter é uma ferramenta de geração de projetos que permite criar estruturas de diretórios personalizadas com facilidade. Com ele, você pode economizar tempo na configuração inicial do projeto e garantir que a estrutura de diretórios esteja sempre consistente. 

## Conclusão

Ao estruturar seu projeto de Machine Learning com uma organização sólida, você economiza tempo e evita dores de cabeça no futuro. Não importa o quão complexo seja o projeto, uma estrutura bem definida é a chave para o sucesso. Portanto, comece com estruturas de projetos mais comuns e adapte-a às necessidades específicas do seu projeto.
