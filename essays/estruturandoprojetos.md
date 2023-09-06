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
